The script looks through the who output and kills any logins idle for too long. If you're not root, though, you can only kill your own processes. The output messages tell you who else has been idle too long, but you can do anything about it unless you're root.

Of course, running killidle manually is a bit silly. You'd have to remember to run it periodically, and it wouldn't be much of a security monitor run if you forget to run it. If you run it from root's crontab, you can set it to run around the clock. As a root cron job, it has root's privileges, so it could kill other login processes without restriction. Finally, since all cron command output is automatically captured and mailed to the user whose crontab is executing, root would receive a mail message containing all of the timeout warnings for each killidle run.

The simplest way to put killidle in the root crontab is to use the line

```
* * * * * /usr/local/bin/killidle
```

assuming that /usr/local/bin is the directory holding the killidle script. The five asterisks tell cron to run killidle once a minute every minute of every day cron is up. That could be extreme, but it would get the job done. To reduce the script's impact on system resources, run it only a few times an hour.

For example, the crontab line

```
0,15,30,45 * * * /usr/local/bin/killidle
```

checks for idle ttys every 15 minutes. Considering that the script's default is 20 minutes idle, the worst case idle time would be 29 minutes for a login started one minute after cron's last run. Fourteen minutes later, cron runs again, but the tty has run for only 14 minutes, which is less than killidle's 20, so killidle leaves it alone. Fifteen minutes later, a total of 29 minutes, cron runs killidle again and catches the old tty.

You could run killidle with a 15-minute option. If you do that, however, the same timing problem appears. A login that is only 14 minutes old when cron runs killidle would survive this run. killidle would eliminate the login 15 minutes later if the login were still idle. That login would have survived for a total of 29 minutes.