
www.mindspring.com/~cavu/rwls/

为了防止本书读者以外的人下载文件，FTP 访问可能需要提供账户和密码。如果需要，账户和密码将是：

- `penguin`
  `WorldDom`

真正偏执的人会从两个站点下载他们想要的对象并进行对比，其理论是两个站点同时被创建的概率较低，并且肯定会验证 GPG 签名。可以通过以下方式联系作者（此处未提供具体邮箱，保留原文逻辑）：

# 附录 A • 最新入侵与防御的互联网资源

该程序需要 `GTK+`、`libpcap` 以及 `Perl`。如果需要解压缩，则需要 `zlib`。这些可以从以下地址下载：

```
http://ethereal.zing.org/
ftp://ftp.ee..lbl.gov/
www.gtk.org/
```

## A.5.10 sniffit 工具

此工具比 `tcpdump` 更复杂，它还可以显示数据包的内容而不仅仅是头部。尽管它可以被用于不道德的目的，但黑客反正会这样做。

```
http://sniffit.rug.ac.be/~coder/sniffit/sniffit.html
```

## A.5.11 下载 Tripwire 工具

`Tripwire` 是一个强大但难以使用的工具，它可以对你系统中你感兴趣的每个文件计算一个硬伪校验和，例如 `/etc` 中的系统配置文件、`/bin` 和 `/usr/bin` 中的系统程序以及用户账户。它允许你随时查看任何一个文件是否被修改过。

目前可以在以下站点获取 `Tripwire` 的免费版本。此外，该程序还提供价格昂贵的的增强版本。

```
www://tripwire.com/downloads/
```

你可能还想查看开源开发的相关站点。

```
http://tripwire.org/
```

## A.5.12 下载 Tripwire 的替代品

这些 `Tripwire` 的替代品可能更容易、更愉快的使用，同时提供至少相同的安全水平。

`samhain` 文件系统完整性检查可以从以下地址下载：

```
www.la-samna.de/samhain/index.html
```

`AIDE` 可以从以下地址下载：

```
ftp://ftp.linux.hr/pub/aide/
```

`AIDE` 的当前版本是

```
aide-0.7.tar.gz
```

## A.5 安全工具 URL

`AIDE` 手册可以从以下地址下载：

```
www.cs.tut.fiti/~ramrammer/aide/manual.html
```

`Gog&Magog` 可以从以下地址下载：

```
www.multimania.com/cparisel/gog/
```

以及具有良好的可选 GUI 前端的 `Sentinel`，可以从以下地址下载：

```
http://zurk.netpedia.net/zfile.html
```

`SuAuditisk` 从可引导磁盘运行，以提供非常安全的完整性检查。它是 `SuSE` 的标准配置，并可以轻松移植到其他发行版。可以从以下地址下载：

```
www.suse.de/~marc/
```

## A.5.13 下载 Nessus 安全审计器

`Nessus` 是一个强大的工具，用于扫描（探测）你的网络中的开放端口，更重要的是扫描这些服务中的漏洞。它在第 591 页的“`Nessus` 安全扫描器”中进行了简要讨论。

```
www.nessus.org/
```

## A.5.14 下载 SARA 安全审计器

`SARA` 安全审计器是一个基于 `SATAN` 源代码的新工具，但随着新漏洞的发现，它将继续及时地进行增强并持续更新，有时在这些漏洞成为常识之前就会更新。这是一个非常优秀的工具，建议你尝试一下。

```
www-arc.com/sara/
```

此外，他们提供了一个邮件列表，你可以按以下方式订阅：

```
echo subscribe sara-l | Mail -s subscribe list@mail-arc.com
```

## A.5.15 下载 nmap

`nmap` 工具允许映射你网络中系统的开放端口。它在第 592 页的“`nmap` 网络映射器”中被讨论。它可以从以下地址下载：

```
www.insecure.org/nmap/
```

## A.5.16 下载 Snort 攻击检测器

`Snort` 设计用于深度嗅探你的网络，寻找已知攻击的模式并警告你。它拥有包含超过 500 种攻击特征的巨大数据库，并且该数据库保持更新。这是在你遭受攻击时发出第一个警报的优秀工具。它在第 598 页的“`Snort` 攻击检测器”中被讨论，并可以从以下地址下载：

www.snort.org/

## A.5.17 下载 SHADOW

