# Lab: Stored XSS into anchor href attribute with double quotes HTML-encoded

## Goal
 - To solve this lab, submit a comment that calls the *alert* function when the comment author name is clicked.

## Enumeration
 - double quotes encoded, so I need to find a way to escape the double quotes.

## Testing
 - I can't escape by encoding double quotes like %22. However I can use "javascript:alert()" to call an *alert()*

## Exploitation
 Final payload:
```
javascript:alert()
```

## Root cause
 - Unsafe URI schemes are allowed in the href attribute.

## Remediation
 - be aware to link feature
 - properly validate any input
