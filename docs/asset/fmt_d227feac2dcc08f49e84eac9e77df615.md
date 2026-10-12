
```
;; Query time: 75 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Tue Feb 09 12:35:43 EST 2016
;; MSG SIZE rcvd: 68
$
```

如果你需要查询多个服务器或域名的 DNS 信息，`nslookup` 命令提供了一个交互式界面，你可以在其中输入命令：

```
$ nslookup
> www.google.com
Server: 192.168.1.254
Address: 192.168.1.254
Non-authoritative answer:
Name: www.google.com
Address: 172.217.22
> wikipedia.org
Server: 192.168.1.254
Address: 192.168.1.254
Non-authoritative answer:
Name: wikipedia.org
Address: 208.80.153
> exit
```

你也可以动态指定另一个 DNS 服务器地址进行查询，以判断是否是 DNS 解析失败。

# 高级网络排除

除了上一节所示简单测试外，Linux 还有一些高级程序可以提供有关网络环境的复杂信息。查看系统中哪些连接是活跃的解决方法有两种：`netstat` 命令和 `ss`。

# netstat 命令

`netstat` 命令可以为你提供大量信息。默认情况下，它列出所有打开的网络连接：

```
netstat
Active Internet connections (w/o servers)
Proto  Recv-Q  Send-Q   Local Address           Foreign Address       State
unix      2       DGRAM   10825                 /run/dbus/notify      
unix      2       DGRAM   10933                 /run/systemd/shutdown
unix      6       DGRAM   6609                  /run/systemd/socket
unix      25      DGRAM   6611                  /dev/log
tcp      0       STREAM  25693                 0.0.0.0:*               0.0.0.0:*      ESTABLISHED
tcp      0       STREAM  20770                 0.0.0.0:*               0.0.0.0:*      ESTABLISHED
tcp      0       STREAM  19511                 0.0.0.0:*               0.0.0.0:*      ESTABLISHED
tcp      2       DGRAM  24125                 0.0.0.0*               0.0.0.0*      ESTABLISHED
tcp      3       STREAM  19335                 0.0.0.0*               0.0.0.0*      ESTABLISHED
tcp      3       STREAM  18357                 0.0.0.0*               0.0.0.0*            ABLISHED
tcp      3      STREAM  22358                 /run.0...socket      ESTABLISHED
unix      3      STREAM  24818                 /run.dbus/socket
```

`netstat` 命令产生输出日志，因为 Linux 系统通常有多个程序在使用网络服务。你可以通过 `-t` 选项将输出限制为 TCP 连接，通过 `-u` 为 UDP 连接：

```
$ netstat -t
Active Internet connections (w/o servers)
Proto  Recv-Q  Send-Q   Local Address           Foreign Address       State
tcp      1       10.0.2.15:58633        localhost               CLOSE_WAIT
tcp6      1      ip6-localhost:57782     localhost CLOSE_WAIT
```

你可以使用 `-l` 选项获取监听网络端口的应用程序列表：

```
$ netstat -l
Active Internet connections (only servers)
Proto  Recv-Q  Send-Q   Local Address           Foreign Address       State
tcp       0               linux.domain           *:*               LISTEN
tcp       0               localhost              LISTEN
tcp6      0               ipv6-localhost         [::*    LISTEN
udp       0               *                      *::*
udp       0               *:mdns                 *::*
udp       0               *:36355               *::*
udp       0               linux.domain           *::*
udp       0               *:bootp                *::*
udp       0               *:12461               *::*
pdp6      0               [::]:64294             [::*]
pdp6      0               [::]:60259             [::*]
udp       0               *:mdns                 *::*
...
```

你可以看到，仅仅标准的 Linux 工作站后台有大量的活动在等待连接。`netstat` 命令的另一个伟大功能是 `-s` 选项显示系统在网络上使用的不同类型包的统计信息：
