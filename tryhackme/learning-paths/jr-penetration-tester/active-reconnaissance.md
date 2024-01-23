---
description: Twelfth section in Jr Penetration Tester learning path.
---

# Active Reconnaissance

### Web Browser

The web browser can be used in several ways for information gathering. Web browsers connect to:

* TCP port 80 by default when a site is accessed over HTTP
* TCP port 443 by default when a site is accessed over HTTPS

It is also possible to connect to a site over a custom port, for example https://127.0.0.1:9999 will connect to localhost on port 9999, if there is a listening HTTPS server there then we will receive a webpage.

### Ping

Ping sends a packet to a remote system, and if you receive a reply, you can conclude that the system is online and the network is working. The syntax for this is very simple: `ping IP_ADDR/HOSTNAME`. You can also define a certain number of packets to send using `-c PACKETS` or `-n PACKETS` on Windows.

### Traceroute

Traces the route taken by the packets from your system to a host. This is used to find the IP addresses of the routers or hops that a packet traverses as it goes from your system to a host. The syntax for this is: `traceroute IP_ADDR` on Linux and `tracert IP_ADDR` on Windows.

### TELNET (Teletype Network)

Developed in 1969 to communicate with a remote system via CLI, hence the command `telnet` uses the TELNET protocol. TELNET is not secure but can be used to connect to any service and grab its banner, for example, you could connect to a server listening on port 80 with `telnet IP_ADDR 80` and then issue `GET / HTTP/1.1`. You can specify something other than the default with `GET /page.html HTTP/1.1`.

### NETCAT

Netcat supports TCP and UDP protocols. It can function as a client that connects to a listening port or it can act as a server that listens on a port of your choice. You can connect to a server like with telnet using nc IP\_ADDR PORT. You can also use it to listen on a port by using nc -nvlp PORT.&#x20;

| Option | Meaning                               |
| ------ | ------------------------------------- |
| -l     | Listen mode.                          |
| -p     | Port Number.                          |
| -n     | Numeric only; no hostname resolution. |
| -v     | Verbose.                              |
| -vv    | Very Verbose                          |
| -k     | Keep listening after disconnect.      |

Port numbers less than 1024 require root privileges to run.
