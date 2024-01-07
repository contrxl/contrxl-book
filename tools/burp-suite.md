---
description: Web application penetration testing tool.
---

# Burp Suite

### Introduction

Burp Suite Community Edition can be downloaded [here](https://portswigger.net/burp/communitydownload).

Burp is a framework written in Java for web app penetration testing. Also used commonly in testing mobile applications as the features for web app testing translate directly into testing APIs (Application Programming Interfaces). Burp can capture and manipulate all traffic between an attacker and a webserver. It can be used to intercept, view and modify web requests before they are sent to the server. There are various editions of Burp available, Community is the standard free version, Burp Suite Professional and Burp Suite Enterprise require expensive licenses but have powerful features.

Burp Suite Professional comes with:

* Automated vulnerability scanner
* Fuzzer/bruteforcer that is not rate limited
* Saving projects & report generation
* Built-in API for integration with other tools
* Unrestricted access to add new extensions
* Access to Burp Suite Collaborator

Burp Suite Enterprise is used for continuous scanning, it can periodically scan web apps for vulnrabilities.

### Features of Burp Suite Community

* Proxy : allows interception and modification of requests/responses when interacting with web apps.
* Repeater : allows the capture, modification and resending of a request numerous times.
* Intruder : rate limited in Community, allows an endpoint to be sprayed with requests.
* Decoder : helps transform data by decoding captured info or encoding a payload.
* Comparer : allows comparison of two pieces of data at a word or byte level.
* Sequencer : assesses randomness of tokens like cookie values or random data, if it is not truly random, it opens avenues for attack
