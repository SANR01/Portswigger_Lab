# SQL Injection: Oracle Database Version Extraction using UNION

## Objective
The objective of this lab was to exploit a SQL Injection vulnerability in a product category filter to determine the number of columns in the query and extract the Oracle database version using a UNION-based SQL Injection attack.


## Lab Overview
The application contains a product filter feature where the `category` parameter is passed directly into a backend SQL query.

This query is vulnerable to SQL Injection, allowing manipulation using UNION SELECT statements.


## Recon (Request Interception)
Using Burp Suite, I intercepted the request that sets the product category filter.

I modified the `category` parameter to test SQL injection behavior.


## Problem Faced

Initially, it was unclear: <br>
- How many columns the original SQL query was returning
- Which columns could display text data

Without this information, a UNION-based injection could fail.


## Determining Number of Columns
To identify the correct number of columns and text compatibility, I used a test payload:

sql id="coltest"
'+UNION+SELECT+'abc','def'+FROM+dual--

## Observation:
The application accepted the payload <br>
It confirmed that the query returns 2 columns <br>
Both columns support text data

## Exploitation (Database Version Extraction)

After confirming the column structure, I extracted the Oracle database version using:

'+UNION+SELECT+BANNER,+NULL+FROM+v$version--

## Explanation:

BANNER → contains Oracle version information <br>
NULL → placeholder for second column <br>
v$version → Oracle system view containing version details

## Result

The application successfully returned the Oracle database version in the response, confirming:

SQL Injection vulnerability <br>
Oracle database backend <br>
Successful UNION-based data extraction

## Impact

Database fingerprinting (type and version exposure) <br>
Increased risk of targeted exploitation <br>
Information disclosure of internal system details

## Mitigation
Use parameterized queries (prepared statements) <br>
Restrict access to database metadata views <br>
Avoid direct string concatenation in SQL queries <br>
Implement proper input validation and output encoding

## Learning Outcome
Learned UNION-based SQL Injection technique <br>
Understood how to determine column count in SQL queries <br>
Practiced Oracle-specific database version extraction <br>
Improved Burp Suite interception and request manipulation skills
