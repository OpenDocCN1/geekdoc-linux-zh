
```
Using logical device ie0 [/dev/nit] Output to stdout.
Log started at => Mon Nov 6 10:29:07 [pid 13146]
- - TCP/IP LOG -- TM: Mon Nov 6 10:30:50 --
PATH: distant.host.bar.edu(52864) => local.host.foo.edu(telnet)
STAT: Mon Nov 6 10:52:07, 34 pkts, 73 bytes [TH_FIN]
DATA: (255)(253)C(255)(251)(255)(250)X
: VT100(255)(240)(255)(253)^A(255)(252)^Auser id
: password
- - TCP/IP LOG -- TM: Mon Nov 6 10:35:17
PATH: distant2.bar.edu(52897) => local2.host.foo.edu(ftp)
STAT: Mon Nov 6 10:58:17, 14 pkts, 62 bytes [TH_FIN]
DATA: USER user id
: : PASS password
: :
```

## 什么是 Rootkit？

严格来说，Rootkit 的打包清单包括以下项目：

- 一个以记录密码为特化的以太网嗅探器；
- 一个带有后门的特洛伊木马登录替换程序；
- 支持程序，它们是 UNIX 实用程序的直接替换（例如，`ps`、`netstat`、`ifconfig`），这些程序可能允许某人检测到已安装的以太网嗅探器；以及
- 一个用于安装特洛伊系统程序的实用程序，使其具有与被替换文件相同的日期、权限、UID、GID 和校验和。

某些 Rootkit 变种还包括以下项目：

- `ls` 和 `du` 的替换程序；
- `in.telnetd` 的替换程序；以及
- `chfn`、`csh`、`inetd`、`top`、`rshd` 和 `syslogd` 的特洛伊木马替换程序。

## Rootkit 样本

我分析了七个不同的 SunOS Rootkit 样本和三个 Linux Rootkit 样本。SunOS 变种分为两种不同的菌株，而 Linux 变种全部属于单一菌株。

## SunOS 菌株

这两种 SunOS 菌株可以通过用于隐蔽的辅助工具、特洛伊系统程序的“智能”程度、提供的破解工具数量以及错误修复来区分。版本 1 菌株是最古老的，并且附带更多用于隐藏入侵者的辅助程序，例如 `zap`、`ls` 和 `du` 特洛伊木马替换程序。版本 2 菌株源自较旧的版本 1 菌株。版本 2 菌株修复了修改后的 SunOS 源代码中的许多错误，并改变了支持程序的构成。出于某种原因，`ls` 和 `du` 的隐蔽版本被移除了。然而，正如表 19.1 所描述的，添加了多个破解工具。

嗅探器是来自 `Phrack Magazine` 的 `Esniff.c` 程序 [第 5 卷，第 45 期，第 28 个文件中的第 5 个：1994 年 3 月 30 日（ISSN 1068-1035）]。嗅探缓冲区从 128 字节到 1024 字节不等。各种 Rootkit 将其称为 `es`、`watch` 或 `rpc.rarpd`。`login`、`ps`、`netstat` 和 `ifconfig` 都是对 Sun Microsystems 专有的 SunOS v4.1.x 源代码的破解版本。它们都读取掩码文件以指定要隐藏的输出。版本 1 菌株将文件名硬编码为 `/dev/ptyX`，其中 X 是一个小写字母（`p`、`q` 和 `r` 最受欢迎）。通常，SunOS v4.x `pty` 设备文件形式为 `ptyld`、`q`、`r` 后跟一个十六进制数字，因此很容易注意不到这些添加的文件。在版本 2 菌株中，文件名是 Rootkit 构建时 data/ 目录中的 ns.f 和 ps.f。这些掩码文件可以非常表达性强。（请参阅侧边栏“掩码文件格式”以获取示例。）

登录特洛伊木马允许任何人在提供魔术密码时通过网络以 root 身份登录。最早的版本将此密码硬编码。我见过 D13hhf 和 fasune。较新的版本在安装 Rootkit 时会查询密码。无论使用何种方法，登录特洛伊木马二进制文件中都不包含明文密码（它可以用 `strings` 找到）。当密码被硬编码时，它会通过将每个字母分配给字符数组的一个元素来隐藏在 strings 的视线之外。当密码在安装期间被选择时，密码字母的按位表示会被存储在二进制文件中。特洛伊木马登录随后在运行时解密魔术密码。其中一些登录特洛伊木马还将用户名密码对存储在文件中以供以后收集。

| 工具 | 描述 |
|------|-------------|
| strobe | Julian Assange 的（又名 Proff）超优化 TCP 端口探测器。官方分发版为 ftp://suburbia.apana.org.au/pub/users/proff/original/strobe.tgz。 |
| iss.sh | Christopher Klaus 的 Internet Security Scanner v1.21。官方分发版为 ftp://ftp.iss.net/pub/iss/iss21.shar。 |
| traceroute.c | Van Jacobson 的著名 traceroute 程序。官方分发版在 ftp://ftp.ee.lbl.gov/ 中。 |
| nuke | 一个用于向指定主机发送 ICMP“主机不可达”数据包的程序。定期发布到 Usenet alt.2600 新闻组。 |
| nfs shell | Leendert van Doom 的（leendert@cs.vu.nl）提供对 NFS 文件系统访问的 shell。 |
| ypx | Rob J. Nauta 的（rob@wzv.win.tue.nl）用于在本地网络之外传输 NIS 映射的程序；发布到 Usenet alt.sources 新闻组。 |
| bootparam | 一个可用于确定默认路由器和有关引导服务器的其他信息的程序（SunOS 专有代码）。 |

The `netstat` Trojan hides network connections. With the network connections (e.g., telnet and ftp) hidden, the intruder is free to pick up the bounty of sniffed passwords or use your site as a springboard from which to attack other sites.

The `ifconfig` Trojan hides the fact that your network interface is in promiscuous mode. There is no config file associated with the `ifconfig` Trojan.

The `ps` Trojan hides running processes belonging to a specified UID, TTY, or program name. Many of the Trojans have an added "showall" option (`-a`) that ignores the contents of the mask file.

## Mask File Formats

### ps Mask File

The following is an example `/dev/ptyp` mask file.

```
0 0      # Strips all output with processes running under root
1 p0     # Strips all output associated with tty typ0
2 sniffer # Strips from output all programs with the name sniffer
```
