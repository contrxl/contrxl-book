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
\-sC : Script scan\
\-PR : ARP only scan.

### Quick Command Line Option Ref

| Scan Type              | Example Command                            |
| ---------------------- | ------------------------------------------ |
| ARP Scan               | sudo nmap -PR -sn \[IP\_ADDR]/24           |
| ICMP Echo Scan         | sudo nmap -PE -sn \[IP\_ADDR]/24           |
| ICMP Timestamp Scan    | sudo nmap -PP -sn \[IP\_ADDR]/24           |
| ICMP Address Mask Scan | sudo nmap -PM -sn \[IP\_ADDR]/24           |
| TCP SYN Ping Scan      | sudo nmap -PS22,80,443 -sn \[IP\_ADDR]/30  |
| TCK ACK Ping Scan      | sudo nmap -PA22,80,443 -sn \[IP\_ADDR]/30  |
| UDP Ping Scan          | sudo nmap -PU53,161,162 -sn \[IP\_ADDR]/30 |

Adding -sn tells nmap to perform host discovery only and no port-scanning. -n will prevent DNS lookup, -R will do reverse-DNS for all hosts.

### Useful Common Syntax

\-p- : tell nmap to scan all ports\
\-A : aggressive mode, should not be used against networks without prior permission.\
\-v or -vv : verbose or very verbose mode\
\-sL : check list of hosts that will be scanned, nmap will attempt reverse-DNS resolution\
\-n : do not attempt DNS resolution\
\-iL : provide a txt file for input\
\-PP : use ICMP timestamp requests

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

### Spoofing and Decoy Scanning

A spoofed scan be be run using `nmap -e [NET_INTERFACE] -Pn -S [SPOOF_IP] [TARGET_IP]`, this will specify a network interface for nmap and give it a spoofed IP address to use. This type of scanning is useless unless you are able to monitor the network for responses. If you are on the same subnet as the target you can also use `--spoof-mac [SPOOF_MAC]` to spoof your MAC address.

A decoy can be launched by using `-D` and specifying a specific/random IP address. For example, a scan like `nmap -D 10.10.10.10,10.10.10.11,ME [TARGET_IP]` would show the scan as coming from 10.10.10.10 and 10.10.10.11 as well as your own IP address. Another way to run this is `nmap -D 10.10.10.10,10.10.10.11,RND,RND,ME [TARGET_IP]` where "RND" will generate a random IP address assignment.

