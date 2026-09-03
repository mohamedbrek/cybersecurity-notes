# Linux Notes

## Introduction

These are my personal Linux learning notes as I build practical skills for cybersecurity and SOC operations.

The notes cover Linux command-line fundamentals, file management, permissions, processes, networking, logs, SSH and useful commands for security investigations.

---

## 1. Linux File System

Linux uses a hierarchical file system that starts from the root directory.

### Important Directories

`/`

Root of the Linux file system.

`/home`

Contains users' personal directories.

`/etc`

Contains system and application configuration files.

`/var`

Contains variable data such as logs.

`/var/log`

Contains system and application logs.

`/tmp`

Used for temporary files.

`/usr`

Contains many user applications and system resources.

`/dev`

Contains files representing devices.

`/proc`

Contains information about running processes and the Linux kernel.

---

## 2. Navigating the File System

### pwd

Shows the current working directory.

Example:

`pwd`

### ls

Lists files and directories.

`ls`

Shows files in the current directory.

`ls -l`

Shows detailed information.

`ls -la`

Shows detailed information including hidden files.

### cd

Changes the current directory.

`cd Documents`

Moves into the Documents directory.

`cd ..`

Moves to the parent directory.

`cd ~`

Moves to the user's home directory.

`cd /`

Moves to the root directory.

---

## 3. Working With Files and Directories

### touch

Creates an empty file.

`touch notes.txt`

### mkdir

Creates a directory.

`mkdir cybersecurity`

### cp

Copies files.

`cp notes.txt backup.txt`

### mv

Moves or renames files.

`mv notes.txt old-notes.txt`

### rm

Removes files.

`rm notes.txt`

### rm -r

Removes a directory and its contents.

`rm -r folder`

Be careful when using rm because deleted files may not be easily recoverable.

---

## 4. Viewing Files

### cat

Displays the contents of a file.

`cat notes.txt`

### less

Allows a file to be viewed page by page.

`less notes.txt`

Press q to exit.

### head

Displays the beginning of a file.

`head notes.txt`

### tail

Displays the end of a file.

`tail notes.txt`

### tail -f

Continuously displays new lines added to a file.

`tail -f application.log`

This can be useful when monitoring logs in real time.

---

## 5. Searching

Searching is especially useful when investigating logs.

### grep

Searches for specific text.

`grep "error" application.log`

### grep -i

Searches without considering uppercase and lowercase differences.

`grep -i "error" application.log`

### grep -n

Shows the line number of matching results.

`grep -n "failed" application.log`

### grep -r

Searches recursively through directories.

`grep -r "password" /var/log`

### find

Searches for files and directories.

`find /var/log -name "auth.log"`

---

## 6. File Permissions

Linux controls access to files using permissions.

The three main permissions are:

Read

Write

Execute

The three main permission categories are:

Owner

Group

Others

### ls -l

Shows file permissions.

`ls -l`

Example:

`-rwxr-xr--`

The permissions can be understood as:

Owner permissions

Group permissions

Other users' permissions

### chmod

Changes file permissions.

`chmod 755 script.sh`

### chmod +x

Makes a file executable.

`chmod +x script.sh`

### chown

Changes the owner of a file.

`sudo chown user file.txt`

---

## 7. Users

### whoami

Shows the current username.

`whoami`

### id

Shows information about the current user and groups.

`id`

### who

Shows users currently logged into the system.

`who`

### last

Shows previous login activity.

`last`

### sudo

Runs a command with elevated privileges.

`sudo command`

Use sudo carefully because commands executed with elevated privileges can affect the entire system.

---

## 8. Processes

A process is a running program or task.

### ps

Shows processes associated with the current terminal.

`ps`

### ps aux

Shows running processes for all users.

`ps aux`

This is useful when investigating suspicious or unexpected processes.

### top

Displays running processes and system resource usage.

`top`

### pgrep

Searches for a process by name.

`pgrep ssh`

### kill

Terminates a process using its process ID.

`kill PID`

---

## 9. System Information

### uname

Displays system information.

`uname -a`

### hostname

Shows the system hostname.

`hostname`

### uptime

Shows how long the system has been running.

`uptime`

### free

Displays memory usage.

`free -h`

### df

