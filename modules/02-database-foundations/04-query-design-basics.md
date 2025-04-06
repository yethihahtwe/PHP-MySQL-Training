# Query Design Basics

## Introduction to Database Queries

Database queries are requests for information from a database. Well-designed queries are essential for extracting meaningful insights from your data, generating reports, and supporting operations. In this lesson, we'll focus on the fundamentals of query design before diving into SQL syntax in future lessons.

## Purpose of Queries

Queries serve multiple purposes in a database system:

1. **Data Retrieval**: Extracting specific information
2. **Data Analysis**: Aggregating and summarizing data
3. **Data Manipulation**: Adding, updating, or deleting data
4. **Data Definition**: Creating or modifying database structures

For JRS, queries might be used to:
- Generate reports on services provided in a specific time period
- Identify clients who haven't received services recently
- Calculate metrics for program effectiveness
- Update client information when their status changes

## Query Planning Process

Effective query design follows a structured approach:

### 1. Define Information Requirements

Start by clearly defining what information you need:
- What specific data are you looking for?
- What conditions or filters should be applied?
- How should the results be organized or grouped?
- What calculations or transformations are needed?

**Example**: For a monthly report on JRS services, you might need:
- Number of clients served by each program
- Demographic breakdown of clients
- Comparison with previous month's figures

### 2. Identify Required Data Sources

Determine which tables contain the data you need:
- Which entities are involved?
- What relationships connect these entities?
- Are there any lookup tables needed for reference data?

**Example**: For the monthly report, you might need:
- Clients table (for demographic information)
- Programs table (for program details)
- Enrollments table (for relating clients to programs)
- Services table (for service delivery information)

### 3. Define Relationships and Joins

Determine how the tables should be connected:
- Which keys link the tables?
- What type of join is needed (inner, left, right, full)?
- Are multiple joins required?

**Example**: For the monthly report, you might need to:
- Join Clients and Enrollments on client_id
- Join Enrollments and Programs on program_id
- Join Enrollments and Services on enrollment_id

### 4. Specify Filtering Conditions

Define criteria to filter the data:
- Which records should be included or excluded?
- What date ranges are relevant?
- Are there specific categories to focus on?

**Example**: For the monthly report, you might filter:
- Services delivered in the current month
- Active clients only
- Specific program categories

### 5. Determine Output Structure

Define how the results should be structured:
- Which columns should be included?
- How should the data be sorted?
- Are any groupings or aggregations needed?

**Example**: For the monthly report, you might structure results:
- Grouped by program type
- Sorted by number of clients served (descending)
- Including counts, averages, and percentages

## Types of Queries

Understanding different query types helps you choose the right approach for your needs:

### Select Queries

Select queries retrieve data without modifying it. They're the most common type and form the foundation of data analysis.

**Components of a select query**:
- Table(s) to retrieve data from
- Columns to display
- Conditions for filtering
- Sort order

**Example structure**:
```
SELECT [columns]
FROM [tables]
WHERE [conditions]
GROUP BY [grouping columns]
HAVING [group conditions]
ORDER BY [sort order]
```

### Action Queries

Action queries modify data or database structure:

- **Insert queries**: Add new records
- **Update queries**: Modify existing records
- **Delete queries**: Remove records
- **Create/Alter Table queries**: Modify database structure

### Simple vs. Complex Queries

Queries range from simple to complex:

**Simple queries**:
- Single table
- Basic filtering
- No calculations or aggregations

**Complex queries**:
- Multiple tables with joins
- Advanced filtering
- Calculations and aggregations
- Subqueries or nested logic

## Designing Query Parameters

Parameters make queries flexible and reusable:

- **Date ranges**: For time-based filtering
- **Status values**: For filtering by status
- **IDs or codes**: For entity-specific queries
- **Search terms**: For text-based searches

**Example**:
Instead of hardcoding a date range like:
```
WHERE service_date BETWEEN '2025-01-01' AND '2025-03-31'
```

Design a parametrized query like:
```
WHERE service_date BETWEEN {start_date} AND {end_date}
```

This allows the same query to be reused with different date ranges.

## Query Performance Considerations

Even at the design stage, consider how your query will perform:

### 1. Data Volume

Consider how much data your query will process:
- Full table scans are expensive for large tables
- Retrieving only necessary columns reduces data transfer
- Limit result sets when possible

### 2. Join Complexity

