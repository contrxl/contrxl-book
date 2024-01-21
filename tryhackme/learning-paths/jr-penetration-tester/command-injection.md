---
description: Ninth section in Jr Penetration Tester learning path.
---

# Command Injection

### Introduction

Command Injection is the abuse of an application's behaviour to execute commands on the OS, using the same privileges that the application is running with. For example, if you had command injection on a web server running as "joe", then you would be able to execute commands with his permissions.&#x20;

Command injection is often called RCE (Remote Code Execution) as it allows you to execute code directly in the application. For example, if you could run the command whoami in an application that would be an example of RCE.

### Blind Command Injection

For this, you will need to use payloads that cause a time delay, for example, `ping` or `sleep`. Using ping, the application will hang for x seconds in relation to how many pings were specified. Another way to detect blind command injection is to force output, for example using `>`. We can tell the application to execute `whoami` and then redirect that to a file, and then use `cat` to read the file's contents.

### Verbose Command Injection

This is where the application provides instant feedback or output about executed commands. For instance, running `whoami` would display the output on the web application.

### Useful Linux Payloads

* whoami : see what user the app is running under
* ls : list contents of current directory
* ping : invoke the app to hang
* sleep : invoke the app to hang
* nc : can be used to spawn a reverse shell on the app

### Useful Windows Payloads

* whoami : see what user the app is running under
* dir : list contents of current directory
* ping : invoke the app to hang
* timeout : invoke the app to hang
