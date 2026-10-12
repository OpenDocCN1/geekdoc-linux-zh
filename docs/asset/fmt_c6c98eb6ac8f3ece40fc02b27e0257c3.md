
```
# netstat -a
Active Internet connections (including servers)
Proto  Recv-Q Send-Q Local Address   Foreign Address   State
tcp        0      0 *:sunrpc        *:*             LISTEN
tcp        0      0 *:time          *:*             LISTEN
tcp        0      0 *:ftp           *:*             LISTEN
tcp        0      0 *:telnet        *:*             LISTEN
tcp        0      0 *:shell         *:*             LISTEN
tcp          0 0 *:login                 *:*                        LISTEN
tcp          0 0 *:pop3                  *:*                        LISTEN
tcp          0 0 *:imap2                 *:*                        LISTEN
tcp          0 0 *:finger                *:*                        LISTEN
tcp          0 0 *:systat                *:*                        LISTEN
tcp          0 0 *:netstat               *:*                        LISTEN
tcp          0 0 *:auth                  *:*                        LISTEN
tcp          0 0 *:printer               *:*                        LISTEN
tcp          0 0 *:711                   *:*                        LISTEN
tcp          0 0 *:2049                  *:*                        LISTEN
tcp          0 0 *:smtp                  *:*                        LISTEN
tcp          0 0 *:www                   *:*                        LISTEN
udp          0 0 *:sunrpc                *:*                        
udp          0 0 *:syslog                *:*                        
udp          0 0 *:time                  *:*                        
udp          0 0 *:biff                  *:*                        
udp          0 0 *:ntalk                 *:*                        
udp          0 0 *:708                   *:*                        
udp          0 0 *:2049                  *:*                        
raw          0 0 *:1                     *:*

Active UNIX domain sockets (including servers)

Proto RefCnt Flags      Type    State    I-Node Path
unix 2    [ ]          STREAM CONNECTED  486
unix 1  [ ACC ]        STREAM LISTENING 499   /dev/log
unix 1  [ ACC ]        STREAM LISTENING 527   /dev/printer
unix 2    [ ]          STREAM CONNECTED 533
unix 2    [ ]          STREAM CONNECTED 534   /dev/log
unix 2    [ ]          STREAM CONNECTED 553
unix 2    [ ]          STREAM CONNECTED 554   /dev/log
unix 2    [ ]          STREAM CONNECTED 812
unix 2    [ ]          STREAM CONNECTED 813   /dev/log
unix 2    [ ]          STREAM CONNECTED 816   /dev/log
unix 2    [ ]          STREAM CONNECTED 826
unix 1  [ ACC ]        STREAM LISTENING 841   /var/run/gpmctl
```

当您的网络连接正常工作后，您可以使用`traceroute`命令来确定如何从您的地址到达网络上的另一个地址。您可以查看需要多少跳（hops），以及沿途经过哪些地址。

```
# traceroute www.yahoo.com
traceroute to www9.yahoo.com (204.71.200.74), 30 hops max, 40 byte packets
 1 core1-fe8-1-0.mv.best.net (206.184.139.129)  3.406 ms   0.685 ms   0.510 ms
 2 so-0-l.br1.NUO.globalcenter.net (206.251.0.89)  2.253 ms   2.163 ms   2.124 ms
 3 fe5-1.cr1.NUO.globalcenter.net (206.251.1.33)  28.193 ms  2.663 ms   2.759 ms
 4 pos0-0.wr1.NUO.globalcenter.net (206.251.0.122) 2.541 ms 2.404 ms 2.318 ms
 5 pos1-0C12.wr1.SNV.globalcenter.net (206.251.0.74) 3.808 ms 3.880 ms 2.908 ms
 6 pos5-0.cr1.SNV.globalcenter.net (206.251.0.105) 3.684 ms 3.544 ms 5.642 ms
 7 www9.yahoo.com (204.71.200.74) 3.604 ms 3.321 ms 3.268 ms
```

## Linux 防火墙

由于`Linux`可以处理多块网络接口卡（`NIC`），因此它也可以用作防火墙。`Linux`确实自带内置的防火墙：`ipfw`、`ipfwadm`和`xfw`。

![](img/8ad518fddafc7f5e73715a2604b61d50_390_0.png)

### 清单 11-5：在 /proc/net 中查看路由信息
