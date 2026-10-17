
### C.5.6 Pretty Good Privacy (PGP)

Pretty Good Privacy 软件（PGP）可用于保护电子邮件、磁盘文件以及几乎任何其他数据，但不包括 TCP 会话或 UDP 数据包。（TCP 会话可以通过 SSH 相当不错地得到保护。）以下网站为美国公民和在美国的永久居民，以及加拿大的公民提供 PGP 的下载。过去，其他人曾在美国以外地区找到网站，或获得了包含源代码的 Zimmermann 的书（该书目前已绝版）。

请注意，邮寄印刷版的源代码到海外是合法的，但包含相同信息的磁带则不合法。早在 2000 年初，美国政府开始放宽对加密软件的出口管制，因此当你阅读此内容时，这些限制可能已不再适用。

我记得这些出口管制大约在 1981 年首次生效，当时我公司 Onyx 不得不将我们的 UNIX 发行版拆分为两个版本：一个完整的国内版本，以及一个不包含解密库和程序的国际化版本。

请注意，单向加密是被允许的（因为它不能用于“隐藏”信息），所以 UNIX/Linux 密码加密仍然是合法的。

可以从以下站点下载 PGP：

`http://web.mit.edu/network/pgp.html`

### C.5.7 GNU 隐私守卫 (GPG)

GNU 隐私守卫（GPG）是自由软件基金会（Free Software Foundation）对 Philip Zimmermann 的 Pretty Good Privacy 的开源实现。它首次发布于 1999 年底。它不受 PGP 许可和出口限制的影响。任何人都可以合法地从以下地址下载：

`www.gnupg.org/`

### C.5.8 tcpdump 实用工具

美国政府的能源和核研究实验室之一，劳伦斯伯克利实验室（LBL），提供 `tcpdump` Linux/UNIX 实用工具。该工具是一种嗅探器，旨在供系统管理员分析其计算机和网络中的通用网络问题和安全问题。因此，它显示的数据包信息不足以，例如，查看邮件内容（尽管修改这一点很容易）。我发现在开发客户端/服务器软件期间，它对于调试也相当有用。`tcpdump` 程序及相关软件可以从下列 URL 列出的实验室下载。它设置和使用起来很容易。

- `ftp://ftp.ee.lbl.gov/libpcap.tar.Z`
- `ftp://ftp.ee.lbl.gov/pcapture-0.2.1.tar.Z`
- `ftp://ftp.ee.lbl.gov/tcpdump-3.4.tar.Z`

### C.5.9 基于图形界面的 Ethereal 嗅探器

这是一个开源的基于图形界面的嗅探器，除了 `tcpdump` 的“显示每个数据包”理念外，它还允许轻松监视特定会话。它允许观察实际数据，因此在使用其时诚实性很重要。它甚至允许解压缩 gzipped 流。它是作者最喜欢的嗅探器。

它需要 `GTK+` 和 `libpcap`，以及 `Perl`。如果需要解压缩，则还需要 `zlib`。这些可以从以下地址下载：

- `http://ethereal.zing.org/`
- `ftp://ftp.ee.lbl.gov/`
- `www.gtk.org/`

### C.5.10 sniffit 实用工具

此实用工具比 `tcpdump` 更复杂，并且不仅显示报头，还显示数据包的内容。虽然这可以用于不道德的目的，但黑客反正会那样做。

`http://sniffit.rug.ac.be/~coder/sniffit/sniffit.html`

### C.5.11 下载 Tripwire 实用工具

`Tripwire` 是一个强大但难以使用的工具，它计算系统上你感兴趣的每个文件（例如 `/etc` 中的系统配置文件、`/bin` 和 `/usr/bin` 中的系统程序以及用户账户）的难以伪造的校验和。它允许你在任何时候查看任何文件是否已被修改。

目前可以在以下站点获取 `Tripwire` 的免费版本。也有付费提供的增强版程序。

`www.tripwire.com/downloads/`

你还可以查看相关的开源开发站点。

`http://tripwire.org/`

### C.5.12 下载 Tripwire 的替代工具

这些 `Tripwire` 的替代工具可能更简单、更易于使用，同时提供至少相同级别的安全性。

`samhain` 文件系统完整性检查器可以从以下地址下载：

`www.la-samna.de/samhain/index.html`

`AIDE` 可以从以下地址下载：

`ftp://ftp.linux.hr/pub/aide/`

