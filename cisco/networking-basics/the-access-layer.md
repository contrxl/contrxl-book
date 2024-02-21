---
description: Module 7.
---

# The Access Layer

### Encapsulation

The process of placing one message format inside another message format is encapsulation. De-encapsulation is when the process is reversed by the recipient. Each message is encapsulated in a specific format, called a frame, before it is sent.

### MAC Address Table

An Ethernet switch is used at Layer 2. When a host sends a message to another host on the same switched network, the switch decodes the frames to read the MAC address portion of the message. The MAC Address Table contains a list of all active ports and their associated host MAC addresses. When a message is received, the switch checks to see if the destination MAC is in the table, if it is, the switch starts a temporary connection (circuit) between the source and destination.

The MAC Address Table is built by examining the source MAC of each frame sent.
