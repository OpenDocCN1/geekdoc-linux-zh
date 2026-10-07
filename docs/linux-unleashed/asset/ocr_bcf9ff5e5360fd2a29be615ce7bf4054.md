> Always submit a change to cron using the crontab file and an edited ASCII file. Never make changes to the file in /usr/spool/cron/crontabs.

You can see what you have submitted to cron by using the -l (list) option. This shows all the crontab entries that the cron utility knows about (essentially displaying the contents of the file with your username from /usr/spool/cron/crontabs). For example, the command shows all cron tasks for the user who submits the command:

```
crontab -l
```

If you want to remove your crontab file and not replace it, it is easily done with the -r (remove) option. This simply erases the file with your filename from the /usr/spool/cron/crontabs directory. To remove your crontab file, issue the command

```
crontab -r
```

Finally, crontab lets you call up your current cron file and start an editor (the default editor as defined by your environment variables or a system default variable) by using the -e (editor) option. When you issue the following command crontab reads your existing crontab file and loads it into the default editor (such as vi):

```
crontab -e
```

When you save the file, it is submitted to cron automatically.

Changes to the crontab file are usually effective within five minutes at most because cron reads the contents of the /usr/spool/cron/crontab file at least once every five minutes and often more frequently than that (most Linux systems have cron check the directories every minute). This also means that execution of a process you submit to cron can sometimes be delayed by a few minutes, so don’t rely on cron to be exactly on time. The more heavily loaded a system is, the more delay in execution that you can expect.

On some systems, system administrators can log all cron usage by modifying an entry in the file /etc/default/cron. One line in the file should contain the variable CRONLOG. Set the value equal to YES, and cron logs every action it takes to the file /usr/lib/cron/log. Not all versions of Linux allow cron logging. If you do enable cron logging, check the log file frequently because it can grow to a large size quite quickly.