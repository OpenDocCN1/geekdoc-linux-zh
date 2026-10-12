

## 红帽 LINUX

网络

管理工具

![](img/f265c9d1f2610aca197c430cbfcd51f5_0_0.png)

![](img/f265c9d1f2610aca197c430cbfcd51f5_0_1.png)

steve_maxwell

![](img/f265c9d1f2610aca197c430cbfcd51f5_1_0.png)

## 网络管理工具

![](img/f265c9d1f2610aca197c430cbfcd51f5_1_1.png)

P/N 212261-7

![](img/f265c9d1f2610aca197c430cbfcd51f5_1_2.png)

版权所有 © 2000 The McGraw-Hill Companies, Inc.
保留所有权利。

## 红帽 Linux 网络管理工具

## McGraw-Hill 工具系列丛书：

- Maxwell UNIX 网络管理工具 0-07-913782-2
- Medinets UNIX Shell 编程工具 0-07-913790-3
- Carasik UNIX 安全 Shell 0-07-134933-2
- Ross UNIX 系统安全工具 0-07-913788-1
- Medinets PHP3：基于浏览器的应用程序编程 0-07-135342-9
- Fisher 红帽 Linux 系统管理工具 0-07-134746-1
- Cervone Solaris 7 性能管理工具 0-07-212211-0

如需订购或获取这些或任何其他 McGraw-Hill 丛书的更多信息，在美国请致电 1-800-722-4726，或访问 www.computing.mcgraw-hill.com。在其他国家，请联系您当地的 McGraw-Hill 代表。

## 红帽 Linux 网络管理工具

*Steve Maxwell*

**McGraw-Hill**

纽约 • 旧金山 • 华盛顿特区 • 奥克兰 • 波哥大 • 加拉加斯
里斯本 • 伦敦 • 马德里 • 墨西哥城 • 米兰 • 蒙特利尔 • 新德里
圣胡安 • 新加坡 • 悉尼 • 东京 • 多伦多

美国国会图书馆版本目录数据

Maxwell, Steven.
红帽 Linux 网络管理工具 / Steve Maxwell 著。
页。
厘米。
ISBN 0-07-212262-5
1. Linux。2. 操作系统（计算机）。3. 计算机网络—管理。I. 书名。
QA76.76.M63 M373339 2000
050.4'649--dc21

99-088793

## McGraw-Hill

![](img/f265c9d1f2610aca197c430cbfcd51f5_5_0.png)

版权所有 © 2000 The McGraw-Hill Companies, Inc. 保留所有权利。在美国印刷。除 1976 年《美国版权法》许可的情况外，未经出版商事先书面许可，不得以任何形式或任何方式复制或分发本出版物的任何部分，或将其存储在数据库或检索系统中。
1 2 3 4 5 6 7 8 9 0 AGM/AGM 0 5 4 3 2 1 0
P/N 0-07-212260-9
ISBN 0-07-212262-5 的一部分
本书的策划编辑是 Simon Yates，制作主管是 Clare Stanley。由 TIPS Technical Publishing 使用 Sabon 字体排版。
由 Quebecor/Martinsburg 印刷和装订。

McGraw-Hill 丛书可提供特殊数量折扣，用作赠品和销售促销，或用于企业培训计划。如需更多信息，请写信给 Director of Special Sales, McGraw-Hill, 2 Penn Plaza, New York, NY 10121。或联系您当地的书店。

全书使用了商标名称。我们没有在每个商标名称后加上商标符号，而是仅以编辑方式使用这些名称，并有利于商标所有者，无意侵犯商标。本书中出现此类标识时，我们均以首字母大写形式印刷。

本书所含信息由 The McGraw-Hill Companies, Inc.（以下简称“McGraw-Hill”）从被认为可靠的来源获取。然而，McGraw-Hill 及其作者不保证此处发布的任何信息的准确性或完整性，对于因使用该信息而产生的任何错误、遗漏或损害，McGraw-Hill 及其作者概不负责。出版本书的理解是 McGraw-Hill 及其作者提供信息，但不提供工程或其他专业服务。如需此类服务，应寻求适当专业人士的协助。

本书印刷在含有至少 50% 再生脱墨纤维的再生无酸纸上。

![](img/f265c9d1f2610aca197c430cbfcd51f5_5_1.png)

献给 Gimmy，永远永远……

## 目录

- 图目录 xi
- 表目录 xvii
- 代码清单 xxii
- 前言 xxiii

- 01 **网络管理概述** 1
  - 网络管理组件 4

- 02 **简单网络管理协议** 21
  - SNMP 操作 23
  - 管理信息库 (MIB) 25
  - SNMP 版本概述 40
  - 主代理和子代理 54

- 03 **TCP/IP 协议族** 57
  - TCP/IP 协议族 58
  - OSI 模型 60
  - TCP/IP 协议架构 61
  - 最终用户工具 64
  - 地址解析协议 95

- 04 **核心系统实用程序和工具** 105
  - ARP 工具 106
  - Ifconfig 工具 115
  - Netstat 工具 125
  - Ping 工具 143
  - Tcpdump 工具 153
  - Traceroute 工具 171

