# SQL Injection Vulnerability in WHERE Clause Allowing Retrieval of Hidden Data

## Objective
The goal of this lab was to identify a SQL Injection vulnerability and use it to view hidden data from the application.

---

## What I Observed
I noticed that the website was filtering products using a category parameter in the URL.

This made me think that the input might be connected to a database query.

---

## Initial Testing
I started testing simple characters to check the application behavior.

First, I used:

```sql
'
After adding this character, the application response changed, which indicated that the input might not be properly filtered.

Problem Faced

At first, I was confused about how the backend query was working.

I also did not know which payload would successfully change the query logic without causing errors.

Exploitation

After testing different payloads, I used:
