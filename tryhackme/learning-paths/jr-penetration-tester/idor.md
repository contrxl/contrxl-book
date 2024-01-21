---
description: Fifth section in Jr Penetration Tester learning path.
---

# IDOR

### Introduction

IDOR or Insecure Direct Object Reference is an access control vulnerability which can be occur when a web-server receives user-supplied input to retrieve objects. If this data is not validated on the server-side to confirm it belongs to the user who requested it, this can lead to an IDOR vulnerability.

### IDOR in Encoded IDs

When passing data from page to page, web developers will often take the raw data and encode it. Encoding ensures the server can understand the contents. The most common encoding on websites is base64. For example, an encoded string with an ID of 10 could be decoded, changed from 10 to 20 and encoded again to exploit an IDOR vulnerability.

### Hashed IDs

The same idea as encoded IDs, except a bit harder to crack. They can be passed to Crackstation or john to be cracked if they are common integer values.

### Unpredictable IDs

A good method for IDOR detection is to create two accounts and then swap the ID numbers between them, if you can view the other account using their ID number while logged out (or logged in as a different account) then you have found an IDOR vulnerability.

