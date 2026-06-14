# Permission Analysis (Part E)

Linux permissions are a 3-digit octal number — one digit each for **Owner**, **Group**, and **Others**. Each digit is a sum of:

- **4** = Read (r)
- **2** = Write (w)
- **1** = Execute (x)

---

## 755 → `rwxr-xr-x`

| | Permission | Meaning |
|---|---|---|
| Owner | rwx (7) | Full control — read, write, execute |
| Group | r-x (5) | Can read and execute, cannot modify |
| Others | r-x (5) | Can read and execute, cannot modify |

**Real-world use case:** The standard permission for executable scripts/binaries (`/usr/bin/*`) and browsable directories. The owner (root or the developer) can edit it; everyone else can run/enter it but not tamper with it.

---

## 644 → `rw-r--r--`

| | Permission | Meaning |
|---|---|---|
| Owner | rw- (6) | Read and write |
| Group | r-- (4) | Read-only |
| Others | r-- (4) | Read-only |

**Real-world use case:** The default for most regular files — configs, documents, source code, web pages. The owner can edit; everyone else (including a web server process) can only view.

---

## 777 → `rwxrwxrwx`

| | Permission | Meaning |
|---|---|---|
| Owner | rwx (7) | Full control |
| Group | rwx (7) | Full control |
| Others | rwx (7) | Full control |

**Real-world use case:** Almost never appropriate. Sometimes (wrongly) used on shared upload/scratch folders. This is the textbook over-permissioned file — any user or process on the system, including a compromised low-privilege one, can read, modify, or execute it.

---

## 600 → `rw-------`

| | Permission | Meaning |
|---|---|---|
| Owner | rw- (6) | Read and write |
| Group | --- (0) | No access |
| Others | --- (0) | No access |

**Real-world use case:** Private keys and credential files — e.g. `~/.ssh/id_rsa`. SSH will actually refuse to use a private key if its permissions are looser than this.

---

## 700 → `rwx------`

| | Permission | Meaning |
|---|---|---|
| Owner | rwx (7) | Full control |
| Group | --- (0) | No access |
| Others | --- (0) | No access |

**Real-world use case:** Private directories such as `~/.ssh/` itself, or a personal scripts folder. Execute permission on a *directory* is what lets the owner `cd` into it or list its contents — no one else should even see what's inside.
