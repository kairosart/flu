A foothold in the lab will be gained by exploiting an **unauthenticated OGNL/template-injection vulnerability (CVE-2022-26134)** in an exposed **Atlassian Confluence 7.13.6** instance, achieving pre-authentication remote code execution and a reverse shell as the **`confluence`** user. Privileges will then be escalated by **hijacking a root-owned cron job** that executes a script writable by the `confluence` account, yielding a **root** shell. This lab focuses on *exploiting a well-known web-application CVE and on cron/script-hijack privilege escalation*.

## Learning Objectives

**After completion of this lab, learners will be able to:**

- Fingerprint an unknown web service from its HTTP response headers, cookies, and meta tags.
- Identify **Atlassian Confluence 7.13.6** and map it to the public vulnerability **CVE-2022-26134**.
- Exploit the **unauthenticated OGNL injection** to achieve remote code execution.
- Use `through_the_wire` to send the injection payload and obtain a reverse shell.
- Enumerate writable files and cron jobs to find a privilege-escalation path.
- Hijack a **root cron job** by appending a reverse shell to a writable script (`/opt/log-backup.sh`) and catch the resulting root shell.

## Lab Description

This lab demonstrates a straightforward but high-impact attack chain. An administrator has exposed an outdated **Confluence 7.13.6** server on port `8090`; this version is vulnerable to **CVE-2022-26134**, allowing an unauthenticated attacker to inject OGNL expressions via the URL path and run arbitrary commands. Exploitation returns a shell as the `confluence` service account. From there, local enumeration reveals that `/opt/log-backup.sh` — a log-backup script — is owned by `confluence` yet executed by **root's crontab**. Because the script is writable, appending a reverse shell to it results in code execution as **root** at the next cron interval. A second port (`8091`, a Clojure "Aleph" service returning `204` to every request) serves as a decoy. The lab emphasizes web-application CVE exploitation, reverse-shell handling, and privilege escalation through misconfigured scheduled tasks.

## Areas Improved

*Web Application Penetration Testing
Vulnerability Research & CVE Exploitation
Remote Code Execution (OGNL Injection)
Reverse Shell Handling
Linux Privilege Escalation (Cron / Script Hijack)
Local Enumeration
Penetration Testing Methodology*
