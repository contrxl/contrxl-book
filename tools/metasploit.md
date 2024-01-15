---
description: Penetration testing framework.
---

# Metasploit

### Introduction

Metasploit is the most widely used exploitation framework. It supports penetration testing from information gathering to post-exploitation. There are two main versions: Pro and Framework. The Pro version allows automation and task management, as well as provides a GUI. The Framework version works from the command line and is used commonly for penetration testing Linux.

The main components of Metasploit are:

* msfconsole : the main CLI.
* Modules : supporting modules like exploits and scanners.
* Tools : stand-alone tools which help research and testing. Some of these tools are msfvenom, pattern\_create and pattern\_offset.

### Main Components of Metasploit

Repeating concepts in Metasploit that are important to understand:

* Exploit : piece of code using a vulnerability on a target system.
* Vulnerability : design, code or logic flaw affecting a target system.
* Payload : the code that will run on a target system.

To see auxiliary (supporting) modules in Metasploit like scanners, crawlers and fuzzers, run the follwing command in `msfconsole`: `show auxiliary`. For cleaner output, run `tree -L 1 auxiliary/` from the Metasploit modules directory (/usr/share/metasploit-framework/modules on Kali).

Encoders allow the exploit and payload to be encoded to try to bypass signature based antivirus solutions, to see all encoders run the following command in `msfconsole`: `show encoders`. For cleaner output, run `tree -L 1 encoders/` from the Metasploit modules directory (/usr/share/metasploit-framework/modules on Kali).

To view evasion modules, which help evade antivirus solutions directly, run the following command in `msfconsole`: `show evasion`. For cleaner output, run `tree -L 2 evasion/` from the Metasploit modules directory (/usr/share/metasploit-framework/modules on Kali).

To view exploits, run the following command in `msfconsole`: `show exploits`. For cleaner output, run `tree -L 1 exploits/` from the Metasploit modules directory (/usr/share/metasploit-framework/modules on Kali).

NOPs (No OPerations) do nothing, they are represented in the Intel x86 family by 0x90, after which the CPU will do nothing for one cycle, these are often used to achieve consistent payload sizes, to view NOPs run the following command in `msfconsole`: `show nops`. For cleaner output, run `tree -L 1 nops/` from the Metasploit modules directory (/usr/share/metasploit-framework/modules on Kali).

Payloads are code that runs on target systems, exploits leverage a vulnerability and payloads run to achieve the desired results. To view payloads, run the following command in `msfconsole`: `show payloads`. For cleaner output, run `tree -L 1 payloads/` from the Metasploit modules directory (/usr/share/metasploit-framework/modules on Kali). Payloads are separated into four different directories:

* Adapters : wraps single payloads to convert them into different formats. A normal single payload can be wrapped inside a PowerShell adapter, which makes a single PowerShell command that will execute the payload.
* Singles : self-contained payloads (add user, launch notepad.exe etc.) that do not need extra components to run.
* Stagers : set up channels between Metasploit and the target, useful when working with payloads which upload a stager to the target then download the rest of the payload.
* Stages : downloaded by stager, allows user of larger sized payloads.

Metasploit helps differentiate between single payloads and staged payloads:

* generic/shell\_reverse\_tcp : single payload, indicated by the "\_" between "shell" and "reverse".
* windows/x64/shell/reverse\_tcp : staged payload, indicated by the "/" between "shell" and "reverse".

Post modules are used on the final stage of the penetration testing process. To view post modules run the following command in `msfconsole`: `show post`. For cleaner output, run `tree -L 1 post/` from the Metasploit modules directory (/usr/share/metasploit-framework/modules on Kali). Payloads are separated into four different directories:

### MSFCONSOLE

Msfconsole operates like a normal command line for the most part, you can run commands like `ls`, `ping` etc. within the msfconsole. The `history` command can be used to see commands used previously. Msfconsole supports tab completion and is managed by context, meaning that unless set as a global variable, all parameter settings will be lost when you change the module you are using.&#x20;

You can select a module using `use [modulename]` and then show the options the module takes by using `show options`. Further info on a selected module can be shown by typing `info` whilst in the module context. You can leave context is msfconsole by using the `back` command.

You can search Metasploit by using `search [cve_number/target_system/exploit_name]`. You can use any module returned in a search by typing `use [result_line_number]` e.g. to use the first result from your search you could type `use 0`. You can search using keywords like type by using the syntax `search type:[type] [cve_number/target_system/exploit_name]`.

Search returns some essential info, like the type of module (auxiliary, exploit etc.) as well as the module category (Windows, Unix, Scanner etc.) and the "rank" column, exploits are ranked based on reliability, the table here shows their descriptions:

| Ranking          | Description                                                                                                                                                                                              |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ExcellentRanking | Exploit will never crash the service, this is the case for SQLInjection, CMD Execution, RFI, LFI etc. No typical memory corruption exploit gets this ranking unless there are exceptional circumstances. |
| GreatRanking     | Exploit has a default target and auto-detects the target or uses an app-specific return address after a version check.                                                                                   |
| GoodRanking      | Exploit has a default target and it is "common case" for the software (English, Win 7 for desktop app, 2012 for Server etc.)                                                                             |
| NormalRanking    | Exploit is otherwise reliable but depends on a specific version and can't reliably auto-detect.                                                                                                          |
| AverageRanking   | Exploit is unreliable or hard to exploit.                                                                                                                                                                |
| LowRanking       | Almost impossible to exploit.                                                                                                                                                                            |
| ManualRanking    | Impossible to exploit and basically a DoS. Also used when module has no use unless specifically configured by user.                                                                                      |

### Working with Modules & Good Practice

Good practice is to always run `show options` once a module has been selected to set the required parameters. Parameters are set simply using `set [parameter]`. Some common parameters are:

* RHOSTS : "remote hosts", the IP address of your target system, a single IP or network range can be set. This supports CIDR notation or a network range. A file can also be provided where targets are listed one target per line by using `file:/path/to/target.txt`.
* RPORT : "remote port", the port on the target system the vulnerable app runs on.
* PAYLOAD : the payload to be used.
* LHOST : "localhost", the attacking machine, your IP.
* LPORT : "localport", the port to use for a reverse shell to connect back to, this is a port on your attacking machine and can be any port not used by another app.
* SESSION : used with post-exploit modules that connect using an existing connection.

Any set parameter can be overriden by using the `set` command again, or all parameters can be cleared using `unset all`. The `setg` command can be used to set a value that will be used for all modules, for example if you used `setg RHOSTS 10.10.10.10` then this would now be set for all modules. You can clear values set with this using `unsetg`.

Once you have set up a module, you can run it using the `exploit` command or the `run` command. You can use this with no parameters or the `-z` parameter. `-z` will run the exploit and background the session as soon as it opens.

When a vulnerability has been exploited, a session is created. This is the communication channel from Metasploit to the target, you can use `background` to go back to the msfconsole prompt and leave the session running (CTRL+Z also does this).  The `sessions` command can be run from `msfconsole` to see currently active sessions. To interact with a session you can use `sessions -i [session_id]`.
