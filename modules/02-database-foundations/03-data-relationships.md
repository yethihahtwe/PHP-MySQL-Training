# Data Relationships

## Understanding Data Relationships

In relational databases, relationships between tables are crucial for maintaining data structure and integrity. These relationships define how data in one table relates to data in another table, allowing you to:

- Eliminate data redundancy
- Maintain data integrity
- Efficiently retrieve related information
- Model real-world connections between entities

## Types of Relationships

There are three primary types of relationships in relational databases:

1. One-to-One (1:1)
2. One-to-Many (1:N)
3. Many-to-Many (M:N)

Let's explore each type in detail, with examples relevant to the JRS context.

### One-to-One (1:1) Relationships

In a one-to-one relationship, each record in the first table corresponds to exactly one record in the second table, and vice versa.

**Characteristics:**
- Relatively uncommon
- Often used to separate sensitive data or to split a table with many columns
- Implemented using primary and foreign keys, often with unique constraints

**Example in JRS Context:**
A client might have one detailed medical record, and each medical record belongs to only one client.

```
CLIENTS                         MEDICAL_RECORDS
+----------------+              +-------------------+
| client_id (PK) |<----------->| record_id (PK)    |
| first_name     |              | client_id (FK,UQ) |
| last_name      |              | medical_history   |
| date_of_birth  |              | allergies         |
| ...            |              | medications       |
+----------------+              | ...               |
                                +-------------------+
```

*Implementation:*
```sql
CREATE TABLE clients (
    client_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    date_of_birth DATE
);

CREATE TABLE medical_records (
    record_id INT AUTO_INCREMENT PRIMARY KEY,
    client_id INT UNIQUE,
    medical_history TEXT,
    allergies TEXT,
    medications TEXT,
    FOREIGN KEY (client_id) REFERENCES clients(client_id)
);
```

Note the `UNIQUE` constraint on `client_id` in the `medical_records` table, ensuring each client has only one medical record.

### One-to-Many (1:N) Relationships

In a one-to-many relationship, each record in the first table can be related to multiple records in the second table, but each record in the second table is related to only one record in the first table.

**Characteristics:**
- Most common type of relationship
- Implemented by placing the primary key of the "one" side as a foreign key on the "many" side

**Example in JRS Context:**
A case manager (staff member) might handle multiple clients, but each client is assigned to only one case manager.

```
STAFF                           CLIENTS
+---------------+               +------------------+
| staff_id (PK) |<------------->| client_id (PK)   |
| first_name    |               | first_name       |
| last_name     |               | last_name        |
| position      |               | date_of_birth    |
| ...           |               | staff_id (FK)    |
+---------------+               | ...              |
                                +------------------+
```

*Implementation:*
```sql
CREATE TABLE staff (
    staff_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    position VARCHAR(100)
);

CREATE TABLE clients (
    client_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    date_of_birth DATE,
    staff_id INT,
    FOREIGN KEY (staff_id) REFERENCES staff(staff_id)
);
```

In this example, `staff_id` in the `clients` table is a foreign key referencing the `staff_id` primary key in the `staff` table.

### Many-to-Many (M:N) Relationships

In a many-to-many relationship, each record in the first table can be related to multiple records in the second table, and vice versa.

**Characteristics:**
- Requires a junction (or bridge) table to implement
- The junction table typically contains the primary keys from both related tables as foreign keys
- May include additional attributes specific to the relationship

**Example in JRS Context:**
Clients might participate in multiple services/programs, and each service/program can have multiple clients.

```
CLIENTS                     ENROLLMENTS                  PROGRAMS
+---------------+           +-----------------+          +---------------+
| client_id (PK)|<--------->| client_id (FK)  |<-------->| program_id (PK)|
| first_name    |           | program_id (FK) |          | program_name  |
| last_name     |           | start_date      |          | description   |
| ...           |           | end_date        |          | ...           |
+---------------+           | status          |          +---------------+
                            +-----------------+
```

*Implementation:*
```sql
CREATE TABLE clients (
    client_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL
);

CREATE TABLE programs (
    program_id INT AUTO_INCREMENT PRIMARY KEY,
    program_name VARCHAR(100) NOT NULL,
    description TEXT
);

CREATE TABLE enrollments (
    client_id INT,
    program_id INT,
    start_date DATE NOT NULL,
    end_date DATE,
    status VARCHAR(20),
    PRIMARY KEY (client_id, program_id),
    FOREIGN KEY (client_id) REFERENCES clients(client_id),
    FOREIGN KEY (program_id) REFERENCES programs(program_id)
);
```

In this example, `enrollments` is a junction table that contains foreign keys to both the `clients` and `programs` tables, along with additional attributes specific to the enrollment relationship.

## Self-Referencing Relationships

Sometimes, records in a table can be related to other records in the same table. This is known as a self-referencing relationship.

**Example in JRS Context:**
Family relationships among clients. A client might be related to other clients (spouse, child, parent, etc.).

```
CLIENTS
+---------------+
| client_id (PK)|
| first_name    |
| last_name     |
| ...           |
+---------------+
        ^
        |
        |
CLIENT_RELATIONSHIPS
+------------------+
| relationship_id  |
| client_id1 (FK)  |
| client_id2 (FK)  |
| relationship_type|
+------------------+
```

