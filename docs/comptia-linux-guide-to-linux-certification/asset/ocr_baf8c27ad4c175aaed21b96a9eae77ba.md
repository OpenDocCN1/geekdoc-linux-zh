For more detailed information regarding system processes during the startup process and afterwards, you can view the contents of the /var/log/messages or /var/log/syslog files on most Linux distributions. A sample syslog file from an Ubuntu Server system is shown in the following output:

```
root@server1:~# tail /var/log/syslog
Sep 30 09:56:48 server1 kernel: [ 38.357431] cgroup: systemd-logind (619)
created nested cgroup for controller "memory" which has incomplete
hierarchy support. Nested cgroups may change behavior in the future.
Sep 30 09:56:48 server1 kernel: [ 38.357435] cgroup: "memory" requires
setting use_hierarchy to 1 on the root.
Sep 30 09:57:07 server1 ntpdate[2031]: step time server 91.189.89.199
offset17.350701 sec
Sep 30 09:56:57 server1 kernel: [ 46.667766] audit_printk_skb: 48 callbacks
suppressed
Sep 30 09:56:57 server1 kernel: [ 46.667770] type=1400 audit
(1412085417.259:28): apparmor="STATUS" operation="profile_replace"
profile="unconfined"name="/usr/lib/cups/backend/cups-pdf" pid=2146 com-m="apparmor_parser"
Sep 30 09:56:57 server1 kernel: [ 46.667776] type=1400 audit
(1412085417.259:29): apparmor="STATUS" operation="profile_replace" pro-file="unconfined" name="/usr/sbin/cupsd" pid=2146 comm="apparmor_parser"
Sep 30 09:56:57 server1 kernel: [ 46.668185] type=1400 audit
(1412085417.259:30): apparmor="STATUS" operation="profile_replace" pro-file="unconfined" name="/usr/sbin/cupsd" pid=2146 comm="apparmor_parser"
Sep 30 09:57:13 server1 kernel: [ 63.274963] hv_balloon: Received INFO_TYPE_MAX_PAGE_TYPE
Sep 30 09:57:13 server1 kernel: [ 63.274970] hv_balloon: Data Size is 8
Sep 30 10:09:01 server1 CRON[2290]: (root)CMD [ -x /usr/lib/php5/ maxlength ] && [ -x /usr/lib/php5/sessionclean ] && [ -d /var/lib/php5 ] && /usr/lib/php5/sessionclean /var/lib/php5 $(/usr/lib/php5/maxlifes time))
root@server1:~# _
```

In Fedora 20, the logging system used to record the messages normally stored within /var/log/boot.log, /var/log/messages, or /var/log/syslog has been replaced by a journaling database system called **journald**. You can use the **journalctl** command on a Fedora 20 system with the -b option to view the same information that would normally be stored within /var/log/boot.log, /var/log/messages, or /var/log/syslog files. Since the journalctl command will display entries for each boot process, it is important to narrow down the time frame. The following command only displays boot information from the current day:

```
[root@server1 ~]# journalctl -b -since=today | less
- Logs begin at Tue 2015-09-16 21:56:29 EDT, end at Tue 2015-09-30 10:20:47
EDT.
-
Sep 30 11:02:08 localhost.localdomain systemd-journal[71]: Runtime journal is using 8.0M (max 99.8M, leaving 149.7M of free 990.2M, current limit 99.8M).
Sep 30 11:02:08 localhost.localdomain systemd-journal[71]: Runtime journal is using 8.0M (max 99.8M, leaving 149.7M of free 990.2M, current limit 99.8M).
```