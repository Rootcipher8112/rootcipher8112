# Basic Linux Commands

This file contains a list of fundamental Linux commands for navigating the file system, managing files and directories, and handling basic tasks. These commands are often the first ones learned and are essential for working efficiently in a Linux environment.

---

## 1. Navigation and Directory Management

| Command           | Description                                               | Example                               |
|-------------------|-----------------------------------------------------------|---------------------------------------|
| `pwd`             | Print the current working directory path.                 | `pwd`                                 |
| `ls`              | List the contents of a directory.                         | `ls`, `ls -l`, `ls -a`                |
| `cd`              | Change the current directory.                             | `cd /path/to/directory`               |
| `mkdir`           | Create a new directory.                                   | `mkdir new_directory`                 |
| `rmdir`           | Remove an empty directory.                                | `rmdir empty_directory`               |
| `tree`            | Display directory structure in a tree-like format.        | `tree /path/to/directory`             |

---

## 2. File Management

| Command           | Description                                               | Example                               |
|-------------------|-----------------------------------------------------------|---------------------------------------|
| `touch`           | Create a new, empty file or update an existing file's timestamp. | `touch new_file.txt`              |
| `cp`              | Copy files or directories.                                | `cp file1.txt file2.txt`              |
| `mv`              | Move or rename files or directories.                      | `mv old_name.txt new_name.txt`        |
| `rm`              | Remove files or directories (use with caution!).          | `rm file.txt`, `rm -r directory/`     |
| `cat`             | Display the contents of a file.                           | `cat file.txt`                        |
| `more`            | View file contents page-by-page.                          | `more file.txt`                       |
| `less`            | Similar to `more`, but allows backward movement.          | `less file.txt`                       |
| `head`            | Display the first 10 lines of a file.                     | `head file.txt`, `head -n 20 file.txt`|
| `tail`            | Display the last 10 lines of a file.                      | `tail file.txt`, `tail -n 20 file.txt`|
| `nano`            | Open a simple text editor for creating/editing files.     | `nano file.txt`                       |
| `vi` / `vim`      | Open the `vi` or `vim` text editor.                       | `vim file.txt`                        |

---

## 3. Viewing and Searching File Content

| Command           | Description                                               | Example                               |
|-------------------|-----------------------------------------------------------|---------------------------------------|
| `grep`            | Search for patterns within files.                         | `grep "pattern" file.txt`             |
| `find`            | Search for files and directories in a directory hierarchy.| `find / -name "file.txt"`             |
| `locate`          | Quickly find files by name (uses a database).             | `locate file.txt`                     |
| `which`           | Show the path of a command.                               | `which python`                        |
| `type`            | Display the type of a command (e.g., alias, binary).      | `type ls`                             |
| `wc`              | Word, line, character, and byte count for files.          | `wc file.txt`, `wc -l file.txt`       |
| `diff`            | Compare two files line by line.                           | `diff file1.txt file2.txt`            |
| `sort`            | Sort lines in a file.                                     | `sort file.txt`, `sort -r file.txt`   |
| `uniq`            | Remove duplicate lines from sorted data.                  | `uniq file.txt`, `sort file.txt | uniq`|

---

## 4. File Permissions and Ownership

| Command           | Description                                               | Example                               |
|-------------------|-----------------------------------------------------------|---------------------------------------|
| `chmod`           | Change file permissions.                                  | `chmod 755 file.txt`                  |
| `chown`           | Change file owner and group.                              | `chown user:group file.txt`           |
| `chgrp`           | Change file group ownership.                              | `chgrp group file.txt`                |
| `umask`           | Set default permissions for new files and directories.    | `umask 022`                           |
| `ls -l`           | Display detailed file information, including permissions. | `ls -l file.txt`                      |

---

## 5. System Information

| Command           | Description                                               | Example                               |
|-------------------|-----------------------------------------------------------|---------------------------------------|
| `uname`           | Display system information.                               | `uname -a`                            |
| `df`              | Report file system disk space usage.                      | `df -h`                               |
| `du`              | Estimate file and directory disk usage.                   | `du -sh /path/to/directory`           |
| `free`            | Display memory usage.                                     | `free -m`                             |
| `uptime`          | Show how long the system has been running.                | `uptime`                              |
| `top`             | Display real-time system information (processes, memory). | `top`                                 |
| `htop`            | Enhanced `top` command with more features (if installed). | `htop`                                |
| `ps`              | Display information about active processes.               | `ps aux`, `ps -ef`                    |

---

## 6. Package Management

| Command           | Description                                               | Example                               |
|-------------------|-----------------------------------------------------------|---------------------------------------|
| `apt`             | Package management for Debian-based systems.              | `apt update`, `apt install package`   |
| `yum`             | Package management for Red Hat-based systems.             | `yum install package`, `yum update`   |
| `dnf`             | Modern replacement for `yum` on newer Red Hat systems.    | `dnf install package`                 |
| `zypper`          | Package management for openSUSE-based systems.            | `zypper install package`              |
| `pacman`          | Package management for Arch-based systems.                | `pacman -Syu`, `pacman -S package`    |

---

## 7. Networking Commands

| Command           | Description                                               | Example                               |
|-------------------|-----------------------------------------------------------|---------------------------------------|
| `ping`            | Test network connectivity to a host.                      | `ping google.com`                     |
| `ifconfig`        | Display or configure network interfaces (deprecated).     | `ifconfig`                            |
| `ip`              | Newer tool for network interface management.              | `ip a`, `ip link show`                |
| `netstat`         | Display network connections, routing tables, and more.    | `netstat -an`                         |
| `ss`              | Replacement for `netstat` to view socket statistics.      | `ss -tuln`                            |
| `traceroute`      | Show route packets take to reach a host.                  | `traceroute google.com`               |
| `nslookup`        | Query DNS to get domain/IP information.                   | `nslookup google.com`                 |
| `dig`             | DNS lookup tool providing detailed query information.     | `dig google.com`                      |

---

## 8. Miscellaneous Commands

| Command           | Description                                               | Example                               |
|-------------------|-----------------------------------------------------------|---------------------------------------|
| `echo`            | Print text to the terminal or redirect it to a file.      | `echo "Hello World"`, `echo "Text" > file.txt` |
| `date`            | Display or set the system date and time.                  | `date`, `date +"%Y-%m-%d %H:%M:%S"`   |
| `cal`             | Show a calendar for the current month or year.            | `cal`, `cal 2024`                     |
| `who`             | Show who is logged into the system.                       | `who`                                 |
| `whoami`          | Display the current user's username.                      | `whoami`                              |
| `history`         | Show command history for the current session.             | `history`                             |
| `alias`           | Create an alias for a command.                            | `alias ll='ls -l'`                    |
| `clear`           | Clear the terminal screen.                                | `clear`                               |

---

This list of basic commands is a solid foundation for Linux users to navigate, manage files, monitor the system, and handle basic administrative tasks. Each command includes an example to demonstrate its usage, making this a helpful reference.
