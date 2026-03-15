# 🐧 The Ultimate Linux & DevOps Interview Master Guide (50 Questions)

In DevOps, "it works on my machine" is not enough. Real-world infrastructure requires predictable automation, secure permissions, proper process management, and reliable troubleshooting.

---

## 🔵 Module 1: System Foundations & Shell Basics

### ### 1. What is the Linux Kernel?
* **The Logic:** The Kernel is the core "engine" of the OS. It sits between software and hardware. 
* **Explanation:** When an application (like a web browser) needs to use the RAM or CPU, it sends a "System Call" to the Kernel. The Kernel then manages the hardware to fulfill that request.
* **Example Command:** You can check your kernel version and system info with:
`uname -a`

### ### 2. What is a Shell in Linux?
* **The Logic:** It is a command interpreter.
* **Explanation:** The Kernel doesn't understand English. The Shell is the bridge. It takes the words you type (like `ls`) and translates them into instructions for the Kernel.
* **Common Shells:** `bash` (standard), `zsh` (Mac/Advanced), `sh` (basic).
* **Check your shell:**
`echo $SHELL`

### ### 3. Why do scripts start with `#!/bin/bash`?
* **The Logic:** This is called a **Shebang**.
* **Explanation:** It tells the Kernel exactly which program (interpreter) to use to execute the script. Without this, the system might try to run a Bash script with an incompatible shell, leading to errors.
* **Example:**
`#!/bin/bash` (Always put this on the very first line of your `.sh` files).

### ### 4. Why do DevOps scripts use `set -euo pipefail`?
* **The Logic:** This is "Professional Strict Mode."
* **Explanation:** * `-e`: Stops the script if any command fails.
  * `-u`: Stops if you use a variable that hasn't been defined (prevents typos).
  * `-o pipefail`: If a command inside a pipe (like `grep | sort`) fails, the whole script fails.
* **Why it matters:** It prevents "silent failures" where a script keeps running even after a mistake.

### ### 5. Difference between `touch` and `vim`?
* **The Logic:** Creation vs. Editing.
* **Explanation:** `touch` just "pokes" the system to create an empty file. `vim` is a full editor where you actually go *inside* the file to write text.
* **Commands:**
`touch newfile.txt` (Create)
`vim newfile.txt` (Edit)

### ### 6. What is the difference between `>` and `>>`?
* **The Logic:** Overwrite vs. Append.
* **Explanation:** `>` wipes the file clean and puts in new text. `>>` adds the new text to the bottom of the existing content.
* **Commands:**
`echo "Hello" > file.txt` (File now says: Hello)
`echo "World" >> file.txt` (File now says: Hello \n World)

### ### 7. Absolute vs. Relative Paths
* **The Logic:** Full address vs. Directions from current location.
* **Absolute Path:** Starts from the root `/` (e.g., `/home/akash/file.txt`).
* **Relative Path:** Starts from where you are (e.g., `Documents/file.txt`).
* **Check current location:**
`pwd`

### ### 8. What are Environment Variables?
* **The Logic:** System-wide settings.
* **Explanation:** They store info that all processes can access, like your username or the location of your home folder.
* **View all variables:**
`printenv`

### ### 9. What is the `$PATH` variable?
* **The Logic:** The "Search Directory."
* **Explanation:** When you type a command like `git`, the shell looks through every folder in your `$PATH` to find the `git` program. If the folder isn't listed there, you'll get "Command not found."
* **View PATH:**
`echo $PATH`

### ### 10. What is the `history` command?
* **The Logic:** Your command diary.
* **Explanation:** It shows a numbered list of everything you've typed. You can repeat command number 10 by typing `!10`.
`history`

---

## 🟢 Module 2: Access, Permissions & Filesystem

### ### 11. What are Linux File Permissions?
* **The Logic:** Access control (Read, Write, Execute).
* **Values:** Read (4), Write (2), Execute (1).
* **Structure:** Owner | Group | Others.
* **Check permissions:**
`ls -l`



