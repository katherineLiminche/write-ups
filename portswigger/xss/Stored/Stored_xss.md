# Lab: Stored XSS into HTML context with nothing encoded

## Goal
 - To solve this lab, submit a comment that calls the alert function when the blog post is viewed.

## Enumeration
 - This lab contains a stored cross-site scripting vulnerability in the comment functionality.
 - User input submitted through the comment form is stored and displayed in the comments section.

## Testing
 - HTML tags are interpreted by the browser rather than displayed as plain text.
```
<h1>Hi!<h1/>
```
Result "Hi!" Is header now in comment section

## Exploitation
 Final payload:
```
<img src=1 onerror='alert()'>
```
The image source points to a non-existent resource, causing the onerror event handler to execute.

## Root cause
 - User-controlled input is rendered in an HTML context without proper output encoding.

## Remediation
 - Apply context-aware output encoding.
 - Sanitize untrusted HTML content.