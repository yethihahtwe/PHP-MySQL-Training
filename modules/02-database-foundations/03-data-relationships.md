# Relationships

In a relational database, each table can be related to each other using relationships. There are three primary types of relationships.

1. One to one
2. One to many
3. Many to many

## One-to-one relationship

Each record from first table relates to exactly one record from second table and vice versa.

One-to-one relationship is often used to separate sensitive data or split a table with multiple columns. It is carried out using primay and foreign keys usually with unique constraint.

**Example**

An employee might have one detailed employment contract at a time. And vice versa, each contract belongs to only one employee.

```
EMPLOYEES                      EMPLOYMENT_CONTRACTS
+----------------+            +-------------------+
| employee_id (PK)|<--------->| contract_id (PK)  |
| first_name     |            | employee_id (FK,UQ)|
| last_name      |            | start_date        |
| date_of_birth  |            | end_date          |
| ...            |            | salary            |
+----------------+            | ...               |
                              +-------------------+
```

**SQL Implementation**

```sql
CREATE TABLE employees (
    employee_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    date_of_birth DATE
);

CREATE TABLE employment_contracts (
    contract_id INT AUTO_INCREMENT PRIMARY KEY,
    employee_id INT UNIQUE,
    start_date DATE NOT NULL,
    end_date DATE,
    salary DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (employee_id) REFERENCES employees(employee_id)
);
```

> `UNIQUE` constraint is added to `employee_id` in the `employment_contracts` table. This makes sure each employee has only one contract. But it depends on the employment policy of the institution. If the employement contract for an employee might be renewed or replaced, the `UNIQUE` constraint is not required.

## One-to-many relationship

Each record from the first table can be related to multiple records from the second table. But each record from the second table is related to only one record from the first table.

This is the most common type of relationship. The primary key from the first table can be implemented as foreign key in the second table. This relationship can also be created with `HasMany` function in Laravel framework.

**Example**

A department/unit manager might supervise more than one employee. But each employee is under direct supervision of only one manager.

```
DEPARTMENTS                   EMPLOYEES
+----------------+            +-------------------+
| dept_id (PK)   |<---------->| employee_id (PK)  |
| dept_name      |            | first_name        |
| manager_id     |            | last_name         |
| location       |            | dept_id (FK)      |
| ...            |            | ...               |
+----------------+            +-------------------+
```

**SQL Implementation**

```sql
CREATE TABLE departments (
    dept_id INT AUTO_INCREMENT PRIMARY KEY,
    dept_name VARCHAR(100) NOT NULL,
    manager_id INT,
    location VARCHAR(100)
);

CREATE TABLE employees (
    employee_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
);
```

The `dept_id` in `employees` table is a foreign key relating to the `dept_id` primary key from `departments` table.

## Many-to-many relationship

Each record from the first table can be related to multiple records from the second table and vice versa.

A many-to-many relationship requires a junction or bridge table. In the context of Laravel, this kind of intermediary table is called a pivot table. We'll be using the term **Pivot table** for these instances. Primary keys from the original tables are relating to each other as foreign keys in the pivot table.

The table can have a new primary key column to identify each relationship or the foreign keys inside can be implemented as composite keys. Other attributes/columns can also be added in a pivot table.

**Example**

More than one employee can join multiple trainings and each training can have multiple participants.

```
EMPLOYEES                   TRAINING_ENROLLMENTS              TRAINING_PROGRAMS
+---------------+           +-----------------+              +---------------+
| employee_id (PK)|<-------->| employee_id (FK)|<------------->| program_id (PK)|
| first_name    |           | program_id (FK) |              | program_name  |
| last_name     |           | enroll_date     |              | description   |
| ...           |           | completion_date |              | duration      |
+---------------+           | status          |              +---------------+
                            +-----------------+
```

**SQL Implementation**

```sql
CREATE TABLE employees (
    employee_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL
);

CREATE TABLE training_programs (
    program_id INT AUTO_INCREMENT PRIMARY KEY,
    program_name VARCHAR(100) NOT NULL,
    description TEXT,
    duration INT COMMENT 'Duration in hours'
);

CREATE TABLE training_enrollments (
    employee_id INT,
    program_id INT,
    enroll_date DATE NOT NULL,
    completion_date DATE,
    status VARCHAR(20),
    PRIMARY KEY (employee_id, program_id),
    FOREIGN KEY (employee_id) REFERENCES employees(employee_id),
    FOREIGN KEY (program_id) REFERENCES training_programs(program_id)
);
```

