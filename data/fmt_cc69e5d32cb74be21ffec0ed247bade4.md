
## tar 命令
`tar cjf file.tar.bz2` 使用 BZip2 压缩创建一个名为 `file.tar.bz2` 的归包
`tar xjf file.tar.bz2` 使用 BZip2 从 `file.tar.bz2` 中提取内容

## gzip 命令
`gzip file` 压缩给定文件
`gzip -d file` 解压缩给定文件

## 打印命令
`lpq` 显示队列中的当前作业
`lprm` 移除队列中的作业

## 网络命令
`ifconfig` 显示所有设备的 IP 地址
`iwconfig` 设置无线参数
`iwlist` 显示无线附加信息
`ping host` 探测主机并显示结果
`whos domain` 打印 WHOIS 信息
`dig domain` 打印 DNS 信息
`dig -x file` 获取反查
`wget file` 下载文件
`wget -c` 继续下载

## SSH 命令
`ssh user@host` 连接到特定主机
`ssh -p port user@host` 连接到特定端口的主
`ssh-copy-id user@host` 将密钥复制到主机以实现免密登录

## 用户管理命令
`adduser accountname` 创建一个新用户 `accountname`
`passwd accountname` 为用户 `accountname` 设置密码
`su` 从当前会话登录超级用户
`exit` 退出超级用户返回普通用户

## 进程管理命令
`ps` 显示所有活动进程
`top` 显示所有运行进程
`kill pid` 根据 ID 杀死进程
`killall proc` 杀死所有名为 `proc` 的进程
`bg` 列出所有停止的作业或后台作业。可恢复后台作业
`fg` 将最近的后台作业调至前台
`fg n` 将名为 `n` 的作业调至前台

## 源码安装命令
`./configure`
`make`
`make install`
`dpkg -i pkg.deb` 安装 DEB 包（Ubuntu/Debian/Linux Mint）
`rpm -Uvhh pkg.rpm` 安装 RPM 包（Fedora/Redhat）

## 停止和启动命令
`shutdown -h now` 现在关闭但不重启
`halt` 停止所有进程
`shutdown -r 5` 5 分钟后关闭并重启
`shutdown -r now` 立即关闭并重启
`reboot` 停止所有进程并重启系统
`startx` 启动 X 系统

## 10. 密码攻击工具
我们将逐一介绍 Kali Linux 中适用于所有类别的工具，并理解每个工具的作用以及它们将如何为安全领域提供帮助。

## 漏洞利用工具
在计算机网络（通常通过互联网）中，存在许多 Web 应用程序，这些应用程序使得系统容易受到恶意代码或服务器上公开访问的开放端口的影响。漏洞利用工具可以帮助你针对系统并利用该系统中的漏洞，从而帮助你修复漏洞。让我们逐一查看 Kali Linux 中提供的所有漏洞利用工具。

### Armitage
Armitage 由 Raphael Mudge 开发，作为 Metasploit 框架的 GUI 前端使用。Armitage 是一款推荐漏洞利用的工具，作为一种图形化形式提供的网络攻击管理工具，它非常简单简单。它是一个开源且免费的安全工具，主要以其在共享会话中提供的数据以及通过单个 Metasploit 实例提供的通信而闻名。Armitage 帮助用户启动漏洞利用和扫描，获取漏洞利用建议，并探索 Metasploit 框架中提供的高级功能。

### 后门工厂 (BDF)
Backdoor Factory 是研究人员和安全专业人员常用的工具。该工具允许用户将其所需的代码包含在系统或应用程序的可执行二进制文件中，如果没有添加额外的代码，则二进制文件将以正常状态继续执行。
你可以使用终端上的以下命令在你的 Kali Linux 系统上安装此工具。
```
apt-get update
apt-get install backdoor-factory
```

### 浏览器漏洞利用框架 (BeEF)
Browser Exploitation Framework 是一种用于在 Web 浏览器上测试漏洞的渗透测试工具。观察发现，Web 浏览器已成为客户端漏洞攻击的目标。BeEF 帮助用户分析客户端的这些攻击向量。与其他工具不同，BeEF 专注于评估作为“敞门”的 Web 浏览器，并跨越了网络层和客户端系统。

### Commix
Commix（Command Injection exploit 的缩写）为渗透测试人员、Web 开发人员和研究人员提供用例，它在简单环境中测试 Web 应用程序。它基本上允许用户发现 Web 应用程序中与命令注入相关的错误、缺陷或漏洞。该工具可以让你轻松识别并利用命令注入漏洞。Commix 工具是使用 Python 语言开发的。

