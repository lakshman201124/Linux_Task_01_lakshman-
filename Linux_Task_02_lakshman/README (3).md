# Linux Task 02: Users, Groups & File Permissions

## Objective
This task covers the foundations of Linux system administration and security: user accounts, group management, file ownership, and the Linux permission model (`chmod` / `chown`).

## Environment
- OS: Kali Linux (Rolling, kernel 6.18.12-1kali1)
- Platform: VirtualBox VM
- User: kali (UID 1000, GID 1000)
- Date performed: 14 June 2026

---

## Part A — Understanding Users

| Command | Output |
|---|---|
| `whoami` | `kali` |
| `id` | `uid=1000(kali) gid=1000(kali) groups=1000(kali),4(adm),20(dialout),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),100(users),101(netdev),102(scanner),104(bluetooth),113(lpadmin),122(wireshark),123(kaboxer),124(vboxsf)` |
| `cat /etc/passwd` | Full user database — see `Screenshots/PartA_Users/` |

### Answers

1. **Current username:** `kali`
2. **UID:** `1000`
3. **GID:** `1000`
4. **What does /etc/passwd contain?**

   `/etc/passwd` is the local user account database. Each line follows the format:

   `username:x:UID:GID:comment:home_directory:shell`

   - `username` — login name
   - `x` — placeholder; the real (hashed) password is stored in `/etc/shadow`
   - `UID` / `GID` — numeric user ID and primary group ID
   - `comment` — optional full name / description (GECOS field)
   - `home_directory` — the user's home folder
   - `shell` — program launched on login (`/usr/bin/zsh` for interactive users, `/usr/sbin/nologin` for service accounts)

   Almost all ~60 entries are system/service accounts (`www-data`, `postgres`, `sshd`, etc.) that run daemons under their own restricted identity. The only interactive human account is `kali:x:1000:1000::/home/kali:/usr/bin/zsh`.

---

## Part B — Create Users & Groups

**Groups created:**
- `interns` → GID 1001
- `cyberteam` → GID 1002

**Users created and assigned:**

| User | UID | Primary GID | Secondary Group(s) |
|---|---|---|---|
| student1 | 1001 | 1003 | interns |
| student2 | 1002 | 1004 | cyberteam |
| student3 | 1003 | 1005 | interns, cyberteam |

Verified with `id student1`, `id student2`, `id student3` — see `Screenshots/PartB_Groups_Users/`.

---

## Part C — File Ownership

Created `~/CyberSecurity_Project/` containing `report.txt`, `notes.txt`, `credentials.txt` — all initially `kali:kali` (see `Screenshots/PartC_Ownership/`).

| File | Original Owner | New Owner | Command Used |
|---|---|---|---|
| `credentials.txt` | kali | student1 | `sudo chown student1 credentials.txt` |

> **Pending:** run the command above, then `ls -l`, and add that screenshot to `Screenshots/PartC_Ownership/` — this step wasn't in the screenshots provided yet.

---

## Part D — File Permissions

`security_policy.txt` was put through three `chmod` stages:

| Stage | Command | Result | Octal |
|---|---|---|---|
| Default | `touch security_policy.txt` | `rw-rw-r--` | 664 |
| Read Only | `chmod 444 security_policy.txt` | `r--r--r--` | 444 |
| Read & Write | `chmod 664 security_policy.txt` | `rw-rw-r--` | 664 |
| Full Access | `chmod 777 security_policy.txt` | `rwxrwxrwx` | 777 |

See `Screenshots/PartD_Permissions/`.

---

## Parts E, F & G

Detailed write-ups in their own files:
- `Permission_Analysis.md` — 755 / 644 / 777 / 600 / 700 breakdown
- `Security_Challenge_Answers.md` — recommended permissions for the admin scenario
- `Research_Answers.md` — file permission importance, 777 risks, least privilege, access restriction

---

## Folder Structure

```
Linux_Task_02_Lakshman/
├── README.md
├── Commands_Used.md
├── Permission_Analysis.md
├── Security_Challenge_Answers.md
├── Research_Answers.md
└── Screenshots/
    ├── PartA_Users/
    ├── PartB_Groups_Users/
    ├── PartC_Ownership/
    └── PartD_Permissions/
```

## Key Takeaway

Many real-world security incidents trace back to misconfigured permissions — world-writable files, credentials with world-readable access, or service accounts running with more privilege than they need. `chmod`, `chown`, and the principle of least privilege are core, everyday Linux security skills.