当前的 `AIDE` 版本是

`aide-0.7.tar.gz`

`AIDE` 手册可以从以下地址下载：

`www.cs.tut.fi/~rammer/aide/manual.html`

`Gog&Magog` 可以从以下地址下载：

`www.multimania.com/cparisel/gog/`

以及 `Sentinel`，它有一个不错的可选图形界面前端，可以从以下地址下载：

`http://zurk.netpedia.net/zfile.html`

`SuSEauditdisk` 从可引导磁盘运行，提供非常安全的完整性检查。它是 SuSE 的标准配置，并且可以轻松地移植到其他发行版。从以下地址下载：

`www.suse.de/~marc/`

### C.5.13 下载 Nessus 安全审计器

`Nessus` 是一个强大的工具，用于扫描（探测）网络中的开放端口，更重要的是，用于检测这些服务中的漏洞。

`www.nessus.org/`

### C.5.14 下载 SARA 安全审计器

`SARA` 安全审计器是一个基于 `SATAN` 源码的新工具，但将继续及时增强并持续更新，以应对新发现的利用方法，有时甚至在这些利用方法成为常识之前。这是一个优秀的工具，建议试一试。

`www-arc.com/sara/`

此外，他们提供一个邮件列表，你可以按如下方式订阅：

```bash
echo subscribe sara-l | Mail -s subscribe list@mail-arc.com
```

### C.5.15 下载 nmap

`nmap` 工具允许映射网络上系统的开放端口。可以从以下地址下载：

`www.insecure.org/nmap/`

### C.5.16 下载 Snort 攻击检测器

`Snort` 设计用于深度嗅探网络，寻找已知攻击的模式并警告你。它拥有包含 500 多个攻击签名的庞大数据库，并且该数据库保持最新状态。当你遭受攻击时，这是一个发出第一警报的绝佳工具。

`www.snort.org/`

### C.5.17 下载 SHADOW

`SHADOW` 是一个复杂的工具，用于分析入侵尝试和成功入侵，并识别大量正常流量中许多入侵尝试的模式，该工具由美国海军海上系统司令部（Naval Surface Warfare Center）提供。

它以近实时方式运行，生成警报并捕获数据包以进行进一步分析和作为后续法律行动的证据。它可以检测通过 TCP“半开”、发送 UDP 回复等进行的隐身扫描。这是一款优秀的免费产品，甚至可以处理非常大的站点。

`www.nswc.navy.mil/ISSEC/CID/`

### C.5.18 下载 SAINT 安全审计器

`SAINT` 是一个扫描系统安全漏洞的程序。它现在能够识别各种 DDoS 程序的僵尸程序，如 `Trin00`、`TFN`、`Stacheldraht`、`Shaft` 和 `mstream`，以及各种 `Sendmail` 和 `WU-FTPD` 弱点。它源自 `SATAN`。

`www.wwdsi.com/saint/`

### C.5.19 下载 IP Chains 配置工具

`PMFirewall` 是 Linux 的 `IP Chains` 防火墙和 Masquerading 配置程序。它旨在允许新手在很少或没有 `IP Chains` 经验的情况下构建自定义防火墙。它在 Tucows 上获得了四只企鹅的评级。它了解工作站、服务器、防火墙和路由器的常见 `IP Chains` 配置。它可以处理多个以太网卡、电缆调制解调器、拨号连接和 Masquerading。它会为每个接口自动确定地址和子网掩码。它几乎可以在所有 Linux 发行版上工作。

`www.pointman.org/PMFirewall/`

### C.5.20 下载 SSL

`SSL` 是 Secure Socket Layer（安全套接字层）的缩写。它是提供加密和身份验证的代码及协议，正是它让 `https`、`pop3s` 和 `imaps` 中的“s”得以成立。它能非常有效地防止网络嗅探和欺骗。即使是互联网银行和商务等高安全性应用程序也依赖于它。据我所知，它从未被攻破。

> 值得注意的是，`SSL` 仅解决网络嗅探和身份验证问题，且前提是使用正确。一些网站并未对所有通过互联网传输的敏感信息使用 `SSL`。尽管 `SSL` 是由 Netscape Communications 发明的，但其浏览器的某些版本曾错误地使用 `SSL`，从而使用户容易受到不良网站的侵害。相关内容在 107 页的“升级 Netscape”中有详细讨论。
