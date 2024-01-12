---
description: A practice and learning tool for many aspects of cyber security.
---

# 🖥 TryHackMe

### Overview

[TryHackMe](https://tryhackme.com/) uses [OpenVPN](https://openvpn.net/) to provide access to their network and vulnerable machines. It also provides you with your own machines via web interface for a small subscription fee.&#x20;

### Editing Hosts File

Some THM labs require the hosts file on your device to be modified to allow for successful connection to the lab. The hosts file on your device is used for local domain name mapping which bypasses any DNS. Being able to access a domain this way makes name-based virtual hosting (or vhosting) possible. This allows multiple websites to be served from a single webserver.

To add or remove from your host file:

* On Linux, naviagate to the hosts file at /etc/hosts/ and open it up using sudo in a text editor and add the required line. This will typically look like:

```
10.10.10.10 web.address.com shell.address.com example.address.com
```

* On Windows, this file can be found at C:\Windows\System32\drivers\etc\hosts. On Windows, modify this text file using "Run as Administrator".