Joins can impact performance:
- Each join adds processing overhead
- Join order affects performance
- Join types (inner vs. outer) have different impacts

### 3. Indexing Strategy

Indexes dramatically affect query performance:
- Filtering on indexed columns is efficient
- Sorting on indexed columns is faster
- Indexes should align with common query patterns

### 4. Aggregation Overhead

Aggregations (COUNT, SUM, AVG) require additional processing:
- Pre-aggregated tables may improve performance for complex reports
- Consider materialized views for frequent complex aggregations

## Common Query Patterns for JRS Database

Understanding common query patterns helps you design effective queries for specific needs:

### 1. Client Lookup

Pattern for finding specific client information:
```
Retrieve client details WHERE client_id, name, or other identifier matches a parameter
```

### 2. Service History

Pattern for retrieving a client's service history:
```
Retrieve service records WHERE client_id matches parameter
ORDER BY service_date DESC
```

### 3. Periodic Reporting

Pattern for generating periodic reports:
```
Retrieve service counts GROUP BY program, service type, etc.
WHERE service_date is within reporting period
```

### 4. Status Monitoring

Pattern for monitoring client status:
```
Retrieve clients WHERE last_service_date is older than threshold
OR status equals specific value
```

### 5. Demographic Analysis

Pattern for analyzing client demographics:
```
Count clients GROUP BY demographic category (age_group, nationality, etc.)
Calculate percentages of total
```

## Entity-Relationship (ER) Diagrams and Query Design

ER diagrams are powerful tools for query design:

- They visualize the relationships between tables
- They help identify the tables needed for a query
- They show the keys used for joining tables
- They illustrate the cardinality of relationships

When designing a query, referring to the ER diagram helps ensure you:
- Include all necessary tables
- Join tables correctly
- Understand potential data multiplications from joins

## Practical Example: Designing a Query for JRS

Let's design a query to find all clients who received services in the past month, along with their case managers and the types of services received.

### Step 1: Define Information Requirements
- Client names
- Case manager names
- Service types received
- Service dates
- Limited to the past month

### Step 2: Identify Required Data Sources
- Clients table (for client information)
- Staff table (for case manager information)
- Services table (for service details)
- Service_delivery table (for relating clients, services, and dates)

### Step 3: Define Relationships and Joins
- Join Clients and Service_delivery on client_id
- Join Staff and Clients on staff_id
- Join Services and Service_delivery on service_id

### Step 4: Specify Filtering Conditions
- Service date within the past month

### Step 5: Determine Output Structure
- Group by client and service type
- Sort by client name, then service date

### Resulting Conceptual Query
```
Retrieve
    client first and last name,
    case manager first and last name,
    service type,
    service date
From
    Clients, Staff, Services, Service_delivery
Where
    Clients and Service_delivery are linked by client_id
    Staff and Clients are linked by staff_id
    Services and Service_delivery are linked by service_id
    Service date is within the past month
Group by
    client, service type
Order by
    client name, service date
```

This conceptual query can then be translated into actual SQL, which we'll cover in upcoming lessons.

## Summary

In this lesson, we've covered:
- The purpose and types of database queries
- A structured process for query design
- Considerations for query parameters and performance
- Common query patterns relevant to JRS
- Using ER diagrams in query design
- A practical example of designing a query for JRS

Effective query design begins with clearly understanding the information needs and the database structure. By following a systematic approach to query design, you can create queries that efficiently retrieve the needed information while maintaining good performance.

## Resources
- [Database Query Design Best Practices](https://www.sisense.com/blog/8-ways-fine-tune-sql-queries-production-databases/)
- [Visual Query Designer Techniques](https://docs.microsoft.com/en-us/visualstudio/data-tools/visual-database-tools/designing-queries-and-views-how-to-topics-visual-database-tools)
- [Query Performance Tuning](https://use-the-index-luke.com/)

## Exercises
1. For a specific information need at JRS (e.g., "Which clients from Myanmar received legal services in the past quarter?"), follow the query design process to outline the tables, relationships, filters, and output structure needed.

2. Review the current JRS database structure and identify three common queries that might be useful for staff. For each query, specify what information would be retrieved and why it would be valuable.

3. For one of the queries identified in Exercise 2, sketch an ER diagram showing the tables involved and how they would be joined.

4. Consider a reporting need at JRS (e.g., monthly service statistics by nationality). Design a parametrized query approach that would allow staff to generate this report for different time periods and demographic filters.
