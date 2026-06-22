# Lab: SQL injection UNION attack, retrieving data from other tables

## Goal
 - Log in as the administrator user.

## Enumeration
 - This lab contains a simple sqli in the category functionality.
 - This is error-based sqli.
 - I can break slq query by typing '.
 - There are 'users' table available.

## Testting
 - There are two parameters in query so I can use exactly two parameters in UNION attack.
 - Found username 'administrator' and password from 'users' table

## Exploitation
 final payload:
 ```
  category=Pets' UNION SELECT username, password FROM users-- 
 ```

## Root cause
 - The application constructs SQL queries using unsanitized user input.

## Remediation 
 - Avoid dynamic SQL query construction.
 - Validate input where appropriate.