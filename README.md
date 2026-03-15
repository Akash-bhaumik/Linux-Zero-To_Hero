# 🐧 The Ultimate Linux & DevOps Interview Master Guide

While learning Linux and Shell Scripting, one thing becomes clear: In DevOps, **"it works on my machine"** is not enough. 

Real-world infrastructure requires:
* predictable automation
* secure permissions
* proper process management
* reliable troubleshooting

This chapter summarizes important Linux interview questions that every DevOps engineer should understand.

---

## 🟢 Module 1: System Foundations & Shell Basics

### 1. What is the Linux Kernel?
The Linux Kernel is the core of the operating system. It acts as the primary layer between the hardware and the software.
It manages:
* CPU scheduling
* memory management
* device drivers
* system calls
* process control
Applications interact with hardware through the kernel.

### 2. What is a Shell in Linux?
A **Shell** is a command-line interface that allows users to interact with the Linux operating system. It acts as a **bridge between the user and the Linux Kernel**.
When a user types a command, the shell:
1. Interprets the command
2. Sends it to the kernel
3. Displays the result

Common Linux Shells:
| Shell | Description |
|------|-------------|
| bash | Bourne Again Shell (most commonly used) |
| sh | Bourne Shell |
| zsh | Advanced interactive shell |
| fish | User-friendly interactive shell |
DevOps engineers use shells to run commands, automate tasks, and write scripts.

