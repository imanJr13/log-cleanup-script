# log-cleanup-script

🧹 Audit Log Cleanup Script for Linux
This script helps clean up old audit logs in /var/log/audit to prevent disk space issues.

🔧 What It Does
Deletes audit log files matching audit.log.* that are older than 7 days

Designed to run weekly using cron

```
#!/bin/bash

# Directory where audit logs are stored
LOG_DIR="/var/log/audit"

# Find and delete files older than 7 days (excluding current log)
find "$LOG_DIR" -type f -name "audit.log.*" -mtime +7 -exec rm -f {} \;
```
✅ Make it executable:

```
chmod +x /usr/local/bin/cleanup-audit-logs.sh

```

⏰ Setup Cron Job
To run the script weekly (e.g., every Sunday at 2:00 AM):

```
crontab -e

0 2 * * 0 /usr/local/bin/cleanup-audit-logs.sh

```

📝 Notes
Adjust -mtime +7 to a different value (e.g., +14) to keep logs longer.

Only files with the pattern audit.log.* are targeted, so the current active audit.log is untouched.

Requires root or appropriate permissions to delete logs in /var/log/audit.
