
```
$ nslookup ibm.com
Server: guardian.egr.edu.edu
Address: 192.102.10.1
```

```
Name: ibm.com
Address: 204.146.80.99
```

$

# 第 14 章 网络与网络互连

`nslookup`命令使用`/etc/resolv.conf`文件来查找运行名称服务器软件的主机并将请求传递给它。名称服务器启动 DNS 服务器为传递给它的主机名查找 IP 地址。在这种情况下，名称服务器是`guardian.egr.edu`，如会话输出所示。

以下“课内练习”旨在通过学习你所在网络中主机的域名和 IP 地址，来加深你对自身网络环境的理解。你还将使用`nslookup`命令将域名翻译为 IP 地址。

# 课内练习

- 14.4. 给出局域网（LAN）上某些主机的域名。如果需要帮助，请询问你的教师。
- 14.5. 用十进制表示列出练习 14.4 中识别的主机的 IP 地址。你的网络属于哪一类（A、B 还是 C）？你是如何发现的？
- 14.6. 运行`nslookup`工具以确认练习 14.4 中识别的主机的 IP 地址。

## 14.6 互联网服务与协议

大多数用户并不理解互联网协议及其架构的复杂性——他们也不需要。他们通过实现各种互联网服务应用层协议的程序访问互联网。最常用的服务及对应的协议如表 14.3 所示。服务按字母顺序列出，而不是根据使用频率。你可以通过查看主机上的`/etc/resolv`文件来查看互联网服务及其已知端口号。

LINUX 操作系统具有一些其他操作系统不一定提供的网络相关服务。它们包括显示局域网内所有登录主机的服务、远程执行命令等。

| 表 14.3 常用互联网服务 | 对应的协议 |
| :--- | :--- |
| 电子邮件 | SMTP (简单邮件传输协议) |
| 文件传输 | FTP (文件传输协议) |
| 远程登录 | Telnet |
| 时间 | Time |
| 网页浏览 | HTTP (超文本传输协议) |

# 客户端-服务器模型

客户端-服务器模型是一种分布式计算架构，其中任务在资源或服务的提供者（称为服务器）和服务的请求者（称为客户端）之间进行划分。在这种模型中，客户端向服务器发起通信，服务器对请求做出响应。

客户端-服务器模型是许多网络应用程序的基础。例如，在 Web 中，网络浏览器是客户端，而 Web 服务器是托管网页的机器。客户端是应用程序的前端，用户与之交互；而服务器是后端，负责处理请求并提供数据。

客户端-服务器模型可以以多种方式实现。在某些情况下，单个服务器可以处理多个客户端。在其他情况下，可以使用多个服务器来平衡负载。这被称为负载均衡。

客户端-服务器模型也用于许多其他应用。例如，在电子邮件中，客户端是电子邮件程序，服务器是存储和传递电子邮件的机器。在在线游戏中，客户端是游戏软件，服务器是管理游戏状态的机器。

客户端-服务器模型是网络和计算中的一个基本概念。它允许资源和服务的分配，并为构建应用程序提供了可扩展的方法。对于任何想要学习网络的人来说，理解客户端-服务器模型都是至关重要的。

# 应用软件 417

```
$ hostname -s
upibm7
$ uname -n
upibm7.egr.up.edu
$
```

## 14.8.2 显示网络上的用户主机列表

你可以使用`rwho`（remote who）命令来显示使用你网络机器的用户信息。该命令的输出与`who`命令相似。每行输出包含用户名、用户登录的计算机和终端，以及用户登录的日期和时间。用户当前正在终端上输入；如果用户有一分钟或更长时间没有输入，`rwho`将以分钟和小时报告此空闲时间。未输入一小时或更长时间的用户用户名将从输出中省略；可以使用`-a`选项显示此类用户。以下会话展示了不带和带有`-a`选项的用法。

```
$ rwho bobk upibm7:ttyC4 Jul 26 12:03 :59
dfrakes upibm47:ttyp2 Jul 26 11:49 :11
lulay upsun17:pts/0 Jul 26 10:17 :23
oster upsun17:pts/2 Jul 26 12:28 :51
sarwar upibm7:ttyp2 Jul 26 11:15 :34
$ rwho -a bobk upibm7:ttyC4 Jul 26 12:03 :59
dfrakes upibm47:ttyp2 Jul 26 11:49 :11
kent upibm48:ttyp0 Jul 26 03:41 8:49
kittyt upibm9:ttyp0 Jul 26 07:36 1:28
kuhn upsun29:console Jul 16 13:11 99:59
lulay upsun17:pts/0 Jul 26 10:17 :23
oster upsun17:pts/2 Jul 26 12:28 :51
pioster upsun20:pts/0 Jul 26 09:53 2:41
sarwar upibm7:ttyp2 Jul 26 11:15 :34
sarwar upsun29:pts/0 Jul 26 11:24 1:00
$
```

