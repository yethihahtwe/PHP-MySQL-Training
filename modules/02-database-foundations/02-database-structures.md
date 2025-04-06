# Database Structures

## Components of a database

### Tables

Tables are the primary storage components in relational databases. A table as similar to a spreadsheet. Each table stores information about an entity (e.g., clients, services, staff). Tables are composed of rows and columns.

Example of a simple CLIENT table:

| client_id | first_name | last_name | date_of_birth | nationality | status    |
|-----------|------------|-----------|---------------|-------------|-----------|
| 1         | John       | Doe       | 1985-03-15    | Myanmar     | Active    |
| 2         | Jane       | Smith     | 1990-07-22    | Syria       | Pending   |
| 3         | Ahmed      | Hassan    | 1978-11-30    | Somalia     | Completed |

### Columns (Fields)

Columns, also known as fields, define the properties of the entity. Each column has a name (e.g., first_name, date_of_birth) and has a specific data type (e.g., integer, varchar, date). Columns may have constraints that limit what data can be stored.

### Rows (Records)

Rows, also called records, contain the actual data. Each row represents one record of the entity (e.g., one client). Rows must follow the structure defined by the columns. Each row has a unique identifier.

### Data Types

Every column in a database table must have a specified data type. Common MySQL data types are -

| Data Type Category | Examples | Use Cases |
|--------------------|----------|-----------|
| Numeric | INT, DECIMAL, FLOAT | Client IDs, ages, financial amounts |
| String | VARCHAR, TEXT, CHAR | Names, addresses, descriptions |
| Date and Time | DATE, DATETIME, TIMESTAMP | Birth dates, appointment times |
| Boolean | BOOLEAN (TINYINT(1)) | Active status, eligibility flags |
| Binary | BLOB, BINARY | Documents, images (though often stored outside DB) |

> The difference between FLOAT and DECIMAL is that DECIMAL stores exact values (ideal for financial data where precision is important), while FLOAT stores approximate values and is more efficient for scientific calculations where absolute precision is less important.

> CHAR has fixed length and is faster for short strings of consistent size, VARCHAR allows variable length up to a maximum and saves space, while TEXT is for large variable-length content with no practical size limit but slower performance.

Choosing the right data type is important for **Data integrity**, **Storage efficiency** and **Query performance**.

## Keys: The Foundation of Relationships

Keys are special fields that uniquely identify records and establish relationships between tables.

### Primary Keys

A primary key uniquely identifies each record in a table:

- No two rows can have the same primary key value
- Primary keys cannot contain NULL values
- A table can have only one primary key (though it can consist of multiple columns)
- Common primary keys include IDs or codes

Example:
```sql
CREATE TABLE clients (
    client_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL
);
```

In this example, `client_id` is the primary key that uniquely identifies each client.

### Foreign Keys

Foreign keys establish relationships between tables:

- A foreign key in one table refers to a primary key in another table
- Foreign keys enforce referential integrity
- They prevent orphaned records (records with references to non-existent data)

Example:
```sql
CREATE TABLE appointments (
    appointment_id INT AUTO_INCREMENT PRIMARY KEY,
    client_id INT NOT NULL,
    appointment_date DATETIME NOT NULL,
    FOREIGN KEY (client_id) REFERENCES clients(client_id)
);
```

Here, `client_id` in the appointments table is a foreign key that references the `client_id` primary key in the clients table.

### Composite Keys

Sometimes, a single column isn't enough to uniquely identify a record. In such cases, we use composite keys:

- A composite key consists of two or more columns
- The combination of these columns must be unique for each record

Example:
```sql
CREATE TABLE enrollment (
    program_id INT,
    client_id INT,
    enrollment_date DATE,
    PRIMARY KEY (program_id, client_id),
    FOREIGN KEY (program_id) REFERENCES programs(program_id),
    FOREIGN KEY (client_id) REFERENCES clients(client_id)
);
```

In this table, neither `program_id` nor `client_id` alone can be a primary key, but their combination is unique.

## Database Schema Design

