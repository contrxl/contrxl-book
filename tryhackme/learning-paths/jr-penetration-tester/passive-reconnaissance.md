---
description: Eleventh section in Jr Penetration Tester learning path.
---

# Passive Reconnaissance

### WHOIS

WHOIS is a request and response protocol which listens on TCP port 43 for incoming requests. The domain registrar is responsible for maintaining the WHOIS records for the domains it is leasing. The WHOIS server replies with various info related to the requested domain, we can learn:

* Registrar : which registrar was used to register the domain?
* Contract info of Registrar : name, organisation, address, phone (unless hidden via privacy service)
* Creation, update and expiration dates : when was the domain created, updated and when does it need renewed?
* Name server : which server to ask to resolve the domain name?

The syntax is very simple: `whois DOMAIN_NAME`

### NSLOOKUP and DIG

NSLookup (Name Server Lookup) can be used to find the IP address of a domain, the syntax for this is: `nslookup OPTIONS DOMAIN_NAME SERVER`. The three main parameters are:

* OPTIONS : query type as shown below, you can use A for IPv4 and AAAA for IPv6.
* DOMAIN\_NAME : name of domain to look up.
* SERVER : DNS server to query, any local or public one can be chosen. Cloudflare offers `1.1.1.1` and `1.0.0.1`, Google offers `8.8.8.8` and `8.8.4.4` and Quad9 offers `9.9.9.9` and `149.112.112.112`.

| Option | Description        |
| ------ | ------------------ |
| A      | IPv4 Addresses     |
| AAAA   | IPv6 Addresses     |
| CNAME  | Canonical Name     |
| MX     | Mail Servers       |
| SOA    | Start of Authority |
| TXT    | TXT Records        |

Example usage would be: `nslookup -type=A example.com 1.1.1.1`. This will return all IPv4 addresses in use by example.com.

DIG (Domain Information Grouper) can be used for more advanced DNS queries. The syntax for this is typically: `dig DOMAIN_NAME TYPE`, but we can also use `dig @SERVER DOMAIN_NAME TYPE` if we wish to specifiy the server to query.
