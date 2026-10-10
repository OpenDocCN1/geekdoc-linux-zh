
# 第 6 章 - Kali Linux 安装

Kali Linux 可以像任何其他 GNU/Linux 发行版一样安装到硬盘上。它也可以安装并配置为与 Windows 操作系统进行双启动。同样，它可以安装到 USB 驱动器上，或者安装在加密磁盘上。

建议查阅有关 Kali Linux 各种安装选项的详细信息，访问以下页面：[http://docs.kali.org/category/installation](http://docs.kali.org/category/installation)

## 更改 Root 密码

作为一种良好的安全实践，建议更改分配给 root 用户的默认密码。这将使恶意用户难以使用此默认密码访问系统。

```
# passwd root
Enter new UNIX password:
Retype new UNIX password:
```

> [\*] 只要输入密码，它就不会显示，并且必须输入两次。

## 启动网络服务

Kali Linux 的网络服务包括 HTTP、Metasploit、MySQL、OpenVAS 和 SSH。

如果需要启动 HTTP 服务，必须执行以下命令：

```
#/etc/init.d/apache2 start
```

这些服务也可以通过菜单启动和停止：应用程序 -> Kali Linux -> 系统服务。

Kali Linux 提供了关于其多个方面和功能特性的官方文档。这些文档正在不断编写和更新中。可以在以下页面找到这些文档：http://docs.kali.org/

## Kali Linux 工具

Kali Linux 包含大量来自不同来源、与安全及取证领域相关的工具。

所有这些工具的列表及其快速参考指南提供在以下网站：http://tools.kali.org/

## Shell 脚本编写

Shell Bash 允许你自动化操作或执行消耗大量时间的重复性任务。在以下练习中，将使用一个发布代理列表的网站。

使用 bash shell 命令，代理的 IP 地址和端口将被提取到一个文件中。

```
# wget http://www.us-proxy.org/
# grep "<tr> <td>" index.html | cut -d ">" -f 3,5 | cut -d "<" -f 1,2 | sed 's / \\/ td> /: / g'
```

## 捕获信息

此阶段旨在尽可能多地收集关于目标的信息，例如可能的用户名、IP 地址、名称服务器以及其他相关信息。在此阶段中，获取的每一份信息都很重要，不应被低估。请记住，收集更多的信息将为成功的攻击产生更大的概率。

信息捕获过程可以以两种方式划分——主动信息捕获和被动信息捕获。在第一种方式中，通过向目标网络发送流量来收集信息，例如执行 ICMP ping 和 TCP / UDP 端口扫描。在第二种情况下，使用第三方服务或来源（如 Google、Bing 或社交网络）获取目标网络的信息。

## 公共来源

互联网上有各种公共资源可用于收集关于目标的信息。使用此类资源的优势在于不会生成直接指向目标的流量，从而最小化被检测到的概率。

### 捕获文档

- "-dnsserver" 选项定义了使用特定的 DNS 服务器进行主机名查询。
- "-dns" 选项定义了要扫描的域名。
- "-wordlist" 选项定义了用于发现子域名的单词列表。
- "-file" 选项定义了输出文件。

[\*] dnseanum 工具包含一个单词列表“dns.txt”，它可与任何需要它的其他工具一起使用，正如这里所示。

### Dmitry

DMitry 是一个针对 Linux 的在线命令行程序，允许你尽可能多地捕获有关主机的信息，从简单的 Whois 查询到运行时间报告或端口扫描。

```
# dmitry
# dmitry -w -e -n -s [Domain] -o /tmp/resultado_dmitry.txt
```

- "-w" 选项允许对主机的 IP 地址进行 whois 查询。
- "-e" 选项允许搜索所有可能的电子邮件地址。
- "-n" 选项尝试从 Netcraft 获取有关主机的信息。
- "-s" 选项允许搜索可能的子域名。
- "-o" 选项允许定义用于保存结果的文件名。

虽然 dmitry 中有一个选项允许从 Netcraft 获取有关主机域名的信息，但获取这些信息是不可行的。这些信息可以直接从 Netcraft 网站获取：

[http://searchdns.netcraft.com](http://searchdns.netcraft.com)

## 路由信息 Traceroute

http://linux.die.net/man/8/traceroute

Traceroute 跟踪数据包在 IP 网络上到达指定主机所经过的路径。这利用 IP 协议中的 "TTL" 字段，并尝试通过路由中的每个网关从目标主机引发 ICMP TIME_EXCEEDED 响应。

GNU / Linux 系统上的 traceroute 版本默认使用 UDP 数据包。

```
# traceroute --help
# traceroute [IP Address]
```

## Tctraceroute

http://linux.die.net/man/1/tctraceroute

tctraceroute 使用 TCP 数据包跟踪到目标主机的路径。

```
# tctraceroute --help
# tctraceroute [IP Address]
```

使用搜索引擎

## Theharvester

https://code.google.com/p/theharvester/

```
# nping -h
# nping [IP Address]
```

Nping 默认使用 ICMP 协议。如果目标主机正在阻止此协议，可以使用 TCP 测试模式。

```
# nping --tcp [IP Address]
```

"--tcp" 选项是一种允许用户创建和发送任何类型 TCP 数据包的 模式。这些数据包被嵌入在也可以调整的 IP 数据包中发送。

## 识别操作系统

此过程试图确定运行在活动目标上的操作系统，以了解尝试渗透的操作系统类型和版本。

```
nmap
http://nmap.org/
# nmap -O [IP Address]
```

## 服务列表

确定每个特定端口上正在运行的服务，可以确保在目标网络上进行令人满意的渗透测试。你还可以消除在操作系统指纹识别过程中产生的任何疑虑。

```
Nmap
http://nmap.org/
# nmap -sV [IP Address]
```

nmap 的 “-sV” 选项启用了版本检测。在使用 nmap 提供的某些扫描发现 TCP 和 UDP 端口后，版本检测会询问这些端口，以确定更多关于当前运行内容的信息。

数据库包含用于查询各种服务的测试和匹配表达式，以识别和解释响应。Nmap 试图确定服务协议、应用程序名称、版本号、主机名和设备类型。

## 利用目标

在发现了主机或目标网络中的漏洞之后，现在是时候尝试利用它们了。利用阶段有时标志着渗透测试过程的结束，但这取决于合同，因为有些情况下你需要更深入地进入目标网络，目的是在整个网络中扩展攻击并获取所有可能的权限。

## 包含 Exploit 的存储库

每天都会报告各种类型的漏洞，但目前只有其中一小部分被公开或免费发布。

可以从维护存储库的网站下载其中一些 "exploits"。

## Metasploit 框架控制台

http://www.metasploit.com/

Metasploit 控制台 (msfconsole) 主要用于管理 Metasploit 数据库、管理会话，以及配置和执行 Metasploit 模块。其基本目的是利用。该工具允许你连接到目标，以便针对它执行 exploits。

由于 Metasploit 框架使用 PostgreSQL 作为其数据库，首先必须启动它，然后启动 Metasploit 框架控制台。

```
# service postgresql start
```

要验证服务是否正确启动，必须执行以下命令。

```
# netstat -tna | grep 5432
```

要显示 Metasploit 框架帮助。

```
# msfconsole -h
# msfconsole
```

一些用于与控制台交互的有用命令是：

- msf> help
- msf> search [模块名称]
- msf> use [模块名称]
- msf> set [选项名称] [模块名称]
- msf> exploit
- msf> run
- msf> exit

以下示例详细介绍了辅助模块 "SMB 用户枚举 (SAM EnumUsers)" 的使用。