### ### 12. What is the `chmod` command?
* **The Logic:** Changing *what* can be done.
* **Explanation:** Used to give or take away permissions.
* **Example:** Make a script executable:
`chmod +x myscript.sh`

### ### 13. What is the `chown` command?
* **The Logic:** Changing *who* owns it.
* **Explanation:** Changes the User or Group that owns a file.
* **Example:**
`sudo chown akash:devs data.txt`

### ### 14. If you have permission for a file but not its directory, can you access it?
* **The Logic:** Directory access is the "Gatekeeper."
* **Answer: No.** * **Analogy:** Think of the directory as a **Bank Building** and the file as your **Locker**. Even if you have the locker key (file permission), if security won't let you in the building (directory execute permission), you cannot reach your locker.

### ### 15. Hard Link vs. Soft Link (Symbolic Link)
* **Soft Link (`ln -s`)**: A shortcut to the filename. If the original is deleted, the link breaks.
* **Hard Link (`ln`)**: A direct link to the data on the disk. If the original filename is deleted, the data is still safe via the hard link.
* **Example:**
`ln -s original.txt shortcut.txt`

### ### 16. What is the `/etc` directory?
* **The Logic:** The Configuration Hub.
* **Explanation:** Stores all system-wide settings, like user lists (`/etc/passwd`) or network maps (`/etc/hosts`).

### ### 17. What is the `/var` directory?
* **The Logic:** Variable/Growth folder.
* **Explanation:** Stores data that changes constantly, like logs (`/var/log`) and databases.

### ### 18. What is the `tar` command?
* **The Logic:** Archiving and Compression.
* **Explanation:** Bundles many files into one "Tarball" to save space or for easy moving.
* **Create a backup:**
`tar -czvf backup.tar.gz /path/to/folder`

---

## 🟡 Module 3: Process & Service Management

### ### 19. `ps -ef` vs `ps aux`
* **`ps -ef`**: Best for seeing the **Process Hierarchy** (Parent/Child relationships).
* **`ps aux`**: Best for seeing **Resource Consumption** (%CPU, %Memory).

### ### 20. Difference between `kill` and `kill -9`
* **`kill` (SIGTERM)**: Polite. Asks the app to save its work and close.
* **`kill -9` (SIGKILL)**: Forceful. Kills the app instantly. **Warning:** Can cause data corruption.
`kill 1234`

### ### 21. Process vs. Service
* **Process:** Any running program (e.g., `python script.py`). Stops when the job is done.
* **Service:** A background program (e.g., `nginx`). Managed by the system to run forever.
`systemctl status nginx`

### ### 22. What is a Zombie Process?
* **The Logic:** A ghost entry.
* **Explanation:** A process that finished running, but the parent process hasn't acknowledged its death yet. It occupies a spot in the "Process Table."

### ### 23. What is a daemon?
* **The Logic:** Background workers.
* **Explanation:** Services that run in the background waiting for work (e.g., `sshd` waits for you to login).

### ### 24. What is the root user?
* **The Logic:** Superuser.
* **Explanation:** The user with UID 0 who can bypass all security and permissions. Always use `sudo` instead of logging in as root directly.

### ### 25. `su` vs `sudo`
* **`su`**: You "become" the other user (requires their password).
* **`sudo`**: You run a command with root privileges (requires your own password).

---

## 🟠 Module 4: The Beginner's Guide to Troubleshooting

### ### 26. Difference between `df` and `du`?
* **`df -h`**: "Disk Free." Shows usage of the whole disk filesystem.
* **`du -sh`**: "Disk Usage." Shows the size of a specific folder.
`df -h`

### ### 27. Why might `df` show Full, but `du` shows Empty?
* **The Problem:** You deleted a large log file, but `df` still says 100% full.
* **The Reason:** A running process (like a web server) still has that file **open**. Linux won't release the disk space until the process stops.
* **The Fix:** Find the process with `lsof | grep deleted` and restart it.

### ### 28. Disk is full! How do you investigate?
1. `df -h` (Find the full partition).
2. `du -sh /*` (Find the biggest main folder).
3. `du -sh /var/log/*` (Drill down into logs/backups).

