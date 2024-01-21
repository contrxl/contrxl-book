---
description: Fourth section in Jr Penetration Tester learning path.
---

# Authentication Bypass

### Username Enumeration

A list of usernames can be helpful, we can use website error messages to get this information. For example, if we try various usernames on a login forms and get an error "An account with this username already exists" - we can use this to generate a list of potentially valid usernames. An example of this with ffuf:

```
ffuf -w list.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://[IP_ADDR]/signup -mr "Username exists"
```

### Brute Force

With a valid list of usernames, a brute force attack can be attempted with ffuf.

```
ffuf -w users.txt:W1,passwords.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded -u http://[IP_ADDR]/login -fc 200
```

### Logic Flaw

A logic flaw is when the logical path of an app is bypassed, circumvented or otherwise manipulated.&#x20;

### Cookie Tampering

Editing cookies in an online session can have multiple outcomes. The contents of cookies can be in plain text and obvious, for example, a cookie could be:

Set-Cookie: logged\_in=true

Cookies can also be set as hashes, online tools like Crackstation can be used to crack them and figure out what they are. Similarly, they can also be encoded to obfuscate what they actually are.
