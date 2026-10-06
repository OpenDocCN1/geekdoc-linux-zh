# 7.1.9 Scheduling

To access the scheduling feature, go to **File>Scheduler** on the menu.

![](bbox=[0.273, 0.11, 0.843, 0.427])

BRU provides a scheduling utility to automate the backup process for the bus administrator. There are three predefined definitions: Full, Level 1, and Level 2. These are the same definitions in 7.1.7, “The big buttons in BRU” on page 185. You can create your own definitions in the Creating Archives interface.

From the BRU for X11 Scheduler interface, you can set scheduled backups based on weekly, monthly, or single dates. The scheduler is very flexible. In order to take advantage of the scheduling options, you must save your desired scheduler configuration and verify that the scheduler is running from cron. To verify or add the cron entry, log in as root and type:

```
crontab -e
```

Insert the following line:
`0/5 * * * * /usr/local/bin/bruscale`

If you choose a different path for the binaries during installation, change the entry accordingly.

188 Linux System Administration and Backup for IBM @server xSeries and Netfinity