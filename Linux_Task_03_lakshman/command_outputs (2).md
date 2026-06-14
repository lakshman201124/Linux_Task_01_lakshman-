# Command Outputs — Linux Task 03

**Submitted by:** Lakshman
**Date:** 14 June 2026

---

## Part A — Process Monitoring

### ps
**Purpose:** Shows only the processes currently running in the active terminal session.
**Output:**
```
  PID TTY          TIME CMD
 7321 pts/0    00:00:02 zsh
 7422 pts/0    00:00:00 ps
```

### ps aux
**Purpose:** Displays all running processes on the system for every user with CPU%, memory%, PID and command details.
**Output:** Shows full list of all system processes including root and kali user processes.

### top
**Purpose:** A real-time interactive process viewer that updates every few seconds showing CPU, memory and all running processes.
**Key stats:**
```
Tasks: 216 total, 1 running, 215 sleeping
CPU: 6.4% used
Memory: 1.9Gi total, 1017M used
```

### htop
**Purpose:** An improved version of top with colour coded display, easier navigation and more visual CPU/memory bars.
**Installation:** `sudo apt update && sudo apt install htop`

### Answers

**1. What is a Process?**
A process is any program that is currently being executed by the operating system. Each time you run a command or open an application, the system creates a new process for it with its own memory space and resources.

**2. What is a PID?**
PID stands for Process ID. It is a unique number the operating system assigns to every running process. You use the PID to manage a specific process — for example to kill it or check its resource usage.

**3. Which process is consuming the most CPU?**
`Xorg` was consuming the most CPU as shown in the htop output at the top of the process list.

**4. Which process is consuming the most Memory?**
`Xorg` was also consuming the most memory among all running processes.

---

## Part B — Process Management

### Commands Used
```
sleep 300          # Start sleep in foreground
ps aux | grep sleep  # Find the process — PID: 72140
kill 72140           # Terminate gracefully
sleep 300 &          # Run in background
kill -9 <PID>        # Force terminate
```

### Documentation

| Field | Value |
|-------|-------|
| PID Found | `72140` |
| Command Used | `kill 72140` then `kill -9` |
| Result | Process successfully terminated |

**Difference between kill and kill -9:**
- `kill PID` — sends SIGTERM signal asking the process to shut down gracefully
- `kill -9 PID` — sends SIGKILL signal which immediately forces the process to stop with no cleanup

---

## Part C — System Monitoring

### free -h
**Purpose:** Shows total, used and available RAM and swap memory in a human readable format.
**Output:**
```
       total    used    free   shared  buff/cache  available
Mem:   1.9Gi   872Mi   224Mi    31Mi       1.0Gi      1.1Gi
Swap:  953Mi   105Mi   848Mi
```

### df -h
**Purpose:** Displays disk space usage for all mounted file systems.
**Output:** `dif` command not found error shown — correct command is `df -h`
```
Filesystem  Size  Used  Avail  Use%  Mounted on
/dev/sda1    79G   16G    59G   22%  /
```

### uptime
**Purpose:** Shows how long the system has been running and the current load averages.
**Output:**
```
04:22:54 up 2:20, 1 user, load average: 0.22, 0.29, 0.18
```

### uname -a
**Purpose:** Displays complete kernel and system architecture information.
**Output:**
```
Linux kali 6.18.12+kali-amd64 #1 SMP PREEMPT_DYNAMIC Kali 6.18.12-1kali1 (2026-02-25) x86_64 GNU/Linux
```

### System Summary

| Field | Value |
|-------|-------|
| Total RAM | 1.9GiB |
| Available RAM | 1.1GiB |
| Disk Size | 79G |
| Disk Used | 16G (22%) |
| System Uptime | 4 hours 30 minutes |
| Kernel Version | Linux kali 6.18.12+kali-amd64 |

---

## Part D — Service Monitoring

### systemctl status ssh
**Purpose:** Checks whether the SSH remote access service is running.
**Output:**
```
ssh.service - OpenBSD Secure Shell server
Active: inactive (dead)
Loaded: disabled; preset: disabled
```

### systemctl status NetworkManager
**Purpose:** Checks the status of the network management service.
**Output:**
```
NetworkManager.service - Network Manager
Active: active (running) since Sun 2026-06-14 01:50:39 EDT; 2h 33min ago
Loaded: enabled; preset: enabled
Main PID: 743 (NetworkManager)
```

### Answers

**1. What is a Service?**
A service is a background process that starts automatically and runs continuously to handle a specific system function such as network management, SSH access or logging. Services run without user interaction.

**2. Why are services important?**
Services keep core system functions running at all times. Without NetworkManager the system loses internet access. Without SSH, remote server management becomes impossible. Services ensure the system stays functional and accessible.

**3. How can a stopped service affect a system?**
A stopped service removes the functionality it provides. If SSH stops, no one can remotely access the server. If NetworkManager stops, all network connections drop. In production environments this can cause serious downtime and data loss.

---

## Part E — Shell Script

### Script: system_report.sh
```bash
#!/bin/bash
echo "System Information Report"
echo "User: $(whoami)"
echo "Hostname : $(hostname)"
echo "Date: $(date)"
echo "Current Directory: $(pwd)"
echo ""
echo "Memory Usage:"
free -h
echo ""
echo "Disk Usage:"
df -h
```

### Execution
```
chmod +x system_report.sh
./system_report.sh
```

### Output
```
System Information Report
User: kali
Hostname : kali
Date: Sun Jun 14 04:30:09 AM EDT 2026
Current Directory: /home/kali

Memory Usage:
       total    used    free  available
Mem:   1.9Gi   857Mi   224Mi     1.1Gi

Disk Usage:
/dev/sda1   79G   16G   59G   22%   /
```