`SHADOW` 是一个复杂的工具，用于分析入侵尝试和成功，并从海量的正常流量中识别大量入侵尝试的模式，由美国海军水面作战战中心提供。

它实时运行，生成警报并捕获数据包以便进一步分析以及作为后续法律行动的证据。它可以检测通过 TCP “半开连接”、发送 UDP 回复等的隐蔽扫描。这是一个可以处理非常大型站点的优秀免费产品。它在第 599 页的“使用 `SHADOW` 进行扫描和分析”中被讨论。

www.nswc.navy.mil/ISSEC/CID/

## A.5.18 下载 SAINT 安全审计器

`SAINT` 是一个扫描系统安全漏洞的程序。它现在可以识别各种 DDoS 程序的僵尸程序（如 `Trin00`、`TFN`、`Stacheldraht`、`Shaft` 和 `mstream`），以及各种 `Sendai` 和 `WU-FTPD` 的缺陷。它源自 `SATAN`。

www.wwdsi.com/saint/

## A.5.19 下载 IP Chains 配置工具

`PMFirewall` 是一个用于 Linux 的 `IP Chains` 防火墙和伪装（Masquerading）配置程序。它旨在让新手在几乎或完全没有 `IP Chains` 经验的情况下构建自定义防火墙。

## A.5.20 下载 SSL

`SSL` 是 `Secure Socket Layer`（安全套接层）的缩写。它是一种提供网络安全通信的加密协议。许多应用程序它来防止数据被拦截或篡改。

## A.5.21 下载 sslwrap

`sslwrap` 程序允许将任何 TCP 服务封装在 `SSL` 中。对于不支持原生 `SSL` 的服务，特别推荐。

## A.5.22 下载 SSH 封装的 CVS

`CVS` 是一个用于软件开发的非常有用的工具，自诞生以来一直是 Linux 的一部分。遗憾的是，它本身是不安全的。通过少量的努力，它可以被 `SSH` 封装。

## A.5.23 下载加密磁盘驱动程序

堆叠在磁盘驱动之上的加密设备驱动 `PDD`（实用隐私磁盘驱动）可以从以下地址下载：

```
http://linux01.gwdg/~alatham/ppdd.html
```

## A.5.24 无 root Sendmail

此页面解释了如何设置 `sendmail` 不以 `root` 身份运行，并通过 `inetd` 调用以允许使用 `TCP Wrapper` 并防御反向 DNS 欺骗。

```
www.coker.com.au/~russell/sendmail.html
```

## A.5.25 下载 postfix

`postfix` 程序是 `sendmail` 的替代品，一些安全专家认为由于使用了“安全环”，它要安全得多。它的优势在第 174 页的“`Sendmail`”中被讨论。

```
www.postfix.org/
```

## A.5.26 Libsafe

这种创新的库可以了某些导致缓冲区溢出的常见 C 语言错误。这些漏洞是 Linux 攻击的最常见的入口点之一，仅凭良好的系统管理实践无法完全克服。该库通过拦截这些代码调用的常用字符串处理库程序来缓解该问题。

其创新之处在于 `Libsafe` 不需要你重新编译甚至重新链接所有代码。相反，它作为动态库运行，只需要“丢进去”即可。由于所有的程序都是动态链接的，它们都能从这种保护中受益。它由贝尔实验室创建。它在光盘上，也可以从以下地址下载：

```
www.research.availabs.com/project/libsafe/
```

## A.6 文档链接

## A.5.27 已发现的攻击

该网站发布了针对各种端口发起的各种攻击；换句话说，在这些端口上发现了木马程序。通过理解这些内容，你可以获得关于你的某些系统可能发生了哪些入侵的宝贵线索。

```
www.robertgraham.com/pubs/firewall-seen.html
```

## A.5.28 使用 Sam Spade 分析你的攻击者

这个有趣的网站提供了许多分析其他网站的工具。它可以告诉你某个 IP 地址属于哪个域名，安全地分析 Web 页面（尽管 `tcpread` 也能做到这一点），允许在不暴露你的 IP 地址的情况下查看网站，并可以检查你的邮件服务器是否允许了访问。遗憾的是，这个网站也可以被用于作恶，但黑客们终会发现它的。我认为它对白帽客的价值值得列出。

```
www.samspade.org/
```

## A.6 文档链接

这些链接包含了有用且编写良好的文档。其中部分内容已翻译成英语以外的语言。
