

## 16.10.2 查看端口和套接字使用情况

可以使用 "netstat -a" 命令显示集群成员（或任何系统）上端口和套接字的当前使用情况。以下输出中的本地地址和外地地址列以最后一点之后的数字或助记符形式显示端口号（"molari.dec.com.4035" 中的端口号为 4035）。

```
# netstat -a

Active Internet connections (including servers)
Proto Recv-Q Send-Q Local Address          Foreign Address        (state)
tcp    0     0  molari.dec.com.4035    dns5.dec.com.domain    TIME_WAIT
tcp    0   217  molari.dec.com.telnet  laptop2.dec.com.1184   ESTABLISHED
tcp    0     0  babylon5.dec.com.domain *.*                    LISTEN
tcp    0     0  molari.dec.com.domain  *.*                    LISTEN
tcp    0     0  localhost.domain       *.*                    LISTEN
tcp    0     0  molari-ics0.domain     *.*                    LISTEN
tcp    0     0  *.*.596                 *.*                    LISTEN
--
(lots more)
tcp    0     0  molari.dec.com.1153    *.*                    LISTEN
tcp    0     0  localhost.1153         *.*                    LISTEN
tcp    0     0  molari-ics0.1153       *.*                    LISTEN
tcp    0     0  molari.dec.com.1152    *.*                    LISTEN
tcp    0     0  localhost.1152         *.*                    LISTEN
tcp    0     0  molari-ics0.1152       *.*                    LISTEN
tcp    0     0  *.830                  *.*                    LISTEN
tcp    0     0  *.2049                 *.*                    LISTEN
tcp    0     0  *.1022                 *.*                    LISTEN
tcp    0     0  *.gill                 *.*                    LISTEN
tcp    0     0  *.tftp                 *.*                    LISTEN
udp    0     0  *.2049                 *.*
udp    0     0  *.time                 *.*
udp    0     0  babylon5.dec.com.domain *.*
udp    0     0  molari.dec.com.domain  *.*
udp    0     0  localhost.domain       *.*
udp    0     0  molari-ics0.domain     *.*
udp    0     0  *.111                  *.*
udp    0     0  *.1139                 *.*
udp    0     0  *.1144                 *.*
udp    0     0  *.1145                 *.*
udp    0     0  *.1146                 *.*
udp    0     0  babylon5.dec.com.ntp   *.*
udp    0     0  molari.dec.com.ntp     *.*
udp    0     0  localhost.ntp          *.*
--
(lots more)
--
```

通过在之前的 netstat 命令中添加 "-n" 选项，可以更轻松地辨别原始端口号。同样，最右边的点之后的数字是端口号。

```
# netstat -an
Active Internet connections (including servers)
Proto Recv-Q Send-Q Local Address          Foreign Address        (state)
tcp      0      0 192.168.0.69:4034      192.168.0.2:53         TIME_WAIT
tcp      0      0 192.168.0.69:4035      192.168.0.2:53         TIME_WAIT
tcp      0  300 192.168.0.69:23        192.168.0.2:1184       ESTABLISHED
tcp      0      0 192.168.0.70:53        *:*                    LISTEN
tcp      0      0 192.168.0.69:53        *:*                    LISTEN
tcp      0      0 127.0.0.1:53           *:*                    LISTEN
tcp      0      0 10.0.0.2:53            *:*                    LISTEN
tcp      0      0 *:596                  *:*                    LISTEN
...(lots more)
tcp      0      0 192.168.0.69:1153      *:*                    LISTEN
tcp      0      0 127.0.0.1:1153         *:*                    LISTEN
tcp      0      0 10.0.0.2:1153          *:*                    LISTEN
tcp      0      0 192.168.0.69:1152      *:*                    LISTEN
tcp      0      0 127.0.0.1:1152         *:*                    LISTEN
tcp      0      0 10.0.0.2:1152          *:*                    LISTEN
tcp      0      0 *:830                  *:*                    LISTEN
tcp      0      0 *:2049                 *:*                    LISTEN
tcp      0      0 *:1022                 *:*                    LISTEN
tcp      0      0 *:61                   *:*                    LISTEN
tcp      0      0 *:111                  *:*                    LISTEN
udp      0      0 *:2049                 *:*
udp      0      0 *:37                   *:*
udp      0      0 192.168.0.70:53        *:*
udp      0      0 192.168.0.69:53        *:*
udp      0      0 127.0.0.1:53           *:*
udp      0      0 10.0.0.2:53            *:*
udp      0      0 *:111                  *:*
udp      0      0 *:1139                 *:*
udp      0      0 *:1144                 *:*
udp      0      0 *:1145                 *:*
udp      0      0 *:1146                 *:*
udp      0      0 192.168.0.70:123       *:*
udp      0      0 192.168.0.69:123       *:*
udp      0      0 127.0.0.1:123          *:*
...(lots more)
```

## 16.10.3 动态分配的端口号

可以通过检查 /etc/services 文件将端口号与实际应用程序关联起来（参见第 16.10.1 节）。请注意，并非所有数字都可以在该文件中找到。例如，检查 /etc/services 文件中的 telnet 条目会显示 telnet 与 TCP 端口号 23 相关联。但连接有两端。telnet 连接的另一端使用什么端口号？运行 telnetd 的服务器端将与端口号 23 相关联。客户端将分配一个为用户请求保留的端口。

这些客户端端口由内核中的网络软件动态选择。由于客户端通常不是集群成员，因此客户端可用的这些“临时”端口往往很充足。但我们是否曾说过集群不能作为客户端？

