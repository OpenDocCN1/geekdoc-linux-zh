♦ /var/adm/utmpx. The utmp x database file contains user access and accounting information for commands such as who, write, and login. The utmp x file is where information such as the terminal line and login time are stored for access by the who command.

♦ /var/adm/wtmp x. The wtmp x file contains the history of user access and accounting information for the utmp x database. The wtmp x file keeps track of logins and logouts since reboot. The last command, described in Chapter 8, “System Security,” reads that file and processes the information.

♦ /var/adm/acct. This is the system accounting file. If enabled, the accounting file records a record for every process listing the following information: the name of the user who ran the command, the name of the command, the CPU time used, the completion timestamp of the process, and a flag indicating completion status. Accounting information can be very useful in monitoring who is doing what on your system.

♦ /var/adm/sulog. The sulog file holds records for everyone who has used the su command on the system. Here is a sample:

```
SU 04/29 09:39 + console root-daemon
SU 04/29 15:29 + console root-daemon
SU 05/02 05:38 + console root-daemon
SU 05/12 06:20 + console root-daemon
SU 05/12 07:59 + pts/1 root-bcalkins
```

♦ /var/cron/log. Keeps a record of all cron activity.

Good system administration requires that you look over your system logs frequently and keep their size in check. Some of these files can grow extremely large and fill up a file system quickly.