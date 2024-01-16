---
description: Metasploit payload that supports penetration testing.
---

# Meterpreter

### How it Works

Meterpreter runs on the target but is not installed, it runs in memory. It runs in RAM to avoid being detected by any antivirus scans, this way it is seen as a process rather than a file on the system. Meterpreter also uses encrypted communication on the server where Metasploit is running to evade IDS/IPS. Most antivirus will still be able to detect meterpreter.

Available versions of Meterpreter can be listed using `msfvenom --list payloads | grep meterpeter`. The decision on which version to use should be based on:

* Target system : is it Linux? Windows? Mac? Android?
* Components on target : is Python installed? Is it a PHP website?
* Network connection types within target : can you have raw TCP? Can you only have HTTPS? Are IPv6 addresses monitored?

Each version of Meterpreter has different commands, so running `help` is always useful. Common commands in each category will be covered here.

### Core Commands

* `background` : background current session
* `exit` : terminate session
* `guid` : get session GUID
* `help` : show help
* `info` : shows info about a post module
* `irb` : open interactive Ruby shell
* `load` : load one or more extensions
* `migrate` : migrate meterpreter to another process
* `run` : execute meterpreter script or post module
* `sessions` : switch to another session

### File System Commands

* `cd` : change directory
* `ls` : list current directory files
* `pwd` : print working directory
* `edit` : allows editing of a file
* `cat` : output file contents
* `rm` : delete file
* `search` : search for files
* `upload` : upload a file or directory
* `download` : download a file or directory

### Networking Commands

* `arp` : display host ARP cache
* `ifconfig` : display available network interfaces
* `netstat` : display network connections
* `portfwd` : forward local port to remote service
* `route` : view and modify routing table

### System Commands

* `clearev` : clear event logs
* `execute` : execute command
* `getpid` : show current process ID
* `getuid` : show user Meterpreter is running as
* `kill` : terminate a process
* `pkill` : terminate a process by name
* `ps` : list running processes
* `reboot` : reboot the computer
* `shell` : drop into system command shell
* `shutdown` : shuts down computer
* `sysinfo` : get remote system info

### Misc Commands

* `idletime` : returns number of seconds remote user has been idle
* `keyscan_dump` : dumps keystroke buffer
* `keyscan_start` : starts capturing keystrokes
* `keyscan_stop` : stops capturing keystrokes
* `screenshare` : see remote users desktop in real time
* `screenshot` : screenshot interactive desktop
* `record_mic` : record audio from default device
* `webcam_chat` : start video chat
* `webcam_list` : lists webcams
* `webcam_snap` : takes screenshot from webcam
* `webcam_stream` : plays video stream from webcam
* `getsystem` : attempt to elevate to local system privilege
* `hashdump` : dumps contents of SAM database
