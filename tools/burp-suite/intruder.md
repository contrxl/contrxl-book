---
description: Usage of Burp Suite Intruder tool.
---

# Intruder

### Introduction

Burp Suite Intruder allows automated request manipulation and enables tasks like fuzzing and brute-forcing. Intruder allows for customisable, automated attacks and provides the ability to modify specific parts of a request and perform repetitive tests with variations of input data. The functionality is comparable to CLI tools like Wfuzz or ffuf. It should be noted that in the Community Edition of Burp Suite, Intruder is heavily rate limited.

There are four tabs within intruder:

* Positions : allows selection of an attack type and where the payload should be inserted.
* Payloads : allows selection of payloads for insertion into defined positions. There are various options such as loading items from a wordlist.
* Resource Pool : not particularly important in Community Edition, allows for resource allocation among automated tasks.
* Settings : configure attack behaviours, e.g. tell Burp to flag requests with specific text.

### Positions

Burp will automatically try to detect the most probable payload positions. Where these are not correct you can modify them with the "Add", "Clear", and "Auto" options on the right hand side.

### Payloads

Allows you to create, assign and configure attack payloads. This tab is divided into four sections:

1. Payload sets : choose the position to put a payload set and select the type of payload to use. If using an attack type that only allows a single payload set, the "Payload Set" drop-down will have only one option. Using attack types that require multiple payload sets will show one item in the drop-down for each position.&#x20;
2. Payload settings : provides options specific to the select payload type. For example, when using the "Simple List" payload type, we can manually add or remove payloads to or from the set using Add, Paste or Load buttons.
3. Payload processing : define rules to apply to each payload in the set before it is sent to the target.
4. Payload encoding : customise encoding options for payloads.

### Sniper

Default attack type and most commonly used, very effective in single position attacks such as brute-forcing or fuzzing for API endpoints.

### Battering Ram

Like Sniper except it places the payload in every position simultaneously.&#x20;

### Pitchfork

Equivalent to having multiple Sniper attacks running simultaneously, pitchfork uses one payload set per position and iterates through them simultaneously.

### Cluster Bomb

Allows multiple payload sets to be chosen, one per position. Cluster bomb iterates through each of these individually, ensuring every combination is tested.
