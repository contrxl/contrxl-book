---
description: Open-source packet analyser.
---

# Wireshark

### Overview

Wireshark is an open-source tool capable of sniffing and investigating live traffic, as well as analysing packet captures (PCAP).&#x20;

Wireshark is one of the most potent tools available in the wild, it can be used for:

* Detecting and troubleshooting network problems, such as network failure points.
* Detecting security anomalies, like rogue hosts, abnormal port usage and suspicious traffic.
* Investigating and learning protocol details, like response codes and payload data.

The Wireshark GUI opens with a single, all-in one page. There are five main sections:

* Toolbar: contains menus and shortcuts for packet sniffing and processing. This includes filtering, sorting, summarising, exporting and merging.
* Display Filter Bar: main query and filtering section.
* Recent Files: a list of recently investigated files. Listed files can be recalled with a double-click.
* Capture Filter & Interfaces: capture filters and available sniffing points (interfaces). The network interface connects a computer and network, whilst a software connection (lo, eth0, ens33) enable networking hardware.
* Status Bar: Tool status, profile and numeric packet info.

When a file is opened or Wireshark starts capturing, packet info is displayed in different panes:

* Packet List Pane: summary of each packet. Each packet can be clicked for more information, once a packet is chosen, its info appears in other panels.
* Packet Details Pane: detailed protocol breakdown of the chosen packet.
* Packet Bytes Pane: hex and decoded ASCII of the selecting packet, highlights teh packet field depending on the clicked section.

Wireshark can also merge two PCAP files into one file with "File > Merge". Note that the merged file needs to be saved before it can be worked on. Wireshark can also capture a files properties (a file hash, capture time, capture comments, interface and statistics). This can be done with "Statistics > Capture File Properties".

### Packet Dissection

Also known as protocol dissection, this is investigation of packet details by decoding available protocols and fields. Wireshark supports a long list of protocols and you can also write custom dissection scripts.

Each packet is broken down into five to seven layers based on the OSI model. At most a packet will have seven distinct layers:

1. The Frame (Layer 1): the frame/packet you are looking at, and details specific to the physical layer of the OSI model.
2. Source \[MAC] (Layer 2): the source and destination MAC addresses from the data link layer of the OSI model.
3. Source \[IP] (Layer 3): source and destination IPv4 addresses from the network layer of the OSI model.
4. Protocol (Layer 4): details of the protocol used (UDP/TCP) and the source & destination ports from the transport layer of the OSI model.
5. Protocol Errors: continuation of the 4th layer showing TCP segments that need reassembled.
6. Application Protocol (Layer 5): details specific to protocol used, such as HTTP, FTP and SMB from the application layer of the OSI model.
7. Application Data: extension of the 5th layer showing application-specific data.

### Packet Navigation

Wireshark assigns a unique number for each packet, making it easy to analyse big captures and go to a specific packet. You can use "Go > Go To Packet" to quickly jump to a specific packet number.

You can also find packets by content using "Edit > Find Packet" which will search inside the packets for an event of interest. There are two crucial parts to this: knowing the input type and choosing the search field. The input type can be: display filter, hex, string and regex - the most commonly used are string or regex. The search field can be the packet list, packet details or packet bytes. If you try to find info in the packet details pane by searching the packet list pane, Wireshark will not find it.

You can mark or comment on packets by right-clicking them and choosing "Mark/Unmark Packet(s)" or "Packet Comment..." respectively. Note that packet markers will be removed after you close the capture file.

You can export only certain packets (like marked ones) with "File > Export Specified Packets" - this can help narrow down analysis.

You can export objects/files through the wire using "File > Export Objects". Note that files can only be extracted for the selected protocols streams e.g. DICOM, HTTP etc.

You can have Wireshark show you the exact time a packet was captured with "View > Time Display Format > UTC Data and Time of Day" (the default is "Seconds since Beginning of Capture).

Wireshark also marks packets a colour based on the state of the protocol, these are only suggestions and there are always chances for false positives/negatives but are as follows:

| Severity | Colour | Info                                       |
| -------- | ------ | ------------------------------------------ |
| Chat     | Blue   | Info on usual workflow.                    |
| Note     | Cyan   | Notable events like app error codes.       |
| Warn     | Yellow | Unusual error codes or problem statements. |
| Error    | Red    | Malformed packets.                         |

This "Expert Information" can be viewed under "Analyse > Expert Information".

### Packet Filtering

Wireshark offers two kinds of filtering: capture and display filters. Capture filers are for only the packets valid for the used filters. Display filters are for viewing the packets valid for the used filter.

The most basic way to filter traffic, is to right click a packet and choose "Apply As Filter", alternatively you can use "Analyse > Apply As Filter". If you wanted to find a specific packet and all linked packets, you can use "Analyse > Conversation Filter" to filter for conversations.

This can also be done with "View > Colourise Conversation" to do this without filtering out other packets. This can be undone with "View > Colourise Conversation > Reset Colourisation".

The "Prepare as Filter" option is similar to "Apply as Filter" except it waits for additional input like "and/or" or an execution command with enter.

You can right-click a value in the packet details pane and choose "Analyse > Apply as Column" to add it to the packet list pane, this helps analyse the appearance of a specific value or field.

Streams can be reconstructed to allow viewing of raw traffic by using "Analyse > Follow TCP/UDP/HTTP Stream" which will show the streams in a separate dialogue box.
