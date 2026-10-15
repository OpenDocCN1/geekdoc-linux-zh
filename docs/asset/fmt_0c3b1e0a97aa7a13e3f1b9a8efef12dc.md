
`Changes` `Time-modules` `new-annotation-base.xml` `utilities`

```
root@unixhost> ./snortsnarf.pl /var/log/snort/alert
```

```
root@unixhost> ls

.  README  Usage  nmap2html

..  README.SISR  cgi  sisr

COPYING  README.nmap2html  include

Changes  Time-modules  new-annotation-base.xml  snortsnarf.pl
```

```
root@unixhost> ls snfout.alert/

.  ..  192  212  SDlogo.gif  index.html  sig  topdests.html  topsrcs.html
```

目录 `snfout.alert` 包含由脚本生成的网站。这组 HTML 页面可以用任何 Web 浏览器打开。如果你点击 Summary，就会看到有关警报的所有详细信息（见图 7.2）。

甚至可以点击 IP 地址来快速查看系统详情以及执行名称解析的链接（见图 7.3）。

还有许多脚本可以帮助你分析日志文件。你只需在 `http://www.snort.org/dl/contrib/data_analysis/` 选择你的武器即可。

大多数 IDS 系统的工作方式与此处所示类似。甚至还有一些系统应该能够根据所提供的信息进行“学习”。这意味着这些系统能够适应你网络中的网络流量。此类系统始终应由像 `Snort` 这样的纯基于规则的系统控制。然后你应比较两个系统的结果，以了解两种方法的优缺点。

# SCAN nmap XMAS 1 个源 1 个目标

优先级：2 分类：尝试信息泄露

`[sid:1228]` `[arachNIDS:30]`

## 触发此攻击签名的源

| Source | # Alerts (sig) | # Alerts (total) | # Dsts (sig) | # Dsts (total) |
| 192.168.0.3 | 60 | 62 | 1 | 1 |

## 接收此攻击签名的目标

| Destinations | # Alerts (sig) | # Alerts (total) | # Srcs (sig) | # Srcs (total) |
| 192.168.0.5 | 60 | 62 | 1 | 1 |

## 图 7.2 报警详情。

`192.168.0.3` 作为源存在 3 种不同的签名

- 1 次 ICMP PING 实例
- 1 次 ICMP PING NMAP 实例
- 60 次 SCAN nmap XMAS 实例

此页面类型警报中存在 1 个不同的目标 IP。

| WhoIs 查询于： | ARIN | RIPE | APNIC | Geektools |
| 192.168.0.3 DNS 查询于： | Amenesi | TRIUMF | Princeton |
| 更多查询信息 | ... | ... |

```
[**] [1:469:3] ICMP PING NMAP [**]

[Classification: Attempted Information Leak] [Priority: 2]

09/16-16:51:05.190140 192.168.0.3 -> 192.168.0.5

ICMP TTL:47 TOS:0x00 ID:30504 IpLen:20 DgmLen:28

Type:8 Code:0 ID:6158 Seq:1 MDM

[xref => http://www.whitehats.com/info/ids162]
```

```
[**] [1:384:5] ICMP PING [**]

[Classification: Misc activity] [Priority: 3]
```

## 图 7.3 IP 地址的详细信息。

### 7.4.7 防火墙

在最常见的理解中，防火墙是一段运行在专用硬件上的软件，通过控制和限制对网络的访问来保护你的网络免受外部世界的威胁。这句话引出了许多问题。例如，如果守护网络的防火墙失效了，那么 sed quis custodiet ipsos custodes（谁来守护守护者）？

仅为网络设置一个防火墙，而让其他一切都未受保护，是不够的。除了在需要时创建防火墙层之外，在单台机器上部署保护似乎是答案。它不会是“包治百病”的秘密成分，但能使你的系统在内部和外部威胁面前更加坚固。突破防火墙并不是进入网络的唯一途径；大多数公司会为其员工，或至少是其中一些员工提供笔记本电脑。备份它们，更不用说保护它们，都可能相当复杂。针对该操作系统的病毒无法伤害 *NIX 系统，但特洛伊木马或间谍软件的最新版本会对网络内所有未加密的流量构成安全风险。

可以在笔记本电脑进入安全网络之前对其进行测试，但这耗时且容易出错。确保所有补丁都已部署需要持续关注。* NIX 为基础的笔记本电脑数量不断增长，这在一定程度上缓解了问题，但它们也需要打补丁。如果你的网络中受所有其他系统信任的一台服务器被攻破，问题会变得更糟。最后一道防线始终应该是保护系统本身的防火墙，其配置仅允许以受控方式到达该机器的预期流量。

#### 7.4.7.1 在每台系统上使用防火墙

在网络中的每台系统上使用防火墙是有原因的。例如，使用 `nmap` 扫描一台刚安装的 GNU/Linux 系统，显示的结果与清单 7.38 所示类似。

### 清单 7.38 新安装系统的 nmap 扫描

```
root@unixhost:~> nmap 192.168.0.2

Starting nmap V. 3.00 ( www.insecure.org/nmap/ )

Interesting ports on linuxhost (192.168.0.2):

(The 1596 ports scanned but not shown below are in state: closed)

Port     State    Service

22/tcp   open     ssh

111/tcp  open     sunrpc

631/tcp  open  ipp

6000/tcp open  X11

10000/tcp open  snet-sensor-mgmt

Nmap run completed -- 1 IP address (1 host up) scanned in 1 second
```

清单 7.38 中的系统是手工加固的，但仍有一些端口是开放的。现在只需简单启动提供的防火墙，情况看起来就不同了，而系统管理员的工作量并不大（参见清单 7.39）。

### 清单 7.39 运行防火墙的同一系统的 nmap 扫描

```
root@unixhost:~> nmap 192.168.0.2

Starting nmap V. 3.00 ( www.insecure.org/nmap/ )

Interesting ports on linuxhost (192.168.0.2):

(The 1596 ports scanned but not shown below are in state: filtered)

Port     State    Service

22/tcp   open     ssh

113/tcp  closed   auth

Nmap run completed -- 1 IP address (1 host up) scanned in 160 seconds
```

清单 7.39 中的输出应该在系统无人看管时让你安心一些，而实现这一状态的工作量只是几次鼠标点击。

如今大多数 *NIX 发行版都自带防火墙，为什么不使用它呢？SuSE Linux 和 Apple 的 OS X 中的防火墙可以用或多或少友好的 GUI 配置。Solaris 提供的防火墙可以通过 GUI 或命令行配置。命令行方法有一些缺点，但允许更精确地保护系统。例如，你无法使用 SuSE GUI 将 ssh 连接限制在某些网络范围内。

已安装系统和准备投入生产的系统之间的区别在第 5.2 节“如何使系统准备好投入生产”中进行了讨论。这种系统之间的差异比大多数人意识到的要大得多。参见清单 7.40，了解对一台刚安装的 Solaris 系统进行 nmap 运行的输出。

### 清单 7.40 Solaris 系统的 nmap 扫描

```
root@unixhost:~> nmap 192.168.0.5

Starting nmap V. 3.00 ( www.insecure.org/nmap/ )

Interesting ports on unixhost (192.168.0.5):
```
