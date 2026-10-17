
每个 TCP 数据包都封装在 IP 数据包的数据字段内，该字段紧随 IP 头部之后。以下表示 TCP 头部的布局。请注意，头部的顶部数字每个代表一个字节。

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_35_1.png)

更多细节请参阅 RFC 793：[http://www.faqs.org/rfcs/rfc793.html](http://www.faqs.org/rfcs/rfc793.html)。

### UDP（用户数据报协议）头部

与 TCP 类似，每个 UDP 数据包也封装在 IP 头部的数据字段内。以下表示 UDP 头部的布局。头部的顶部数字每个代表一个字节。

![](img/1b84de2bb5e7ca74dd76d8f9ae35b93d_36_0.png)

更多细节请参阅 RFC 768：http://www.faqs.org/rfcs/rfc768.html。

### 在线资源

除了书中提到的各种在线资源外，本节还提供了指向其他资源的指针，这些资源可用于了解安全领域的最新动态。

> 记得检查 <http://www.hacknotes.com/> 以获取最新的安全资源。

#### 黑客工具

下表列出了当今黑客最常用的黑客工具。本表中提到的大多数工具都在本书第一部分中使用。还提供了可以从其中下载这些工具的 URL。

| 名称 | 描述 | 位置 |
|:---|:---|:---|
| Aircrack | 流行的 WEP 破解器 (802.11b) | <http://airsnort.shmoo.com/> |
| Adore | 后门 | <http://www.team-teso.net/releases.php> |
| Amap | 识别远程应用程序 | <http://www.tcr.org/releases.php> |
| Cheops | 基于 GUI 的工具，用于识别网络上主机的信息 | <http://www.marko.net/cheops/> |
| Desproxy | 通过 Web 代理隧穿 TCP 流量的命令行工具 | <http://desproxy.sourceforge.net/> |
| Dsniff | 网络嗅探工具套件 | <http://monkey.org/~dugsong/dsniff/> |
| Ethereal | 基于 GUI 的网络嗅探器 | <http://www.ethereal.com/> |
| Etercap | 基于 Ncurses 的网络嗅探器 | <http://etercap.sourceforge.net/> |
| Fake-IP | 在 802.11 网络上执行拒绝服务攻击 | <http://www.loud-fat-bloke.co.uk/w80211.html> |
| Firewall | 类似于 traceroute 的工具，用于确定网关访问控制列表 | <http://www.packetfactory.net/projects/firewall/> |
| Fragroute | 拦截、修改和重写网络流量 | <http://www.monkey.org/~dugsong/fragroute/> |
| Hping2 | 命令行 TCP/IP 数据包组装器和分析器 | <http://www.hping.org/> |
| 名称 | 描述 | 位置 |
|:-------|:--------------|:-----------------|
| Hunt | 执行 TCP 劫持 | http://lin.fsld.cvut.cz/-kra/index.html#HUNT |
| Hydra | 主动密码暴力破解器 | http://www.thc.org/releasess.php |
| John | 被动密码破解器 | http://www.openwall.com/john/ |
| Kismet | 识别区域内无线网络的嗅探器 | http://www.kismetwireless.net/download.shtml |
| Knark | Rootkit | http://www.packetstormsecurity.org/ |
| Linux Root Kit (LRK) | Rootkit | http://www.packetstormsecurity.org/ |
| Loki2 | 后门 | http://www.phrack.com/show.php?p=51&a=6 |
| Nemesi s | 命令行网络数据包注入套件 | http://www.packetfactory.net/projects/nemesi s/ |
| Nessus | 漏洞扫描器 | http://www.nessus.org/ |
| Netcat | 在网络间读取和写入数据。支持 TCP 和 UDP 协议。 | http://www.atstake.com/research/tools/network_utilities/ |
| Ngrep | 类似于 grep 命令，但用于分析网络数据包。 | http://www.packetfactory.net/projects/ngrep/ |
| Nikto | Web 服务器和 Web 应用程序漏洞扫描器 | http://www.cirt.net/code/nikto.shtml |
| Nmap | 端口扫描器 | http://www.insecure.org/nmap/ |
| Openssl | 建立 SSL 连接 | http://www.openssl.org/ |
| Snmpwalk | SNMP 查询工具 | http://www.net-snmp.org/ |
| Snort | 网络嗅探器和入侵检测系统 | http://www.snort.org/ |
| Spike Proxy | HTTP 和 HTTPS 代理 | http://www.immunitysec.com/spikeproxy.html |
| Stunnel | SSL 封装器 | http://www.stunnel.org/ |
| Tcpdump | 命令行嗅探器 | http://www.tcpdump.org/ |
| Tormkit | Rootkit | http://www.packetstormsecurity.org/ |

#### 在线资源 RC 17

| 名称 | 描述 | 位置 |
| :--- | :--- | :--- |
| Wget | 命令行 HTTP、HTTPS 和 FTP 客户端 | http://wget.sunsite.dk/ |
| Wlan-Jack | 对 802.11 网络执行拒绝服务攻击 | http://802.11ninja.net/ |
| Xkey | 记录远程 X 会话的按键 | http://packetstormsecurity.org/ |
| Xprobe2 | 使用 ICMP 数据包进行操作系统指纹识别 | http://www.sys-security.com/html/tools/tools.html |
| Xremote | 向远程 X 会话发送鼠标和键盘事件 | http://www.infa.abo.fi/~chakie/xremote/ |
| Xscan | 记录远程 X 会话的按键 | http://packetstormsecurity.org/ |
| Xwatchwin | 监视远程 X 客户端 | http://packetstormsecurity.org/ |
| Vnccrack | 破解和暴力破解 VNC 密码 | http://www.phenoelit.de/vnccrack/ |
| Whisker | Web 服务器和 Web 应用程序漏洞扫描器 | http://www.wiretrip.net/rfp1/doc.asp/i2/d21.htm |
| Zap3 | 日志擦除器 | http://www.packetstormsecurity.org/ |
| Zbedee | 创建安全的 TCP 和 UDP 隧道 | http://www.winton.org.uk/zbedee/ |

#### Web 资源

下表提供了最受欢迎的安全相关 Web 门户的位置。经常访问这些资源是个好主意，以便跟上最新的安全新闻。

| 描述 | 位置 |
| :--- | :--- |
| 新闻、文章、邮件列表、漏洞和漏洞利用数据库 | http://securityfocus.com/ |
| 新闻、工具、公告和漏洞利用 | http://packetstormsecurity.nl/ |
| 工具、文章和链接 | http://insecure.org/ |
| CERT 协调中心：漏洞事件、安全实践、统计数据和培训 | http://www.cert.org/ |
| CVE（通用漏洞披露） | http://www.cve.mitre.org/ |
