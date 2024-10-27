# Network Management: Firewall Management

This document covers essential commands for managing firewalls in Linux, including commands for `iptables`, `firewalld`, and `ufw`. Proper firewall configuration is critical for securing network traffic.

---

## 1. Managing Firewalls with `iptables`

The `iptables` command is a powerful tool for configuring packet filtering, NAT, and other firewall capabilities. Note that some modern distributions now use `nftables` as the default, which replaces `iptables`.

| Command                                  | Description                                               | Example                                 |
|------------------------------------------|-----------------------------------------------------------|-----------------------------------------|
| `iptables -L`                            | List all current rules in the default filter table.       | `iptables -L`                           |
| `iptables -A INPUT -p tcp --dport port -j ACCEPT` | Allow incoming TCP connections on a specific port. | `iptables -A INPUT -p tcp --dport 22 -j ACCEPT` |
| `iptables -A INPUT -s IP -j DROP`        | Block all traffic from a specific IP address.             | `iptables -A INPUT -s 192.168.1.100 -j DROP` |
| `iptables -D INPUT rule_number`          | Delete a specific rule by its number.                     | `iptables -D INPUT 1`                   |
| `iptables -F`                            | Flush all firewall rules (clear all rules).               | `iptables -F`                           |
| `iptables-save > /path/to/file`          | Save current `iptables` rules to a file.                  | `iptables-save > /etc/iptables/rules.v4` |
| `iptables-restore < /path/to/file`       | Restore `iptables` rules from a saved file.               | `iptables-restore < /etc/iptables/rules.v4` |

---

## 2. Managing Firewalls with `firewalld`

`firewalld` is a dynamic firewall manager for modern Linux distributions, providing easier firewall management compared to `iptables`. It organizes rules by zones.

| Command                                  | Description                                               | Example                                 |
|------------------------------------------|-----------------------------------------------------------|-----------------------------------------|
| `firewall-cmd --state`                   | Check the status of `firewalld` (running or not).         | `firewall-cmd --state`                  |
| `firewall-cmd --list-all`                | List all settings for the default zone.                   | `firewall-cmd --list-all`               |
| `firewall-cmd --zone=zone --add-port=port/protocol` | Allow a port in a specific zone.               | `firewall-cmd --zone=public --add-port=80/tcp` |
| `firewall-cmd --zone=zone --remove-port=port/protocol` | Remove a port from a specific zone.          | `firewall-cmd --zone=public --remove-port=80/tcp` |
| `firewall-cmd --zone=zone --add-service=service` | Allow a predefined service in a zone.          | `firewall-cmd --zone=public --add-service=http` |
| `firewall-cmd --reload`                  | Reload `firewalld` to apply changes.                      | `firewall-cmd --reload`                 |
| `firewall-cmd --runtime-to-permanent`    | Make current runtime rules permanent.                     | `firewall-cmd --runtime-to-permanent`   |

---

## 3. Managing Firewalls with `ufw` (Uncomplicated Firewall)

`ufw` is a user-friendly firewall tool for Debian-based systems, simplifying the process of adding and removing firewall rules.

| Command                                  | Description                                               | Example                                 |
|------------------------------------------|-----------------------------------------------------------|-----------------------------------------|
| `ufw status`                             | Display the current firewall status and rules.            | `ufw status`                            |
| `ufw enable`                             | Enable the firewall with the current rules.               | `ufw enable`                            |
| `ufw disable`                            | Disable the firewall.                                     | `ufw disable`                           |
| `ufw allow port`                         | Allow traffic on a specific port.                         | `ufw allow 22`                          |
| `ufw deny port`                          | Deny traffic on a specific port.                          | `ufw deny 22`                           |
| `ufw delete allow port`                  | Delete a rule allowing traffic on a specific port.        | `ufw delete allow 22`                   |
| `ufw allow from IP to any port port`     | Allow incoming traffic from a specific IP to a port.      | `ufw allow from 192.168.1.100 to any port 22` |

---

### Examples of Firewall Management Commands in Action

1. **Allow incoming HTTP traffic on port 80 with `firewalld`**:

   ```bash
   firewall-cmd --zone=public --add-service=http --permanent
   firewall-cmd --reload

2. **Allow SSH traffic on port 22 with ufw**:

   ```bash
   ufw allow 22
   ufw enable

3. **Block traffic from a specific IP address with iptables**:

    ```bash
    iptables -A INPUT -s 192.168.1.100 -j DROP

4. **List all active rules in iptables**:

    ```bash
    iptables -L

