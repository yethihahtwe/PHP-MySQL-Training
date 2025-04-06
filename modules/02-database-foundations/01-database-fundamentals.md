# Database Fundamentals

## What is a Database?

A database is an organized collection of structured information or data, typically stored electronically in a computer system. Databases are designed to efficiently store, retrieve, and manage data, making them essential components of modern information systems.

### Key Characteristics of Databases

| Characteristics | Description |
|--|--|
| **Organized structure** | Data is arranged systematically |
| **Persistent storage** | Data persists beyond program execution |
| **Efficient retrieval** | Optimized for quick data access |
| **Data integrity** | Rules to maintain accuracy and consistency |
| **Concurrent access** | Multiple users can access data simultaneously |
| **Security** | Controls for who can view or modify data |

## Why Use Databases?

Before databases, file-based systems were used to store data, which had significant limitations.

| File-Based Systems | Database Systems |
|-------------------|------------------|
| Data redundancy and inconsistency | Minimal redundancy |
| Difficult data access | Efficient data retrieval |
| Limited data sharing | Concurrent access |
| No integrity constraints | Enforced data integrity |
| Security issues | Robust security features |
| No recovery mechanisms | Backup and recovery tools |

> Data redundancy is storing the same piece of information in multiple places inside the same system. When an information is updated, it would require to update in every other places.

Database systems are implemented as they're able to maintain accurate records, generate reports for stakeholders and support in decision making processes.

## Types of Databases

### 1. Relational Databases (RDBMS)

Relational databases store data in table formats with relationships. They use Structured Query Language (SQL) for defining and handling the data. Examples include MySQL, MariaDB, PostgreSQL, Oracle, Microsoft SQL Server.

In relational databases, data is organized in tables (like rows and columns on a spreadsheet). Tables can be related to each other (like two spreadsheets can be linked together). SQL is used to get desired results from tables (like we use formula in Excel or Google sheet).

### 2. NoSQL Databases

NoSQL ("Not only SQL") databases store and retrieve data in a different way. NoSQL databases include **Document databases** which stores data in JSON-like documents (e.g. MongoDB), **Key-value stores** with simple key-value pairs (Redis, DynamoDB), **Wide-column stores** which stores data in tables with dynamic columns (Cassandra, HBase), **Graph databases** representing data as nodes and edges (Neo4j, Amazon Neptune).

> MySQL is suitable for web applications and is the database system most commonly used with PHP 

## Database Management Systems (DBMS)

A Database Management System is software that interacts with the database, applications, and users to capture and analyze data. Using a DBMS, we can create new databases, store data in the database, modify existing data, retrieve data with queries, manage database security and handle database transactions. MySQL is a DBMS we'll be using throughout this training.

## Practical Example

```
CLIENT DATABASE
+-----------------+        +-------------------+        +------------------+
| CLIENTS         |        | SERVICES          |        | APPOINTMENTS     |
+-----------------+        +-------------------+        +------------------+
| client_id (PK)  |<------>| service_id (PK)   |<------>| appointment_id   |
| first_name      |        | service_name      |        | client_id (FK)   |
| last_name       |        | description       |        | service_id (FK)  |
| date_of_birth   |        | duration          |        | date_time        |
| nationality     |        | staff_required    |        | status           |
| status          |        | active            |        | notes            |
+-----------------+        +-------------------+        +------------------+
```

In this example -
- The CLIENTS table stores information about clients.
- The SERVICES table contains different services provided by the institution.
- The APPOINTMENTS table tracks when clients receive services

## Summary

In this lesson, we've covered -
* What are databases and why they're important
* The advantages of database systems over file-based systems
* Various types of databases with a focus on relational databases
* Introduction to MySQL as our DBMS of choice

## Resources
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [W3Schools SQL Tutorial](https://www.w3schools.com/sql/)

## Exercises
1. List three types of data that you currently collects that would benefit from being stored in a database.
2. Identify two challenges that might occur if you used file-based storage (like Excel spreadsheets) instead of a database.