### 3. Why do scripts start with #!/bin/bash ?
This line is called a **shebang**.
Example:
```bash
#!/bin/bash
echo "Hello Linux"
Purpose: tells the system which interpreter should run the script.
Example interpreters: /bin/bash, /bin/sh, /usr/bin/python.
Many systems link /bin/sh to dash, which does not support all Bash features. Using #!/bin/bash ensures consistent script behavior.

4. Why do DevOps scripts use set -euo pipefail ?
Professional shell scripts often start with: set -euo pipefail. This prevents hidden errors.

set -e: Exit script if any command fails.

set -u: Exit if an undefined variable is used.

set -o pipefail: If any command in a pipeline fails, the whole pipeline fails.
Example: grep "test" file | sort. Without pipefail, errors might go unnoticed.

5. What is the difference between a relative path and an absolute path?
Absolute Path: Full path starting from the root directory /.
Example: /home/akash/project/file.txt

Relative Path: Path relative to the current working directory.
Example: project/file.txt
Check current directory with: pwd.

6. Difference between touch and vim
touch (touch file.txt): creates empty file, updates file timestamp, non-interactive. Used in automation.

vim (vim file.txt): opens text editor, used to modify files, interactive. Used for manual configuration.

7. What is the difference between > and >>?
Both are output redirection operators.

>: Overwrites the file. Example: echo "Hello" > file.txt

>>: Appends to the file. Example: echo "Hello again" >> file.txt
DevOps engineers use redirection in logs and automation scripts.

8. What are Environment Variables?
Environment variables store system-wide configuration values.
Examples:
| Variable | Purpose |
|----------|---------|
| PATH | Locations of executable programs |
| HOME | User home directory |
| USER | Current logged-in user |
Example: echo $PATH. You can set a variable temporarily: export MY_VAR="hello"

9. What is the $PATH variable?
PATH is an environment variable that tells the shell where to find executable commands.
Example: echo $PATH
Output example: /usr/local/bin:/usr/bin:/bin
If a command is inside these directories, you can run it directly. Example: ls instead of /bin/ls.

10. What is the history command?
The history command shows previously executed commands.
Example: history
Example output:

ls

cd /var/log

cat syslog
Run a previous command: !3

🟡 Module 2: User Access & Permissions
11. What are Linux File Permissions?
Linux permissions control who can access files.
Permission types:
| Permission | Value |
|------------|-------|
| Read | 4 |
| Write | 2 |
| Execute | 1 |

Example: -rwxr-xr--
Meaning:

Owner → read write execute

Group → read execute

Others → read
Important commands: chmod, chown, chgrp. Permissions are critical for system security.

12. What is the chmod command?
chmod changes file permissions.
Syntax: chmod permissions file
Example: chmod 755 script.sh
755 means: Owner → read, write, execute; Group → read, execute; Others → read, execute.

13. What is the chown command?
chown changes file ownership.
Example: chown user:group file.txt
Example command: chown akash:developers project.txt
DevOps engineers often change ownership for services and applications.

14. If you have permission to a file but not to its directory, can you access the file?
Answer: No.
Linux requires execute permission on the directory to access files inside it. Even if you have permission on the file itself, the system cannot reach it without directory access.

Real-Life Analogy (Bank and Locker)
Think of this as: Bank Building → Directory | Locker → File.
Scenario: You have permission to open the locker but you are not allowed inside the bank. Can you open the locker? ❌ No. Because you cannot reach it. Same logic applies in Linux file systems.

15. What is the root user in Linux?
The root user is the superuser with full system privileges.
Capabilities: Install software, Modify system files, Manage users, Control services.
Example: sudo su.
Best practice in DevOps: Avoid logging in directly as root. Use sudo for better security and auditing.

16. What is the difference between su and sudo?
su: Switches to another user. Example: su root. You must know the root password.

sudo: Runs a command with temporary root privileges. Example: sudo apt update. Requires the user's own password.
Best practice: Use sudo instead of logging in as root to improve system security.

17. What is the difference between apt and yum?
Both are package managers.
| Package Manager | Distribution |
|-----------------|--------------|
| apt | Debian / Ubuntu |
| yum | RedHat / CentOS |
Example Ubuntu: sudo apt install nginx. Example CentOS: sudo yum install nginx.

🟠 Module 3: File System Structure & Links
18. What is the difference between a Hard Link and a Soft Link?
Linux supports two types of links.

Hard Link: Points directly to the inode of the file. If the original file is deleted, the hard link still works. Example: ln file.txt hardlink.txt

Soft Link (Symbolic Link): Points to the path of another file. If the original file is deleted, the link becomes broken. Example: ln -s file.txt softlink.txt
Simple idea: Hard link → same file | Soft link → shortcut to file.

19. What is the /etc directory?
/etc is one of the most important directories in Linux. It stores system configuration files.
Examples:
| File | Purpose |
|------|---------|
| /etc/passwd | User account information |
| /etc/shadow | Encrypted passwords |
| /etc/hosts | Local DNS mappings |
| /etc/fstab | Filesystem mount configuration |
| /etc/ssh/sshd_config | SSH server configuration |
Example: cat /etc/passwd.

20. What is the /var directory used for?
/var stands for variable data. It stores files that change frequently.
Common contents:
| Directory | Purpose |
|-----------|---------|
| /var/log | System logs |
| /var/spool | Mail and print queues |
| /var/cache | Cached data |
Example: cd /var/log. Log analysis is a key DevOps skill.

21. What is the tar command used for?
tar is used to archive and compress files.

Create archive: tar -cvf archive.tar folder/

Extract archive: tar -xvf archive.tar

Compressed archive: tar -czvf archive.tar.gz folder/
tar is widely used for backups and deployment packaging.

22. How do you find files in Linux?
Use the find command.
Example: find /home -name file.txt (searches for file.txt inside /home).
Example with extension: find / -name "*.log". find is heavily used in server troubleshooting and automation scripts.

23. What is grep used for?
grep searches for specific patterns inside files.
Example: grep "error" logfile.txt.
Useful options:

grep -i → case insensitive

grep -r → search recursively

grep -n → show line numbers
It is one of the most important Linux commands for log analysis and debugging.

🔵 Module 4: Process & Service Management
24. What is the difference between ps -ef and ps aux?
Both commands display running processes in Linux.

ps -ef: Uses UNIX style options. Shows full process information. Important columns: UID (User), PID (Process ID), PPID (Parent PID), STIME (Start time), CMD.

ps aux: Uses BSD style options. Shows resource usage. Important columns: USER, %CPU, %MEM, VSZ (Virtual memory), RSS (Physical memory).
Key idea: ps -ef → process hierarchy | ps aux → resource usage.

25. What is the difference between a Process and a Service?
Process: A running instance of a program. Examples: nginx, docker, python, mysql. View processes: ps aux.

Service: A background program managed by the system. Examples: nginx, sshd, docker, mysql. Managed using: systemctl start nginx.
Simple explanation: Process → running program | Service → managed background process.

26. Difference between kill PID and kill -9 PID
Linux processes can be terminated using signals.

kill PID (SIGTERM 15): polite request to stop, process can close files, allows cleanup.

kill -9 PID (SIGKILL 9): forcefully kills process, cannot be ignored, no cleanup happens.
Best practice: Use kill first; Use kill -9 only if necessary. DevOps engineers usually try graceful termination first.

27. What is a Zombie Process?
A zombie process is a process that has finished execution but still has an entry in the process table. It happens when the parent process does not collect the exit status. Check zombies: ps -ef | grep defunct.

28. What is a daemon in Linux?
A daemon is a background process that runs continuously.
Examples:
| Daemon | Purpose |
|--------|---------|
| sshd | SSH server |
| httpd | Web server |
| dockerd | Docker service |
Check daemon status: systemctl status sshd.

29. How do you check running services?
Use: systemctl list-units --type=service.
Check specific service: systemctl status nginx. This command shows: service state, logs, and error messages.

30. What is top command?
top shows real-time system monitoring information. It displays: CPU usage, memory usage, running processes, and system load. DevOps engineers use it to identify high CPU or memory processes.

🔴 Module 5: Advanced Troubleshooting (CPU, Disk, Memory)
31. Server CPU suddenly becomes 100%. How will you debug it?
First check which process is consuming CPU: top or htop. Then identify the process ID (PID).
Example: ps -p PID -o %cpu,%mem,cmd.
If the process is abnormal:

restart the service

investigate logs

or terminate it carefully (kill PID)
DevOps Tip: Always check logs before killing production processes.

32. Server becomes slow. What steps will you take?
Check system resources:

CPU usage: top

Memory usage: free -h

Disk I/O: iostat

Disk space: df -h

Running processes: ps aux --sort=-%cpu
These checks usually reveal the performance bottleneck.

33. How do you check memory usage in Linux?
Use: free -h. Output shows: total memory, used memory, free memory, and swap usage. For detailed view: top. Memory problems often occur due to memory leaks in applications.

34. What is the difference between df and du?
Both commands check disk usage.

df (df -h): Shows disk space usage of file systems. Example output columns: Filesystem, Size, Used, Avail.

du (du -sh folder): Shows size of directories and files.
Key difference: df → disk usage of filesystem | du → disk usage of files/folders.

35. Disk is full. How do you investigate it?
First check disk usage: df -h. Then check which directories are consuming space: du -sh /*. Find the largest directories. Often the problem is: large logs, unused files, docker images, or backups.

36. df shows disk full but du does not. Why?
This usually happens when a deleted file is still being used by a running process. Example scenario: A log file is deleted but the application still holds the file descriptor.
Find such files: lsof | grep deleted.
Solution: Restart the process or service holding the file.

37. How do you find the largest files in a server?
Use: du -ah / | sort -rh | head -20. This command shows the largest files and directories. Useful when disk suddenly fills up or storage alerts appear.

38. Application is not starting. What will you check first?
Follow a basic troubleshooting checklist. Check:

Service status: systemctl status service_name

Logs: journalctl -u service_name

Configuration errors

Port conflicts

Permission issues
Most failures happen due to misconfiguration or missing dependencies.

39. A service keeps crashing. How will you debug it?
Steps:

Check service status: systemctl status service

Check logs: journalctl -u service

Check configuration files

Verify dependencies

Restart service: systemctl restart service
Understanding logs is the most important skill in troubleshooting.

40. Application is running but website is not opening. What could be wrong?
Possible reasons:

Port not open

Firewall blocking traffic

DNS issue

Reverse proxy misconfiguration

Load balancer issue
Check if service is listening: ss -tuln. Test locally: curl localhost:PORT.

🛠 Module 6: Networking & Automation
41. What is SSH?
SSH (Secure Shell): It is a protocol used to securely connect to remote servers.
Example: ssh user@server_ip.
DevOps engineers use SSH to manage remote servers, deploy applications, and run remote commands.

42. How do you check which process is using a port?
Example: check port 8080
lsof -i :8080 or netstat -tulpn | grep 8080.
This shows the process using that port. Useful when application cannot start or port is already in use.

43. How do you check open ports in Linux?
Use: ss -tuln or netstat -tuln. These commands show listening ports, protocols, and services using those ports.

44. How do you monitor logs in real time?
Use: tail -f logfile.
Example: tail -f /var/log/syslog or tail -f /var/log/nginx/error.log.
This shows live updates of logs. Very useful when debugging applications, monitoring servers, or troubleshooting production systems.

45. How do you schedule automated tasks in Linux?
Use cron jobs. Edit crontab: crontab -e.
Example job: 0 2 * * * /backup/script.sh.
This runs the script every day at 2 AM. Cron is widely used for backups, automation, and maintenance tasks.

46. How do you check system uptime?
Use the command: uptime.
Example output: 10:30:15 up 5 days, 3 users, load average: 0.45, 0.30, 0.25.
This shows how long the system has been running, number of logged-in users, and system load averages.

47. What is the Linux Boot Process?
The sequence of steps when a system starts:

BIOS / UEFI: Hardware initialization and system checks.

Bootloader (GRUB): Loads the Linux Kernel.

Kernel Initialization: Kernel loads device drivers and mounts the root filesystem.

Init System (systemd): Starts system services.

User Space: Login prompt or graphical interface appears.

48. Important Linux Troubleshooting Commands Table
Task	Command
Check running processes	ps, top, htop
Check disk space	df -h
Check folder size	du -sh
Check memory usage	free -h
Search files	find
Search text	grep
Check ports	ss -tulnp
View logs	tail -f logfile
49. Permission Calculation Guide
Permission	Value
Read	4
Write	2
Execute	1
Example: chmod 755 script.sh	
Meaning: Owner (4+2+1=7), Group (4+1=5), Others (4+1=5). Permissions are critical for system security.	
50. Final Troubleshooting Takeaway
Troubleshooting is about logic and logs. Whether it is a CPU spike, a full disk, or a crashing application, always follow the data: Check resources (top, df, free), then check the status (systemctl), and finally deep dive into the logs (tail -f, journalctl).
