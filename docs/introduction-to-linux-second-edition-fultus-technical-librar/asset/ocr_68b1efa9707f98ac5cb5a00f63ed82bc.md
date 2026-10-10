After adding a new scheduled task, the system will tell you that a new crontab is installed. You do not need to restart the *cron* daemon for the changes to take effect.
In the example, *billy* added a new line pointing to a backup script:

```
billy:~-> crontab -e
45 15 * * 3 mail -s "sports evening" billy
4 4 * * 4,7 /home/billy/bin/backup.sh
<--write and quit-->
crontab: installing new crontab
billy:~->
```

The *backup.sh* script is executed every Thursday and Sunday. See Section 7.2.5 for an introduction to shell scripting. Keep in mind that output of commands, if any, is mailed to the owner of the crontab file. If no mail service is configured, you might find the output of your commands in your local mailbox, `/var/spool/mail/<your_username>`, a plain text file.

# Who runs my commands?

You don't have to specify the user who should run the commands. They are executed with the user's own permissions by default.

# 4.5 Summary

Linux is a multi-user, multi-tasking operating system that has a UNIX-like way of handling processes. Execution speed of commands can depend on a thousand tiny things. Among others, we learned a lot of new commands to visualize and handle processes. Here's a list:

| Command | Meaning |
|:---|:---|
| `at` | Queue jobs for later execution. |
| `atq` | Lists the user's pending jobs. |
| `atrm` | Deletes jobs, determined by their job number. |
| `batch` | Executes commands when system load level permits. |
| `crontab` | Maintain crontab files for individual users. |
| `halt` | Stop the system. |
| `init runlevel` | Process control initialization. |
| `jobs` | Lists currently executing jobs. |
| `kill` | Terminate a process. |