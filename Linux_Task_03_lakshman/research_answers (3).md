# Research Answers — Linux Task 03

**Submitted by:** Lakshman
**Date:** 14 June 2026

---

## Part F — Security Monitoring Commands

### 1. netstat
**Purpose:** Displays all active network connections, listening ports and routing information.
**Example Output:**
```
Proto  Local Address      Foreign Address    State
tcp    0.0.0.0:22         0.0.0.0:*          LISTEN
tcp    10.0.2.15:443      142.250.1.1:54321  ESTABLISHED
```
**Security Use Case:** Security analysts use netstat to detect unexpected open ports or outbound connections that could indicate malware or a backdoor communicating with an attacker.

---

### 2. ss
**Purpose:** A faster and more detailed modern tool for viewing socket statistics and network connections, replacing netstat.
**Example Output:**
```
Netid  State   Recv-Q  Send-Q  Local Address:Port   Peer Address:Port
tcp    LISTEN  0       128     0.0.0.0:22            0.0.0.0:*
tcp    ESTAB   0       0       10.0.2.15:55210       8.8.8.8:443
```
**Security Use Case:** Used to quickly audit all network connections. If a process is connecting to an unknown IP address on an unusual port, it could be malware exfiltrating data.

---

### 3. who
**Purpose:** Lists all users who are currently logged into the system along with their terminal and login time.
**Example Output:**
```
kali    pts/0    2026-06-14 02:00 (:0)
root    pts/1    2026-06-14 03:45 (192.168.1.10)
```
**Security Use Case:** Helps detect unauthorised logins. An unexpected user logged in from an unknown IP address is a strong indicator of a security breach.

---

### 4. w
**Purpose:** Shows who is currently logged in and exactly what command each user is running, along with CPU usage and idle time.
**Example Output:**
```
USER   TTY   FROM          LOGIN@  IDLE  WHAT
kali   pts/0  :0           02:00   0s    w
root   pts/1  192.168.1.10  03:45  1:00  bash
```
**Security Use Case:** More useful than `who` for security purposes because it shows what each logged-in user is actively doing. A user running unusual or suspicious commands can be spotted immediately.

---

### 5. last
**Purpose:** Displays a complete history of all user logins and logouts including the source IP and session duration.
**Example Output:**
```
kali   pts/0   :0           Sun Jun 14 02:00   still logged in
root   pts/1   192.168.1.10 Sat Jun 13 22:00 - 23:30 (01:30)
```
**Security Use Case:** Essential for incident response and security audits. Analysts use it to trace when and from where users logged in, helping identify brute force attacks or suspicious login patterns outside of business hours.

---

## Part G — Mini SOC Activity

### Scenario: System is running slowly

**1. How would you identify resource-heavy processes?**
The first tool I would use is `htop` or `top` to get a real-time view of all running processes sorted by CPU and memory usage. The heaviest processes appear at the top of the list. I would also run `free -h` to check if the system is running low on available memory and `df -h` to see if the disk is almost full — both can slow the system significantly. Running `ps aux --sort=-%mem` gives a sorted list of processes by memory which helps quickly identify the biggest consumers.

**2. How would you determine whether a process is suspicious?**
I would check several indicators. First, is the process name familiar or does it look randomly generated? Legitimate processes have recognisable names. Second, which user is running it — a system-level process running under a regular user account is unusual. Third, is it consuming abnormally high resources with no clear reason? I would also check the file path using `ls -l /proc/PID/exe` to see where the executable is stored — processes running from `/tmp` or unusual hidden directories are a red flag. Finally I would use `ss` or `netstat` to see if the process has any active network connections to unknown external addresses.

**3. What information would you collect before terminating a process?**
Before terminating anything I would document: the exact PID and process name, the full command being run, the user account running it, current CPU and memory usage, how long it has been running (start time), any open network connections using `ss`, and the parent process ID (PPID) to understand how it was started. I would save all this to a log file or take a screenshot for the incident report. This is important because killing the wrong process could crash a critical service, and the documentation helps the security team investigate the root cause even after the process is terminated.