- 05 **其他系统实用程序和工具** 183
  - Arpwatch 工具 184
  - Ethereal 工具 188

Fping 工具 210

Nmap 工具 218

Xtraceroute 工具 239

## 06 MIB-II 概述 245

## 07 使用 SNMP 代理 325

代理概述 326

安全注意事项 331

Linux SNMP 代理 332

Sun 主代理 377

Sun SNMP 代理 391

## 08 SNMP 工具 411

监控/管理功能 412

UCD 命令 414

Snmpdelta 工具 422

Snmpget 工具 425

Snmpgetnext 工具 427

Snmpgetstat 工具 429

Snmpset 工具 434

Snmpstatus 工具 437

Snmpstable 工具 440

Snmptest 工具 443

Snmptranslate 工具 443

Snmptrap 工具 445

Snmprapd 工具 446

Snmpwalk 工具 450

Snmpbulkwalk 工具 451

Snmpconf 工具 454

Tkmb 工具 458

## 09 支持 Web 的工具 465

MRTG 工具 466

MRTG 问题排查 497

Ntop 工具 500

## 10 Linux 控制面板 533

控制面板 534

使用网络配置器 537

## 11 tkined 工具—网络编辑器 567

tkined 概述 568

管理网络 589

菜单参考 613

附录 A 工具一览 621

附录 B 安装过程和软件说明 625
使用 RPM 安装软件包 628
非 RPM 包安装过程 633

附录 C 网络/网络管理术语词汇表 645

索引 655

## 图目录

- 1.1 网络管理的三个要素。 2
- 1.2 管理器/代理关系。 5
- 1.3 网络设备中的代理。 5
- 1.4 代理功能图。 8
- 1.5 SNMP 代理和 MIB 对象。 9
- 1.6 基于代理的系统。 11

- 2.1 SNMP 管理器和代理关系。 24
- 2.2 MIB 结构和组织。 26
- 2.3 MIB 浏览器。 27
- 2.4 MIB 结构示例。 32
- 2.5 MIB-II 接口组结构。 35
- 2.6 来自私有分支的企业 MIB。 39
- 2.7 SNMP 报文格式。 43
- 2.8 GetRequest 报文格式。 45
- 2.9 GetResponse 报文格式。 48
- 2.10 Trap 报文格式。 49

- 2.11 主/子代理架构。 56

- 3.1 OSI 网络模型上的 TCP/IP。 62
- 3.2 TCP/IP 协议族。 64
- 3.3 TCP 段号的实际运作。 71
- 3.4 处理 Telnet 请求的 INETD 运作。 73
- 3.5 来自相同源/目的地的两个 TCP 会话。 74
- 3.6 使用三次握手打开 TCP 连接。 75
- 3.7 关闭 TCP 连接。 76
- 3.8 TCP 状态机。 77
- 3.9 TCP 段格式。 78
- 3.10 三个主要 IP 地址类别。 83
- 3.11 子网寻址。 85
- 3.12 子网计算。 85
- 3.13 子网示例。 86
- 3.14 主子网计算器窗口。 88
- 3.15 子网计算窗口。 90

- 3.16 ICMP 回显请求/回复。 91
- 3.17 ICMP 源抑制重定向。 93
- 3.18 ICMP 重定向。 94
- 3.19 ARP 请求。 96
- 3.20 ARP 回复。 97
- 3.21 ARP/RARP 报文格式。 98
- 3.22 数据链路地址格式。 100
- 3.23 IEEE OUI 搜索页面。 102
- 3.24 OUI 搜索结果。 103
- 4.1 不可达节点问题。 146
- 4.2 tcpdump 数据包过滤器图。 164
- 4.3 单跳的 traceroute。 174
- 4.4 双跳的 traceroute。 175
- 5.1 Ethereal 主窗口。 189
- 5.2 Ethereal 捕获首选项窗口。 193
- 5.3 Ethereal 捕获/回放窗口。 193
- 5.4 选中的 ARP 数据包及详细信息。 194
- 5.5 TCP 数据包过滤器窗口。 197
- 5.6 Ethereal 过滤器窗口。 198
- 5.7 IP 广播过滤器选择。 199
- 5.8 显示的 Ethereal 过滤器。 199
- 5.9 按协议类型排序的大量数据包列表。 200
- 5.10 FTP 显示过滤器。 200
- 5.11 Ethereal 保存窗口。 202
- 5.12 Ethereal 首选项窗口。 203
- 5.13 Ethereal 打印首选项。 204
- 5.14 a2ps 输出预览。 204
- 5.15 Ethereal 时间字段显示选项窗口。 205
- 5.16 使用“时间”选项显示的数据包。 206
- 5.17 TCP 登录会话信息。 206
- 5.18 FTP 目录列表。 208
- 5.19 Ethereal 数据包摘要窗口。 208
- 5.20 TCP 数据包过滤器窗口。 240
- 5.21 新跟踪窗口。 241
- 5.22 新主机记录对话框。 241
- 5.23 目的地跳数信息。 242
- 6.1 mib-2 组视图。 247
- 6.2 系统组视图。 248

