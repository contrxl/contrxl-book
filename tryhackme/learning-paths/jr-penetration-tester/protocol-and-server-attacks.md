---
description: Fourteenth section in Jr Penetration Tester learning path.
---

# Protocol and Server Attacks

### Introduction

Servers implementing protocols from [Protocols and Servers](protocols-and-servers.md) are subject to many attack types, such as:

1. Sniffing Attack (Network Packet Capture)
2. Man-in-the-middle (MITM) Attack
3. Password Attack (Authentication Attack)
4. Vulnerabilities

Knowing that the goal is to protect CIA (confidentiality, integrity and availability), the aim of an attack is to cause DAD (disclosure, alteration, destruction). The attacks mentioned directly affect system security. Network packet capture violates confidentiality, successful password attacks can lead to disclosure and man-in-the-middle attacks breach integrity.

### Sniffing Attack

A sniffing attack is using a network packet capture tool to gather information about the target. If a protocol communicates in cleartext, then the data exchange can be captured by a third party for analysis. If data is not encrypted in transit, a simple packet capture can lead to disclosure. There are many programs available for network packet capture:

* Tcpdump : open source CLI program
* Wireshark : open source GUI available for Linux, Mac and Windows
* Tshark : CLI alternative to Wireshark

A quick example to capture POP3 traffic with tcpdump would be the command: `sudo tcpdump port 110 -A`. `port 110` is used to filter to only port 110 which POP3 uses, and `-A` is to display the output as ASCII.

### Man-in-the-Middle (MITM) Attack

A MITM attack occurs when a target believes they are communicating with a legitimate destination, but is actually communicating with an attacker. This attack is relatively simple if the two parties are not confirming the authenticity and integrity of each message. Any time you are browsing over HTTP you are exposed to a MITM attack.&#x20;

MITM can affect many cleartext protocols like FTP, SMTP and POP3. Mitigation against this requires cryptography. The solution is to use proper authentication along with encryption or message signing. PKI (Public Key Infrastructure), trusted root certificates and Transport Layer Security (TLS) help protect from MITM attacks.

### Transport Layer Security (TLS)

SSL (Secure Sockets Layer) began in 1194, SSL 3.0 was released in 1996. When more security was needed, TLS was introduced in 1999. So far, protocols covered are all on layer 7 (the application layer). Encryption can be added to protocols via the presentation layer, resulting in data being presented in an encrypted format instead of its original form.

TLS is more secure than SSL, but SSL/TLS is still a widely used term, even though most modern servers use solely TLS. TLS can be used to upgrade HTTP, FTP, SMTP, POP3 and IMAP. This changes these like below:

<table><thead><tr><th>Protocol</th><th>Default Port</th><th width="161">Secured Protocol</th><th>Default Port with TLS</th></tr></thead><tbody><tr><td>HTTP</td><td>80</td><td>HTTPS</td><td>443</td></tr><tr><td>FTP</td><td>21</td><td>FTPS</td><td>990</td></tr><tr><td>SMTP</td><td>25</td><td>SMTPS</td><td>465</td></tr><tr><td>POP3</td><td>110</td><td>POP3S</td><td>995</td></tr><tr><td>IMAP</td><td>143</td><td>IMAPS</td><td>993</td></tr></tbody></table>

### Secure Shell (SSH)

SSH was created to provide a secure way to perform remote system administration. Simply, SSH allows:

1. Confirmation of remote server identity
2. Exchanged messages can be encrypted and only decrypted by the intended recipient
3. Both sides can detect any modification in messages

### Password Attacks

Attacks against passwords are typically carried out by:

1. Password Guessing: requires knowledge of the target, like a pet's name and their birthday
2. Dictionary Attack: includes many/all valid words in a wordlist
3. Brute-Force Attack: attacker can attempt to guess the password by trying all possible combos

Attacks against login systems can be carried out using a tool like Hydra, mitigations against tools like this include:

* Password Policy: enforces a minimum complexity
* Account Lockout: locks account after a set number of tries
* Throttling Authentication Attempts: delays response to a login attempt
* CAPTCHA: Completely Automated Public Turing Test to differentiate computers and people.
* Require the use of a public certificate to authenticate.
* 2FA: ask users to provide a code via smartphone or email