### Crackle
Kali Linux 中的 Crackle 工具是一种暴力破解实用程序，用于破解和拦截蓝牙设备之间的流量。大多数蓝牙设备具有 4-6 位的配对代码，这些是加密格式。使用 Crackle，如果两个设备之间的配对过程被拦截，这些代码就可以被解密，从而允许你监听两个设备之间发生的所有通信。

### jboss-autopwn
JBoss Autopwn 是一种用于 JBoss 应用程序的渗透测试工具。Github 上的 JBoss Autopwn 版本已经过时，最后更新是2011年。这是一个历史工具，现在不再经常使用。

### Linux Exploit Suggester
Linux Exploit Suggester 工具提供了一个脚本，跟踪漏洞并显示所有可能的利用，帮助用户在渗透测试期间获取 root 权限。
该脚本使用 `uname -r` 命令来查找 Linux 操作系统的内核版本。此外，它还会提供 `-k` 参数，用户可以通过它手动输入 Linux 操作系统的内核版本。

### Maltego Teeth
Maltego 是一种用于数据挖掘的交互式工具。它提供了一个交互式界面并输出图表，有助于链路分析。由于它允许链路分析，Maltego 用于互联网调查，以寻找分散在互联网各个 Web 页面上的信息之间的关系。Maltego Teeth 是后期开发的，增加了一个功能，使渗透测试人员能够使用图形界面进行密码破解、SQL 注入和漏洞检测。

### sqlmap
`sqlmap` 是一个开源的 Kali 工具，用于渗透测试。它允许自动检测 SQL 注入漏洞并利用该漏洞来接管数据库服务器。它带有一个非常强大的检测引擎、一系列可以帮助高级渗透测试人员的工具，以及帮助获取信息（如数据库指纹、从数据库检索数据、访问操作系统文件系统以及在操作系统上执行命令）的。

### Yersinia
Yersinia 是一种检测网络协议漏洞并利用其漏洞的工具。它是一个用于测试和分析网络及系统部署的坚实框架。它包含了二层攻击，利用了给定网络中各种二层协议的弱点，从而允许渗透测试人员检测二层网络中的缺陷。Yersinia 在渗透测试期间用于对诸如 DHCP 服务器、交换机等使用生成树协议（STP）的网络设备发起攻击。

### Cisco-global-exploiter
Cisco Global Exploiter (CGE) 工具是一种安全测试利用引擎/工具，简单、快速且先进。Cisco 交换机和路由器有 14 个可以使用 Cisco Global Exploiter 工具利用的漏洞。Cisco Global Exploiter 基本上是一个 perl 脚本，通过命令行驱动，并带有一个简单易用的前端。

### Cisco-torch
Cisco Torch 是一种漏洞利用工具，它与普通扫描器的不同之处在于，它可以在特定时间启动多次并行扫描，从而使任务完成更快、更高效。除了网络层，它还帮助识别 OSI 模型应用层中的系统指纹。这是即使是像 NMAP 这样的工具也无法做到的。

## 取证工具
我们现在列出并学习 Kali Linux 中用于取证领域的工具。

### Binwalk
Binwalk 工具在处理二进制镜像文件时非常有用。它允许你扫描镜像文件中的可能嵌入的可执行代码。对于了解操作的用户来说，这是一个非常强大且实用的工具，因为它可以检测隐藏在固件或镜像文件中的目标信息。
Binwalk 工具使用 python 开发，并利用 python 的 `libmagic` 库，因此是为 Unix 文件系统创建魔数签名的合适工具。为了让调查领域的测试人员使用更舒适，它包含了全球范围内常见的签名数据库。这使其成为检测异常的便利工具。

### Bulk-extractor
Bulk-extractor 工具是一个有趣的工具，用于调查人员从数字文件中提取特定数据。该工具帮助检索 URL、电子邮件地址、信用卡/借记卡号等。该工具可以扫描文件、目录甚至磁盘镜像。最棒的是，即使数据部分损坏或处于压缩格式，该工具仍然能深入寻找数据。
该工具的另一个有趣功能是，如果存在反复的数据（例如电子邮件地址、URL），你可以为它们创建搜索模式，并以直方图的形式显示。它还会为给定的数据集创建一个发现的单词列表，这些单词可能用于破解加密文件的密码。
