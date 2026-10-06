
Configure /etc/security/audit_control to choose what events to log. See http://www.securityfocus.com/infocus/1362 for detailed instructions. Reboot for the changes to take effect.

# /var/adm/loginlog

After five unsuccessful login attempts, all further attempts are logged to this file. Each log event contains the login name, ty information, and time. This file is logged only if it exists. Therefore, create this file if it doesn't exist, using the touch command. Make sure this file is readable by root.

# /var/adm/sulog

The command is used to log in another user's account. For example, user joe may say su to log in jack's account:

```
joe's_bash]$ su - jack
Password:jackpassword
[jack's_bash]$
```

Similarly, a user may log in as root local users:

```
joe's_bash]$ su - 
Password:rootpassword
[root's_bash]$
```

It is important to log all su attempts. Doing so will help detect brute-force password guessing attempts by malicious local users. Edit /etc/default/su and make sure the value of SULOG points to /var/adm/sulog. You may also enable syslogd logging by setting the value of SYSLOG to YES.

# /var/log/cron

The cron daemon logs information to this file. Edit /etc/syslog.conf and make sure the following line is:

```
cron.*[tab]/var/log/cron
```

# /var/log/maillog

This file contains information logged by the host's mail server. Details about outgoing and incoming e-mails and appropriate error messages are logged to this file. Edit /etc/syslog.conf and make sure the following line exists:

```
mail.*[tab]/var/log/maillog
```

# /var/log/messages

This file contains informational messages logged by syslogd. To enable logging to this file, a line similar to the following must be present in /etc/syslog.conf.

```
*info:mail.none;authpriv.none;cron.none[tab]/var/log/messages
```

# /var/log/secure

Processes that authenticate via username and password or other mechanisms usually log to this file. Make sure this file is read only by root. A line similar to the following must exist in /etc/syslog.conf:

```
authpriv.*[tab]/var/log/secure
```

# /var/log/wtmp

This file contains information about all the logins that have occurred on the host. It is not an ASCII file and therefore must be viewed using tools such as last. The following example shows the five recent login or logout attempts:

```
[bash]$ last  | head -5
nit pts/0      gateway        Apr 11 10:12 still logged in
anita pts/1      nest           Thu 10 21:14 still logged in
ozzy pts/1      gateway        Thu 10 21:06 - 21:08 (00:02)
kelly pts/1      ftpserver      Thu 10 20:01 - 20:02 (00:00)
asharon pts/0    wireless       Thu 10 16:34 - 21:26 (04:52)
```

# /var/run/utmp

This file contains information about users that are currently logged on the host. It is not an ASCII file and therefore must be viewed using tools such as w or who.

```
[bash]$ who
deepti pts/0      Apr 14 10:12 (intranet)
yash pts/1       Apr 13 21:14 (egmoreftp)
atasha pts/0      Apr 13 20:10 (punehtup)
```

# Log Rotation

Log files have the propensity to grow very fast and consume large amounts of disk space. For some environments, it makes sense to delete old log contents. To enable log rotations, most distributions use tools such as newsyslog or logrotate. These tools should be called on a frequent time ideal using the cron daemon. Check the man pages for newsyslog or logrotate.

# Free Space in /var

Depending on the environment, the /var directory can get big. It is a good idea to routinely check the amount of free space in /var using the df command. The /var must be mounted as a separate partition. Please see "Disk Partitions" in Chapter 8 for more.

# PATCHING

It is most important to stay up-to-date with software patches. Depending on your distribution, the table follows lists most popular Unix and Linux distributions where to obtain patches:

| Distribution | Patches |
|---|---|
| AIX | http://www.ibm.com/ |
| BSD | http://www.bsdi.com/ |
| Caldera OpenLinux | ftp://calderasystems.com/ |
| Debian Linux | http://www.debian.org/ |
| FreeBSD | ftp://freebsd.org/ |
| IRIX | http://www.sgi.com/ |
| HP Unix | http://www.hp.com/ |
| Mandrake Linux | http://www.mandrake.com/ |
| NetBSD | http://www.netbsd.org/ |
| OpenBSD | ftp://openbsd.org/ |
| Red Hat Linux | http://www.redhat.com/ |
| Slackware Linux | ftp://slackware.com/ |
| Solaris | http://www.sun.com/ |
| SuSE Linux | http://www.suse.com/ |
