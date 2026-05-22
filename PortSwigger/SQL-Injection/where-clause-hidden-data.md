# SQL Injection Lab: WHERE Clause Allowing Retrieval of Hidden Data

## Objective
The objective of this lab was to exploit a SQL Injection vulnerability in the WHERE clause of a product filtering feature in order to retrieve hidden data from the database.

---

## What is Happening in the Lab
The application contains a product filter (such as category selection).  
When a user selects a category, the application sends this value to the backend database query.

Example of normal query:

'''sql id="sqlnormal"
SELECT * FROM products WHERE category = 'food'

This query returns only products from the selected category.

## Vulnerability

The application directly uses user input inside the SQL query without proper validation or sanitization.

This leads to a SQL Injection vulnerability, where an attacker can manipulate the query structure.

## Testing

I tested the input field by inserting a single quote:

'

The application response changed, indicating that the input was being processed inside a SQL query.

This confirmed a possible SQL injection point.

## Exploitation

I used a boolean-based SQL injection payload:

' OR 1=1--

This payload modifies the SQL query logic:

' breaks the original query string
OR 1=1 makes the condition always true
-- comments out the rest of the query

## Result

The modified query returns all records from the database instead of only the selected category.

As a result, hidden products that were not normally visible were displayed.

## Impact
Unauthorized access to hidden data
Exposure of sensitive database content
Potential for further exploitation in real-world applications

## Mitigation
Use parameterized queries (prepared statements)
Properly validate and sanitize user input
Avoid directly concatenating user input into SQL queries
Apply least privilege access to the database

## Learning Outcome
Understood how SQL Injection works in WHERE clauses
Learned basic boolean-based SQL injection technique
Practiced identifying and exploiting vulnerable input parameters
Gained understanding of secure database query handling
