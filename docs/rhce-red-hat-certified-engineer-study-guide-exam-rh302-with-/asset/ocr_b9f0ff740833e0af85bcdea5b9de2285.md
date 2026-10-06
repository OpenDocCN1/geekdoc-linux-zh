# TABLE 4.3 Important Linux Daemons Using inetd (continued)

| Daemon | Description |
|---|---|
| shell | Provides remote shell service. |
| swat | Provides Web-based administration for the Samba package. |
| systat | Provides process performance data. |
| talk | Provides remote user communication. |
| telnet | Provides remote login. |
| tftp | Transfers files to and from remote hosts with minimal authentication and overhead. |

You can determine what daemons are currently running by issuing the command

ps x

The output of this command includes the process ID (PID) and the command associated with each daemon:

| PID TTY STAT TIME COMMAND |
|---|---|---|---|
| 1 ? | S | 0:03 init |
| 391 ? | S | 0:17 syslog -m 0 |
| 402 ? | S | 0:00 klogd |
| 430 ? | S | 0:00 crond |
| 444 ? | S | 2:37 apachewatch -i eth0 |
| 458 ? | S | 0:18 named |
| 472 ? | S | 0:28 /usr/sbin/sshd -p 23 |
| 478 ? | S | 0:14 xntpd -A |
| 491 ? | SL | 0:00 lpd -l |
| 506 ? | S | 0:06 /usr/sbin/dhcpd |
| 521 ? | S | 0:00 sendmail: accepting connections |
| 556 ? | S | 0:00 -1 |
| on port 25 571 ttyS0 | S | 0:00 gpm -t MouseMan |
| 585 ? | S | 0:00 httpd |
| 602 ? | S | 0:00 logger |