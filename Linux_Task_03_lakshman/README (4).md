# Linux Task 03 — Process Management, System Monitoring & Basic Shell Scripting

**Intern:** Lakshman
**Date:** 14 June 2026
**Organization:** White Band Associates
**OS:** Kali Linux 2026.1 on Oracle VirtualBox

---

## 📁 Repository Structure

| File/Folder | Description |
|-------------|-------------|
| `Screenshots/` | All screenshots for Part A, B, C, D & E |
| `Shell_Script/system_report.sh` | Part E — Shell script file |
| `System_Report/system_report.md` | Part C — System summary report |
| `Command_Outputs/command_outputs.md` | Part A, B, C, D & E — All command outputs and answers |
| `Research_Answers/research_answers.md` | Part F & G — Security monitoring research and SOC activity |

---

## 📋 Summary of Findings

### 🔍 Part A — Process Monitoring
Ran `ps`, `ps aux`, `top` and `htop`. The system had 216 running tasks with a load average of 0.29. `htop` was installed using `sudo apt update && sudo apt install htop`. `Xorg` appeared at the top of both CPU and memory usage lists. A process is a running program instance and a PID is its unique identification number assigned by the OS.

### ⚙️ Part B — Process Management
Launched `sleep 300` and located it using `ps aux | grep sleep` with PID **72140**. Terminated it using `kill 72140`. Started a new background sleep and force killed it using `kill -9`. The `kill` command sends a graceful SIGTERM signal while `kill -9` sends SIGKILL for immediate forced termination.

### 💻 Part C — System Monitoring
Gathered complete system details using 4 commands:
- **Total RAM:** `1.9GiB` | **Available:** `1.1GiB`
- **Disk:** `79G` total, `16G` used, `59G` free (22% used)
- **Uptime:** `4 hours 30 minutes, 1 user`
- **Kernel:** `Linux kali 6.18.12+kali-amd64 x86_64 GNU/Linux`

### 🔧 Part D — Service Monitoring
SSH service was `inactive (dead)` and disabled — remote SSH access unavailable. NetworkManager was `active (running)` and enabled — handling all network connections. A stopped service removes the functionality it provides and can cause system downtime or loss of remote access.

### 📝 Part E — Shell Scripting
Created and executed `system_report.sh` — a bash script displaying user, hostname, date, current directory, memory and disk usage in a formatted report. Made executable with `chmod +x` and run with `./system_report.sh`.

### 🔒 Part F — Security Monitoring Research
Researched 5 security commands — `netstat` and `ss` for network connection monitoring, `who` and `w` for active user monitoring, and `last` for login history auditing. All are critical tools for detecting unauthorised access and suspicious network activity.

### 🛡️ Part G — Mini SOC Activity
To investigate a slow system, I would use `htop` to identify resource-heavy processes, check for unknown process names running from unusual paths like `/tmp`, verify network connections with `ss`, and fully document PID, user, CPU/memory usage and open connections before terminating anything. Proper documentation is essential for incident response.
