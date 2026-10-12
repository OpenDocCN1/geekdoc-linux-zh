# **Listing 8.1 A Typical `/etc/crontab` File Used by the System for Regular Maintenance**

```
SHELL=/bin/bash
PATH=/sbin/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

The list of environment variables that appears at the beginning of the output is one of the added features that come with the Vixie Cron package. You specify the shell, path, and home directory for each of these tasks, and stipulate who receives via e-mail the results of the crontab run after the task is either successfully or unsuccessfully carried out. Each entry as listed in the /etc/crontab file points to a certain file that contains additional scripts. If you want the system to run a definitive task at a specified time, here is where you can also enter the script or modify an existing one to your liking. Users who prefer to rotate their log files at shorter intervals can find this specific system task in this location as well.

> **CAUTION**
> 
> Bear in mind that any additions to these files will affect the system globally, whereas each user's crontab entries affect only the individual's files. Exercise caution when changing system files. If you break something, certain logs and files may stop working. As a precautionary measure, always make a backup before changing any system file.

# **Editing crontab Files**

If you need to remove the cron files of a particular user, simply deleting the user's file from the /var/spool/cron directory is normally sufficient. This is useful if the user is no longer present on the system or if you need to lock his or her account.