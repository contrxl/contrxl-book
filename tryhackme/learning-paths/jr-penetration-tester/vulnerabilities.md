---
description: Fifteenth secition in Jr Penetration Tester learning path.
---

# Vulnerabilities

### Introduction

NIST defines a vulnerability as "weakness in an information system, system security procedures, internal controls, or implementation that could be exploited or triggered by a threat source". Arguably, there are five main categories of vulnerability:

| Vulnerability               | Description                                                                                                                                       |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| Operating System            | Found within an OS and often result in privilege escalation.                                                                                      |
| (Mis)Configuration-based    | Found in incorrectly configured apps or services, for example, a website exposing customer details.                                               |
| Weak or Default Credentials | Apps and services with authentication often come with default credentials, for example, an admin account having a default password of "admin".    |
| Application Logic           | Result of poorly designed applications, for example, poorly implemented authentication resulting in an attacker being able to impersonate a user. |
| Human-Factor                | Vulnerabilities which leverage human behaviour, for example, phishing emails.                                                                     |

### Scoring Vulnerabilities (CVSS & VPR)

Vulnerability management is the process of evaluating, categorising and remediating threats faced by an organisation. It is estimated that only 2% of vulnerabilities ever end up being exploited, so vulnerability management is about assessing the most dangerous ones and reducing the likelihood of an attack being used to exploit a system.

The Common Vulnerability Scoring System (CVSS) was introduced in 2005 and has three major iterations. A vulnerability is given a classification (out of 5) based on its assigned score. This looks like the below:

| Rating   | Score    |
| -------- | -------- |
| None     | 0        |
| Low      | 0.1-3.9  |
| Medium   | 4.0-6.9  |
| High     | 7.0-8.9  |
| Critical | 9.0-10.0 |

The advantages and disadvantages of CVSS are as follow:

| Advantages of CVSS                            | Disadvantages of CVSS                                                                                                       |
| --------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| CVSS has existed for a long time              | Never designed to prioritise vulnerabilities, only to assign a severity value                                               |
| CVSS is popular in organisations              | CVSS assess vulnerabilities based on available exploits, however, only 20% of all vulnerabilities have an exploit available |
| CVSS is free to adopt and recommended by NIST | Vulnerabilities rarely change scoring despite new developments & exploits being found                                       |

Vulnerability Priority Rating (VPR) is a more modern framework developed by Tenable. This framework is risk-driven - meaning vulnerabilities are scored with a heavy focus on the risk they post to the organisation itself, rather than using factors like impact.

Unlike CVSS, VPR accounts for the relevancy of a vulnerability, for example, no risk is given to a vulnerability if it does not apply to the organisation. VPR is also dynamic in its scoring, meaning a vulnerability score can change based on new developments. VPR uses a similar scoring range to CVSS:

| Rating   | Score      |
| -------- | ---------- |
| Low      | 0.0 - 3.9  |
| Medium   | 4.0 - 6.9  |
| High     | 7.0 - 8.9  |
| Critical | 9.0 - 10.0 |

The advantages and disadvantages of VPR are as follows:

| Advantages of VPR                                         | Disadvantages of VPR                                                                                                         |
| --------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| VPR is modern & real-world                                | VPR is not open-source                                                                                                       |
| VPR considers over 150 factors in risk calculation        | VPR can only be adopted as part of a commercial platform                                                                     |
| VPR is risk-driven and helps prioritise vulnerabilities   | VPR does not consider the CIA triad as extensively as CVSS does, meaning risk to CIA does not play a large factor in scoring |
| Scoring is dynamic and can change as a vulnerability ages | Blank on purpose                                                                                                             |
