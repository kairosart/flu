# Flags — OffSec PG "flu"

| Flag | Path | Value |
|------|------|-------|
| User (local) | `/home/confluence/local.txt` | `200cc2b7da11821c04d8679132346baa` |
| Root (proof) | `/root/proof.txt` | `9e3f5a6cd336b6484534968851db36fb` |

## Other Loot

| Item | Path | Value |
|------|------|-------|
| Email | `/root/email8.txt` | `1889faf8@offsec.com` |

## Attack Path (TL;DR)

1. **Recon** → `8090/tcp` = Atlassian Confluence **7.13.6** (port `8091` = decoy).
2. **Initial access** → **CVE-2022-26134** unauthenticated OGNL injection → RCE → shell as `confluence`. [[Offsec/flu/B. POST-EXPLOITATION/1. Initial Access (CVE-2022-26134)]]
3. **Privesc** → `/opt/log-backup.sh` owned by `confluence` and run by **root cron** → append reverse shell → wait → shell as `root`. [[Offsec/flu/c. LOCAL PRIVILEGE ESCALATION/1. Cron - log-backup.sh]]
