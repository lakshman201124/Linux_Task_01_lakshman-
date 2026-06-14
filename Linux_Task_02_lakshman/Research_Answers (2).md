# Linux Security Research (Part G)

## 1. Why are file permissions important?

File permissions are the first and most fundamental layer of access control on a Linux system. Every file and directory has an owner, a group, and read/write/execute rules for "owner", "group", and "everyone else." Without this, any user or process on a multi-user system could read, modify, or delete any other user's files — including system configs, password databases, and service data.

Permissions enforce confidentiality (preventing unauthorized reading of SSH keys, password hashes, etc.), integrity (preventing unauthorized modification of scripts, configs, or logs), and availability (preventing accidental or malicious deletion of critical files). They're also the foundation that higher-level tools — SELinux, AppArmor, ACLs, sudo policies — build on top of. If the base permission model is wrong, those higher layers can't fully compensate.

## 2. What happens if sensitive files are given 777 permissions?

Setting `777` (`rwxrwxrwx`) removes essentially all access control on a file. Any user — and any process running as any user, including a low-privilege web server account, a guest account, or malware executing as an unprivileged user — can:

- **Read** it: if it's something like `/etc/shadow`, a private key, or a database config with a connection string, the attacker now has those secrets directly.
- **Write/modify** it: an attacker could replace a config, inject malicious code into a script root later executes, or tamper with a log to cover their tracks.
- **Execute** it: if it's a script or binary, anyone can run it — and if it's a cron job or setuid binary, this can be a direct path to privilege escalation.

In short, `777` on a sensitive file turns a single low-privilege foothold into a system-wide compromise. It's a constant finding in real-world security audits, almost always the result of someone using `chmod 777` as a lazy fix for a "permission denied" error instead of diagnosing the real ownership/group issue.

## 3. What is the Principle of Least Privilege?

The Principle of Least Privilege (PoLP) states that every user, process, and program should be granted only the minimum level of access — and for the minimum time — necessary to do its job, nothing more.

On Linux, in practice this means:
- A web server runs as `www-data`, not `root`, so a vulnerability in the web app can't directly compromise the whole machine.
- A user who only needs to read shared reports gets read-only group access — not write access, and definitely not sudo.
- A backup script that only needs to read source files and write to one backup directory is given exactly those two permissions, nothing else.

The benefit is damage containment: if any single component is compromised (phished account, vulnerable service, buggy script), the blast radius is limited to whatever that component was allowed to touch.

## 4. Why do organizations restrict user access?

- **Reducing attack surface** — every privileged account is a potential entry point (phishing, credential theft, insider misuse). Fewer privileged accounts means fewer ways in.
- **Containing insider threats and human error** — most breaches and outages come from employees (accidentally or intentionally) touching something they had no business touching. Restricting access limits the blast radius of any single mistake.
- **Compliance and auditing** — regulations like GDPR, HIPAA, PCI-DSS, and ISO 27001 require demonstrating that access to sensitive data is restricted to those with a legitimate "need to know," and that access is logged and reviewable.
- **Separation of duties** — splitting responsibilities (e.g., the person who writes deployment scripts isn't the one who approves and runs them in production) makes fraud and unilateral mistakes harder.
- **Predictability and stability** — if everyone has root on production, the system becomes a moving target where no one can be sure what changed or why. Restricted, role-based access keeps the environment auditable and reproducible.

Ultimately, restricting access is how the principle of least privilege gets enforced at organizational scale — across hundreds or thousands of accounts — instead of relying on individual discipline.