你可以使用`rusers`（remote users）命令来显示登录到本地网络机器上的用户名称。当前使用机器的用户登录名以每台机器一行的格式显示。以下是该命令的简要描述。

```
rusers [options] [host_list]
语法：
目的：显示登录到本地网络中所有机器的用户登录名
输出：显示网络中主机上登录的用户信息，格式为每台机器一行
常用的选项/功能：
-a 如果没有用户正在使用该主机，则显示主机名
-1 以类似于`who`命令显示的长格式显示用户信息
```

`rusers`命令向网络上的所有主机发送广播，请求它们回复用户信息。它收集所有回复并按接收顺序显示信息。它会等待一分钟以捕获迟的响应。以下是该命令的简单运行示例。注意主机名显示在 16 个字符的字段中，这就是为什么名称中的`edu`部分没有完全显示的原因。如命令输出所示，用户`kent`两次登录到`upibm8.egr.up.edu`主机，`sarwar`登录了`usun29.egr.up.edu`，而用户`kittitt`和`debarras`登录了：

```
$ rusers
upibm48.egr.up.e kent kent
usun29.egr.up.e sarwar
upibm6.egr.up.ed kittitt kittitt debarras
$
```

你可以通过指定主机作为`rusers`命令的参数来显示特定主机上的用户名称。以下命令显示登录到`upibm7`主机的用户登录名。

```
$ rusers upibm7
upibm7.egr.up.edu uppppp44 uppppp uppppp26 kathek khnguyen upppp14 leslie sarwar
sarwar
$
```

如下会话所示，你可以使用带有`-a`选项的`rusers`命令，即使没有用户登录，也能显示主机名。这样做可以让你发现网络上所有主机的名称。

```
$ rusers -a
uupsun12.egr.up.e
...
uupsun27.egr.up.e
uupibm48.egr.up.e kent kent
uupsun29.egr.up.e sarwar
uupsqt.egr.up.ed
...
uupibm3.egr.up.ed
uupibm6.egr.up.ed kittyt kittyt deborah
$
```

根据网络的复杂性，`rusers`命令可能需要几秒钟完成执行。

## 14.8.3 显示网络上主机的状态

你可以使用`runtime`（remote uptime）命令来显示连接到局域网（LAN）的所有计算机的状态。输出的每行格式如下：计算机（主机）名称、系统状态（运行/关闭）、计算机运行的时间；`+`号表示登录到每个主机的用户数，以及每个主机的负载。你可以使用`-u`命令按人数显示状态。其他有用的选项有`-l`按负载排序，`-t`按运行时间排序。以下是不带和带有`-u`选项的`runtime`使用示例。

```
$ runtime
uupibm0+09:16, 0 users, load 0.00
...
uupsun29+23:51, 2 users, load 1.48, 1.35
$ runtime -u
uupibm7+09:25, 10 users, load 0.00, 0.00
uupibm47+20:01,
uupsun17+08:25, 2 users, load 0.00, 0.03
uupsun29+23:57, 1 user, load 1.30, 1.31
```

注意`usun29`已经运行了近 70 天。在接下来，你将使用`uptime`、`rwho`命令查看语法输出并了解网络情况。

## 14.8.4 测试网络连接

你可以使用`ping`命令测试网络或特定主机的状态。如果`ping`命令不起作用，请使用`whereis`更新你的路径并 debarras 再次尝试。以下是`ping`的简要描述。

`ping [options] hostname`

目的：向 'hostname' 发送 IP 数据报以测试网络是否连通；如果主机在线，它将简单地回显数据报。

常用的选项/功能：

- `-c count` 发送并接收`count`个包；只有超级用户可以使用此选项。
- `-f` 每秒发送 100 个包。
- `-s size` 发送大小为`size`的字节包（默认为 56 字节）。

以下会话说明了带和不带选项的`ping`命令。由于执行命令的主机与目标主机（`pcc.edu`和`lumps.edu.pk`）之间的物理距离和通信通道质量，往返时间存在差异。我们在后续中使用`-c`选项发送并接收三个消息。最后一个命令中使用`-c`和`-s`选项发送并接收两个 2048 字节（加上 8 字节 ICMP 头）。

```
$ ping pcc.edu
ping pcc.edu (192.220.1.109): 56 data bytes
64 from 192.220.1.109: icmp_seq=0 ttl=246 time=13.3 ms
64 from 192.220.1.109: icmp_seq=1 ttl=246 time=13.1 ms
<Ctrl-C>
--- pcc.edu ping statistics ---
2 packets transmitted, 2 packets received, 0% packet loss
round-trip min/avg/max = 13.1/13.2/13.3 ms
```

$ ping lumps.edu.pk

ping lumps.edu.pk (203.128.0.2): 56 data bytes

64 from 203.128.0.2: icmp_seq=0 ttl=238 time=1409.7 ms

64 from 203.128.0.2: icmp_seq=1 ttl=238 time=1485.5 ms

64 from 203.128.0.2: icmp_seq=2 ttl=238 time=1641.0 ms

<Ctrl-C>

