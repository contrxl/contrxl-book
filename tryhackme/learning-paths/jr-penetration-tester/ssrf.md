---
description: Seventh section in Jr Penetration Tester learning path.
---

# SSRF

### Introduction

SSRF (Server-Side Request Forgery) allows an attacker to make an additional or edited HTTP request to a resource of their choosing. There are two kinds of SSRF: regular SSRF where the attacker has info returned to them, and blind SSRF, where no info is returned to the attacker.

SSRF can result in access to unauthorised areas, access to confidential data, ability to scale to internal networks or revelation of authentication tokens/credentials.

### Finding SSRF

To look for SSRF:

* Check if a full URL is used in the address bar e.g. https://example.com/form?server=http://store.example.com/store
* Check for a hidden field in a form e.g. a preset in page source like value="http://example.com"
* A partial URL like just the hostname e.g. https://example.com/form?server=api
* The path of the URL e.g. https://example.com/form?dst=/forms/contact

### Defeating Common SSRF Defence

Developers aware of SSRF vulnerabilities may implement checks. These are commonly in the form of an allow list or a deny list.

An allow list is where all requests are denied unless they match a pattern or appear in a preset list. For example, the URL must begin with http://example.com. This can be circumvented by creating a subdomain on the attackers domain, like http://example.com.attacking-domain.com. The app logic would then let an attacker control the HTTP request.

A deny list is where all requests are accepted unless they match a pattern or appear in a preset list. For example, domains like localhost and 127.0.0.1 would appear on deny lists. This can be circumvented by using alternative localhost references like 0.0.0.0, 127.1, 127.\*.\*.\*, 2130706433 and so on.

If the above workarounds don't work, another solution is an open redirect. This is an endpoint on the server that automatically redirects elsewhere, like http://example.com/link?=http://example2.com. This would allow an attacker to redirect the internal HTTP request to a domain of their choice.