*Implementation:*
```sql
CREATE TABLE clients (
    client_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL
);

CREATE TABLE client_relationships (
    relationship_id INT AUTO_INCREMENT PRIMARY KEY,
    client_id1 INT,
    client_id2 INT,
    relationship_type VARCHAR(50),
    FOREIGN KEY (client_id1) REFERENCES clients(client_id),
    FOREIGN KEY (client_id2) REFERENCES clients(client_id)
);
```

## Cardinality and Modality

When discussing relationships, two important concepts are cardinality and modality:

### Cardinality

Cardinality refers to the numerical relationship between two entities:

- **One-to-one (1:1)**: Each entity in the first table corresponds to exactly one entity in the second table
- **One-to-many (1:N)**: Each entity in the first table corresponds to multiple entities in the second table
- **Many-to-many (M:N)**: Multiple entities in the first table correspond to multiple entities in the second table

### Modality

Modality refers to whether a relationship is required or optional:

- **Mandatory**: The relationship must exist (1 or more)
- **Optional**: The relationship may or may not exist (0 or more)

These concepts are often represented in database diagrams with specific notation.

## Common Notation for Relationships

### Crow's Foot Notation

One of the most common notations for representing database relationships is Crow's Foot:

```
One (1)                 Many (N)
 -----+----             -----<----

Optional (0 or more)    Mandatory (1 or more)
 -----O----             -----|----- 
```

Example of a one-to-many relationship where a staff member can have multiple clients, but each client must have one staff member:

```
STAFF                               CLIENTS
+---------------+                   +------------------+
| staff_id (PK) |-------|-------<---| client_id (PK)   |
| first_name    |                   | first_name       |
| last_name     |                   | last_name        |
| position      |                   | staff_id (FK)    |
+---------------+                   +------------------+
```

## Integrity Constraints for Relationships

To maintain the integrity of relationships, databases use several types of constraints:

### Referential Integrity

Referential integrity ensures that relationships between tables remain consistent. It's enforced through foreign key constraints, which prevent:

- Creating records with references to non-existent records
- Deleting records that have dependent records in related tables

### ON DELETE and ON UPDATE Actions

When defining foreign keys, you can specify actions to take when the referenced record is updated or deleted:

- **CASCADE**: Automatically update or delete related records
- **SET NULL**: Set the foreign key to NULL
- **SET DEFAULT**: Set the foreign key to its default value
- **RESTRICT**: Prevent the update or deletion if related records exist
- **NO ACTION**: Similar to RESTRICT, but checked at the end of the statement

Example:
```sql
CREATE TABLE clients (
    client_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    staff_id INT,
    FOREIGN KEY (staff_id) REFERENCES staff(staff_id)
    ON DELETE SET NULL
    ON UPDATE CASCADE
);
```

In this example:
- If a staff member is deleted, their clients' `staff_id` will be set to NULL
- If a staff member's ID is updated, the change will cascade to all their clients

## Practical Example: JRS Database Relationships

Let's visualize a more comprehensive set of relationships in a JRS database context:

```
STAFF                               CLIENTS
+---------------+                   +------------------+
| staff_id (PK) |-------|-------<---| client_id (PK)   |
| first_name    |                   | first_name       |
| last_name     |                   | last_name        |
| position      |                   | staff_id (FK)    |
+---------------+                   +------------------+
       |                                     |
       |                                     |
       |                                     |
       v                                     v
APPOINTMENTS                      CLIENT_PROGRAMS
+------------------+              +------------------+
| appointment_id   |              | client_id (FK)   |
| staff_id (FK)    |              | program_id (FK)  |
| client_id (FK)   |              | start_date       |
| date_time        |              | end_date         |
| notes            |              | status           |
+------------------+              +------------------+
                                           |
                                           |
                                           v
                                  PROGRAMS
                                  +------------------+
                                  | program_id (PK)  |
                                  | program_name     |
                                  | description      |
                                  | active           |
                                  +------------------+
```

This diagram shows:
- A one-to-many relationship between staff and clients
- A many-to-many relationship between clients and programs (implemented through the client_programs junction table)
- A many-to-many relationship between staff, clients, and appointments

## Summary

In this lesson, we've covered:
- The three main types of relationships in relational databases: one-to-one, one-to-many, and many-to-many
- How to implement each type of relationship using primary and foreign keys
- Self-referencing relationships for connecting records within the same table
- Cardinality and modality concepts
- Common notation for visualizing relationships
- Integrity constraints for maintaining relationship consistency
- A practical example of relationships in a JRS database context

Understanding these relationships is essential for designing a database that accurately reflects real-world connections between entities, maintains data integrity, and supports efficient data retrieval.

## Resources
- [Visual Guide to SQL Joins](https://blog.codinghorror.com/a-visual-explanation-of-sql-joins/)
- [Database Relationships Explained](https://www.ibm.com/docs/en/informix-servers/14.10?topic=design-relationships-between-tables)
- [Entity-Relationship Model](https://en.wikipedia.org/wiki/Entity%E2%80%93relationship_model)

## Exercises
1. For the JRS context, identify one example each of a one-to-one, one-to-many, and many-to-many relationship.
2. Create an entity-relationship diagram (you can draw this on paper) for a simple system that tracks:
   - Clients
   - Services they receive
   - Staff members who provide the services
3. Write SQL statements to create tables for the entities and relationships you identified in Exercise 2.
4. Consider the implications of deleting a staff member record in your database. What ON DELETE action would you choose for foreign keys referencing staff members, and why?