### ### 29. How do you find the largest files on a server?
Run this one-liner:
`du -ah / | sort -rh | head -20`
* `du -ah`: List all files/folders with sizes.
* `sort -rh`: Sort by size, biggest first.
* `head -20`: Show top 20.

### ### 30. Server CPU is at 100%. How do you debug?
1. Run `top` or `htop`.
2. Find the **PID** (Process ID) at the top of the list.
3. Check the command name. If it's abnormal, investigate logs before killing it.

### ### 31. Server is slow. What 4 things do you check?
Check the "4 Pillars":
1. **CPU** (`top`)
2. **RAM** (`free -h`)
3. **Disk Space** (`df -h`)
4. **I/O Wait** (Is the disk slow at reading?)

### ### 32. How do you check Memory (RAM) usage?
`free -h`
* **Check "Swap":** If Swap is being used heavily, the server will be slow because it's using the hard drive as RAM.

### ### 33. How to check who is using a specific port (e.g., 80)?
If an app won't start because the port is "already in use":
`sudo lsof -i :80`

### ### 34. How do you monitor logs in real-time?
`tail -f /var/log/syslog`
(The `-f` stands for "follow." New errors pop up live).

### ### 35. Application is not starting. Troubleshooting checklist?
1. **Status:** `systemctl status myapp`
2. **Logs:** `journalctl -u myapp -f`
3. **Port:** Is the port taken? (`ss -tulnp`)
4. **Config:** Check for typos in the configuration files.

### ### 36. A service keeps crashing. How do you debug?
1. Check `journalctl -xe` for recent crash messages.
2. Check for "Out of Memory" (OOM) errors in `/var/log/messages`.
3. Verify that the service has permission to write its logs.

### ### 37. App is running, but the website won't open.
1. Is the port listening? (`ss -tuln`).
2. Is the Firewall blocking it? (`sudo ufw status`).
3. Can you reach it from the server itself? (`curl localhost:80`).

### ### 38. How to check open ports?
`ss -tuln`
(Shows all active "doors" open on your server).

### ### 39. How do you check running services?
`systemctl list-units --type=service`

---

## 🔴 Module 5: Tools, Networking & Automation

### ### 40. What is `grep`?
* **The Logic:** The Search Filter.
* **Example:** Find the word "Error" in a giant log file:
`grep "Error" logfile.txt`

### ### 41. What is the `top` command?
The real-time task manager. It shows you the health of your CPU and RAM and every active process.

### ### 42. How do you find a specific file?
`find / -name "config.yml"`
(Searches the whole system for that specific name).

### ### 43. What is `uptime`?
Shows how long the server has been running and the **Load Average**.
`uptime`

### ### 44. What is SSH?
**Secure Shell.** The standard protocol to securely log into and manage a remote server.
`ssh user@server-ip`

### ### 45. `apt` vs `yum`
The "App Stores" of Linux.
* **`apt`**: Ubuntu/Debian.
* **`yum`**: RedHat/CentOS.

### ### 46. How to schedule automated tasks?
Use **Cron Jobs**.
`crontab -e`
(Schedule scripts to run at 2 AM every night).

### ### 47. The Linux Boot Process
1. **BIOS/UEFI** (Hardware check)
2. **GRUB** (Bootloader/Choose OS)
3. **Kernel** (Connects hardware)
4. **systemd** (Starts services like SSH/Web)
5. **Login** (User access)

### ### 48. Essential Troubleshooting Table
| Task | Command |
| :--- | :--- |
| **CPU Health** | `top` / `htop` |
| **Memory usage** | `free -h` |
| **Disk space** | `df -h` |
| **Live Logs** | `tail -f` |
| **Port check** | `ss -tulnp` |

### ### 49. How do you find files with specific extensions?
`find /var/log -name "*.gz"`
(Finds all compressed log files).

### ### 50. Final Troubleshooting Takeaway
Always follow the data trail: Check **Resources** (`top`, `df`), then **Status** (`systemctl`), then **Logs** (`tail -f`, `journalctl`). **The logs will always tell you what's wrong if you look close enough.**