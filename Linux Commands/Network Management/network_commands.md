# Network Management: Network Commands

This document covers essential commands for managing and troubleshooting networks in Linux. These commands help monitor network interfaces, configure IP addresses, and diagnose network connectivity issues.

---

## 1. Viewing and Configuring Network Interfaces

| Command                         | Description                                               | Example                                 |
|---------------------------------|-----------------------------------------------------------|-----------------------------------------|
| `ifconfig`                      | Display or configure network interfaces (deprecated in favor of `ip`). | `ifconfig`                 |
| `ip a`                          | Display IP addresses and status for all interfaces.       | `ip a`                                  |
| `ip link show`                  | Show details for network interfaces.                      | `ip link show`                          |
| `ip addr add IP dev interface`  | Assign an IP address to a network interface.              | `ip addr add 192.168.1.10/24 dev eth0`  |
| `ip addr del IP dev interface`  | Remove an IP address from a network interface.            | `ip addr del 192.168.1.10/24 dev eth0`  |
| `ip link set interface up`      | Bring a network interface up.                             | `ip link set eth0 up`                   |
| `ip link set interface down`    | Bring a network interface down.                           | `ip link set eth0 down`                 |

---

## 2. Checking Network Connections

| Command                         | Description                                               | Example                                 |
|---------------------------------|-----------------------------------------------------------|-----------------------------------------|
| `ping hostname_or_IP`           | Test network connectivity to a host.                      | `ping google.com`                       |
| `traceroute hostname_or_IP`     | Show the path packets take to reach a host (install `traceroute` if not available). | `traceroute google.com`  |
| `tracepath hostname_or_IP`      | Alternative to `traceroute`, often pre-installed on Linux. | `tracepath google.com`           |
| `nslookup hostname`             | Query DNS to get information about a domain or IP.        | `nslookup google.com`                   |
| `dig domain`                    | Perform DNS lookups and display detailed information.     | `dig google.com`                        |

---

## 3. Displaying Active Connections and Listening Ports

| Command                         | Description                                               | Example                                 |
|---------------------------------|-----------------------------------------------------------|-----------------------------------------|
| `netstat -tuln`                 | Display all listening ports and active connections (may require installation). | `netstat -tuln`          |
| `ss -tuln`                      | Replacement for `netstat` to display listening ports and connections. | `ss -tuln`                  |
| `lsof -i`                       | List all open Internet sockets (connections).             | `lsof -i`                               |
| `lsof -i :port_number`          | List processes using a specific port.                     | `lsof -i :80`                           |
| `ss -s`                         | Display network statistics summary.                       | `ss -s`                                 |

---

## 4. Viewing and Configuring Routing

| Command                         | Description                                               | Example                                 |
|---------------------------------|-----------------------------------------------------------|-----------------------------------------|
| `ip route`                      | Display the current routing table.                        | `ip route`                              |
| `route -n`                      | Display the current routing table with numeric addresses. | `route -n`                              |
| `ip route add network via gateway` | Add a route to a network.                            | `ip route add 192.168.2.0/24 via 192.168.1.1` |
| `ip route del network`          | Delete a route to a network.                             | `ip route del 192.168.2.0/24`           |
| `ip route get IP_address`       | Display the route a packet would take to a given IP.      | `ip route get 8.8.8.8`                  |

---

## 5. Network Diagnostics and Performance Monitoring

| Command                         | Description                                               | Example                                 |
|---------------------------------|-----------------------------------------------------------|-----------------------------------------|
| `ifstat`                        | Display network interface statistics (requires installation). | `ifstat`                         |
| `iftop`                         | Display real-time bandwidth usage by host (requires installation). | `iftop`                          |
| `nmap IP_or_network`            | Perform a network scan to discover hosts and services (requires installation). | `nmap 192.168.1.0/24`         |
| `ethtool interface`             | Display or modify Ethernet device settings (e.g., speed, duplex). | `ethtool eth0`               |
| `mtr hostname_or_IP`            | Combined ping and traceroute tool for diagnosing network issues (requires installation). | `mtr google.com`   |

---

### Examples of Network Commands in Action

1. **Assign an IP address to a network interface**:

   ```bash
   ip addr add 192.168.1.10/24 dev eth0

2. **Display the current routing table**:

    ```bash
    ip route

3. **Test network connectivity to a remote host**:

    ```bash
    ping google.com

4. **List all listening ports and active network connections**:

     ```bash
     ss -tuln
