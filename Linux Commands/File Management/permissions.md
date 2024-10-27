# File Management: Permissions

This document covers commands for managing file and directory permissions in Linux. Properly configuring permissions ensures that users only have the access they need, which is essential for maintaining system security.

---

## 1. Viewing Permissions

| Command           | Description                                               | Example                                 |
|-------------------|-----------------------------------------------------------|-----------------------------------------|
| `ls -l`           | Display permissions, ownership, and other details of files. | `ls -l file.txt`                      |
| `stat`            | Display detailed information about a file, including permissions. | `stat file.txt`               |

*Permissions format*: In `ls -l` output, permissions appear as a string of characters like `-rw-r--r--`, where:
- The first character indicates the type (e.g., `-` for a file, `d` for a directory).
- The next nine characters represent permissions for **Owner**, **Group**, and **Others** in three groups (`rwx` - read, write, execute).

---

## 2. Changing File Permissions with `chmod`

The `chmod` command changes permissions for files and directories. Permissions can be specified using **symbolic mode** or **octal mode**.

### Symbolic Mode

| Command               | Description                                           | Example                                 |
|-----------------------|-------------------------------------------------------|-----------------------------------------|
| `chmod u+r file`      | Add read permission to the **Owner**.                 | `chmod u+r file.txt`                    |
| `chmod g-w file`      | Remove write permission from the **Group**.           | `chmod g-w file.txt`                    |
| `chmod o+x file`      | Add execute permission for **Others**.                | `chmod o+x file.txt`                    |
| `chmod u=rw,g=r,o=r`  | Set specific permissions for **Owner**, **Group**, and **Others**. | `chmod u=rw,g=r,o=r file.txt` |

### Octal Mode

Each permission is represented by an octal digit (read = 4, write = 2, execute = 1). Sum of values represents specific permissions.

| Command       | Description                                | Example                                 |
|---------------|--------------------------------------------|-----------------------------------------|
| `chmod 755 file` | Set permissions to `rwxr-xr-x` (Owner: read, write, execute; Group/Others: read, execute). | `chmod 755 file.txt` |
| `chmod 644 file` | Set permissions to `rw-r--r--` (Owner: read, write; Group/Others: read only). | `chmod 644 file.txt` |
| `chmod 700 file` | Set permissions to `rwx------` (Owner: read, write, execute; no access for Group/Others). | `chmod 700 file.txt` |

---

## 3. Changing Ownership with `chown` and `chgrp`

The `chown` and `chgrp` commands modify the ownership of files and directories.

| Command               | Description                                               | Example                                 |
|-----------------------|-----------------------------------------------------------|-----------------------------------------|
| `chown user file`     | Change the **Owner** of a file.                           | `chown john file.txt`                   |
| `chown user:group file` | Change the **Owner** and **Group** of a file.         | `chown john:staff file.txt`             |
| `chgrp group file`    | Change the **Group** of a file.                           | `chgrp staff file.txt`                  |
| `chown -R user:group dir` | Recursively change the **Owner** and **Group** of a directory and its contents. | `chown -R john:staff /path/to/dir` |

---

## 4. Special Permissions

### Setuid, Setgid, and Sticky Bit

These special permissions grant elevated privileges for files or directories.

| Command               | Description                                               | Example                                 |
|-----------------------|-----------------------------------------------------------|-----------------------------------------|
| `chmod u+s file`      | Set **Setuid** permission, allowing a file to run with the privileges of the file's owner. | `chmod u+s executable` |
| `chmod g+s dir`       | Set **Setgid** permission, making files created within a directory inherit the group of the directory. | `chmod g+s /path/to/dir` |
| `chmod +t dir`        | Set **Sticky Bit** on a directory, allowing only the file owner to delete files within it. | `chmod +t /path/to/dir` |

### Octal Representation for Special Permissions

- Setuid = `4xxx`
- Setgid = `2xxx`
- Sticky Bit = `1xxx`

For example:
- `chmod 4755 file` sets Setuid with `rwsr-xr-x` permissions.
- `chmod 2755 dir` sets Setgid with `rwxr-sr-x` permissions.
- `chmod 1777 dir` sets Sticky Bit with `rwxrwxrwt` permissions.

---

## 5. Default Permissions with `umask`

The `umask` command sets default permissions for newly created files and directories.

| Command           | Description                                               | Example                                 |
|-------------------|-----------------------------------------------------------|-----------------------------------------|
| `umask`           | Display the current `umask` value.                        | `umask`                                 |
| `umask 022`       | Set default permissions for new files and directories (e.g., 755 for directories, 644 for files). | `umask 022` |

The `umask` value subtracts permissions from the default (777 for directories, 666 for files). For example, `umask 022` results in 755 for directories and 644 for files.

---

### Examples of Permissions Commands in Action

1. **Make a script executable for the owner only**:

   - **Command**: `chmod 700 my_script.sh`

2. **Give read and execute permissions to everyone for a directory**:

   - **Command**: `chmod 755 /path/to/directory`

3. **Set the Setgid bit on a directory so files inherit the group**:

   - **Command**: `chmod g+s /project_directory`

4. **Set Sticky Bit on `/shared` directory** so only file owners can delete their own files:

   - **Command**: `chmod +t /shared`


This file provides a detailed reference for handling permissions in Linux, with examples for both standard and special permissions. 

