# Linux Task 01 — Linux Environment Setup & Essential Commands

**Intern:** Lakshman
**Date:** 14 June 2026
**Organization:** White Band Associates
**OS:** Kali Linux 2026.1 on Oracle VirtualBox

---

## 📁 Repository Structure

| File/Folder | Description |
|-------------|-------------|
| `Screenshots/` | Part A, B, C, D & E — All command screenshots |
| `Command_Outputs/command_outputs.md` | Part B, C, D & E — All command outputs with purposes |
| `Answers.md` | Part F — Linux research answers |
| `Notes.md` | Personal notes and observations |

---

## 📋 Summary of Findings

### 🖥️ Part A — Linux Installation
Successfully installed **Kali Linux 2026.1** on Oracle VirtualBox. Kali Linux was selected because it is purpose-built for cybersecurity and ethical hacking with hundreds of pre-installed tools. Screenshots of the desktop environment, terminal and `uname -a` system info are in the Screenshots folder.

### 🧭 Part B — Basic Navigation Commands
Practised 8 core terminal commands. `pwd` showed the home directory as `/home/kali`. `ls` listed visible folders and `ls -la` revealed hidden files too. `cd Desktop` navigated into the Desktop folder. `clear` cleaned the screen, `history` showed all previous commands, `whoami` returned `kali` as the user and `hostname` returned `kali` as the machine name.

### 📁 Part C — Directory Management
Built the `CyberSecurity_Lab` folder with 5 subfolders — `Networking`, `Linux`, `CyberSecurity`, `EthicalHacking` and `Reports` — using `mkdir` for each. Used `cd` to navigate inside and `tree` to display the full structure. Tree confirmed `6 directories` created successfully.

### 📄 Part D — File Management
Created `notes.txt`, `linux_commands.txt` and `report.txt` using `touch`. Copied `notes.txt` to `Networking/` using `cp`. Moved `linux_commands.txt` to `EthicalHacking/` and `report.txt` to `Reports/` using `mv`. Deleted `CyberSecurity/notes.txt` using `rm`.

### ⚙️ Part E — System Information
- **Kernel:** `Linux kali 6.18.12+kali-amd64 x86_64 GNU/Linux`
- **Username:** `kali`
- **Hostname:** `kali`
- **Directory:** `/home/kali/CyberSecurity_Lab`
- **Date:** `Sun Jun 14 02:30:00 AM EDT 2026`
- **Uptime:** `31 minutes, 1 user`

### 🔬 Part F — Linux Research
Linux is a free and open source OS that powers most of the world's servers and cybersecurity tools. It is the preferred choice for ethical hackers because of its powerful terminal, complete system control and hundreds of pre-installed security tools in Kali Linux. Unlike Windows, Linux is free, highly customisable and much more secure.
