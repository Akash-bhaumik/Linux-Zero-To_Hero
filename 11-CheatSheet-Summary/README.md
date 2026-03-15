# Linux Command CheatSheet (Interview Revision)

This chapter contains a **quick summary of the most important Linux commands** covered in this repository.  
It is designed for **fast revision before interviews or practical work**.

---

# 1. System Navigation Commands

| Command | Purpose |
|------|------|
| `pwd` | Show current directory |
| `ls` | List files in directory |
| `ls -l` | Detailed file listing |
| `ls -a` | Show hidden files |
| `cd /path` | Change directory |
| `clear` | Clear terminal screen |

---

# 2. File & Directory Management

| Command | Purpose |
|------|------|
| `mkdir folder` | Create directory |
| `rmdir folder` | Remove empty directory |
| `rm file` | Delete file |
| `rm -r folder` | Delete folder recursively |
| `cp file1 file2` | Copy file |
| `cp -r dir1 dir2` | Copy directory |
| `mv file newname` | Move or rename file |
| `touch file.txt` | Create empty file |

---

# 3. File Viewing Commands

| Command | Purpose |
|------|------|
| `cat file` | Display file content |
| `less file` | Scroll through file |
| `more file` | View file page by page |
| `head file` | First 10 lines |
| `tail file` | Last 10 lines |
| `tail -f file` | Live log monitoring |

---

# 4. User Management

| Command | Purpose |
|------|------|
| `useradd username` | Create new user |
| `adduser username` | Interactive user creation |
| `passwd username` | Change password |
| `usermod -aG group user` | Add user to group |
| `groups username` | Show user groups |
| `userdel username` | Delete user |
| `userdel -r username` | Delete user with home directory |

Important Files:


/etc/passwd
/etc/shadow
/etc/group


---

# 5. File Permissions

### Permission Types

| Permission | Value |
|------|------|
| Read | 4 |
| Write | 2 |
| Execute | 1 |

### Example


-rwxr-xr-- file.sh


Meaning:


User = rwx
Group = r-x
Others = r--


### Important Commands

| Command | Purpose |
|------|------|
| `chmod 755 file` | Change permissions |
| `chmod +x file` | Add execute permission |
| `chown user file` | Change owner |
| `chgrp group file` | Change group |

---

# 6. Process Management

| Command | Purpose |
|------|------|
| `ps aux` | Show running processes |
| `pgrep process` | Find process PID |
| `pidof process` | Get process ID |
| `kill PID` | Terminate process |
| `kill -9 PID` | Force kill process |
| `pkill process` | Kill by name |

### Background Jobs

| Command | Purpose |
|------|------|
| `command &` | Run process in background |
| `jobs` | Show background jobs |
| `fg %1` | Bring job to foreground |
| `bg %1` | Resume job in background |

---

# 7. System Monitoring

| Command | Purpose |
|------|------|
| `top` | Real-time process monitoring |
| `htop` | Advanced process viewer |
| `free -m` | Memory usage |
| `vmstat` | CPU & memory stats |

---

# 8. Disk Usage

| Command | Purpose |
|------|------|
| `df -h` | Disk space usage |
| `du -sh folder` | Folder size |
| `lsblk` | List disks |
| `fdisk -l` | Show partitions |

---

# 9. Disk Management

| Command | Purpose |
|------|------|
| `fdisk /dev/sdX` | Partition disk |
| `mkfs.ext4 /dev/sdX1` | Format disk |
| `mount /dev/sdX1 /mnt` | Mount disk |
| `umount /mnt` | Unmount disk |

---

# 10. Networking Commands

| Command | Purpose |
|------|------|
| `ip a` | Show IP address |
| `ping google.com` | Check connectivity |
| `netstat -tulnp` | Show open ports |
| `ss -tulnp` | Socket statistics |
| `curl url` | Fetch webpage |
| `wget url` | Download file |
| `ssh user@host` | Remote login |

---

# 11. Package Management

### Ubuntu / Debian

| Command | Purpose |
|------|------|
| `sudo apt update` | Update package list |
| `sudo apt upgrade` | Upgrade packages |
| `sudo apt install pkg` | Install package |
| `sudo apt remove pkg` | Remove package |
| `sudo apt autoremove` | Clean dependencies |

---

# 12. Log Monitoring

| Command | Purpose |
|------|------|
| `journalctl` | System logs |
| `journalctl -f` | Live logs |
| `dmesg` | Kernel logs |
| `tail -f /var/log/syslog` | Monitor logs |

---

# Quick Linux Workflow Example

Example daily workflow:

Update system

sudo apt update && sudo apt upgrade

Check disk

df -h

Monitor processes

top

Check running services

systemctl list-units --type=service

Check logs

journalctl -f


---

# Quick Interview Tips

Most commonly asked commands:


ls
cd
cp
mv
rm
chmod
chown
ps
top
kill
df
du
ip a
ping
ssh
apt


Understanding these commands **covers 80% of Linux interview questions.**

---

# Conclusion

This cheat sheet summarizes the **most essential Linux commands** required for:

• System administration  
• DevOps workflows  
• Troubleshooting servers  
• Linux interviews  

Use it as a **quick revision guide before interviews or while working with Linux systems.**