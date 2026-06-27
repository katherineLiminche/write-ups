# Lab: Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped

## Goal
 - To solve this lab, perform a cross-site scripting attack that breaks out of the JavaScript string and calls the alert function.

## Enumeration
This lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality where angle brackets and double are HTML encoded and single quotes are escaped.

## Testting
 - A single quote (') is escaped as \', preventing a direct breakout from the JavaScript string.
 - By injecting a backslash before the single quote (\'), I was able to escape the escape character, allowing the following single quote to terminate the string.

## Exploitation
 final payload:
 ```
  \' - alert() //
 ```
First we escaped string and then concatenate alert. Then comment other.

## Root cause
User-controlled input is inserted into a JavaScript string without sufficient context-aware escaping. Although some characters are escaped, the escaping mechanism can be bypassed, allowing JavaScript injection.

## Remediation 
 - Use context-aware output encoding when inserting user input into JavaScript.
 - Avoid embedding untrusted user input directly into inline JavaScript.