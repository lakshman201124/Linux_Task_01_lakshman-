# Linux Task 01 — Command Outputs

**Submitted by:** Lakshman
**Date:** 14 June 2026

---

## Part B — Basic Navigation Commands

### 1. pwd
**Purpose:** Prints the full path of the current working directory so you know exactly where you are in the file system.
**Output:**
```
/home/kali
```

### 2. ls
**Purpose:** Lists all visible files and folders in the current directory.
**Output:**
```
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
```

### 3. ls -la
**Purpose:** Lists all files and folders including hidden ones (starting with `.`), with full details like permissions, owner, file size and last modified date.
**Output:**
```
total 168
drwx------ 16 kali kali  4096 Jun 14 02:06 .
drwxr-xr-x  3 root root  4096 Mar 20 02:45 ..
-rw-r--r--  1 kali kali   220 Mar 20 02:45 .bash_logout
-rw-r--r--  1 kali kali  5578 Mar 20 02:45 .bashrc
drwxr-xr-x  2 kali kali  4096 Jun 14 01:59 Desktop
drwxr-xr-x  2 kali kali  4096 Jun 14 01:59 Documents
...
```

### 4. cd
**Purpose:** Changes the current directory to a specified location.
**Example:** `cd Desktop` moves into the Desktop folder, changing the prompt to `(kali@kali)-[~/Desktop]`

### 5. clear
**Purpose:** Clears all text from the terminal screen to give a clean workspace. Previous commands can still be accessed by scrolling up.

### 6. history
**Purpose:** Displays a numbered list of all commands previously entered in the terminal session.

### 7. whoami
**Purpose:** Prints the username of the currently logged in user.
**Output:**
```
kali
```

### 8. hostname
**Purpose:** Displays the name of the computer on the network.
**Output:**
```
kali
```

---

## Part C — Directory Management

### Commands Used
```
mkdir CyberSecurity_Lab
cd CyberSecurity_Lab
mkdir Networking
mkdir Linux
mkdir CyberSecurity
mkdir EthicalHacking
mkdir Reports
tree
```

**Output of tree:**
```
.
├── CyberSecurity
├── EthicalHacking
│   └── linux_commands.txt
├── Linux
├── Networking
│   └── notes.txt
└── Reports
    └── report.txt

6 directories, 3 files
```

---

## Part D — File Management

### touch — Create files
**Purpose:** Creates new empty files instantly without opening any editor.
```
touch notes.txt linux_commands.txt report.txt
```

### cp — Copy files
**Purpose:** Creates a copy of a file in a new location while keeping the original.
```
cp notes.txt Networking/
```

### mv — Move and Rename files
**Purpose:** Moves a file to a new location or renames it.
```
mv linux_commands.txt EthicalHacking/
mv report.txt Reports/
```

### rm — Delete files
**Purpose:** Permanently removes a file from the system with no recycle bin.
```
rm CyberSecurity/notes.txt
```

---

## Part E — System Information

```
$ uname -a
Linux kali 6.18.12+kali-amd64 #1 SMP PREEMPT_DYNAMIC Kali 6.18.12-1kali1 (2026-02-25) x86_64 GNU/Linux

$ hostname
kali

$ whoami
kali

$ date
Sun Jun 14 02:30:00 AM EDT 2026

$ uptime
02:30:00 up 0:31, 1 user, load average: 0.15, 0.18, 0.12

$ pwd
/home/kali/CyberSecurity_Lab
```
