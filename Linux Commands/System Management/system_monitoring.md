# System Management: System Monitoring

This document covers essential commands for monitoring system performance in Linux, including CPU, memory, disk usage, and overall system load.

---

## 1. Monitoring CPU Usage

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `top`                      | Display real-time CPU usage and process information.      | `top`                                   |
| `htop`                     | Enhanced version of `top` with a more user-friendly interface (if installed). | `htop` |
| `mpstat`                   | Report per-processor CPU statistics (part of `sysstat` package). | `mpstat`                      |
| `sar -u`                   | Display CPU usage statistics over time.                   | `sar -u 5 10`                           |
| `iostat`                   | Report CPU and input/output statistics.                   | `iostat`                                |

---

## 2. Monitoring Memory Usage

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `free -m`                  | Display memory usage in megabytes.                        | `free -m`                               |
| `vmstat`                   | Report memory, swap, and process statistics.              | `vmstat 5`                              |
| `top`                      | View real-time memory usage per process.                  | `top`                                   |
| `smem`                     | Display memory usage for processes (requires installation). | `smem`                             |
| `cat /proc/meminfo`        | View detailed memory information from the `/proc` filesystem. | `cat /proc/meminfo`             |

---

## 3. Monitoring Disk Usage

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `df -h`                    | Display disk usage of all mounted filesystems in a human-readable format. | `df -h`               |
| `du -sh /path/to/dir`      | Show disk usage of a specific directory.                  | `du -sh /var/log`                       |
| `lsblk`                    | List all block devices and their mount points.            | `lsblk`                                 |
| `iostat -dx`               | Display detailed disk I/O statistics.                     | `iostat -dx`                            |
| `smartctl -H /dev/sda`     | Check the health of a storage device (part of `smartmontools` package). | `smartctl -H /dev/sda`   |

---

## 4. Monitoring Network Usage

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `ifconfig`                 | Display information about network interfaces (deprecated in favor of `ip`). | `ifconfig`                 |
| `ip -s link`               | Show statistics for network interfaces.                   | `ip -s link`                            |
| `ss -tuln`                 | Display listening sockets and their statuses.             | `ss -tuln`                              |
| `netstat -i`               | Show network interface statistics.                        | `netstat -i`                            |
| `nload`                    | Real-time network traffic monitoring tool (requires installation). | `nload`                     |

---

## 5. Monitoring System Load

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `uptime`                   | Display system uptime and average load.                   | `uptime`                                |
| `top`                      | View system load and CPU usage per process.               | `top`                                   |
| `w`                        | Show logged-in users and their load on the system.        | `w`                                     |
| `cat /proc/loadavg`        | Display system load averages directly from `/proc`.       | `cat /proc/loadavg`                     |
| `dstat`                    | View CPU, memory, network, disk, and system load statistics (requires installation). | `dstat`                    |

---

### Examples of System Monitoring Commands in Action

1. **View memory usage in real time with `top`**:

   ```bash
   top

2. **Display disk usage for all mounted filesystems**:

    ```bash
    df -h

3. **Check network traffic in real time**:

    ```bash
    nload

4. **View system load and uptime**:

    ```bash
    uptime
