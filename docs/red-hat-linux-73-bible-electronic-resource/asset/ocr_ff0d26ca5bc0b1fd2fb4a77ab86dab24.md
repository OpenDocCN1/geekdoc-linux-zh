```
Security report is in `/var/spool/logs/security.report.ratbert.glaci.com.010123-17:39`
```

As noted, this file can be found in the `/var/spool/tiger/logs` directory. Use the `cd` command to change to that directory and then use the `more` command or an editor to view its contents. Here is part of a typical Tiger security report:

```
# Performing NFS exports check...
--FAIL-- [nfs006f] Directory /home exported R/W to everyone.
--FAIL-- [nfs006f] Directory /var exported R/W to everyone.
# Performing check of system file permissions...
--WARN-- [perm006w] /root/.bashrc should not have group read.
--WARN-- [perm006w] /root/.bashrc should not have world read.
--WARN-- [perm006w] /root/.cshrc should not have group read.
--WARN-- [perm006w] /root/.cshrc should not have world read.
--FAIL-- [perm007f] /etc/aliases should not have group read.
--FAIL-- [perm007f] /etc/aliases should not have world read.
```

The security report is divided into sections with each section labeled with a comment. In the above example, the NFS exports section has two problems. The `/home` and `/var` partitions are exported without restrictions. The system file permissions section reports several problems. Some are labeled with `--WARN--` in front of them. These are not as critical as the ones with `--FAIL--` in front of them. Nevertheless, in both cases you should use the `chown` or `chgrp` command to alter the permissions.

# ## Detecting Intrusions from Log Files

Preparing your system for a cracker attack is only part of the battle. You must also recognize a cracker attack when it is occurring. Understanding the various log files in which Red Hat Linux records important events is critical to this goal. The log files for your Red Hat Linux system can be found in the `/var/log` directory. You can `cd` to that directory and use the `ls` command to list its contents. Table 14-8 lists some of the log files.

# Table 14-8: Log Files in the /var/log Directory

| Filename | Description |
| :--- | :--- |
| boot.log | Contains messages indicating which systems services have started up and shut down successfully and which (if any) have failed to start or stop. |
| cron | Contains status messages from the `crond`, a daemon that periodically runs scheduled jobs, such as backups and log file rotation. |
| dmesg | A recording of messages printed by the kernel when the system boots. |
| lastlog | The latest login date and time for each user on the system. |