Shows available disk space.

`df -h`

### du

Shows how much space a directory uses.

`du -sh folder`

---

## 10. Linux Networking

Networking commands are particularly important for cybersecurity and SOC work.

### ip addr

Displays network interfaces and IP addresses.

`ip addr`

### ip link

Displays network interfaces.

`ip link`

### ip route

Displays the routing table.

`ip route`

### ping

Tests network connectivity.

`ping 8.8.8.8`

### ss

Displays network connections and listening ports.

`ss -tuln`

### ss -tunap

Displays network connections together with associated processes when permitted.

`ss -tunap`

### hostname -I

Displays the system's IP address.

`hostname -I`

### dig

Performs DNS queries.

`dig example.com`

### nslookup

Performs DNS lookups.

`nslookup example.com`

### curl

Makes requests to web servers.

`curl example.com`

---

## 11. Linux Logs

Logs are very important in security investigations because they provide evidence of system activity.

Common Linux logs can be found in:

`/var/log`

Useful commands include:

`ls /var/log`

Lists available log files.

`less /var/log/syslog`

Views the system log on systems that use syslog.

`tail -f /var/log/syslog`

Monitors new system log entries.

`journalctl`

Displays logs collected by systemd.

`journalctl -f`

Follows new log entries in real time.

`journalctl -b`

Shows logs from the current boot.

`journalctl -u ssh`

Shows logs related to the SSH service when the service is named ssh.

### Security investigation examples

Search for failed events:

`grep -i "failed" /var/log/syslog`

Search for authentication-related activity:

`grep -i "authentication" /var/log/syslog`

The exact log files and messages can vary between Linux distributions.

---

## 12. SSH

SSH allows secure remote connections to Linux systems.

### Connect to a system

`ssh username@IP`

### Specify a port

`ssh -p 2222 username@IP`

### Exit an SSH session

`exit`

SSH is commonly used by administrators and is also an important source of authentication logs during security investigations.

---

## 13. File Hashing

Hashes can be used to identify files and verify whether files have changed.

### SHA256

`sha256sum file.txt`

### MD5

`md5sum file.txt`

SHA256 is generally preferred over MD5 for modern integrity verification because MD5 has known security weaknesses.

---

## 14. Useful Cybersecurity Commands

These commands are useful when investigating a Linux system.

### Identify current user

`whoami`

### Check user information

`id`

### Check running processes

`ps aux`

### Check listening ports

`ss -tuln`

### Check network interfaces

`ip addr`

### Check routing

`ip route`

### Search logs

`grep -i "failed" logfile`

### Find files

`find /path -name "filename"`

### Calculate file hash

`sha256sum file`

### Identify a file

`file filename`

### Extract readable strings

`strings filename`

---

## 15. TShark

TShark is the command-line version of Wireshark and is useful for network traffic analysis.

### List capture interfaces

`sudo tshark -D`

### Start a capture

`sudo tshark -i eth0`

### Capture a specific number of packets

`sudo tshark -i eth0 -c 20`

### Save a capture

`sudo tshark -i eth0 -w capture.pcapng`

### Read a capture

`tshark -r capture.pcapng`

### Display traffic statistics

`tshark -r capture.pcapng -q -z io,stat,0`

### Display IP conversations

`tshark -r capture.pcapng -q -z conv,ip`

### Extract DNS queries

`tshark -r capture.pcapng -Y "dns.qry.name"`

---

## 16. Command Help

It is not necessary to memorize every Linux command.

Linux provides built-in help.

### man

Opens the manual for a command.

`man chmod`

### help

Some commands provide help directly.

`command --help`

### history

Shows previously executed commands.

`history`

When I forget a command, I can use these resources to find the correct syntax instead of trying to memorize everything.

---

## 17. Commands I Am Currently Practicing

I am focusing on becoming comfortable with:

`pwd`

`ls`

`cd`

`mkdir`

`touch`

`cp`

`mv`

`rm`

`cat`

`less`

`head`

`tail`

`grep`

`find`

`chmod`

`whoami`

`id`

`ps`

`top`

`ip addr`

`ip route`

`ping`

`ss`

`dig`

`journalctl`

`ssh`

`sha256sum`

`tshark`

---

