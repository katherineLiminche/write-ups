# Lab: Reflected XSS in canonical link tag

## Goal
 - To solve the lab, perform a cross-site scripting attack on the home page that injects an attribute that calls the alert function.

## Enumeration
 - The application reflects user-controlled input from the URL into the href attribute.

## Testing
 - I was able to break out of the href attribute by injecting a single quote (').
 - After escaping the attribute, I was able to inject additional HTML attributes.

## Exploitation
 Final payload:
```
Https://.../?'accesskey='x'onclick='alert()
```
After typing 'x' onclick will execute alert()

## Root cause
 - User-controlled input is reflected into an HTML attribute without proper escaping.

## Remediation
 - Properly escape user input before inserting it into HTML attributes.
