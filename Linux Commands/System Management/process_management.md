# System Management: Process Management

This document covers essential commands for managing processes in Linux. Proper process management is key to maintaining system performance and stability.

---

## 1. Viewing Running Processes

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `ps aux`                   | Display a detailed list of all processes.                 | `ps aux`                                |
| `ps -ef`                   | Alternative process listing format showing all processes. | `ps -ef`                                |
| `top`                      | Display real-time system summary and process usage.       | `top`                                   |
| `htop`                     | Enhanced version of `top` with a more user-friendly interface (if installed). | `htop` |
| `pgrep process_name`       | Search for processes by name or pattern.                  | `pgrep apache2`                         |

---

## 2. Process Monitoring and System Load

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `uptime`                   | Display system uptime and load averages.                  | `uptime`                                |
| `vmstat`                   | Report on system memory, processes, and CPU usage.        | `vmstat 5`                              |
| `iostat`                   | Report CPU and input/output statistics.                   | `iostat`                                |
| `sar`                      | Collect, report, and save system activity information.     | `sar -u 5 10`                           |
| `pidstat`                  | Report statistics for individual processes.               | `pidstat 1`                             |

---

## 3. Controlling Processes

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `kill PID`                 | Terminate a process by its Process ID (PID).              | `kill 1234`                             |
| `killall process_name`     | Terminate all processes with a specified name.            | `killall apache2`                       |
| `pkill pattern`            | Kill processes matching a pattern.                        | `pkill -f "java"`                       |
| `kill -9 PID`              | Forcefully kill a process (SIGKILL signal).               | `kill -9 1234`                          |
| `xkill`                    | Terminate a graphical application by clicking its window (useful in GUI environments). | `xkill`               |

---

## 4. Managing Process Priorities

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `nice -n priority command` | Start a command with a specified priority (default is 0; lower values = higher priority). | `nice -n 10 gzip largefile` |
| `renice priority PID`      | Change the priority of an existing process.               | `renice 15 1234`                        |
| `top`                      | Adjust process priority interactively (use `r` command within `top`). | `top`                         |

---

## 5. Viewing Process Details

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `pstree`                   | Display processes in a tree structure.                    | `pstree`                                |
| `pidof process_name`       | Display the PID of a running process by name.             | `pidof sshd`                            |
| `strace -p PID`            | Trace system calls and signals of a running process.      | `strace -p 1234`                        |
| `lsof -p PID`              | List open files associated with a process.                | `lsof -p 1234`                          |
| `lsof /path/to/file`       | List processes that have a specific file open.            | `lsof /var/log/syslog`                  |

---

## 6. Background and Foreground Processes

| Command                    | Description                                               | Example                                 |
|----------------------------|-----------------------------------------------------------|-----------------------------------------|
| `command &`                | Run a command in the background.                          | `sleep 60 &`                            |
| `jobs`                     | List all background jobs in the current session.          | `jobs`                                  |
| `fg %job_number`           | Bring a background job to the foreground.                 | `fg %1`                                 |
| `bg %job_number`           | Move a suspended job to the background.                   | `bg %1`                                 |
| `disown %job_number`       | Remove a job from the job table, allowing it to run independently. | `disown %1`                   |

---

### Examples of Process Management Commands in Action

1. **List all running processes and filter by name**:

   ```bash
   ps aux | grep process_name

2. **Kill all processes with a specific name (e.g., apache2)**:

    ```bash
    killall apache2

3. **Start a CPU-intensive process with a lower priority**:

    ```bash
    nice -n 19 gzip largefile

4. **Bring a background job to the foreground**:

   ```bash
   fg %1
