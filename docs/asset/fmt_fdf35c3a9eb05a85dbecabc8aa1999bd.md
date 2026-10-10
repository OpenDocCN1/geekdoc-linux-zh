
```text
# File:/etc/sysctl.conf
#-----------------------------
#Disable routing triangulation. Respond to queries out the same interface, not another. Helps to maintain state
#Also protects against IP spoofing
#-----------------------------
net/ipv4/conf/all/rp_filter=1
#
#Enable logging of packets with malformed IP addresses
#-----------------------------
net/ipv4/conf/all/log_martians=1
#
# Disable redirects
#-----------------------------
net/ipv4/conf/all/send_redirects=0
# Disable source routed packets
#-----------------------------
net/ipv4/conf/all/accept_source_route=0
#
# Disable acceptance of ICMP redirects
#-----------------------------
net/ipv4/conf/all/accept_redirects=0
#
# Turn on protection from Denial of Service (DOS) attacks
#-----------------------------
net/ipv4/tcp_syncookies=0
#
# Disable responding to ping broadcasts
#-----------------------------
net/ipv4/icmp_echo_ignore_broadcasts=0
#
# Enable IP routing. Required if your firewall is protecting a network
#NAT included
#-----------------------------
net/ipv4/ip_forward=0
```

# 工具：SARA（安全审计员研究助手）

安全审计员研究助手（`SARA`）是一款第三代安全分析工具。它受类 GNU GPL 的开源许可协议保护。它基于 `SATAN`（安全管理员网络分析工具）模型构建。它通过网络开发人员的协作进行更新，以应对最新的威胁。

以下是 `SARA` 的部分功能：

- 运行于 UNIX、Linux、MAC OS X 和 Windows 系统
- 支持 FBI/SANS 前 20 大共识
- 能够适应多种防火墙环境
- 支持远程自扫描和 API 功能
- 拥有企业搜索模块
- 支持独立或守护进程模式运行

![](img/0c79e6db97822eb68322dfe40d8564fe_41_0.png)

- 经过 SANS/SIOTS 认证
- 提供用户扩展支持
- 提供用于第三方应用程序的插件功能
- 提供用于 SMB 安全分析的 SAMBA 透明接口

# 工具：Netcat

`Netcat`（图 1-11）是一种网络实用工具，它可以利用 TCP/IP 或 UDP 在网络连接上读取和写入数据。它旨在成为一种可靠的后台工具，可直接使用，也可以轻松由其他程序和脚本驱动。它是一个功能丰富的网络调试和探索工具；因此，它可以创建用户所需的任何类型的连接。它具有多种内置功能。

它提供了对以下重要特性的访问权限：

- 到任意端口的入站和出站连接，支持 TCP 或 UDP
- 内置端口扫描功能，带有随机化器
- 隧道模式，允许某些不同的隧道类型，如 TCP 或 UDP，可以识别所有网络参数
- 某些高级用法，如缓冲发送模式以及对传输和接收数据的十六进制转储

# 工具：Tcpdump

`Tcpdump` 是一种用于网络监控和数据采集的网络流量分析器，允许管理员转储网络上的流量。顾名思义，它将 TCP 流量“转储”到屏幕或文件中以备后续使用。`Tcpdump` 从默认网络接口读取流量，并将完整输出转储到控制台。它使用命令将 TCP 流量的行为更改为更易管理的形式。

`Tcpdump` 打印与网络接口上的布尔表达式匹配的数据包头。它可以配合 `-w` 标志运行，使其将数据包数据保存到文件中以备后续使用。或者，它可以配合 `-b` 标志运行，使其从保存的数据包文件而不是从网络读取数据。

`Tcpdump` 充当 `Snort` 和 `Shadow` 等其他网络分析工具的后台程序。它可以作为追踪网络问题、检测 ping 攻击或监控网络活动的工具。

图 1-12 展示了 `Tcpdump` 的工作原理。图 1-13 和图 1-14 展示了来自 `Tcpdump` 的屏幕截图。

![](img/0c79e6db97822eb68322dfe40d8564fe_42_0.png)