A database schema is the blueprint of your database structure. Proper schema design is crucial for database performance, data integrity, and future scalability.

### Normalization

Normalization is the process of organizing data to minimize redundancy:

- **First Normal Form (1NF)**: Eliminate repeating groups and create separate tables for each set of related data
- **Second Normal Form (2NF)**: Meet 1NF requirements and ensure all non-key attributes depend on the entire primary key
- **Third Normal Form (3NF)**: Meet 2NF requirements and ensure all attributes depend directly on the primary key

Benefits of normalization:
- Reduces data redundancy
- Improves data integrity
- Makes the database more flexible for queries

### Denormalization

Sometimes, we intentionally denormalize (add redundancy) for performance reasons:

- Can improve read performance by reducing joins
- Useful for reporting databases or data warehouses
- Trade-off between data integrity and performance

### JRS Database Example

Let's consider how we might structure part of the JRS database:

```
CLIENTS                           SERVICES
+-----------------+               +------------------+
| client_id (PK)  |               | service_id (PK)  |
| first_name      |               | service_name     |
| last_name       |               | description      |
| date_of_birth   |               | duration         |
| nationality     |               +------------------+
| status          |                        ^
+-----------------+                        |
        ^                                  |
        |                                  |
        |      SERVICE_DELIVERY            |
        +----> +---------------------+ <---+
               | delivery_id (PK)    |
               | client_id (FK)      |
               | service_id (FK)     |
               | delivery_date       |
               | staff_id (FK)       |
               | notes               |
               +---------------------+
                        |
                        v
                    STAFF
               +------------------+
               | staff_id (PK)    |
               | first_name       |
               | last_name        |
               | position         |
               | email            |
               +------------------+
```

This schema demonstrates:
- Primary keys (PK) that uniquely identify each record
- Foreign keys (FK) that establish relationships
- Tables organized by entity type
- Normalized structure to minimize redundancy

## Indexes

Indexes improve the speed of data retrieval operations:

- Similar to an index in a book
- Increases read performance, but may slow down writes
- Should be created on columns frequently used in WHERE clauses, joins, and sorting

Types of indexes:
- **Primary key index**: Automatically created for primary keys
- **Unique index**: Ensures all values in a column are unique
- **Composite index**: Index on multiple columns
- **Full-text index**: For text searching

Example:
```sql
CREATE INDEX idx_client_nationality ON clients(nationality);
```

This creates an index on the nationality column to speed up queries that filter by nationality.

## Constraints

Constraints enforce rules on data to maintain integrity:

- **NOT NULL**: Ensures a column cannot have NULL values
- **UNIQUE**: Ensures all values in a column are distinct
- **CHECK**: Ensures values meet specified conditions
- **DEFAULT**: Provides a default value when none is specified
- **FOREIGN KEY**: Ensures referential integrity

Example:
```sql
CREATE TABLE clients (
    client_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    age INT CHECK (age >= 0),
    registration_date DATE DEFAULT CURRENT_DATE
);
```

## Summary

In this lesson, we've covered:
- The fundamental structures of relational databases (tables, columns, rows)
- Different data types and when to use them
- The importance of keys in establishing relationships and ensuring data integrity
- Basic principles of database schema design
- How indexes can improve query performance
- Constraints that help maintain data integrity

Understanding these structures will help you design and interact with databases effectively, making it easier to manage and retrieve the information needed for JRS operations.

## Resources
- [Database Normalization Explained](https://www.essentialsql.com/get-ready-to-learn-sql-database-normalization-explained-in-simple-english/)
- [MySQL Data Types](https://dev.mysql.com/doc/refman/8.0/en/data-types.html)
- [Database Indexing Strategies](https://use-the-index-luke.com/)

## Exercises
1. Identify three entities (tables) that might exist in the JRS database and list potential columns for each.
2. For each table identified in Exercise 1, determine appropriate primary keys and any potential foreign keys.
3. Choose appropriate data types for 5 different pieces of information that JRS might collect about clients.
4. Consider a table that stores client case notes. What indexes might improve performance when searching through this data?
