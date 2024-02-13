---
description: Third section in Jr Penetration Tester learning path.
---

# Subdomain Enumeration

### SSL/TLS Certificates

When an SSL/TLS (Secure Socket Layer/Transport Layer Security) certificate is created for a domain by a CA (Certificate Authority). CA's partake in Certificate Transparency Logs (CT Logs). These are publicly viewable logs of every certificate created for a domain name, this is designed to stop malicious and accidentally created certificates from being used.&#x20;

### Search Engines

Using advanced search on Google can help find subdomains, for example you can use "-site:www.domain.com site:\*.domain.com" would only contain results leading to the domain.com address but exclude any links containing "www.domain.com".

### DNS Bruteforce

Tools like [dnsrecon](https://github.com/darkoperator/dnsrecon) can be used to find subdomains from a list of common subdomains.

### Sublist3r

[Sublist3r](https://github.com/aboul3la/Sublist3r) can be used to search for subdomains like dnsrecon.

### Virtual Hosts

Subdomains are not always publicly accessible, for example, development versions of a web app or admin portal. The DNS record for these could be kept on a private DNS server or recorded on the developer's machines. This can be automated using ffuf like:

```
ffuf -w /wordlist/names.txt -H "Host: FUZZ.example.com" -u http://[IP_ADDR]
```
