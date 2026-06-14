# Security Challenge (Part F)

Acting as the Linux Administrator, here's the recommended permission for each file and the reasoning.

| File | Recommended Permission | Symbolic | Reason |
|---|---|---|---|
| `password_backup.txt` | **600** | `rw-------` | Contains credentials/secrets. Only the owning account should ever read or write it — any group/other access would let another local user exfiltrate it. |
| `public_notice.txt` | **644** | `rw-r--r--` | Meant to be read by everyone (announcement file). Owner can update it; no one else should be able to modify it and post a fake notice. |
| `system_log.txt` | **640** | `rw-r-----` | Logs often contain sensitive operational data (IPs, usernames, traces). Owning service/admin gets read+write, a trusted admin group gets read for monitoring, "others" get nothing. |
| `personal_notes.txt` | **600** | `rw-------` | Private personal content — no one but the owner has any legitimate reason to read or write it. |

## Reasoning Summary

The pattern follows the **principle of least privilege**: every file gets the minimum access required to do its job, nothing more.

- Files containing **secrets** (`password_backup.txt`, `personal_notes.txt`) get `600` — owner-only, full stop.
- Files meant for **broad consumption** (`public_notice.txt`) get `644` — readable by all, writable only by the owner, so the content can't be tampered with.
- **System logs** sit in between (`640`) — sensitive enough to hide from regular users, but a sysadmin group may legitimately need read access for auditing without needing full root access.

None of these files should ever be `777`. Granting write (and especially execute) access to "others" on any of them means any local account — or any process running under any account, including a compromised one — could read, corrupt, or replace the file.
