# Lab: Reflected XSS with some SVG markup allowed

## Goal
 - To solve the lab, perform a cross-site scripting attack that calls the alert() function.

## Enumeration
 - Site is blocking common tags but misses some SVG tags and events.

## Testing
 - tag animateTrasform and svg are allowed
 - Checked all posible events. Allowed only *onbegin* event.
So onbegin triggers after animation starts, this Is why we need animateTransform which can be placed into svg.

## Exploitation
 Final payload:
```
<svg><animateTransform onbegin='alert()'>
```

## Root cause
 - Incomplete input filtering.

## Remediation
 - Restrict which HTML and SVG elements are allowed in the search input.
