# Commands Used — Linux Task 02

All commands executed on Kali Linux as user `kali` (UID 1000) on 14 June 2026. Screenshots for each section live in the matching `Screenshots/PartX_*` folder.

## Part A — Understanding Users

```bash
whoami
# kali

id
# uid=1000(kali) gid=1000(kali) groups=1000(kali),4(adm),20(dialout),24(cdrom),
# 25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),100(users),
# 101(netdev),102(scanner),104(bluetooth),113(lpadmin),122(wireshark),
# 123(kaboxer),124(vboxsf)

cat /etc/passwd
# Full user database dump (~60 lines), ending with:
# kali:x:1000:1000::/home/kali:/usr/bin/zsh
```

## Part B — Create Users & Groups

```bash
# Create groups
sudo groupadd interns
sudo groupadd cyberteam

# Verify groups exist
cat /etc/group | grep interns
# interns:x:1001:
cat /etc/group | grep cyberteam
# cyberteam:x:1002:

# Create users with home directories
sudo useradd -m student1
sudo useradd -m student2
sudo useradd -m student3

# Add each user to the appropriate group(s)
sudo usermod -aG interns student1
sudo usermod -aG cyberteam student2
sudo usermod -aG interns,cyberteam student3

# Verify group membership
id student1
# uid=1001(student1) gid=1003(student1) groups=1003(student1),1001(interns)

id student2
# uid=1002(student2) gid=1004(student2) groups=1004(student2),1002(cyberteam)

id student3
# uid=1003(student3) gid=1005(student3) groups=1005(student3),1001(interns),1002(cyberteam)
```

## Part C — File Ownership

```bash
mkdir CyberSecurity_Project
cd CyberSecurity_Project
touch report.txt notes.txt credentials.txt

ls -l
# -rw-rw-r-- 1 kali kali 0 Jun 14 03:47 credentials.txt
# -rw-rw-r-- 1 kali kali 0 Jun 14 03:47 notes.txt
# -rw-rw-r-- 1 kali kali 0 Jun 14 03:47 report.txt

# --- Ownership change (still to run + screenshot) ---
sudo chown student1 credentials.txt
ls -l
# expect: -rw-rw-r-- 1 student1 kali 0 Jun 14 03:47 credentials.txt
```

## Part D — File Permissions

```bash
touch security_policy.txt
ls -l security_policy.txt
# -rw-rw-r-- 1 kali kali 0 Jun 14 03:48 security_policy.txt   (664, default)

chmod 444 security_policy.txt
ls -l security_policy.txt
# -r--r--r-- 1 kali kali 0 Jun 14 03:48 security_policy.txt   (Read Only)

chmod 664 security_policy.txt
ls -l security_policy.txt
# -rw-rw-r-- 1 kali kali 0 Jun 14 03:48 security_policy.txt   (Read & Write)

chmod 777 security_policy.txt
ls -l security_policy.txt
# -rwxrwxrwx 1 kali kali 0 Jun 14 03:48 security_policy.txt   (Full Access)
```
