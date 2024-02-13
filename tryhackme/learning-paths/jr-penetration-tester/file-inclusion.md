---
description: Sixth section in Jr Penetration Tester learning path.
---

# File Inclusion

### Introduction

In some scenarios, web apps are configured to request access to files on a given system, including images, static text etc. Parameters are query parameter strings attached to the URL. File inclusion vulnerabilities are commonly exploited in programming languages for web apps like PHP that are poorly written and implemented. An attacker could leverage these vulnerabilities to leak data like code, credentials or other files. If the attacker can write files, then this could also be used to gain RCE (Remote Code Execution).

### Path Traversal

Also known as directory traversal, a web app vulnerability can be used to allow an attacker to read OS resources like local files on the server. Path traversal occurs when the user's input is passed to a function like "file\_get\_contents" in PHP.&#x20;

The behaviour of the URL can be tested by using the dot-dot-slash attack. An example of this would be modifying a URL to: http://app.com/get.php?file=../../../../etc/passwd, if this returns the contents of /etc/passwd then we have a path traversal vulnerability.

### Local File Inclusion (LFI)

LFI attacks are often due to developers lack of security awareness, in PHP, functions like include, require, include\_once and require\_once often contribute to vulnerable web apps. Along with the dot-dot-slash attack we can experiment with null bytes, a null byte is %00 or 0x00 in hex and is used to terminate a string. Adding a null byte to the end of a payload tells the function to ignore everything after it.

### Remote File Inclusion (RFI)

RFI is used to include remote files, like LFI, RFI occurs when input is not sanitised correctly. The risk of RFI is higher as it allows attackers to gain RCE on a server, other consequences of this include: sensitive information disclosure, cross-site scripting (XSS) and denial of service (DoS).
