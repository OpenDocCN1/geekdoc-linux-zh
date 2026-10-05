# OffSec

# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.

# Output of the crontab jobs (including errors) is sent through
# email to the user crontab files to (unless redirected)

# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/

# For more information see the manual pages of crontab(5) and cron(8)

```
* m h dom now command
```

| Listing 467 - Listing cron jobs for the current user |

In the above output, only the commented instructions are present, meaning cron job has been configured for the user joe. However, if we try to run the same command with the sudo prefix, we discover that a backup script is scheduled to run every minute.

```
joe@debian-prefix$: sudo crontab -l
[sudo] password for joe:
# Edit this file to introduce tasks to be run by cron.
* m h dom now command
* * * * /bin/bash /home/joe/.scripts/user_backups.sh
```

| Listing 468 - Listing cron jobs for the root user |

Listing cron jobs using sudo reveals jobs run by the root user. In this example, it shows a backup script running as root. If this file has weak permissions, we may be able to leverage it to escalate our privileges.

> As we learn later in this Module, the joe user has granted specific sudo permission to list cron jobs running as the root user. This permission cannot be abused to obtain a root shell.

At some point, we may need to leverage an exploit to escalate our local privileges. If so, our search for a working exploit begins with the enumeration of all installed applications, noting the version of each. We can use this information for a matching exploit.

Manually searching for this information could be very consuming and ineffective, so we'll learn how to automate this process in the next section. However, we should know how to manually query installed packages is needed to correlate information obtained during previous enumeration steps.

Linux-based systems use a variety of package managers. For example, Debian-based distributions, like the one in our lab, use dpkg,842 while Red Hat-based systems use rpm.843