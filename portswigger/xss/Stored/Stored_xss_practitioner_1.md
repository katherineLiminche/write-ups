# Lab: Stored XSS into `onclick` Event with Angle Brackets and Double Quotes HTML-Encoded and Single Quotes and Backslashes Escaped

## Goal

Submit a comment that calls the `alert()` function when the comment author's name is clicked.

## Enumeration

* The application stores user input from the comment form and reflects it inside an `onclick` event handler.
* Angle brackets (`<` and `>`) and double quotes (`"`) are HTML-encoded, while single quotes (`'`) and backslashes (`\`) are escaped.

## Testing

* I found that `&apos;` is decoded into a single quote by the browser.
* This allowed me to terminate the JavaScript string inside the `onclick` handler.
* I then concatenated `alert(1)` into the existing JavaScript expression.

## Exploitation

Payload:

```
http://foo?&apos;-alert(1)-&apos;
```

When the comment author's name is clicked, the browser decodes `&apos;` into a single quote. This terminates the original JavaScript string, executes `alert(1)`, and then resumes the expression without causing a syntax error.

## Root Cause

The application inserts user-controlled input into an `onclick` event handler without proper context-aware escaping. Although some characters are escaped, HTML entities such as `&apos;` are decoded by the browser, allowing JavaScript injection.

## Remediation

* Use context-aware output encoding for JavaScript event handler attributes.
* Do not rely solely on escaping or filtering specific characters.
* Validate user input on the server side before storing it.
* Avoid inline event handlers such as `onclick` whenever possible.
* Apply a Content Security Policy (CSP) to reduce the impact of XSS vulnerabilities.
