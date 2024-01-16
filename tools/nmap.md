---
description: Network scanning tool.
---

# NMAP

### Overview

Basic scan types:

\-sT : TCP connect scan\
\-sS : SYN "half-open" scan\
\-sU : UDP scan\
\-sN : TCP null scan\
\-sF : TCP FIN scan\
\-sX : TCP Xmas scan\
\-sN : Ping sweep, rely solely on ICMP ping, send TCP/SYN to 443 and TCP/ACK to 80\
\-sV : Probe open ports for service/version info\
\-sC : Script scan

### Useful Common Syntax

\-p- : tell nmap to scan all ports\
\-A : aggressive mode, should not be used against networks without prior permission.\
\-v or -vv : verbose or very verbose mode

### TCP Connect

Performs a three-way handshake with each port in turn to determine if the service is open based on received response. Any SYN packets sent to closed ports will be responded to with RST packets, nany open ports will receive SYN/ACK responses. If a port is open but has a firewall correctly configured, this type of scan is almost impossible to execute.

### SYN "Half-Open" Scan

Unlike TCP connect, a SYN scan will return a RST packet to the server once it receives the SYN/ACK, this prevents the server from repeatedly making the SYN/ACK request. This can bypass many older IDS solutions, SYN scans are also not often logged by listeners as they wait for a connection to be fully established. These scans are much faster than TCP. However, these scans require sudo permission to work properly on Linux and they run the risk of bringing down unstable services.

### UDP Scans

UDP connections are stateless, these rely on sending packets to a target port and hoping they make it. When a packet is received by an open UDP port, it should get no reply - this causes NMAP to mark it "open | filtered". This means the port is open, but it could be firewalled. If a closed UDP port receives a UDP packet, it should respond with an ICMP with an unreachable message, this allows NMAP to mark it closed.

### NULL, FIN and Xmas

NULL scans send TCP requests with no flags at all, if the port is closed, the target should reply with a RST packet.

FIN scans work almost exactly the same way, except they send a request with the FIN flag (used to gracefully close a connection), these should get a RST if closed.

Xmas scans send a malformed TCP packet and expect a RST if a port is closed. It is referred to as Xmas due to the scans appearance in Wireshark scans.

### Ping Sweep

NMAP sends an ICMP request to every possible IP in the network, if it receives a response it marks the IP as alive. CIDR notation can be used or a hyphen e.g. 192.168.0.1-254 or 192.168.0.0/24 would work.

