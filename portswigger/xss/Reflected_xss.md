# Lab: Reflected XSS into HTML context with nothing encoded

## Goal
 - To solve the lab, perform a cross-site scripting attack that calls the alert function.

## Enumeration
 - This lab contains a simple reflected cross-site scripting vulnerability in the search functionality.
 - The search parameter is reflected in the response.

## Testting
 - tag displays like its html code, so I can try to use tags attributes to call alert()

## Exploitation
 final payload:
 ```
  <img src="1" onerror="alert()">
 ```
 it will call alert because scr will call an error.

## Root cause
 - User input is rendered without proper output encoding.

## Remediation 
 - carefully shield input
 - validate user's input