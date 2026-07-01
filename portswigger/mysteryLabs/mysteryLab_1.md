# Mystery Lab

## Goal
 - Find and exploit SQLi.

## Enumeration
 - The application is vulnerable to a UNION-based SQL injection in the stock feature.

## Testting
 - The database is resistant to obvious attacks.
 - Hackvertor successfully hide attack.
 - Only one parameter is available.
 - There are *users* table.
 - There are username and password columns.

## Exploitation
 I have only one parameter to display, so I will concatenate two columns in one.
 final payload:
 ```
  1 UNION SELECT username || '~' || password FROM users 
 ```

## Root cause
 - The application constructs SQL queries using unsanitized user input.

## Remediation 
 - Avoid dynamic SQL query construction.
 - Validate input where appropriate.