# System Management: User Management

This document covers essential commands for managing users and groups in Linux. User management is crucial for controlling access to system resources and maintaining security.

---

## 1. Creating and Managing Users

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `adduser username`         | Add a new user with a home directory and default settings. | `adduser jdoe`                          |
| `useradd username`         | Add a new user with basic settings (may need to create a home directory manually). | `useradd jdoe` |
| `userdel username`         | Delete a user account but leave the home directory.       | `userdel jdoe`                          |
| `userdel -r username`      | Delete a user account and remove the home directory.      | `userdel -r jdoe`                       |
| `passwd username`          | Set or update a user’s password.                          | `passwd jdoe`                           |

---

## 2. Modifying User Accounts

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `usermod -l newname oldname` | Change a user’s username.                               | `usermod -l john jdoe`                  |
| `usermod -d /new/home username` | Change a user’s home directory.                   | `usermod -d /home/newhome jdoe`         |
| `usermod -aG group username`   | Add a user to an additional group.                | `usermod -aG sudo jdoe`                 |
| `usermod -L username`      | Lock a user account to disable login.                    | `usermod -L jdoe`                       |
| `usermod -U username`      | Unlock a user account.                                   | `usermod -U jdoe`                       |

---

## 3. Creating and Managing Groups

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `groupadd groupname`       | Create a new group.                                       | `groupadd developers`                   |
| `groupdel groupname`       | Delete a group.                                           | `groupdel developers`                   |
| `groupmod -n newname oldname` | Rename an existing group.                             | `groupmod -n devs developers`           |
| `gpasswd -a username groupname` | Add a user to a group.                             | `gpasswd -a jdoe developers`            |
| `gpasswd -d username groupname` | Remove a user from a group.                        | `gpasswd -d jdoe developers`            |

---

## 4. Viewing User and Group Information

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `id username`              | Display user ID (UID), group ID (GID), and groups for a user. | `id jdoe`                       |
| `groups username`          | List all groups a user belongs to.                        | `groups jdoe`                           |
| `getent passwd username`   | Retrieve user account details from the system database.   | `getent passwd jdoe`                    |
| `getent group groupname`   | Retrieve group details from the system database.          | `getent group developers`               |
| `finger username`          | Display user information (may need to install `finger`).  | `finger jdoe`                           |

---

## 5. Setting Default Permissions for Users with `umask`

The `umask` command sets default permissions for new files and directories created by a user. It subtracts permissions from the system defaults (usually 666 for files and 777 for directories).

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `umask`                    | Display the current `umask` value for the session.        | `umask`                                 |
| `umask 022`                | Set the default permission to 755 for directories and 644 for files. | `umask 022`                   |

---

## 6. Configuring Login Permissions

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `chage -l username`        | List password expiration information for a user.          | `chage -l jdoe`                         |
| `chage -M days username`   | Set maximum days before password expiration.              | `chage -M 90 jdoe`                      |
| `chage -E date username`   | Set account expiration date.                              | `chage -E 2024-12-31 jdoe`              |
| `faillog -u username`      | Display failed login attempts for a user.                 | `faillog -u jdoe`                       |
| `faillog -r -u username`   | Reset failed login attempts for a user.                   | `faillog -r -u jdoe`                    |

---

### Examples of User Management Commands in Action

1. **Create a new user with a home directory and set a password**:

   ```bash
   adduser newuser
   passwd newuser

2. **Add a user to the sudo group to grant administrative privileges**:

   ```bash
   usermod -aG sudo newuser

3. **Set password expiration to force a password change every 90 days**:

   ```bash
   chage -M 90 newuser

4. **Lock a user account to prevent login**:

    ```bash
    usermod -L newuser

