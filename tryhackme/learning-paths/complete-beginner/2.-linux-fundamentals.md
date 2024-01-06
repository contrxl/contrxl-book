---
description: Second section in Complete Beginner learning path.
---

# Linux Fundamentals

### Background

More lightweight than Windows, first released in 1991. Powers things like websites, car entertainment & control panels, PoS systems and critical infrastructure/IoT sensors.

Linux is term for OS's built on UNIX. Ubuntu & Debian are common versions of Linux due to their extensibility. Kali is common among security professionals.

### Basic Commands

echo : outputs any text provided to it (echo "Hello world!")\
whoami : tells you who you are currently logged in as\
ls : lists files & folders in current directory\
cd : change directory (cd /Desktop)\
cat : concatenate\
pwd : print working directory\
find : can be used to search the system for a specific file/files\
grep : can be used to search files for specific terms (grep "Hello" test.txt)\
touch : creates a file\
mkdir : creates a folder\
cp : copies a file or folder\
mv : moves a file or folder\
rm : removes a file or folder\
file : determines the type of a file

### Shell Operators

& : runs commands in the background of the terminal\
&& : combine multiple commands into one line\
\> :  redirect output from a command and replace\
\>> : redirect and append rather than redirect and replace

### Flags & Switches

Commands have various arguments that can be provided, these arguments are provided using a hyphen and then a specific keyword known as a flag or switch. For example, ls -a will use the argument "-a" to display all files in a location, including hidden ones.

Commands that accept switches will have a --help or -h option which will show all the possible options a command will accept as well as showing a brief description and an example of how to use it.

### Permissions

Using ls -lh shows permissions for files. Three columns are displayed which determine what actions are and aren't allowed, the columns show r (read), write (w) and execute (e).

### Common Directories

/etc : one of most important directories, stores system files used by the OS. Holds a file called sudoers which shows the users and groups with permissions to run as root. Passwd and shadow are also held here which show how the system stores passwords (encrypted with sha512).

/var : short for variable data, stores data frequently accessed or written by system services and apps. Log files from running services are typically written here in /var/log.

/root : the home folder for the "root" system user, important to remember that for "root" the home directory is this instead of /home.

/tmp : short for temporary, volatile directory used to store data that is only needed once or twice. This folder is wiped once the computer is restarted. Tmp can be written by all users by default.

### Terminal Text Editors

Nano : use nano filename to create or open a file using nano. Lines can be navigated using the up or down arrow keys and pressing enter creates a new line. Nano covers most things a text editor needs like searching, copy/pasting, skipping to a line number and checking your current line number. All nano commands are listed at the bottom and are triggered by pressing CTRL + a key (CTRL is denoted using ^)

VIM : much more advanced editor. Much harder to use but is highly customisable, highlights syntax, works on all terminals.

### Downloading Files

The wget command allows files, scripts, programs or pictures to be downloaded directly from the terminal as long as you have the address of the resource you wish to download. To download a file named "file.txt" assuming yo know the address the command would appear as:

```
wget https://www.mysite.com/file.txt
```

### Transferring Files from Host (SCP)

SCP (Secure Copy) allows secure copying of files over SSH. SCP lets you copy files and directories to and from your system and a remote system. The command to transfer a file from your machine to a remote machine would look like:

```
scp file.txt user@192.168.1.1:/home/user/transfer.txt
```

This uses a few variables; the IP of the host (192.168.1.1), the user on the remote system (user), the name of the file on the local system (file.txt) and the name we want the file to have on the remote system (transfer.txt). Reversing this allows us to transfer data from a remote host to your local host, like:

```
scp user@192.168.1.1:/home/user/file.txt transfer.txt
```

### Serving Files from Host (WEB)

Ubuntu machines come with python2, this provides the HTTPServer module which turns your machine into an easy to use web server to serve files which can be downloaded with curl or wget. HTTPServer will serve files in the directory that you run the command by default. To start HTTPServer use the command:

```
python3 -m http.server
```

Once this is running you can now download fromo this using the computers IP address and the name of the file. This requires you to use the exact name and location of the file you wish to download, there is no indexing. To download we can use:

```
wget http:/127.0.0.1:8000/file
```

### Processes

To view a list of running processes, use the ps command. This shows the process status code, how much CPU is being used and the name of the program. To see processes that run from other users and those that don't run from a session like system processes we use ps aux.

The top command can be used to see real time stats about processes running on the system.

To stop a process running we can use kill \[PID] e.g. kill 209. Signals that can be sent to killed processes are:

* SIGTERM : kill process and allow cleanup
* SIGKILL : kill the process, no cleanup
* SIGSTOP : stop or suspend a process

systemctl allows interaction with the systemd daemon. systemctl uses the format systemctl \[option] \[service]. To tell Apache to start we would use systemctl start apache2. systemctl allows four options:

* Start
* Stop
* Enable
* Disable

### Automation

To have certain actions take place after system boot, cron can be used. cron can be interacted with using crontabs.&#x20;

A crontab is a special file with formatting recognised by the cron process to execute each line. crontabs require:

* MIN : minute to execute at
* HOUR : hour to execute at
* DOM : day of month to execute at
* MON : month of year to execute at
* DOW : day of week to execute at
* CMD : actual command to use

To back up a users documents every 12 hours we could use:

```
0 */12 * * * cp -R /home/user/Documents /var/backups >/dev/null 2>&1
```