`training_enrollments` table is a pivot table containing foreign keys related to `employees` and `training_programs` tables. The same foreign keys together become primary key as composite keys. Not only related foreign keys, some other attributes/columns are also added in the pivot table.


## Self referencing relationship

In a self-referencing relationship, a record can be related to another record from the same table.

**Example**

A category record might be a sub-category of another category record from the same `categories` table.

```
CATEGORIES
+-------------------------+
| category_id (PK)        |
| category_name           |
| parent_category_id (FK) |
| ...                     |
+-------------------------+
         ^    |
         |____|
```

**SQL Implementation**

```sql
CREATE TABLE categories (
    category_id INT AUTO_INCREMENT PRIMARY KEY,
    category_name VARCHAR(50) NOT NULL,
    parent_category_id INT,
    FOREIGN KEY (parent_category_id) REFERENCES categories(category_id)
);
```

The `parent_category_id` foreign key references the `category_id` primary key from the same table. A hierarchical relationship can be created using self-reference.

## Relationship constraints

Relationship constraints make sure the existence of original related items and take care of what happens next when the origial records get deleted or updated.

### REFERENCES

`REFERENCES` constraint makes sure an original related record already exists. If a new record is being created with references to a non-existent record, the `REFERENCES` constraint prevents this. `REFERENCES` constraint alone prevents deleting a parent record which it has related children records.

### ON DELETE and ON UPDATE

When the parent record is deleted or updated, under its foreign key in a related table, we can specify what happens next using `ON DELETE` and `ON UPDATE` keywords.

The `CASCADE` automatically update or delete related records. `ON DELETE CASCADE` means when the parent record is deleted, its related children records will be deleted as well. `ON UPDATE CASCADE` means when the primary key (either integer or varchar) of the parent record is updated, it is also updated in the related children records.

`SET NULL` will simply set foreign key to `NULL` when the parent record is updated or deleted.

**Example**
```sql
CREATE TABLE employees (
    employee_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES departments(dept_id)
    ON DELETE SET NULL
    ON UPDATE CASCADE
);
```
In this example, if the department is deleted, the `dept_id` value for all employees will be set to NULL. If the `dept_id` primary key (can be either int or varchar) is updated in its parent table, it will cascade update the `dept_id` foreign key to all related employees.

**Relationship Example**
```
DEPARTMENTS                      EMPLOYEES
+---------------+                +------------------+
| dept_id (PK)  |-------|-------<| employee_id (PK) |
| dept_name     |                | first_name       |
| manager_id    |                | last_name        |
| location      |                | dept_id (FK)     |
+---------------+                | manager_id (FK)  |
       |                         +------------------+
       |                                 |
       |                                 |
       v                                 v
PROJECTS                        EMPLOYEE_PROJECTS
+------------------+            +------------------+
| project_id (PK)  |            | employee_id (FK) |
| project_name     |            | project_id (FK)  |
| dept_id (FK)     |            | role             |
| start_date       |            | assignment_date  |
| end_date         |            | hours_allocated  |
+------------------+            +------------------+
```
In this diagram, there is a **one-to-many** relationship between departments and employees. A **self-referencing** relationship in `employees` table so that an employee can be a manager of another employee. The `employee_projects` pivot table is created to implment **many-to-many** relationship between employees and their projects.

## Summary

We have covered -
* The three main types of relationships in a relational database. one-to-one, one-to-many and many-to-many.
* How to implement each type of relationship using primary and foreign keys.
* Self-referencing relationship where records can be related to each other in the same table.
* Integrity constraints to maintain consistency

## Resources
- [Visual Guide to SQL Joins](https://blog.codinghorror.com/a-visual-explanation-of-sql-joins/)
- [Database Relationships Explained](https://www.ibm.com/docs/en/informix-servers/14.10?topic=design-relationships-between-tables)
- [Entity-Relationship Model](https://en.wikipedia.org/wiki/Entity%E2%80%93relationship_model)
- [MySQL Documentation on Foreign Keys](https://dev.mysql.com/doc/refman/8.0/en/create-table-foreign-keys.html)

## Exercises

1. If your organization/institution already has an existing database, please identify an example of one-to-one, one-to-many and many-to-many relationships from this.
2. Imagine a department record in your database is going to be deleted. Which `ON DELETE` action would you like to happen for the foreign key of the department to be deleted? And why?
3. How would you modify the employees table to store both a direct supervisor and a project supervisor for each employee? (There's no solid answer for this. Just to brinstorm your ideas.)
