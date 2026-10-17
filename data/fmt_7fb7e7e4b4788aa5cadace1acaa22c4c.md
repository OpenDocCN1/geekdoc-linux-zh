
```
[root@host1] tcpdump -n -nn -i eth2 tcp or udp
tcpdump: listening on eth2
09:31.047327 10.0.0.7447 > 10.0.0.673: . ack 212571 win 49265
<nop,nop,timestamp 92252100 25668411> (DF)
09:31.047570 10.0.0.7447 > P 212571:212579(8) ack 31 win 6432
<nop,nop,timestamp 25668418 92252100> (DF)
09:31.048146 10.0.0.7447 > 10.0.0.673: . ack 22579 win 63712
<nop,nop,timestamp 92252100 25668418> (DF)
09:31.048184 10.0.0.7447 > P 311:315(4) ack 31 win 63712
<nop,nop,timestamp 92252100 25668418> (DF)
09:31.048215 10.0.0.7447 > P 212579:212587(8) ack 31 win 6432
<nop,nop,timestamp 92252100 25668418> (DF)
09:31.051583 10.0.0.673 > . ack 212587 win 63712
<nop,nop,timestamp 92252104 25668418> (DF)
09:31.051683 10.0.0.673 > P 212587:212603(6) ack 31 win 6432
<nop,nop,timestamp 92252104 25668418> (DF)
09:31.051698 10.0.0.7443 > . ack 212603 win 63712
<nop,nop,timestamp 92252104 25668418> (DF)
09:31.051748 10.0.0.7443 > P 315:319(4) ack 31 win 63712
<nop,nop,timestamp 92252104 25668418> (DF)
09:31.051887 10.0.0.673 > F 212603:212603(0) ack 31 win 6432
<nop,nop,timestamp 92252104 25668418> (DF)
09:31.052178 10.0.0.654 > 192.34.10.514: udp 77 (DF)
09:31.054627 10.0.0.7443 > F 319:319(9) ack 31 win 63712
<nop,nop,timestamp 92252104 25668418> (DF)
09:31.054698 10.0.0.673 > . ack 320 win 6432
<nop,nop,timestamp 92252104 25668418> (DF)
09:31.055887 10.0.0.50814: 63885: MX example.com. (25) (DF)
09:31.056023 10.0.0.653 > 10.0.0.70814: 63885/2/6 mail2.example.com. 20. (262) (DF)
09:31.056098 10.0.0.70814 > 10.0.0.653: 63886+ A example.com. (30) (DF)
09:31.056280 10.0.0.653 > 10.0.0.70814: 63886/1/4 A 192.168.237.153 (208) (DF)
```

## 46 第一部分：网络安全上下文

```
09:31:01.564497 10.0.0.7.50814 > 10.0.0.6.53: 63887+ PTR 7.97.107.199.in-addr.arpa, (43) (DF)
09:31:01.568209 10.0.0.6.53 > 10.0.0.7.50814: 63887 1/2/2 (141) (DF)
```

过滤器接收了 342 个包

内核丢弃了 0 个

请注意，每个数据包都列出了其到达时间，精确到微秒。接下来的是源 IP 地址和端口（如果适用），然后是目标 IP 地址和端口。P 和 F 分别表示 TCP 的 PSH 和 FIN 标记。输出还显示了 TCP 序列号和确认号、窗口大小以及选项。学习读取数据包转储需要大量的时间和研究。然而，对于防火墙设计者来说，掌握这项技能是值得的努力。

要将数据包写入捕获文件，请使用 `-w` 标记。要从捕获文件中读取数据包，请使用 `-r` 标记并替换为接口名称。

## tcpdump

`tcpshow` 命令可以帮助你解释 `tcpdump` 的输出。使用 `tcpshow` 的简单方法是将 `tcpdump` 的输出管道给它。

```
[root@host root]# tcpdump -s 1518 -lenx -i eth2 tcp or udp | tcpshow -pp -cooked -terse | less
```

> `tcpshow` 命令未包含在 Red Hat 发行版中。你可以从 http://www.tcpshow.org/ 或 Red Hat 贡献库获取。

## iptraf

`iptraf` 命令用于测量进入或离开网络接口的流量体积。该命令使用字符模式菜单作为用户界面。要查看，请使用此命令：

`iptraf`

菜单如图 2-15 所示。使用方向键导航菜单并按 Enter 键进行选择。

![](img/0f69b2a8749a24b957044e9f26f2d5b4_77_0.png)

图 2-15：iptraf 菜单

常规接口统计（General Interface Statistics）是最有功能之一。图 2-16 显示了相关的输出。报告显示了每个接口接收的数据包数量和数据速率。你可以输入字母 x 返回主菜单。

![](img/0f69b2a8749a24b957044e9f26f2d5b4_77_1.png)

图 2-16：Iptraf 接口统计

## TCP/IP 配置

本节介绍了 Red Hat Linux 中使用的关键 TCP/IP 配置文件。它提供了诸如 `netconfig` 等工具，可以代表你修改这些文件的内容。然而，这些工具及其用户界面在不同版本之间会发生，而配置文件及其结构在许多版本中保持相对稳定。因此，许多系统管理员更倾向于使用文本编辑器微调现有的配置文件，而不是使用配置工具。无疑，理解配置文件有助于你对系统工作原理建立更好的心理模型。

与前节一样，本节并不尝试做到面面。它重点关注防火墙背景下最重要的文件和配置项。欲需更详细、全面的介绍，请参见本章之前引用的 Collings 和 Wall 的书中“域名服务（Domain Name Service）”部分。

### /etc/sysconfig/network

`/etc/sysconfig/network` 文件用于确定主机是否连接到网络，并指定主机名和默认网关。这是一个示例：

```
[root@host sysconfig# more /etc/sysconfig/network
NETWORKING=yes
HOSTNAME=myhost.example.com
GATEWAY=192.0.2.34
```

注意，文件中的所有行都采用 shell 赋值的形式，为环境变量赋值。你可以使用任选的文本编辑器来修改文件内容。然而，在重启网络之前，更改不会生效。

### /etc/sysconfig/static-routes

当主机访问默认网关以外的网关时，使用 `/etc/sysconfig/static-routes` 文件。否则，该文件不存在。这是一个示例：

```
[root@root]# more /etc/sysconfig/static-routes
any 199.199.199.199 netmask 255.255.255.255 gw 192.0.2.34
```

该文件由一行或多行，每行包含以下字段：

- *接口 (Interface)*：网络接口名称或单词，表示该规范适用于所有安装的接口。
- *主机或网络 (Host or network)*：单词 host 或 net，指示 IP 地址是主机的地址还是网络的地址。
- *IP 地址 (IP address)*：目标主机或网络的 IP 地址。
- *网络掩码 (Network mask)*：单词 netmask，后跟目标主机或网络的子网掩码。
- *网关 (Gateway)*：字母 gw，后跟网关的 IP 地址。

与 `/etc/sysconfig/network` 文件一样，你可以使用任选的文本编辑器修改 `/etc/sysconfig/static-routes` 文件的内容。然而，在重启之前，更改不会生效。

![](img/0f69b2a8749a24b957044e9f26f2d5b4_79_0.png)

### 第一部分：网络安全上下文

### /etc/sysconfig/network-scripts/ifcfg-eth