--- lumps.edu.pk ping statistics ---

3 packets transmitted, 3 packets received, 0% packet loss

round-trip min/avg/max = 1409.7/1512.0/1641.0 ms

```

$ ping -c 3 pcc.edu
ping pcc.edu (192.220.1.109): 56 data bytes
64 from 192.220.1.109: icmp_seq=0 ttl=246 time=19.6 ms
64 from 192.220.1.109: icmp_seq=1 ttl=246 time=13.1 ms
64 from 192.220.1.109: icmp_seq=2 ttl=246 time=33.7 ms
--- pcc.edu ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 13.1/22.1/33.7 ms
```

$ ping -c 2 -s 2048 pcc.edu

## 422 第14章 网络与互联网络

PING pcc.edu (192.220.1.109): 2048 data bytes

2056 bytes from 192.220.1.109: icmp_seq=0 ttl=246 time=80.4 ms

2056 bytes from 192.220.1.109: icmp_seq=1 ttl=246 time=81.7 ms

--- pcc.edu ping 统计 ---

发送 2 个包，接收 2 个包，丢包率为 0%

往最小/平均/最大 = 80.4/81.0/81.7 ms

$

你可以在主机名中使用 IP 地址。例如，你可以使用`ping 192.220.1.109`而不是`ping pcc.edu`。

## 14.8.5 显示用户信息

你可以使用`finger`命令显示本地或远程主机上用户的信息。显示的信息是从用户的`~/plan`和`~/project`文件中提取的。以下是该命令的简要描述。

```
finger [options][user_list]
语法：
用途：显示 'user_list' 中用户的信息；如果不提供
'user_list'，命令将显示当前登录到指定主机的所有用户的简短状态报告。

输出：从 ~/project 和 ~/plan 文件中提取的用户信息。

常用选项/功能：
-m 仅将 'user_list' 匹配到登录名
-s 以短格式显示输出
```

接下来的会话显示了命令最简单的用法，即显示主机上单个用户 Birch Tree 的信息。

$ finger Birch

登录名: btree 真实姓名: Birch Tree

目录: /home/student/tree Shell: /bin/ksh

自 7月30日 16:16:02 登录到 pts/0，来自 upibm7.egr.up.edu

无读邮件 (Nounread mail)

## 应用软件 423

项目：为了 LINUX 而学习 LINUX ...

计划：从一个 Windows 蜥虫变成一个 LINUX 大师 ...

$

你可以配合`-s`选项使用`finger`命令短格式显示命令输出，并使用`-m`选项将 'user_list' 匹配到登录名。如果用户的登录名是 tree，那么`finger -m Tree`命令与`finger Birch`命令显示相同的信息（网络命令认为大小写字母相同）。然而，如果用户的登录名是 btree 且系统中不存在登录名 birch，则`finger`命令将显示一条消息通知你。以下是这些选项的用法。

$ finger -s Birch

登录 TTY 空闲 登录时间 办公室电话

brch Birch Tree /0 12月16 10:22 EN29

$ finger -m Birch

finger: Birch: no such user.

$

你可以使用`finger`命令显示 Internet 上某个用户的信息，前提是该主机提供 finger 服务并有 finger 服务器（finger 守护进程：正在运行）。可以使用以下命令显示 iastate.edu 域名（站点）上用户 williams 的信息。

$ finger williams@iastate.edu

[iastate.edu]

爱荷华州立大学全站 finger 服务器。

使用 `finger "h"@iastate.edu` 获取帮助信息。

登录名: williams 真实姓名: John J Williams

地址: GE AT

办公室电话: (515)555-9999 家庭电话: (515)555-0000

计划：

电子邮件: williams@iastate.edu 真真: (515)555-0000

请查看我的个人网页获取我的周表：

http://volcano.ecpe.iastate.edu/-williams/index.html

## 424 第14章 网络与互联网络

用户名 TTY 登录时间 空闲 机器 来自主机

用户未登录。

输出格式通常相同。

在不带任何参数时，`finger`返回当前登录到你机器上的所有用户状态。显示的信息量有所不同，取决于你的主机运行的 LINUX 系统。然而，每个系统都会显示以下信息。以`@hostname`作为参数时，命令显示当前登录到 'hostname' 的所有用户的状态。某些站点对通配符 * 的使用有限制。例如，mit.edu 和 osu.edu 站点要求所有查询至少包含两个字符。接下来的会话显示了登录到本地主机以及允许允许使用通配符的远程主机 iastate.edu 的所有用户状态。

## $ finger

| 登录名 | Tty | 空闲 | 登录时间 | 办公室 | 办公室电话 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| kathek | Kathe Koretsky | C4 | 59 | 7月30 13:55 | | |
| oster | Peter Osterberg | C3 | 29 | 7月30 16:12 | | |
| sarwar | Mansoor | | | | 7月30 15:21 | | |
| upppp | | | | | 7月30 02:22 | | |
| upppp | | | | | 7月30 15:21 | | |
