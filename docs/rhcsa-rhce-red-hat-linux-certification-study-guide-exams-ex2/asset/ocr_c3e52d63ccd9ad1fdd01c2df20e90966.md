environmental variables for the current user, run the env command. If that user is your account, some of the standard variables in RHEL include HOME, which should match your home directory, SHELL, which should match the default shell, and LOGNAME as the username.

Other variables can be set in the /etc/crontab and related files such as /etc/anacrontab and /etc/cron.d/0hourly in the following format:

```
Variable=Value
```

Some variables are already set for you. For example, MAIL for me is /var/spool/mail/michael, LANG is en_US.UTF-8, and PATH is where the shell looks for commands. You can set these variables to different values in various cron configuration files. For example, the default /etc/crontab file includes the following variables:

```
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/
```

Note that the values of PATH, MAILTO, and HOME are different from standard environment variables. The PATH variable in a cron configuration file may be different from the PATH variable associated with a shell. In fact, the two variables are independent. Therefore, you'll want to know the exact path of every command in each cron configuration file. Specify the absolute path with the command if it isn't in the crontab PATH.

The MAILTO variable can help you administer several Linux systems. The cron daemon sends output by e-mail. Just add a line such as MAILTO=me@example.net to route all cron messages associated with that file to that e-mail address.

The format of a line in /etc/crontab is now detailed in comments, as shown in Figure 9-11. Each of these columns is explained in more detail in Table 9-3.

If you see an asterisk in any column, the cron daemon runs that command for all possible values of that column. For example, an * in the minute field means that the command is run every minute during the specified hour(s). Consider another example, as shown here:

```
1 5 3 4 * 1s
```