版权所有 © EC-Council

保留所有权利。严禁复制

**图 1-12**

`Tcpdump` 创建包含网络流量信息的文件。

![](img/0c79e6db97822eb68322dfe40d8564fe_42_1.png)

**图 1-13**

此图展示了 `Tcpdump` 在命令行上运行的情形。

# 工具：Snort

`Snort` 是一个开源网络入侵防御和检测系统，它利用一种规则驱动的语言，结合了以下优势：

- 基于特征的检测
- 基于协议的检测
- 基于异常的检测

![](img/0c79e6db97822eb68322dfe40d8564fe_43_0.png)

**图 1-14**

`Tcpdump` 获取网络流量并记录日志。

以下是 `Snort` 的部分功能：

- `Snort` 是一个嗅探器，这意味着它捕获网络流量以供进一步使用。
  - 它促进了 IP 网络上的流量分析和数据包记录。
  - `Snort` 可以检测各种攻击和探测，例如：
    - 蠕虫
    - 漏洞利用尝试
    - 端口扫描
    - 缓冲区溢出
    - CGI 攻击
    - SMB 探测
  - 它具有实时警报功能，通过 `syslog` 发送警报机制。

图 1-15 和图 1-16 展示了来自 `Snort` 的屏幕截图。

# 工具：SAINT

`SAINT` 是一款漏洞评估工具。`SAINT` 能够执行以下操作：

- 在入侵者利用之前，检测和修复网络安全性中可能存在弱点的区域
- 防止常见的系统漏洞
- 解释符合当前政府法规的情况，如 FISMA、Sarbanes-Oxley、GLBA、HIPAA 和 COPPA

以下步骤展示了 `SAINT` 漏洞扫描器的工作原理：

- 步骤 1：`SAINT` 扫描网络上的每个实时系统以获取 TCP 和 UDP 服务。
- 步骤 2：对于发现的每个正在运行的服务，它启动一组旨在检测任何可能导致攻击者获得未授权访问、创建拒绝服务或获取关于网络的敏感信息的探测。

![](img/0c79e6db97822eb68322dfe40d8564fe_44_0.png)

**图 1-15**

这些是 `Snort` 的命令行选项。

![](img/0c79e6db97822eb68322dfe40d8564fe_44_1.png)

**图 1-16**

`Snort` 捕获网络流量以供分析。

![](img/0c79e6db97822eb68322dfe40d8564fe_45_0.png)

**图 1-17**

`SAINT` 是一个扫描引擎，旨在保护实时系统，例如 Web 服务器。

- 步骤 3：扫描器检查漏洞。
- 步骤 4：当检测到漏洞时，结果会被分类，允许客户针对他们认为最有用的数据进行定位。`SAINT` 可以根据严重程度、类型或数量对漏洞进行分组。它还可以提供关于特定主机或一组主机的信息。`SAINT` 描述其定位的每个漏洞；参考常见漏洞与暴露（CVE）、CERT 公告和 IAVA（信息安全漏洞警报）；并描述纠正漏洞的方法。在许多情况下，`SAINT` 扫描器提供链接，指向将消除已检测漏洞的补丁或新软件版本。

图 1-17 描述了 `SAINT` 的工作原理。图 1-18 展示了来自 `SAINT` 的屏幕截图。

# 工具：Wireshark

`Wireshark` 用于故障排除、分析、软件和协议开发以及教育。`Wireshark` 是在 GNU 通用公共许可协议下发布的开源软件。它在 UNIX、Linux 和 Windows 上运行。它使用 `GTK+`（一种图形用户界面库）和 `libcap`（一种数据包捕获和过滤库）。

以下是 `Wireshark` 的部分特性：

- 可以从以太网、FDDI、PPP、令牌环、IEEE 802.11、经典 IP over ATM 以及回环接口读取实时数据。
- 捕获的网络数据可以通过 GUI 或交互式 TTY 模式程序进行浏览。
- 捕获的文件可以通过 `tshark` 程序的命令行开关进行程序化编辑或转换。
- 数据可以从实时网络连接捕获，或从捕获文件读取。
