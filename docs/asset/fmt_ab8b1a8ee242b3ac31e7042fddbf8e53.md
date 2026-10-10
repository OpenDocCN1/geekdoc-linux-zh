
```
文件 编辑 收藏 帮助
10月15日 09:52:22 crond(CRON): (fork)
10月15日 09:52:22 crond: startup
10月15日 09:52:23 crond: Starting Webmin in /usr/share/webmin
10月15日 09:52:23 crond: Webmin succeeded
10月15日 09:52:23 crond: ifs succeeded
10月15日 09:52:23 crond: (listening on tty1)
10月15日 09:52:23 crond:ancor[143]: Android 2.3 started at 2002-10-15
10月15日 09:52:23 crond:ancor[144]: startup succeeded
10月15日 09:52:23 crond:ancor[145]: Will run cron_daily; in 5 min
10月15日 09:52:23 crond: execution succeeded
10月15日 09:52:23 crond: radcheck; radix started
10月15日 09:52:23 crond: loading default configuration
10月15日 09:52:23 crond: Running Linux hooks; succeeded
10月15日 09:52:23 crond: (version 1.2.4 (release)) (Built Sat Dec
10月15日 17:29:57 PST 2001) standard mode STDOUT
10月15日 09:52:23 crond: listening on IPV6
10月15日 09:52:23 crond: named[1534]: loading configuration from '/etc/named.conf'
10月15日 09:52:23 crond: named[1536]: no IPv6 interfaces found
10月15日 09:52:23 crond: listening on IPv4 Interface, in 172.0.0.1:53
tail --n 20
```

图 13-8：在 Linux 中使用 `tail` 命令查看日志文件。

```
文件 编辑 收藏 帮助
[root@localhost ~]# tail messages
10月15日 10:14:54 gawk:mail[1734]: session opened for root by (uid=0)
10月15日 10:14:54 gdond:master-server[2071]: starting
10月15日 10:11:21 gdond:name-server[2071]: name started
10月15日 10:20:20 crond(2048): (starting) (version 1.2.4), pid 2048 for
root
10月15日 11:52:27 gdond:cron(2048): 21 items remain in the cache after
less than 300 seconds
10月15日 11:56:16 crond(2048): CRON (run-parts /etc/cron/hourly)
10月15日 11:57:16 crond:named[2063]: warning: can't get client address: Transport
error
10月15日 11:52:27 gdond:cron(2048): 18 items remain in the cache after
less than 300 seconds
10月15日 12:01:00 crond(CRON[2524]): root) CMD (run-parts /etc/cron/hourly)
[root@localhost ~
```

图 13-9：使用 `tail` 命令显示文件的末尾。

# 246 第五部分：安全与高级 DNS 技巧

这种方法非常有用，因为在你处理 DNS 服务器时，可以在屏幕角落开启一个 shell 窗口进行监控，实时查看正在发生的情况。按下 `Ctrl-C` 可以中断 `tail -f` 命令。

```
File Edit Settings Help
[root@server ~] tail -f: starting
Oct 15 10:21:52 server[1742]: session opened for root user (uid=0)
Oct 15 10:21:52 gourd[2031]: new process starting
Oct 15 10:21:52 gourd[2048]: starting (version 1.0.4), pid 2048 used
Oct 15 10:21:53 gourd[2048]: 0 items remain in cache after
Oct 15 10:21:54 cron[2063]: CRON: (root) shell (run-parts /etc/cron,hourly)
Oct 15 10:21:54 gourd: can't get client address: Transport endpoint is not connected
Oct 15 10:21:56 gourd: 0 items remain in cache after
ready-synced items older than 300 seconds
Oct 15 10:21:57 gourd: 0 items remain in the cache after
ready-synced items older than 300 seconds
Oct 15 10:22:00 cron[2063]: CRON: (root) shell (run-parts /etc/cron,hourly)
```

查看日志文件的最后方法是使用 `grep <pattern> <file>`，其中 `<pattern>` 是你在 `<file>` 中搜索的内容。在这种情况下，你可以使用 `grep named` 命令查找所有与 DNS 相关的日志条目，如图 13-11 所示。

图 13-11 使用 `grep` 查找所有 DNS 相关的日志条目

```
File Edit Settings Help
[root@server ~] grep named messages
Oct 15 10:21:53 named[1532]: starting BIND 9.2.0
Oct 15 10:21:53 named[1534]: loading configuration from "/etc/bind/named.conf"
Oct 15 10:21:55 named[1536]: no IPv4 interfaces found
Oct 15 10:21:56 named[1538]: listening on IPv4 interface lo, 127.0.0.1
Oct 15 10:21:56 named[1540]: listening on IPv4 interface eth0, 192.168.1.105
Oct 15 10:21:56 named[1542]: command channel listening on 127.0.0.1:53
Oct 15 10:21:53 named[1544]: local:local;no TTL specified using SOA MIN TTL
Oct 15 10:21:53 named[1546]: zone 0.0.127,IN-HBR/APWA: loaded serial 100
Oct 15 10:21:53 named[1548]: local:local;no TTL specified using SOA MIN TTL
Oct 15 10:21:53 named[1550]: zone 192.168.1.0,IN-HBR/APWA: loaded serial 100
Oct 15 10:21:53 named[1552]: zone_sample,tid/IN: loading master file,
Oct 15 10:21:53 named[1554]: running
```
