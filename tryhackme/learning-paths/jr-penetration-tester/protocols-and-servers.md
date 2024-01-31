---
description: Thirteenth section in Jr Penetration Tester learning path.
---

# Protocols and Servers

### Telnet

Telnet is an application protocol used to connect to a virtual terminal on another computer. With Telnet, a user can login to another computer and access its console to run programs, start batch process and provide remote administration. Telnet servers use the Telnet protocol to look for incoming connections on port 23.&#x20;

Telnet is not reliable for remote administration, as all data is sent in cleartext. The secure alternative to this is SSH.

### Hyper Text Transfer Protocol (HTTP)

HTTP is used to transfer web pages, your browser connects to the webserver and uses HTTP to request HTML pages. HTTP sends and receives data as cleartext, so a simple tool like Netcat or Telnet can be used to act like a web browser. Three popular choices for HTTP servers are: Apache, Internet Information Services (IIS) and nginx. Both Apache and nginx are free, whilst IIS requires a license payment.

### File Transfer Protocol (FTP)

FTP was developed to make file transfer between different computers and systems. FTP sends and receives data as cleartext, meaning we can use Netcat or Telnet to communicate with FTP.

Some useful FTP commands are:

`STAT` : provides added information\
`SYST` : shows system type of the target\
`PASV` : switches FTP mode to passive\
`TYPE A` : switches file transfer mode to ASCII\
`TYPE I` : switches file transfer mode to binary

FTP has two main modes: active and passive. Active sends data over a separate channel originating from the FTP server's port 20. Passive sends data over a separate channel originating from an FTP client's port number above 1023. Some common FTP server softwares are: vsftpd, ProFTPD and uFTP.

### Simple Mail Transfer Protocol (SMTP)

Email delivery via the internet requires:

1. Mail Submission Agent (MSA)
2. Mail Transfer Agent (MTA)
3. Mail Delivery Agent (MDA)
4. Mail User Agent (MUA)

The email protocols which we rely on to talk to an MTA and MDA are Simple Mail Transfer Protocol (SMTP) and Post Office Protocol Version 3 (POP3) or Internet Message Access Protocol (IMAP).

SMTP uses cleartext, and so Telnet can be used to connect to a SMTP server and act as an email client (MUA) sending a message. SMP listens on port 25 by default.

### Post Office Protocol Version 3 (POP3)

POP3 is used to download email messages from a Mail Delivery Agent (MDA) server.

### Internet Message Access Protocol (IMAP)

IMAP is more sophisticated than POP3, IMAP allows you to synchronise email across multiple devices and clients, for example, if you mark an email as read - this change will be saved on the IMAP server and replicated anywhere you log in.
