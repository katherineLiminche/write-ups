# Lab: Reflected XSS into a Template Literal with Angle Brackets, Single Quotes, Double Quotes, Backslashes, and Backticks Unicode-Escaped

## Goal

Perform a reflected XSS attack that calls the `alert()` function inside a JavaScript template literal.

## Enumeration

The application reflects user input inside a JavaScript template literal. Angle brackets (`<` and `>`), single quotes (`'`), double quotes (`"`), backslashes (`\`), and backticks (`` ` ``) are escaped or encoded, preventing a direct breakout from the template literal.

## Testing

* Common string-breaking characters were escaped or encoded.
* Although breaking out of the template literal was not possible, the `${...}` syntax was still evaluated as a JavaScript expression.
* This allowed arbitrary JavaScript to execute without closing the template literal.

## Exploitation

Payload:

```
${alert()}
```

The `${...}` syntax is evaluated inside the template literal. When the page processes the template string, the `alert()` function is executed.

## Root Cause

The application inserts user-controlled input into a JavaScript template literal without neutralizing template expression syntax. As a result, `${...}` is evaluated as JavaScript, leading to reflected XSS.

## Remediation

* Escape or neutralize `${` when embedding untrusted input into JavaScript template literals.
* Apply context-aware output encoding for JavaScript.
* Avoid inserting untrusted user input directly into template literals.
* Use a Content Security Policy (CSP) to reduce the impact of XSS vulnerabilities.
