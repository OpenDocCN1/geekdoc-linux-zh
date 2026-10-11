
字段 6 是对该数据包采取的操作，`DENY`。选项包括 `ACCEPT`、`REJECT`、`DENY`、`MASQ`、`REDIRECT` 和 `RETURN`。

字段 7 是数据包进入或离开的网络接口，`eth0`。

字段 8 是数据包中包含的消息协议类型，`PROTO=17`。字段值包括 `6` (`TCP`)、`17` (`UDP`)、`1` (`ICMP`) 以及其他协议类型的 `PROTO=<number>`。

字段 9 是数据包的源地址，`10.10.22.85`。

字段 10 是数据包的源端口，`14386`。

字段 11 是数据包的目的地址，`192.168.10.30`。

字段 12 是数据包的目的端口，`111`。

字段 13 是数据包的长度，`L=316`。

字段 14 是数据包的服务，`S=0x00`。

字段 15 是数据包的标识 ID，`I=14393`。

字段 16 是数据包的标志，`F=0x0000`。

字段 17 是数据包的存活时间（TTL），`T=52`。

## 解析系统日志

在所有可能的端口中，表 6.3 列出了经常被扫描的端口。表 6.3 中的端口与本质上不安全的服务、已知存在漏洞的服务或特定类型攻击的目标有关。

### 表 6.3 经常被扫描的端口

| 服务 | 协议 | 危险性 | 说明 |
| :--- | :--- | :--- | :--- |
| reserved | 0 | TCP/UDP | 高 | 源或目的——无合法用途 |
| echo | 0-5 | TCP | 高 | sscan 签名 |
| | 7 | TCP/UDP | 高 | UDP 攻击 |
| systat | 11 | TCP | 高 | 用户进程 (ps) 信息 |
| netstat | 15 | TCP | 高 | 网络状态：连接、路由表等 |
| chargen | 19 | TCP/UDP | 高 | UDP 攻击 |
| ftp | 21, 20 | TCP | 低-高 | FTP 服务 |
| ssh | 22 | TCP | 中-高 | SSH 服务 |
| ssh | 22 | UDP | 低 | PC Anywhere 的旧版本 |
| telnet | 23 | TCP | 高 | telnet 服务 |
| smtp | 25 | TCP | 高 | 寻找 SPAM 继器或旧版本 |
| domain | 53 | TCP | 高 | TCP 区域传输、DNS 欺骗 |
| bootps | 67 | UDP | 低 | 可能误误 |
| tftpd | 69 | UDP | 中-高 | 不安全的 FTP 替代方案 |
| finger | 79 | TCP | 低 | 用户信息 |
| link | 87 | TCP | 高 | tty 链接——入侵者经常使用 |

## 表 6.3 续

| 服务 | 端口 | 协议 | 危险性 | 解释 |
| :--- | :--- | :--- | :--- | :--- |
| sunprpc | 111 | TCP/UDP | 高 | 最常利用的端口 |
| nntp | 119 | TCP | 中-高 | 公共新闻推送或 SPAM 中继 |
| ntp | 123 | UDP | 低 | 网络时间同步；虽然可以，但不礼貌 |
| netbios-ns | 137 | TCP/UDP | 低-高 | 对 UNIX 无害 |
| netbios-dgm | 138 | TCP/UDP | 低-高 | 对 UNIX 无害 |
| netbios-ssn | 139 | TCP | 低-高 | 对 UNIX 无害 |
| imap | 143 | TCP | 高 | 三个被利用的端口之一 |
| NeWS | 144 | TCP | 高 | 窗口管理系统 |
| snmp | 161, 162 | UDP | 中 | 远程网络管理和查询 |
| xdmcp | 177 | UDP | 高 | X 显示登录管理器 |
| exec | 512 | TCP | 高 | 仅限内网 |
| biff | 512 | UDP | 高 | 仅限内网 |
| login | 513 | TCP | 高 | 仅限内网 |
| who | 513 | UDP | 高 | 仅限内网 |
| shell | 514 | TCP | 高 | 仅限内网 |
| syslog | 514 | UDP | 高 | 仅限内网 |
| printer | 515 | TCP | 高 | 仅限内网 |
| talk | 517 | UDP | 中 | 仅限内网 |
| ntalk | 518 | UDP | 中 | 仅限内网 |
| route | 520 | UDP | 高 | 路由表 |
| uucp | 540 | TCP | 中 | UUCP 服务 |
| mount | 635 | UDP | 高 | mountd 漏洞 |
| socks | 1080 | TCP | 高 | SPAM 中继、代理服务器漏洞 |
| SQL | 1114 | TCP | 高 | sscan 签名 |
| openwin | 2000 | TCP | 高 | OpenWindows |
| NFS | 2049 | TCP/UDP | 高 | 远程文件访问 |
| pcanywhere | 5632 | UDP | 低 | PC Anywhere |
| X11 | 6000+n | TCP | 高 | X Window 系统 |

## 解读系统日志

| 服务 | 端口 | 协议 | 危险性 | 解释 |
| :--- | :--- | :--- | :--- | :--- |
| NetBus | 12345, 12346, 20034 | TCP | 高 | 对 UNIX 无害 |
| BackOrifice | 31337 | UDP | 高 | 对 UNIX 无害 |
| traceroute | 33434-33523 | UDP | 低 | 入站 traceroute |
| ping | | ICMP | 低-高 | 入站 ping |
| redirect | 5 | ICMP | 高 | 重定向炸弹 |
| traceroute | 11 | ICMP | | 出站 traceroute 响应 |
| UNIX OS | 0 | TCP/UDP | 高 | 广播到目标地址 0.0.0.0 |

## 常见端口扫描日志示例

在常见的被探测端口中，你最常看到的日志消息列在此处。如果你的防火墙日志输出让你觉得很奇怪，请跳到下一节。如果你以前没见过防火墙日志条目，这些就是你最常看到的内容。为了避免跨页面换行，日志条目经过了处理：

- 22/UDP—PC Anywhere (旧版本):
  `input DENY eth0 PROTO=17 10.10.22.85:14386 192.168.10.30:22`
- 23/TCP—telnet:
  `input DENY eth0 PROTO=6 10.10.22.85:14386 192.168.10.30:23`
- 25/TCP—smtp:
  `input DENY eth0 PROTO=6 10.10.22.85:14386 192.168.10.30:25`
- 79/TCP—finger:
  `input DENY eth0 PROTO=6 10.10.22.85:14386 192.168.10.30:79`
- 110/TCP—pop-3:
  `input DENY eth0 PROTO=6 10.10.22.85:14386 192.168.10.30:110`
- 111/UDP—sunprpc:
  `input DENY eth0 PROTO=17 10.10.22.85:14386 192.168.10.30:111`
- 119/TCP—ntp:
  `input DENY eth0 PROTO=6 10.10.22.85:14386 192.168.10.30:119`
- 123/UDP—ntp:
  `input DENY eth0 PROTO=17 10.10.22.85:14386 192.168.10.30:123`
- 143/TCP—imap:
  `input DENY eth0 PROTO=6 10.10.22.85:14386 192.168.10.30:143`
- 161/UDP—snmp:
  `input DENY eth0 PROTO=17 10.10.22.85:14386 192.168.10.30:161`
- 520/UDP—route:
  `input DENY eth0 PROTO=17 10.10.22.85:14386 192.168.10.30:520`
- 635/UDP—mount:
  `input DENY eth0 PROTO=17 10.10.22.85:14386 192.168.10.30:635`
- 1080/TCP—socks:
