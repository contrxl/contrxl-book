---
description: Module 9.
---

# IPv4 and Network Segmentation

### Unicast

A unicast transmission is one device sending a message to another device in one-to-one communication. A unicast packet has a destination unicast IP which goes to a single recipient. A source IP can only ever be a unicast address because a packet cannot originate from multiple sources.

IPv4 unicase hosts are in the range 1.1.1.1 - 223.255.255.255.&#x20;

### Broadcast

A broadcast packet as a destination IP address with all ones (1s) in the host portion, or 32 one (1) bits. There are no broadcast packets in IPv6. A broadcast packet must be processed by all devices in the same broadcast domain.

Broadcasts can be directed or limited. A directed broadcast is sent to all hosts on a specific network, for example, 172.16.4.2/24 sends a packet to 172.16.4.255. A limited broadcast is sent to 255.255.255.255. Routers will not forward broadcasts by default.

### Multicast

Multicast reduces traffic by allowing a host to transmit a single packet to a selected set of hosts that subscribe to a multicast group. Hosts which receive multicast packets are called multicast clients. Each multicast group is represented by a single IPv4 multicast destination address. Routing protocols like OSPF use multicast.
