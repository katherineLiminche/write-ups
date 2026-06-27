# Lab: Reflected XSS into a JavaScript string with single quote and backslash escaped

## Goal
 - To solve this lab, perform a cross-site scripting attack that breaks out of the JavaScript string and calls the alert function.

## Enumeration
 - This lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality. The reflection occurs inside a JavaScript string with single quotes and backslashes escaped.

## Testing
 - It was not possible to break out of the JavaScript string using single quotes or backslashes.

## Exploitation
 Final payload:
```
</script><script>alert()</script>
```
First, we close the existing <script> element. Then, we inject a new <script> element that executes alert().

## Root cause
The application escapes characters within the JavaScript string but fails to prevent injection of the closing </script> tag. As a result, an attacker can terminate the existing script block and inject a new one.

## Remediation
 - Escape the </script> sequence when embedding user input inside JavaScript (for example, by escaping the forward slash or using Unicode escapes).
 - Apply context-aware output encoding based on where the data is inserted.
 - Avoid placing untrusted user input directly inside inline JavaScript whenever possible.
 - Use a Content Security Policy (CSP) to reduce the impact of XSS vulnerabilities.