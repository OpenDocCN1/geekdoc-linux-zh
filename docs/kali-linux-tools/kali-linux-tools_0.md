# Kali Linux 工具指南



![](img/cover0019.jpeg)

![](img/image00193.jpeg)



---

## 目录

## 第一章：数据收集 - VOIP 分析
## 第二章：数据收集 - VPN 分析
### 第三章：弱性分析
## 第四章：信息库评估
### 第五章：模糊工具
## 第六章：杂项扫描器
## 第七章：开源评估
## 第八章：Open-VAS
### 第九章：Web 应用程序：CMS 识别
## 第十章：数据集利用
## 第十一章：IDS/IPS 识别
### 第十二章：Web 应用程序模糊器
## 第十三章：Web 应用程序代理
### 第十四章：Web 爬虫
## 第十五章：Web 漏洞扫描器
## 第十六章：密码短语攻击：GPU 工具
## 第十七：离线攻击
## 第十八章：在线攻击

---

## 引言

本参考指南独立地描述了每一个设备，专注于任何需要了解自动化犯罪科学和渗透测试，或希望通过 Kali Linux 中的设备复习相关知识的人员。注意！我已尝试收集了尽可能合理预期的信息，尽管如此，某些章节缺少信息，如果我有幸获得更多信息，我可能会进行更新。此外，错误是所不可避免的。

本书存在的目的是为 Kali Linux 中的每个工具提供逐点资源，以便于快速参考和更好地规划。在有疑问时，每个工具的信息包含：`DESCRIPTION`、`USAGE`、`EXAMPLE` 以及偶尔提供的 `OPTIONS` 和 `IPS`。Kali Linux 机械组件不仅限于 Kali Linux/Backtrack（在考虑所有因素的情况下，大多数可以在其他 Linux 发行版上运行）。此外，某些工具在 Windows 和 Mac OS 等其他操作系统上同样可用。Kali Linux 是一个新的操作系统——随着时间的推移，可能会增加一些、移除一些、删除一些。已知所有工具都以 `root`（或 `head`）身份运行（在 Kali Linux 中，你默认就是 root）。

关于每个设备收集的信息均从互联网免费获取并直接公开。信息来源列在文末。

大多数命令行工具都包含选项，但由于空间限制，只有少数工具记录了选项（在网上搜索选项、阅读文档/手册、使用 `-h` 或 `-help`）。

有关每个工具的更多信息——搜索网络、点击链接或仔细查看末尾的参考文献。

**注意：**

请切勿将 KALI LINUX 和此处列出的工具用于任何非法操作！明确围绕 `DOS`、`DDOS` 或匿名性的工具有时用于经过认证的责任范围内，因此在 Kali Linux 中并未直接呈现。

---

## 第一章：数据收集 - VOIP 分析

### pro
### enumiax

#### Pro

**DESCRIPTION**

`pro` ( `Automated Corporate Enumerator` ) 是一个基础但强大的 VoIP 企业目录规范工具，它模拟 IP 电话的行为，下载给定电话可以在其屏幕界面上显示的名称和扩展字段。专家可以通过两种方式使用它：首先，可以通过 `DHCP` 自动发现 `TFTP Server IP Address`，或者（其次）客户端可以将 `TFTP Server IP address` 作为工具的命令行边界。无论如何，你都应该通过 `-m` 选项提供 IP 电话的 `MAC Address`，工具才能通过 `TFTP` 有效下载配置文件。

**USAGE:** `pro [-I interface] [ - m macintosh address ] [ - t tftp server ip address | - c cdp mode | - v voice vlan id | - r vlan interface | - d verbose mode ]`

**OPTIONS:** `http://ucsniff.sourceforge.net/ace.html`

**EXAMPLE:** `pro - I eth0 - v 96 - m 00:1E:F7:28:9C:8E` (指示语音 VLAN ID 的模式)

**EXAMPLE:** `pro - I eth0 - c 0 - m 00:1E:F7:28:9C:8E` (在 CDP 监听模式下自动查找语音 VLAN ID 的模式)

**EXAMPLE:** `pro - I eth0 - c 1 - m 00:1E:F7:28:9C:8E` (在 CDP 模拟模式下自动查找语音 VLAN ID 的模式)

#### Enumiax

**DESCRIPTION**

`enumIAX` 是一个 Inter Asterisk Exchange 2 (`IAX2` ) 协议用户名枚举器。`enumIAX` 可能以两种不同的模式工作：顺序用户名猜解或字典攻击。

**USAGE:** `enumiax [options]`

**OPTIONS:**

- `-d` 使用文档进行字典攻击
- `-I` 自动保存间隔（活动次数 `#`，默认 1000）
- `-m` # 最小用户名长度（字符）
- `-M` # 最大用户名长度（字符）
- `-r` # 限制调用速率（微秒）
- `-s` 从状态文件中读取会议状态
- `-v` 增加详细程度（重复使用 v 以获得更多详细信息）
- `-V` 打印适配数据并退出
- `-h` 打印帮助/使用数据并退出

**EXAMPLE:** `enumiax 172.16.1.100 – m 4 – M 8 – v` (在四个和八个字符的连续用户名下运行 enumIAX)

**EXAMPLE:** `enumiax 172.16.1.100 – m 4 – M 8 – v` (在以下结构下运行 enumIAX)
**EXAMPLE:** ` 192.168.1.104

---

## 第二章：数据收集 - VPN 分析

### enumiax
#### ike-filter

#### ike-filter

**DESCRIPTION**

`ike-filter` 是一个利用 IKE 协议查找、唯一标记和测试 IPSec 服务器的命令行工具。`ike-filter` 允许你：

- 向多个主机发送 IKE 束，使用可配置的结果容量。这对于 VPN 发现非常有用，此时你可能需要：
- 灵活地开发 IKE 数据包。这包括遵循 RFC 要求的 IKE 数据包。
- 破解强制模式预共享密钥。你可以使用 `ike-output` 获取 PSK 哈希信息。

**USAGE:** `ike-examine [options] [hosts...]`

**OPTIONS:** `http://www.nta-monitor.com/wiki/php/Ike-scan_User_Guide` 或 `ike-filter - - help`

**EXAMPLE`

**EXAMPLE:** `ike-filter - - auth=3 10.0.0/24` (对于每次更改使用带有 RSA 签名的标准更改集，而不是默认的预共享密钥。这种策略对于发现不对标准更改集没有响应的 VPN 服务器非常有效。)

**EXAMPLE:** `ike-check - M - - trans=5,2,1,2 - - showbackoff 10.0.0.1` (退避指纹识别)

---

## 第三章：弱性分析

### cisco-examining instrument
#### cisco-worldwide exploiter
### cisco-ocs
### cisco-light
### Yersinia

#### cisco-inspecting instrument

**DESCRIPTION**

`Cisco Auditing Tool` - 一个 Perl 脚本，用于检查 Cisco 器的常见弱性。检查默认密码、易猜局域网名称以及 IOS 历史漏洞。包含对模块和过滤各种主机的支持。

**USAGE:** `./CAT [options]`

**OPTIONS:**

- `-h` 主机名（检查单个主机）
- `-f` 主机文件（检查多个主机）
- `-p` 端口 #（默认端口为 23）
- `-w` 用于局域网名称猜测的字典表
- `-a passlist（用于密钥猜测的的密码列表）
- `-I [ioshist]`（检查 IOS 历史漏洞）
- `-l` 日志文件（记录到日志，默认为屏幕）
- `-q` 静默模式（无屏幕输出）

**EXAMPLE:** `./CAT - h 192.168.1.100 - w wordlist - a passwords - I`

**EXAMPLE:**./CAT - h 192.168.1.22 - a rundowns/passwords - w records/local area (审计 Cisco Telnet 密码和 SNMP 团体字符串)

#### cisco-worldwide exploiter

**DESCRIPTION:**





## Cisco Global Exploiter (CGE)

CGE 是一种高级、直接且快速的安全测试工具/漏洞利用引擎，可以利用不同 Cisco 交换机和交换机设备中的 14 种漏洞。CGE 是一个命令行驱动的 Perl 脚本，具有简单易于使用的前端。

### 使用方法
`cge.pl<target> <漏洞编号>`

### 选项 (14 种漏洞)
- `[1]` - Cisco 677/678 Telnet 缓冲区溢出漏洞
- `[2]` - Cisco IOS 路由器拒绝服务漏洞
- `[3]` - Cisco IOS HTTP 认证漏洞
- `[4]` - Cisco IOS HTTP 配置任意管理访问漏洞
- `[5]` - Cisco Catalyst SSH 协议不匹配拒绝服务漏洞
- `[6]` - Cisco 675 Web 管理拒绝服务漏洞
- `[7]` - Cisco Catalyst 3500 XL 远程任意命令漏洞
- `[8]` - Cisco IOS 软件 HTTP 请求拒绝服务漏洞
- `[9]` - Cisco 514 UDP 洪水拒绝服务漏洞
- `[10]` - CiscoSecure ACS Windows NT Server 拒绝服务漏洞
- `[11]` - Cisco Catalyst 内存泄漏漏洞
- `[12]` - Cisco CatOS CiscoView HTTP 服务器 缓冲区溢出漏洞
- `[13]` - 0 编码 IDS 绕过漏洞 (UTF)
- `[14]` - Cisco IOS HTTP 拒绝服务漏洞

### 示例
`cge.pl 192.168.1.254 3` (利用 Cisco IOS HTTP 认证漏洞，理想情况下利用良好的连接，我们应该获得对所攻击交换机的基本访问权限（而非赋权）)

### cisco-ocs

### 描述
`cisco-ocs` 也称为 `cisco-ocs` 批量扫描器。该工具提供单一功能，用于检查大范围的 IP 寻找 Cisco 设备或任何监听 TCP 端口 `23` 的设备，尝试使用密钥 `cisco` 通过 `telnet` 登录，然后如果 Cisco 交换机已准备好通过 `telnet` 登录，则发送 `empower` 命令，再次使用 `cisco` 作为 `empower` 密语，最后如果能够通过这些精确步骤获取 `empower` 摘要则报告成功。遗憾的是，这是该工具的主要功能，因为你无法指定尝试的密码列表，或者就目前而言你无法为要扫描的 IP 地址设置任何标识。

### 使用方法
`./ocs <范围起始 IP> <范围结束 IP>`

### 示例
`./ocs 192.168.1.21 192.168.1.23`

### cisco-light

### 描述
Cisco Light 设计用于一种批量扫描、指纹识别和双重处理工具。Cisco Light 与其他工具的独特之处在于它使用各种字符串（分叉方法）来发送过滤进程。它还利用一些策略同时执行应用层指纹识别。Cisco Light 可对服务发送基于字典的密钥攻击，并发现正在运行的服务：`Telnet`、`SSH`、`Web`、`NTP`、`SNMP`。

### 使用方法
`./cisco- light.pl<options> <IP,hostname,network>`
`./cisco- light.pl<options> -F<hostlist>`

### 选项
请查看 http://www.vulnerabilityassessment.co.uk/torch.htm

### 示例
- `./cisco- light.pl - A 10.10.0.0/16`
- `./cisco- light.pl - s - b - F sshtocheck.txt`
- `./cisco- light.pl - w - z 10.10.0.0/16`
- `./cisco- light.pl - j - b - g - F tftptocheck.txt`

### Yersinia

### 描述
Yersinia 是一种旨在利用各种组织协议中某些缺陷的工具。它声称是一个用于调查和测试发送组织和框架的强大结构。针对以下组织协议的攻击：生成树协议 (`STP`)、Cisco 发现协议 (`CDP`)、动态中继协议 (`DTP`)、动态主机配置协议 (`DHCP`)、热备备路由协议 (`HSRP`)、IEEE `802.1Q`、IEEE `802.1X`、交换机链路协议 (`ISL`)、VLAN 传输协议 (`VTP`)。

### 使用方法
`yersinia [-hVID] [-l logfile] protocol [protocol_options]`

### 选项
- `-V` 程序变体。
- `-h` 帮助屏幕。
- `-I` 交互模式 (ncurses)。
- `-D` 守护进程模式。
- `-l logfile` 选择日志文件。
- `-c conffile` 选择配置文件。
- `Protocol` 可以是以下之一之一：`cdp`, `dhcp`, `dot1q`, `dtp`, `hsrp`, `stp`, `vtp`

### 示例
`yersinia – D`（在守护进程模式下运行）

# 第章：数据库评估

- `bbqsql`
- `dbpwaudit`
- `hexorbase`
- `mdb-export`
- `mdb-parsecsv`
- `mdb-sql`
- `mdb-tables`
- `oscanner`
- `sidguesser`
- `sqldict`
- `sqlmap`
- `sqlninja`
- `sqlus`
- `tnscmd10g`

### bbqsql

### 描述
盲 SQL 注入的利用可能非常麻烦。当可用设备工作时它们运行良好，但当它们失效时你需要编写自定义内容。这既无聊又无味。BBQSQL 可以帮助解决这些问题。

BBQSQL 是一个用 `Python` 编写的可视 SQL 注入系统。在攻击有趣的 SQL 注入漏洞时非常有价值。BBQSQL 还是一个自加载工具，允许对那些难以触发的 SQL 注入发现进行大量自定义。该工具被设计为数据库自由思考者，并且具有极强的适应性。它还拥有自然的 UI，使设置攻击变得简单得多。

此外还实现了 `Python gevent`，使得 BBQSQL 异常快速。

### 使用方法
n/a，选择确定/配置

### 选项
https://github.com/Neohapsis/bbqsql

### 示例
n/a

### dbpwaudit

### 描述
DBPwAudit 是一个 `Java` 工具，允许你对许多数据库的密码质量进行在线审查。应用程序配置通过通过将新的 `JDBC` 驱动复制到 `jdbc` 索引来简单添加额外的数据集驱动程序。设计在两个文件中进行，`aliases.conf` 记录为驱动程序规划别名，`rules.conf` 让程序知道如何处理扫描错误信息。

该工具已通过测试并证明适用于：
- Microsoft SQL Server 2000/2005
- Prophet 8/9/10/11
- IBM DB2 Universal Database
- MySQL

### 使用方法
`dbpwaudit - s<server> - d<db> -D<driver> -U<users> -P<passwords> [options]`

### 选项
http://www.edwiget.name/2012/07/evaluating-mysql-passwords-with-dbpwaudit/

### 示例
`./dbpwaudit.sh - s localhost - d mysql - D MySQL - U ~/mysql-users.txt - P ~/mysql-password.txt`（假设我在本地有一个数据库服务器，并且保存在主目录下的 `mysql-users.txt` 中的 mysql 用户名列表以及保存在主目录下的 `mysql-password.txt` 中的尝试密码列表，此命令将审查 mysql 服务器）

**提示**：运行此程序需要额外的程序：http://www.edwiget.name/2012/07/evaluating-mysql-passwords-with-dbpwaudit/

### Hexorbase

### 描述
HexorBase 是一个用于从集中区域管理和检查多个数据库的应用程序，适用于对标准数据库（MySQL, SQLite, Microsoft SQL Server, Oracle, PostgreSQL）执行 SQL 查询和暴力破解。HexorBase 允许通过代理甚至 Metasploit 隧道与隐藏在子网内的某些远程服务器通信。

### 使用方法
n/a；GUI 工具

### 示例
n/a；GUI 工具

### mdb-export

### 描述
MDB Tools 项目是一个记录 Microsoft Access 数据集使用的 MDB 文档设计并提供一组工具和应用程序在不同平台上访问该信息的工作。特别是 MDB Tools 包含了将映射和信息发送 MySQL, Oracle, Sybase, PostgreSQL 等其他数据集的程序。

`mdb-export` 是随 MDB Tools 分发的实用程序。它为指定的表交付 CSV（逗号分隔值）输出。这种结果对于导入到数据库或电子表格。

### 使用方法
`mdb-export [-H] [-d ] [-R ] [[-Q] || [-q [-X ]]] [-I] [-D ] [-S]`

### 选项
http://linux.die.net/man/1/mdb-trade





### mdb-export

### 示例
```
mdb-export - d ';' something.mdb Main > Main.csv
```
```bash
mdb-export - X \ - D "%Y-%m-%d %H:%M:%S" orsk.mdb Main > Main.csv
```

---

### mdb-parsecsv

### 描述
MDB Tools 项目旨在归档 Microsoft Access 数据集包中使用的 MDB 记录设计，并提供一系列工具和应用程序，以便在不同阶段能够访问这些信息。特别是，MDB Tools 包含了将图表和信息交换到 MySQL、Oracle、Sybase、PostgreSQL 等其他不同数据集的项目。

`mdb-parsecsv` 是随 MDB Tools 分发的一个实用程序。`mdb-parsecsv` 读取一个指向信息数据库表的 CSV 记录，并将其转换为 C 导出文件。假设不存在该文档，`mdb-parsecsv` 将搜索带有 `.txt` 后缀的相同文件名。扩展名将被剥离，结果以 `.c` 扩展名保存。

### 使用方法
无

### 示例
无

---

### mdb-sql

### 描述
MDB Tools 项目旨在归档 Microsoft Access 数据包中使用的 MDB 记录设计，并提供一系列工具和应用程序，以便不同阶段访问这些信息。特别是，MDB Tools 包含了将结构和信息交换到 MySQL、Oracle、Sybase、PostgreSQL 等不同数据集的项目。

`mdb-sql` 是一个命令行工具，允许输入 SQL 查询并获取结果。`mdb-sql` 允许使用限制 SQL 子语言对数据集进行查询。

### 使用方法
`mdb-sql [-p] [-d<delimiter>] [-I<file> ] [-o<file> ] [<database>]`

### 选项
http://linux.die.net/mdb-sql

### 示例
无

---

### mdb-tables

### 描述
MDB Tools 项目旨在归档 Microsoft Access 数据包中使用的 MDB 记录设计，并提供一系列工具和应用程序，以便不同阶段访问这些信息。特别是，MDB Tools 包含了将模式和信息交换到 MySQL、Oracle、Sybase、PostgreSQL 等不同数据集的项目。

`mdb-tables` 是随 MDB Tools 分发的实用程序。它提供 MDB 数据集内部表的列表，适用于脚本。

### 使用方法
`mdb-tables [-S] [-1 <delimiter>] <database>`

### 选项
http://linux.die.net/man/mdb-tables

### 示例
`mdb-tables database.mdb`

---

### Oscanner

### 描述
`Oscanner` 是一个用 Java 创建的评估框架。它采用模块化设计，并包含几个模块：枚举、密码测试（普通和字典）、枚举 Oracle 、枚举作业、枚举权限、枚举账户哈希、枚举数据、枚举密码策略、枚举数据库连接。

### 使用方法
`OracleScanner – s<ip> - r<repfile>`
`oscanner – s<ip> - r<repfile>`

### 选项
- `–s<servername>`
- `-f<serverlist>`
- `-P<portnr>`
- `-v` 详细模式

### 示例
`oscanner.sh - s 192.168.0.1`

---

### Sidguesser

### 描述
`sidguesser` 根据预定义的字典文件对 Oracle 数据库进行 `sids/occurrences` 猜测。速度较慢（每秒 80-100 次猜测），但它可以工作。

### 使用方法
`sidguesser - I - d [options]`

### 选项
- `-p<portnr>` 使用端口（默认 1521）
- `-r<report>` 报告到文件
- `-m<mode>` findfirst 或 findall（默认）

### 示例
`sidguesser - I 192.168.0.223 - d words.txt`

---

### Sqldict

### 描述
`SQLdict` 是一个针对命名 SQL 账户进行字典攻击的基本实用程序。

### 使用方法
无；GUI 工具

### 示例
无；GUI 工具

---

### sqlmap

### 描述
`sqlmap` 是一个开源渗透测试工具，自动化识别 SQL 注入漏洞并接管数据库服务器。它有一个强大的引擎，为渗透测试人员提供许多功能，包括数据库指纹、从数据库获取信息、获取隐藏框架以及通过带外连接在框架上执行命令。

### 使用方法
`sqlmap.py [options]`

### 选项
https://github.com/sqlmapproject/sqlmap/wiki/Usage

### 示例
```bash
sqlmap.py -u "http://www.target.com/vuln.php?id=1" --batch --dbs --level （针对单个 URL 运行 sqlmap）
```
```bash
sqlmap.py - g "inurl:\".php?id=1\" （根据你的 GET 结果测试并注入）
```
```bash
sqlmap.py -u "http://www.target.com/vuln.php" --data="id=1" --batch --dbs --level （跟踪 请求 请求跟踪 POST 请求）
```
```bash
sqlmap.py -u "http://192.168.136.131/sqlmap/mysql/get_int.php?id=1" --auth-type Basic --auth-cred "testuser:testpass" （HTTP 验证）
```
```bash
sqlmap.py -l burp.log --scope="(www)?\.target\.(com|net|org)" （使用自定义表达式过滤日志）
```

---

### Sqlninja

### 描述
`Sqlninja` 是一种用于利用使用 Microsoft SQL Server 后端的 Web 应用程序 SQL 注入漏洞的工具。其主要目标是在极其不利的环境下为漏洞数据库服务器提供远程访问。渗透人员可以使用它协助自动化发现 SQL 注入漏洞后控制数据库服务器的过程。

### 使用方法
配置和执行通过 `sqlninja.conf` 完成；更多细节请参见文档。

### 
http://sqlninja.sourceforge.net/sqlninja-howto.html

### 示例
无

---

### Sqlsus

### 描述
`sqls` 是一个开源 MySQL 注入和接管工具。通过命令行界面，你可以恢复数据库结构、输入自己的 SQL 查询（甚至是复杂的）、从 Web 服务器下载、扫描站点的可写目录、传输并控制远程访问、克隆数据库等……在任何情况下，`sqls` 都会模拟 MySQL 控制台输出。

更多信息：http://sqls.sourceforge.net/

### 使用方法
使用 `sqls --genconf my.cfg` 生成配置文件，阅读注释并调整以匹配你的目标。启动 `sqls` 并将你的配置作为参数输入 `sqls my.cfg`，即可获得一个 shell。

### 选项
http://sqls.sourceforge.net/documentation.html

### 示例
无，实际上请查看文档

---

### tnscmd10g

### 描述
`tnscmd` 可用于在基础层面与 Oracle 的 TNS 监听进行通信。TNS 监听（也称为 tnslsnr）是数据库客户端与数据库服务器之间的组织接口。`tnslsnr` 监听 1521/tcp 端口。

`tnslnsr` 保留一个简单的操作日志——简单在于它不记录大量的有用数据。例如，它不记录 TNS 会话的 IP 地址。如果你向 tnslsnr 端口启动 TCP 会话，你不会有进展；它不会给出标记，并且会在你输入内容时断开。放心；这正是 `tnscmd` 的用途。`tnscmd` 本质上与 tnslsnr 交互通信。

### 使用方法
`tnscmd [command] - h hostname` 其中 'command' 是类似 ping、adaptation、status 等命令（默认是 ping）

### 示例
无，实际上请查看文档





示例：`tnscmd [badcommand] - h oraclebox.example.com ("坏的" TNS 数据包可能会导致受众崩溃，无论 DBA 是否设置了秘密口令。`badcommand` 可以是以下任意一个：`trc_file`, `trc_level`, `use_plugandplay`, `trc_directory`, `snmp_visible`, `log_file`, `log_status`, `log_directory`)`

## 第五章：模糊测试工具

* `bed`
* `fuzz_ip6`
* `ohrwurm`
* `powerfuzzer`
* `sfuzz`
* `siparmyknife`
* `spike-generic_chunked`
* `spike-generic_listen_tcp`
* `spike-generic_send_tcp`
* `spike-generic_listen_upd`

### bed

### 描述
`BED`（也称为 `Bruteforce Exploit Detector`，暴力破解检测器）是一种纯文本协议模糊测试器，用于检查程序中的常见漏洞，如支持洪泛、设计字符串漏洞、整数溢出等。该工具目前支持以下协议：`finger`, `ftp`, `http`, `imap`, `irc`, `lpd`, `pjl`, `pop`, `smtp`。

### 用
`./bed.pl – s<Plugin> [options]`

### 选项
* `-s <Plugin>`：要使用的插件（强制性）。主要的模块有：`FTP/SMTP/POP/HTTP/IRC/IMAP/PJL/LPD/FINGER/SOCKS4/SOCKS5`。使用 `"./bed.pl - s "` 获取你想要为该模块设置边界。
* `-t<target>`：要检查的主机（默认：`localhost`）
* `-p<port>`：要交互的端口（默认：标准端口）
* `-o<timeout>`：每次测试后等待的秒数（默认：2 秒）

### 示例
`./bed.pl - s HTTP - t 192.168.100.16 - p 80`

### fuzz_ip6

### 描述
`thc-ipv6` - `THC-IPV6-ATTACK-TOOLKIT` - 直接运行这些工具无需选择，它们将为你提供帮助并显示命令行选项。

`fuzz_ip6` - 对 icmp6 数据包进行模糊测试。

### 特征检测
大多数工具无疑可以被 IDS 或特定的识别程序区分。这样做是故意的，为了让异常使用的识别更简单。这些设备要么确定一个合理的数据包签名，要么惯性地嗅探数据包（例如，对 `icmp6` 邻居请求提供解释，这些请求是从一个不存在的 mac 地址发送的，因此极易识别）。如果你不需要这些，请修改代码。

### 用法
`fuzz_ip6 [-x] [-t number | - T number] [-p number] [-IFSDHRJ] [-X|-1|-2|-3|-4|-5|-6|-7|-8|-9|-0 port] interface unicast-or-multicast-address [address-in-information pkt]`

### 选项
https://github.com/mmoya/thc-ipv6/mass/ace/fuzz_ip6.c

### 示例
无

### ohrwurm

### 描述
`ohrwurm` 是一个小型且基础的 RTP 模糊测试器，它已经在几个 SIP 电话上尝试过，没有手机一个经受住模糊测试。

### 亮点
* 解析 SIP 消息以获取 RTP 端口号数据
* 通过提供 RTP 端口号可以忽略对 SIP 解析，因此任何 RTP 流量都可以被模糊测试
* 可以抑制 RTCP 流量以防止解码器发现“杂音线路”
* 特别考虑了破坏 RTP 自身的处理机制
* RTP 负载使用一致的比特错误率（BER）进行模糊测试
* BER 可配置
* 需要 `dsniff` 中的 `arpspoof` 来执行中间人攻击（MITM）
* 需要两个电话位于交换的局域网中（网关活动仅部分可行）

### 用法
无

### 示例
无

### Powerfuzzer

### 描述
`Powerfuzzer` 是一个高度自动化且完全适应的 Web 模糊测试器（基于 HTTP 协议的应用模糊测试器），参考了许多其他开源模糊测试器以及从各种安全资产和网站积累的数据。它的设计目标是易于理解、现代、可行且有效。更多数据见：http://www.powerfuzzer.com/#news

目前，它适用于识别这些问题：
* 跨站脚本 (XSS)
* 注入 (SQL, LDAP, 代码, 命令和 XPATH)
* CRLF 注入
* HTTP 500 状态（具有潜在配置错误/安全缺陷的特征，包括崩溃洪泛）

### 用法
无；GUI 工具

### 示例
无；GUI 工具

### Sfuzz

### 描述
基础模糊测试器基本上就像看起来那样——一个直接的模糊测试器。不要因缺乏模糊能力而弄巧了简单。此模糊测试器有两种活动模式：用于创建命令行模糊测试脚本的结果模式，另一种是从字面量中获取模糊字符串并根据组合构建字符串。

基础模糊是为了满足一种需求——需要一种快速配置的发现测试工具，该工具不需要关于 C 内部活动的详细信息，也不需要特定的编程环境。其点在于提供一个基础接口、清晰的信息/结果来源以及可用性。

### 用法
`sfuzz [output modes] [logging] [config file] [network host] [variables] [misc]`
`sfuzz – h`（获取帮助）或通过下方链接阅读文档

### 选项
https://github.com/orgcandman/Simple-Fuzzer

### 示例
`sfuzz - T - f/tmp/myfirst.cfg - S foo.com - p 80`

### Siparmyknife

### 描述
`SIP Army Knife` 是一种寻找跨站配置的模糊测试器。

### 用法
（文中未提供用法）

### 示例
（文中未提供示例）





### spike-generic_listen_upd

### 描述
当你真正想要剖析另一个组织关于缓冲区溢出或类似缺陷的规范时，`SPIKE` 是专家决策的工具。虽然使用它需要坚实的的 `C` 信息，但它在该领域内产生最优质的结果。它让你能够将其 API 集成到 `C` 代码中，或者本质上利用基于 `SPIKE` 原生脚本的某些预装工具。

更多数据：http://resources.infosecinstitute.com/introduction to-fluffing/

更多数据：http://resources.infosecinstitute.com/fuzzer-computerization with-spike/

### 用法
n/a

### 示例
n/a

# 六章

## 杂项扫描器
- `lynis`
- `nikto`
- `nmap`
- `unix-privesc-check`

### lynis
### 描述
Lynis 是一个针对 Unix（专家）的评估工具。它通过过滤框架和可访问的程序来识别安全问题。除了安全相关的数据外，它还会筛选一般的框架数据、引入的包和配置错误。

该产品旨在协助计算机检查、补丁管理以及基于 Unix 框架的漏洞和恶意软件检查。它可以在无需预安装的情况下运行，因此无需考虑读取权限（USB 闪盘、硬盘/DVD）。

Lynis 帮助审计人员执行 Basel II、GLBA、HIPAA、PCI DSS 和 SOX（萨班斯-奥克斯法）合规性审查。

### 用法
`./lynis [options] [cronjob]`

### 选项
http://www.rootkit.nl/records/lynis-documentation.html

### 示例
`./lynis - c - - examiner "computer"` – cronjob

### Nikto
### 描述
Nikto 是一个 Web 服务器扫描器，会对 Web 服务器进行长时间的全测试，包括超过 6500 个可能的危险文件/CGI、检查 1250 多个服务器的过时变体，并针对 270 多个服务器识别出特定的配置问题。它还会检查服务器配置项，例如不同文件的存在、HTTP 服务器选项，并尝试识别的 Web 服务器和程序。检查项和模块经常更新，并且可以自动刷新。

### 用法
`nikto.pl [host] [target] [options]`

### 选项
[`cirt.net/nikto2-docs/options.html`](http://cirt.net/nikto2-docs/options.html)

### 示例
`nikto.pl - h 192.168.0.1 - T 58`（检查调优）
`nmap - p80 192.168.0.0/24 - oG - | nikto.pl - h -`（多主机测试）
`nikto.pl - h 192.168.0.1 - p 80,88,443`（多端口测试）
`nikto.pl - h https://192.168.0.1:443/`（利用完整 URL 结构进行基础测试和过滤）
`nikto.pl - h 192.168.0.1 - p 443`（实际查看特定端口）

### Nmap
### 描述
nmap 是公认的顶级扫描器。由于其多功能性，它是任何需要网络识别证明的场景的瑞士军刀。它还允许列出网络主机并过滤它们的端口。

### 用法
`./nmap [Scan Type(s)] [Options] {target specification}`

### 示例
`./nmap - sP 192.168.100.0/24`（列出组织上的主机）
`./nmap - sS - sV 192.168.100.18`（扫描主机。此模型使用 TCP/SYN 输出并尝试识别已发布的服务）

### unix-privesc-check
### 描述
Unix-privesc-checker 是一个对 Unix 框架需求激增的内容。它尝试寻找配置错误，这些错误可能允许相邻的无权客户端提升权限到其他用户，或访问邻近应用程序（例如数据库）。它预期由安全审计人员和渗透分析人员针对他们被要求评估的框架使用，同时也由需要检查“显而易见”配置错误的框架管理员使用。它甚至可以作为 cron 任务运行，以便你可以定期检查可能出现的配置错误。

更多数据：[https://code.google.com/p/unix-privesc-check/wiki/Checks] 和 [http://pentestmonkey.net/apparatuses/unixprivesc-check]

### 用法
`unix-privesc-check { standard | point by point }`

### 示例
`unix-privesc-actually look at standard`

# 七章

## 开源评估
- `casefile`
- `maltego`

### Casefile
### 描述
CaseFile 允许你快速添加、连接和剖析与 Maltego 具有相同绘图能力和执行的信息，而无需插件。通过整合 Maltego 卓越的图表和连接调查，此工具引导调查人员分析物理添加的信息之间的接口，以构建数据绘制思维脑图。

- CaseFile 是一个视觉知识应用程序，用于确定各种类型数据之间的连接和真实性连接。
- 它让你能够快速查看第二、第三和 n 次请求连接，并在任何案例中发现不同类型洞察工具无法发现接口。
- CaseFile 带有通常在调查中使用的各种元素，允许你快速、高效地行动。CaseFile 还可以添加自定义元素类型，允许你将产品扩展到自己的数据索引中。

### 用法
n/a; GUI 工具

### 示例
n/a, GUI 工具

### Maltego
### 描述
Maltego 是一个新平台，旨在为组织声称并运行的环境提供清晰的威胁图谱。Maltego 可以发现、汇总和描绘这些数据。Maltego 是一个用于确定个人、团体（非正式社区）、组织、协会、网站、短语、联盟、文件和记录、网络基础（空间、DNS 名称、网段、IP 地址）之间连接和真实关系的程序。

### 用法
n/a; GUI 工具

### 示例
n/a; GUI 工具

# 八章

## OPEN-VAS
- `penvas-gsd`
- `openvas-arrangement`

### openvas-gsd
### 描述
Open Vulnerability Assessment System 是一个由几个程序和工具组成的结构。该 SSL 管理设计的中心是 OpenVAS 扫描器。扫描器有效地执行真实的网络漏洞测试 (NVTs)，这些测试通过 OpenVAS NVT 馈送或商业反馈管理每日更新。

Greenbone Security Desktop (GSD) 是一个基于 Qt 的 OMP 工作区客户端。

更多数据：http://www.backtrack-linux.org/wiki/index.php/OpenVas

### 用法
n/a; GUI 工具

### 示例
n/a; GUI 工具

### openvas-arrangement
### 描述
Open Vulnerability Assessment System (OpenVAS) 是一个由几个程序和工具组成的结构。该 SSL 管理设计的中心是 OpenVAS 扫描器。扫描器有效地执行真实的网络漏洞测试 (NVTs)，通过 OpenVAS NVT 馈送或商业反馈管理进行每日更新。

更多信息：http://www.backtrack-linux.org/wiki/index.php/OpenVas

### 用法
n/a; GUI 工具

### 示例
n/a GUI 工具

# 九章

## Web 应用：CMS 识别
- `blindelephant`
- `plecost`
- `wpscan`

### Blindelephant
### 描述
BlindElephant Web 应用指纹识别器通过对比已知区域的静态记录与通用交付中这些文档形式的预计算哈希值，尝试寻找（已知）Web 的变体。该过程快速、低数据传输、非侵入、非排他且高度可自动化。BlindElephant 可以直接作为命令行工具使用，也可以作为库为另一个程序提供指纹识别功能。

### 用法
`BlindElephant.py [options] url appName`

### 选项
-h, - - help 显示此帮助消息并退出





### plecost

- `-p PLUGINNAME`: `pluginName=PLUGINNAME` 模块的指纹形式（应适用于指定的 `appname` 中的 Web 应用）
- `-s`: `Skip` 跳过 Web 应用指纹识别，仅标记唯一模块
- `-n NUMPROBES`: `numProbes=NUMPROBES` 获取记录的数量（增加数量可能提高准确性）。默认：`15`
- `-w`: `winnow` 如果返回多种形式，则使用筛选（winnowing）尝试缩小范围（最多额外进行 `numProbes` 次请求）
- `-l`: `List` 列出支持的 Web 应用和模块

### 示例
`BlindElephant.py http://laws.qualys.com movabletype plecost`

### 描述
Wordpress 指纹识别设备 plecost 能够查找并恢复有关 Wordpress 框架中引入的模块变体数据。它可以调查单个 URL，也可以根据 Google 记录的结果执行检查。此外，如果存在，还会显示与每个模块相关的 CVE 代码。Plecost 恢复 Wordpress 支持的 Web 目标包含的数据，并允许对 Google 排序的结果进行追踪。

### 使用方法
`./plecost.py [options] [ URL | [-l num] - G]`

### 选项
https://code.google.com/p/plecost/

### 示例
`plecost - R plugins.txt - n 5` (重新加载初始 5 个模块列表)
`plecost - n 5 - G - I plugins.txt` (搜索初始 5 个模块的弱位置)
`plecost - I plugin_list.txt - s 12 - M 30 - t 20 - o results.txt www.example.com` (为 `www.example.com` 搜索具有 20 个字符串的模块，时间在 12 到 30 秒之间)

---

### wpscan

### 描述
WPScan 是一款 WordPress 漏洞发现扫描器。

### 使用方法
`wpscan.rb – url [target ip] [options]`

### 选项
http://wpscan.org/

### 示例
`ruby wpscan.rb - - url www.example.com` (执行“非侵入性”检查...)
`ruby wpscan.rb - - url www.example.com - - wordlist darkc0de.lst - - strings 50` (利用 50 个线程对计数客户端执行词表秘密短语暴力破解...)
`ruby wpscan.rb - - url www.example.com - - wordlist darkc0de.lst - - username administrator` (仅对 'administrator' 用户名执行词表秘密短语暴力破解...)
`ruby wpscan.rb - - url www.example.com - - count p` (枚举引入的模块...)
`ruby wpscan.rb - - url www.example.com – count` (运行所有识别工具...)

---

## 第十章：数据集利用

- bbqsql
- sqlninja
- sqlsus

### bbqsql

### 描述
盲注 SQL 注入的利用可能非常麻烦。当可用工具工作时它们表现良好，但当它们失效时，你需要编写自定义脚本。这既枯燥又耗时。BBQSQL 可以帮助解决这些问题。

BBQSQL 是一个用 Python 编写的盲注 SQL 注入框架。在攻击脆弱的 SQL 注入漏洞时非常有价值。BBQSQL 还是一个自加载工具，允许对难以触发的 SQL 注入发现进行大量的自定义。该工具设计为数据集逻辑化，且极其灵活。它还具有直观的 UI，使攻击设置变得简单许多。此外实现了 Python gevent，使得 BBQSQL 非常快。

### 使用方法
n/a，手动选择/配置

### 选项
https://github.com/Neohapsis/bbqsql

### 示例
n/a

### sqlninja

### 描述
Sqlninja 是一种用于利用使用 Microsoft SQL Server 作为后端的 Web  SQL 注入漏洞的工具。其基本目标是提供对弱数据库服务器的远程访问，即使在极其不友的环境下。它应被渗透分析师使用，在发现 SQL 注入漏洞后帮助并自动化控制数据库服务器的最常用方法。

### 使用方法
配置和执行通过 `sqlninja.conf` 完成；更多细节请参阅文档

### 选项
http://sqlninja.sourceforge.net/sqlninja-howto.html

### 示例
n/a

### sqlsus

### 描述
sqlsus 是一个开源 MySQL 注入和接管工具。通过命令行界面，你可以恢复数据库结构、注入自己的 SQL 语句（即使是复杂的）、从 Web 服务器下载文档、爬取网站的可写注册表、传输并控制辅助通道、克隆数据库以及更多功能……在任何关键时刻，sqlsus 都会模拟 MySQL 控制台的输出。

更多信息：http://sqlsus.sourceforge.net/

### 使用方法
使用 `sqlsus - genconf my.cfg` 生成配置记录，读取注释并调整以匹配你的目标。运行 `sqlsus` 并将配置作为边界 `sqlsus my.cfg`，即可获得一个 shell。

### 选项
http://sqlsus.sourceforge.net/documentation.html

### 示例
n/a，请查看文档

---

## 第十一章：IDS/IPS 识别

- ua-tester

### ua-tester

### 描述
UATester 是一个 Python 脚本，它要求 Web 服务器提供具有不同客户端代理（User Agent）的页面。通过这些内容，可以快速发现是否存在针对不同客户端的特定页面（例如通用页面、IE 高级页面等）。该设备旨在利用客户端提供的标准和非标准 User Agent 字符串列表（每行一个）来自动检查给定的 URL。这些检查的结果将返回给客户端，以便在需要时进行人工检查。

### 使用方法
`./uatester.py – u<url> [options]`

### 选项
http://packetstormsecurity.com/records/94305/UA-Tester-User-Agent-Tester-1.03.html

### 示例
`./UATester.py - u www.example.com - f ./useragentlist.txt - v`
`./UATester.py - u https://www.wordpress.com`
`./UATester.py - u http://www.defaultserver.com - v - investigate`
`./UATester.py - u facebook.com - v - d MDBX`
`./UATester.py - u https://www.google.com - s "MySpecialUserAgent"`

---

## 第十二章：Web 应用模糊测试器

- burpsuite
- powerfuzzer
- webscarab
- webslayer
- websploit
- wfuzz
- xsser
- zaproxy

### Burpsuite

### 描述
Burp Suite 是一个用于 Web 应用安全测试的集成平台。它的不同工具协同工作，协助整个测试过程，从最初的规划和对应用程序攻击面的分析，到发现和利用安全漏洞。

Burp Suite 包含以下关键部分：
- 一个捕获代理（Proxy），允许你检查并更改程序与目标应用程序之间的流量。
- 一个感知应用程序的爬虫（Spider），用于爬取内容和功能。
- 一个高级 Web 应用扫描器（Scanner），用于自动化识别各种漏洞。
- 一个入侵者工具（Intruder），用于执行强大的自定义攻击以发现并利用意外漏洞。
- 一个 重复器（Repeater），用于控制和重新发送单个请求。
- 一个序列器（Sequencer），用于测试会话令牌的随机性。
- 保存并在稍后继续工作。
- 可扩展性，允许你方便地编写自己的模块，在 Burp 内部执行复杂且高度自定义的任务。

更多信息：http://portswigger.net/burp/

### 使用方法
n/a；GUI 工具

### 示例
n/a；GUI 工具

### Powerfuzzer

### 描述
Powerfuzzer 是一个高度自动化且完全可选的 Web 模糊测试器（基于 HTTP 协议的应用模糊测试器），参考了许多其他可用开源模糊测试器以及来自各种安全资源和网站的数据。它旨在易于使用、现代且有效。

更多信息：http://www.powerfuzzer.com/#news

目前，它可以识别这些问题：
- 跨站脚本 (XSS)
- 注入（SQL, LDAP, 代码, 命令和 XPATH）
- CRLF
- HTTP 500 错误（表明潜在的配置错误/安全缺陷，包括缓冲区溢出）

### 使用方法
n/a；GUI 设备

### 示例
n/a；GUI 设备

### Webscarab

### 描述





### WebScarab

WebScarab 是一种用于调查使用 HTTP 和 HTTPS 协议应用的结构。它用 `Java` 编写，并且对于许多阶段都非常方便。WebScarab 有几种活动方法，由不同的模块执行。在最常用的用法下，WebScarab 作为拦截代理工作，允许管理员在程序发送请求到服务器之前查看并修改请求，并在程序接收来自服务器的响应之前对其审计和更改。WebScarab 可以捕获 HTTP 和 HTTPS 通信。管理员还可以监控通过 WebScarab 的会话（请求和响应）。

更多信息：https://www.owasp.org/index.php/WebScarab_Getting_Started

用法：n/a；GUI 设备

示例：n/a；GUI 设备

### Webslayer

### 描述

WebSlayer 是一种用于驱动 Web 应用程序的工具，它通常用于发现未链接的资源（索引、servlet、脚本等）、强制破解 `GET` 和 `POST` 边界、强制破解结构边界（`用户/密码`）、模糊测试等。该工具具有强大的有效负载生成器和简单且灵活的结果分析器。

更多数据：[`www.owasp.org/index.php/Category:OWASP_Webslayer_Project`](https://www.owasp.org/index.php/Category:OWASP_Webslayer_Project)

用法：n/a；GUI 工具

示例：n/a；GUI 工具

### Websploit

### 描述

WebSploit 用于扫描和调查远程框架以跟踪各种类型的漏洞。该工具非常出色并支持许多漏洞。WebSploit 用于：社会工程攻击、扫描、爬虫和 Web 分析、自动漏洞利用和支持网络攻击。亮点包括：

* `Autopwn` - 来自 `Metasploit` 用于扫描和利用目标服务
* `wmap` - 使用 `Metasploit` `wmap` 模块扫描、爬虫目标
* `design infector` - 在记录设计中注入转向并绑定有效负载
* `phpmyadmin` 扫描器
* `LFI Bypasser`
* `Apache Users` 扫描器
* `Dir Bruter`
* `administrator locater`
* `MLITM Attack` - 人在中间人攻击，XSS 钓鱼攻击
* `MITM` - 人在中间人攻击
* `Java Applet Attack`
* `MFOD Attack Vector`
* `USB Infection Attack`
* `ARP Dos Attack`
* `Web Killer Attack`
* `Counterfeit Update Attack`
* `Counterfeit Access point Attack`

用法：n/a；GUI 设备

示例：n/a；GUI 设备

### Wfuzz

### 描述

Wfuzz 是一种用于强制破解 Web 应用程序的工具，它可以很好地发现未链接的资源（目录、servlet、脚本等）、强制破解 `GET` 和 `POST` 边界以检查不同类型的注入（`SQL`、`XSS`、`LDAP` 等）、强制破解表单边界（`用户/密码`）、模糊测试等。

更多信息：https://code.google.com/p/wfuzz/wiki/Howto

用法：`wfuzz.py [options] [file] [config] [target ip]`

示例：`wfuzz.py - c - z document, wordlists/commons.txt - - hc 404 - R 202 http://www.mysite.com/FUZZ` （路径泄露示例，递归深度为 2）

示例：`wfuzz.py - z file,wordlists/http_methods.txt - X http://testphp.vulnweb.com/(HTTP 策略检查模型)`

示例：`wfuzz.py - z list,TRACE - X http://testphp.vulnweb.com/(使用运行有效负载扫描 TRACE 策略)`

示例：`wfuzz.py - c - z file,wordlists/methods.txt - - hc 404 - v - - follow http://www.mysite.com/FUZZ` （强制破解跟随的 HTTP 重定向）

示例：`wfuzz.py - c - z file,wordlists/commons.txt - - hc 404 - I http://www.mysite.com/FUZZ` （利用 HEAD HTTP 策略强制破解）

示例：`wfuzz.py - z list,http://mysite.com - z list,dir-dir2-dir3 FUZZ/FUZ2Z` （利用 URL 作为有效负载和目录列表进行强制破解）

### Xsser

### 描述

跨站“脚本编写”（也称为 XSSer）是一个用于识别、利用和报告在线应用程序中 XSS 漏洞的程序系统。它包含了一些尝试绕过特定通道的选择以及不同的异常代码注入策略。

用法：`xsser [OPTIONS] [-u |-I |-d ] [-g |-p |-c ] [Request(s)] [Vector(s)] [Bypasser(s)] [Technique(s)] [Final Injection(s)]`

选项：[`xsser.sourceforge.net/`](http://xsser.sourceforge.net/)

示例：`python xsser.py - u http://host.com` （来自 URL 的简单注入）

示例：`python xsser.py - I "file.txt" - - intermediary "http://127.0.0.1:8118" - - referer "666.666.666.666"` （来自文件的简单注入，带有顶级代理并伪造 HTTP Referer 头部）

示例：`python xsser.py - u "http://host.com" - p index.php?target=search&subtarget=top&searchstring=" – s` （来自 URL 的简单注入，利用 POST，带有见解结果）

示例：`python xsser.py - u "http://host.com"` （简单结果）

### Zapxy

### 描述

OWASP Zed Attack Proxy (ZAP) 是一款用于发现 Web 应用程序漏洞的免费开源工具。它旨在供渗透测试初学者以及有经验的专业人士使用。

WEB 应用程序代理

* burpsuite
* paros
* proxystrike
* vega
* webscarab
* zaproxy

用法：n/a；GUI 设备

示例：n/a；GUI 工具



### ProxyStrike

ProxyStrike 是一个功能性的 Web 应用程序代理。它是一个旨在在浏览应用程序时追踪弱点的设备。开发它的理由是：我们在对高度依赖 Javascript 的 Web 应用进行渗透测试时发现，针对这些问题，相对较少的 Web 扫描器在这一阶段表现良好，因此我们开发了这一中间件。目前，它已具备可用的 SQL 注入和 XSS 模块。这两个模块旨在尽可能获取所有弱点，这就是为什么 SQL 注入模块是不可比拟的 DarkRaver "Sqlibf" 的 Python 移植版。交互异常直观，ProxyStrike 自然地运行在端口 8008 上的中间件中，因此你需要查看理想的网站设置，将程序配置为使用 ProxyStrike，随后 ProxyStrike 将会在基础模式下每一个边界。对于客户端来说，它是一个隐性的中间代理，因为你不会看到应用程序的行为有任何异，但在后台它运行非常活跃。

更多信息：[`code.google.com/p/proxystrike`](https://code.google.com/p/proxystrike)

- **用法**: n/a；GUI 工具
- **示例**: n/a；GUI 工具

### Vega

### Description
Vega 是一个测试 Web 应用程序安全的开源平台。Vega 可以帮助你发现和验证 SQL 注入、跨站脚本 (XSS)、意外发现的敏感数据以及其他弱点。

### 亮点：
- 自动化爬虫和漏洞扫描器
- 稳定的 UI
- 站点爬虫
- 拦截代理
- SSL MITM
- 内容分析
- 通过强大的 Javascript 模块 API 扩展
- 可变告报
- 数据库和共享数据模型

- **用法**: n/a；GUI 工具
- **示例**: n/a；GUI 工具

### webscarab

### Description
WebScarab 是一个用于检查使用 HTTP 和 HTTPS 协议应用程序的系统。它用 Java 编写，因此适用于许多阶段。WebScarab 有几种活动方式，由不同的模块执行。在它最常用的用法下，WebScarab 作为一个拦截中间件工作，允许管理员在请求发送到服务器之前检查并修改应用程序提出的请求，并在应用程序获取响应之前审核并更改从服务器返回的响应。WebScarab 可以捕获 HTTP 和 HTTPS 通信。管理员还可以监控通过 WebScarab 的流量（请求和响应）。

更多数据：[`www.owasp.org/index.php/WebScarab_Getting_Started`](https://www.owasp.org/index.php/WebScarab_Getting_Started)

- **用法**: n/a；GUI 设备
- **示例**: n/a；GUI 设备

### Zaproxy

### Description
OWASP Zed Attack Proxy (ZAP) 是一个易用的协同渗透测试工具，用于追踪 Web 应用中的弱点。它旨在供具有广泛安全经验的人员使用，因此对于新渗透测试的设计师和实用分析师来说是丰富的渗透分析人员工具箱的有力扩展。

更多数据：[`code.google.com/p/zaproxy/`](https://code.google.com/p/zaproxy/)

- **用法**: n/a；GUI 设备
- **示例**: n/a；GUI 设备

## 第十四章：WEB 爬虫
- apache-clients
- burpsuite
- cutycapt
- dirb
- dirbuster
- vega
- webscarab
- webslayer
- zaproxy

### apache-users

### Description
apache-users 允许查看服务器用户名目录（如果从 apache Web 服务器使用）允许过滤 apache 客户端列表。该模块对于 WebSploit 工具包非常重要。

- **用法**: n/a
- **示例**: n/a

### Burpsuite

### Description
Burp Suite 是一个用于 Web 应用程序安全测试的集成平台。它的不同工具完美协作工作，帮助整个测试过程，从应用程序攻击表面的初始规划和分析，到发现和利用安全弱点。Burp Suite 包含以下关键部分：

- 拦截代理，允许你评估和调整你的程序与目标应用程序之间的流量。
- 应用程序感知蜘蛛虫 (Spider)，用于爬取内容和功能。
- 高级 Web 应用程序扫描器，用于自动化发现各种弱点。
- 入侵者工具 (Intruder)，用于执行强大的自定义攻击以发现并利用异常弱点。
- 重复器 (Repeater)，用于控制和重新发送单个请求。
- 排序器 (Sequencer)，用于测试会议令牌的随机性。
- 保存工作并在稍后恢复工作的能力。
- 可扩展性，允许你轻松编写自己的模块，在 Burp 内部执行复杂且高度定制的任务。

更多信息：[`portswigger.net/burp/`](http://portswigger.net/burp/)

- **用法**: n/a；GUI 工具
- **示例**: n/a；GUI 设备

### Cutycapt

### Description
CutyCapt 是一个小型跨平台命令行实用程序，用于捕捉 WebKit 将页面渲染为一系列矢量和位图设计，包括 SVG, PDF, PS, PNG, JPEG, TIFF, GIF 和 BMP。

- **用法**: `CutyCapt --url=<target ip> --out=<output file>.<extension>`
- **选项**: [`cutycapt.sourceforge.net/`](http://cutycapt.sourceforge.net/)
- **示例**: `CutyCapt --url=http://www.example.org/ --out=localfile.png`

### 提示：
在没有 X server 使用 CutyCapt：没有 X server 无法使用 CutyCapt，但你可以使用 Xvfb 作为轻量级服务器，假设你没有运行交互式图形工作区环境。

例如，你可以使用：
```
xvfb-run --server-args="-screen 0, 1024x768x24" ./CutyCapt --url=... --out=...
```

### Dirb

### Description
DIRB 是一个 Web 内容扫描器。它搜索现有的（以及隐藏的）Web 对象。它本质上通过对 Web 服务器发送基于字典的攻击并调查响应来工作。DIRB 带有一组预配置的攻击字典列表以便方便使用，但你也可以使用自定义字典列表。此外，DIRB 有时可以用作典型的 CGI 扫描器，但记住——它是一个内容扫描器而不是漏洞扫描器。

更多数据：[`dirb.sourceforge.net/faq.txt`](http://dirb.sourceforge.net/faq.txt)

- **用法**: `dirb <url><your dict file>`
- **示例**: `./dirb http://www.site.com/directory1/wordlist.txt`
- **示例**: `./dirb http://www.site.com/wordlist.txt,dirnamefile.txt`

### Dirbuster

### Description
DirBuster 是一个多线程 Java 应用，旨在暴力破解 Web/应用程序服务器上的目录和文件名。经常当某些看起来处于默认设置状态的 Web 服务器时，实际上——它并不是，并且内部隐藏了页面和应用程序。DirBuster 试图发现这些。

更多信息：[`www.owasp.org/index.php/Category:OWASP_DirBuster_Project`](https://www.owasp.org/index.php/Category:OWASP_DirBuster_Project)

- **用法**: n/a；GUI 工具
- **示例**: n/a；GUI 设备

### Vega
### Description
Vega 是一个测试 Web 应用程序安全的开源平台。Vega 可以帮助你发现和验证 SQL 注入、跨站脚本 (XSS)、意外发现的敏感数据以及其他弱点。

### 亮点：
- 自动化爬虫和漏洞扫描器
- 稳定的 UI
- 站点爬虫
- 拦截代理
- SSL MITM
- 内容分析
- 通过强大的 Javascript 模块 API 扩展
- 可变告报
- 数据库和共享数据模型

- **用法**: n/a；GUI 设备
- **示例**: n/a；GUI 工具

### Webscarab
### Description





### WebScarab

WebScarab 是一个用于调查利用 HTTP 和 HTTPS 协议应用程序的系统。它用 Java 编写，因此适用于许多平台。WebScarab 有几种活动方法，由不同的模块实现。在最常用的用法下，WebScarab 作为一个中间代理，允许管理员在请求发送到服务器之前查看并修改程序提出的请求，并在程序获取来自服务器的响应之前审计并修改。WebScarab 可以拦截 HTTP 和 HTTPS 通信。管理员还可以审计通过 WebScarab 的对话（请求和响应）。

更多数据：[`www.owasp.org/index.php/WebScarab_Getting_Started`](https://www.owasp.org/index.php/WebScarab_Getting_Started)

用法：n/a；GUI 工具

示例：n/a；GUI 工具

### Webslayer

## 

WebSlayer 是一种用于对 Web 应用程序进行强制的工具，通常用于发现隐藏的资源（索引、servlets、脚本等）、强大的 GET 和 POST 边界、强大的结构边界（用户/密码）、模糊测试（fuzzing）等。该工具具有强大的负载生成器和简单灵活的结果分析器。

更多信息：[`www.owasp.org/index.php/Category:OWASP_Webslayer_Project`](https://www.owasp.org/index.php/Category:OWASP_Webslayer_Project)

用法：n/a；GUI 工具

示例：n/a；GUI 工具

### Zaproxy

### 描述

OWASP Zed Attack Proxy (ZAP) 是一个易用的协调入口测试工具，用于跟踪 Web 应用中的漏洞。它旨在供具有广泛安全经验的人员使用，因此非常适合新接触入口测试的工程师和实践分析师，也是资渗透测试人员工具箱的价值扩展。

更多信息：[`code.google.com/p/zaproxy/`](https://code.google.com/p/zaproxy/)

用法：n/a；GUI 工具

示例：n/a；GUI 工具

# 第十五章：WEB 漏洞扫描器

- burpsuite
- zaproxy
- dead body
- davtest
- deblaze
- fimap
- grabber
- joomscan
- nikto
- padbuster
- proxystrike
- skipfish
- sqlmap
- vega
- w3af
- wapiti
- webscarab
- webshag-cli
- webshaggui
- websploit
- wpscan
- xsser

### Burpsuite

### 描述

Burp Suite 是一个执行 Web 应用程序安全测试的协调平台。它的不同工具协同工作，帮助整个测试过程，从最初的规划和应用程序攻击面的检查到发现和利用安全漏洞。Burp Suite 包含以下关键部分：

- 一个拦截代理（Proxy），允许你查看和修改程序与目标应用程序之间的流量。
- 一个感知应用的蜘蛛虫（Spider），用于爬取内容和功能。
- 一个高级 Web 应用扫描器，用于自动化发现各种漏洞。
- 一个入侵者工具（Intruder），用于执行强大的重复攻击以发现并利用异常漏洞。
- 一个 重复器（Repeater），用于控制和重新发送单个请求。
- 一个序列器（Sequencer），用于测试会话令牌的随机性。
- 保存工作并在后恢复工作的能力。
- 可扩展性，允许你有效地编写自己的模块，在 Burp 内部执行复杂且极其自定义的任务。

更多数据：[`portswigger.net/burp/`](http://portswigger.net/burp/)

用法：n/a；GUI 设备

示例：n/a；GUI 工具

### Corp

### 描述

corpse 是 Unix 的命令行 WebDAV 客户端。它支持文档传输、下载、在线显示、命名空间活动（移动/复制）、集合创建和删除以及锁定任务。

用法：`./dead body xxx.xxx.xxx.xxx`

使用 `dead body [-et][-V][-h] http://hostname[:port]/way`

选项：[`linux.die.net/man/1/corpse`](http://linux.die.net/man/1/corpse)

示例：`corpse http://dav.example.com/`（连接到服务器 myserver.example.com，打开根集合）

示例：`corpse http://zope.example.com:8022/Users/fred/`（连接到服务器 zope.example.com，使用端口 8022，打开集合 "/Users/fred/"）

示例：`corpse https://secure.example.com/`（使用 SSL 连接到名为 secure.example.com 的服务器）

提示：`~/.cadaverrc` 可以覆盖 corpse 默认值的个人客户端设置。

### Davtest

### 描述

DAVTest 通过传输测试可执行记录来测试 WebDAV 授权服务器，然后（可选）直接在目标上传输考虑顺序执行或不同活动的文档。亮点

- 在代码执行的情况下，自然发送漏洞记录
- 程序化的目录随机化以助于利用 `MKCOL` 隐藏记录
- 发送消息文档并尝试 `MOVE` 到可执行名称
- 基础和摘要 认证
- 对传输的文档进行程序清理
- 发送任意记录

用法：`davtest.pl – url<url> [options]`

选项：[`code.google.com/p/davtest/wiki/Usage`](https://code.google.com/p/davtest/wiki/Usage)

示例：`davtest.pl - url http://localhost/davdir`（测试此区域的文档传输）

示例：`davtest.pl - url http://localhost/davdir - sendbd auto`（测试此区域的文档传输，并对任何有效执行的发送二次记录）

示例：`davtest.pl - url http://localhost/davdir - auth user:pass - uploadfile secondary passages/perl_cmd.pl - uploadloc perl.pl`（使用验证传输记录，发送 perl_cmd.pl 间接访问并在服务器上调用其 perl.pl）

# Deblaze

### 描述

deblaze 是用于 flex 服务器的远程策略识别工具。该工具允许你对远程远程端点执行技术规范和交叉检查。deblaze 提供了以下功能：暴力破解和服务方法名称、方法查询、Flex 技术指纹识别、参数定位、基础边界模糊、代理 AMF 请求/响应、HTML 提取。

用法：`deblaze [option]`

选项：[`deblaze-tool.appspot.com/utilization`](http://deblaze-tool.appspot.com/utilization)

示例：`deBlaze.py - u http://192.168.165.132:8080/amfphp/gateway.php - s securityService - m sendEmail - p test@test.com`

示例：`python2.5 deblaze-0.3.py - P 8080:targetIP:targetPort`

示例：`python deBlaze.py - u http://192.168.165.132:8080/amfphp/gateway.php - s Discoveryservice - m getServices`

示例：`python deBlaze.py - u http://192.168.165.132:8400/examples/messagebroker/qosamfpolling - 1 names.txt - m test`

### Fimap

### 描述

fimap 是一个微小的 python 工具，可以发现、规划、审查、利用甚至 google 搜索 Web 应用中的本地和远程文件包含问题。fimap 应该类似于 sqlmap，但针对 LFI/RFI 问题而不是 SQL 注入。fimap 的目标是提高网站的质量和安全性。更多信息：https://code.google.com/p/fimap

用法：`./fimap.py [options]` 选项 https://code.google.com/p/fimap/wiki/FimapHelpPage

示例：`fimap - u http://localhost/vulnerable.php?inc=index.php`

示例：`./fimap.py - u 'http://localhost/vulnerable.php?file=bang&id=23'`（扫描单个 URL 的 FI 错误）示例：./fimap.py - m - l '/tmp/urllist.txt'`（扫描 URL 列表的 FI 错误）示例：./fimap.py - g - q 'inurl:include.php'`（扫描 Google 索引列表的 FI 错误）示例：./fimap.py - H - u 'http://localhost' - d 3 - w/tmp/urllist`（采集页面的所有连接，递归深度为 3，并将 URL 写入到/tmp/urllist）

### Grabber

### 描述





# Grabber 是一个 Web 应用扫描器。本质上，它能够识别你网站中的某些漏洞。Grabber 非常直观，虽然不够，但非常紧凑且功能多变。该产品旨在检查小型网站，如个人博客、讨论组等，绝不是用于大型应用程序：那将花费大量时间并让你的组织瘫痪。

### 亮点
- 跨站脚本 (Cross-Site Scripting)
- SQL 注入（同样有一个不常用的盲注 SQL 注入模块）
- 记录包含 (Record Inclusion)
- 强化记录检查
- 基础 AJAX 检查（解析每个 JavaScript 并获取 URL，尝试获取边界）
- 利用 `PHP-SAT` 对 PHP 应用进行交叉调查/水晶球测试
- JavaScript 源代码分析：使用 `JavaScript Lint` 评估 JavaScript 的质量/准确性
- 记录 `[session_id, time(t)]` 的时长，用于后续详细调查。

### 使用方法
`grabber.py [options]`

### 参数
`http://www.securitytube-tools.net/index.php@title=Grabber.html`

### 示例
`read: http://rgaucher.info/beta/grabber/`

### Joomscan

## 
joomscan 可以识别目标 Joomla! 站点的文档、SQL 注入、命令执行漏洞。

### 亮点
- 精确表单探测（扫描器可以确定目标是否运行 1.5.12 版本）
- 常规基于 Joomla! Web 应用防火墙发现
- 查找 Joomla! 及其部分的已知漏洞
- 文本和 HTML 输出
- 通过扫描器或 svn 快速更新能力

### 使用方法
`joomscan.pl - u - x proxy:port`

### 参数
`https://www.owasp.org/index.php/OWASP_Joomla_Vulnerability_Scanner_Usage`

### 示例
`joomscan.pl - pv - u victim.com - x localhost:8080`
`joomscan.pl read DOCFILE`（其中 `DOCFILE` 是以下文件之一：`changelog,release_note,readme,credits,faq,owasp_project`）

### Nikto

## 
Nikto 是一个 Web 服务器扫描器，能够对 Web 服务器进行长时间的大量测试，包括 6500 多个潜在风险记录/CGI，检查超过 1250 多个服务器的过时变，并对 270 多个服务器呈现显式问题。它还会检查服务器配置项，例如各种列表记录的存在、HTTP 服务器选项，并尝试识别引入的 Web 服务器和编程。扫描项目和插件经常更新，并可以自动更新。

### 使用方法
`nikto.pl [host] [target] [options]`

### 参数
`http://cirt.net/nikto2-docs/options.html`

### 示例
`nikto.pl - h 192.168.0.1 - T 58`（检查调整）
`nmap - p80 192.168.0.0/24 - oG - | nikto.pl - h -`（多主机测试）
`nikto.pl - h 192.168.0.1 - p 80,88,443`（多端口测试）
`nikto.pl - h https://192.168.0.1:443/`（基础测试并利用完整 URL 结构）
`nikto.pl - h 192.168.0.1 - p 443`（专门查看特定端口）

### Padbuster

## 
PadBuster - 用于执行填充 Oracle（Padding Oracle）攻击的自动化内容工具。PadBuster 提供了解码自断言密文、编码任意明文以及执行计算机化反应检查的能力，以判断请求对填充 Oracle 攻击是否无效。更多信息和使用方法：`http://blog.gdssecurity.com/labs/2010/9/14/robotized-cushioning-oracleattacks-with-padbuster.html` 和 `http://howtohack.poly.edu/wiki/Padding_Oracle_Attack`

### 使用方法
`padBuster.pl<url><encrypted sample><block size><encoding>`

### 示例
`padBuster.pl http://sampleapp/home.jsp?UID=7B216A634951170FF851D6CC68FC9537858795A28ED4AAC6 7B216A634951170FF851D6CC68FC9537858795A28ED4AAC6 8 - encoding 2`
`padBuster.pl http://sampleapp/home.jsp?UID=7B216A634951170FF851D6CC68FC9537858795A28ED4AAC6 7B216A634951170FF851D6CC68FC9537858795A28ED4AAC6 8 - encoding 2 - plaintext "Scramble TEST"`

### Proxystrike

## 
ProxyStrike 是一个功能性的 Web 应用代理。它是一个旨在浏览应用程序时追踪漏洞的工具。它的开发背景是因为我们在高度依赖 JavaScript 的 Web 应用渗透测试中发现问题时，很少有 Web 扫描器在这一阶段做得很好，因此我们开发了这个中间件。目前它拥有可用的 SQL 注入和 XSS 模块。两个模块都旨在获取尽可能多的漏洞，这就是为什么 SQL 注入模块是无与伦比的 DarkRaver `Sqlibf` 的 Python 端口。交互非常简单，ProxyStrike 像中间代理一样运行在 8008 端口，因此你需要查理想站点设置你的程序使用 ProxyStrike 作为代理，ProxyStrike 将以基础模式解析每一个边界。对于客户端来说，这是一个独立的代理，因为你不会看到应用程序行为有任何变化，但在背后极其动态。

更多信息：`https://code.google.com/p/proxystrike`

### 使用方法
`n/a; GUI 设备`

### 示例
`n/a; GUI 设备`

### Skipfish

## 
Skipfish 是一个功能性的 Web 应用安全监控工具。它通过递归爬取和基于字典的测试为指定站点准备直观的站点地图。随后通过各种动态（理想情况下无害）安全检查的结果生成说明指南。该工具创建的最后报告旨在为 Web 应用安全评估提供基础。

### 使用方法
`./skipfish [options] - o output_dir @/way/to/url_list.txt`

### 参数
`https://code.google.com/p/skipfish/wiki/SkipfishDoc`

### 示例
`./skipfish - o output_dir - S existing_dictionary.wl - W new_dict.wl \ http://www.example.com/a few/beginning/path.txt`
`./skipfish - D test2.example.com - o yield dir http://test1.example.com/`
`./skipfish – D ./skipfish - MEU - S word references/minimal.wl - W new_dict.wl \ - C "AuthCookie=value" - X/logout.aspx - o output_dir \ http://www.example.com/.example.com - o yield dir http://test1.example.com/`

### Sqlmap

## 
sqlmap 是一个开源渗透测试工具，自动化了识别和利用 SQL 注入漏洞以及接管数据库服务器的方法。它配备了强大的发现引擎、许多针对确定渗透分析的特殊功能，以及广泛的开关，从数据库指纹、获取数据库信息到访问基本文件系统以及通过带外连接在运行的操作系统上执行命令。

### 使用方法
`sqlmap.py [options]`

### 参数
`https://github.com/sqlmapproject/sqlmap/wiki/Usage`

### 示例
`sqlmap.py - u "http://www.target.com/vuln.php?id=1" - f - - standard - - dbs – clients`（针对单一目标 URL 运行 sqlmap）
`sqlmap.py - g "inurl:\".php?id=1\""`（根据你的 Google 搜索结果测试并注入依赖 GET 边界）
`sqlmap.py - u "http://www.target.com/vuln.php" - - data="id=1" - f - - standard - - dbs - - clients`（追踪 POST 请求）
`sqlmap.py - u "http://192.168.136.131/sqlmap/mysql/fundamental/get_int.php?id=1" \ - - auth-type Basic - - auth-cred "testuser:testpass"`（HTTP 验证）
`sqlmap.py - l burp.log - - scope="(www)?\.target\.(com|net|org)"`（使用自定义表达式从中间日志中过滤焦点）

### Vega

## 
Vega 是一个测试 Web 应用安全的开源工具。Vega 可以帮助你发现 SQL 注入、跨站脚本 (XSS)、无意暴露的敏感数据以及不同的漏洞。

### 亮点





### w3af

- 机器人爬虫与漏洞扫描器
- 可预测的 UI
- 站点爬虫
- 捕获代理
- SSL MITM
- 内容分析
- 通过强大的 Javascript 模块 API 实现扩展性
- 自适应告警
- 信息库和共享数据模型

**用法**: `n/a; GUI 设备`
**示例**: `n/a; GUI 设备`

### 描述
`w3af` 是一个 Web 应用攻击和审计框架。该项目为 Web 应用提供了漏洞扫描器和滥用工具。它提供了有关安全漏洞的数据并帮助渗透测试工作。w3af 利用超过 130 个模块识别大多数 Web 应用漏洞。在识别后，如（盲注）SQL 注入、操作系统信息、远程文件包含 (PHP)、跨站脚本 (XSS) 和危险文件传输等漏洞可以被利用以获取远程系统的各种访问权限。更多信息：http://w3af.org/

**用法**: `n/a; GUI 设备`
**示例**: `n/a; GUI 设备`

### Wapiti

### 描述
`Wapiti` 允许你审查 Web 应用的安全性。它执行“发现”过滤，例如它不关注应用程序的源代码，而是检查所交付 Web 应用的页面，搜索可以注入信息的内容和结构。当获取此列表后，`Wapiti` 的行为就像一个模糊器（fuzzer），通过注入有效负载来检查内容是否没有防御。`Wapiti` 可以识别以下漏洞：

- 文件处理错误（本地和远程包含/引入，`fopen`, `readfile`...）
- 数据注入（PHP/JSP/ASP SQL 注入和 XPath 注入）
- XSS（跨站脚本）注入
- LDAP 注入
- 命令执行识别 (`eval()`, `framework()`, `passtru()`...)
- CRLF 注入（HTTP 响应拆分，会话固定...)

**用法**: `python wapiti.py http://server.com/base/url/[options]`
**选项**: http://wapiti.sourceforge.net/
**示例**: `python wapiti.py http://127.0.0.1/vuln/ - c cookies.txt - x http://127.0.0.1/vuln/index.php?page=logout

### Webscarab

### 描述
`WebScarab` 是一个调查使用 HTTP 和 HTTPS 协议传输的应用的系统。它用 Java 编写，因此适用于许多平台。`WebScarab` 有由不同模块执行的活动方法。在最常用的情况下，`WebScarab` 作为一个捕获中间件，允许管理员在请求发送到服务器之前审查并调整程序提出的请求，并在程序接收来自服务器的响应之前进行审计和修改。`WebScarab` 可以同时捕获 HTTP 和 HTTPS 通信。管理员还可以审查通过 `WebScarab` 的对话（请求和响应）。

更多信息：https://www.owasp.org/index.php/WebScarab_Getting_Started

**用法**: `n/a; GUI 工具`
**示例**: `n/a; GUI 工具`

### webshag-cli

### 描述
`Webshag` 是一个多线程、多阶段的 Web 服务器审查工具。用 Python 编写，收集了许多 Web 服务器评估的功能，如站点爬取、URL 过滤或记录抓取。`Webshag` 可通过中间件并使用 HTTP 验证（Basic 和 Digest）来检查 HTTP 或 HTTPS 下的 Web 服务器。尽管它提出了创新的 IDS 规避功能，使连接之间的请求更加复杂（例如使用交替的任意请求 HTTP 中间服务器）。`webshag` 的普通功能是：

- 端口扫描
- Web 爬虫
- Url 扫描
- 恢复域名列表
- 记录抓取

更多信息：http://www.scrt.ch/en/assault/downloads/webshag

**用法**: `./webshag-cli - m pscan < target-ip >`
**用法**: `./webshag_cli.py - m bug - p 80/< target-ip >`
**示例**: `./webshag_cli.py - m uscan - x - o html - f '/root/Desktop/hackingDNA.html'`

### webshag-gui

### 描述
`Webshag` 是一个多线程、多阶段的 Web 服务器审查设备。用 Python 编写，收集了许多 Web 服务器评估的功能，如站点爬取、URL 检查或记录抓取。`Webshag` 可通过中间件并使用 HTTP 验证（Basic 和 Digest）来检查 HTTP 或 HTTPS 下的 Web 服务器。尽管它提出了创新的 IDS 规避功能，使连接之间的请求更加复杂（例如使用交替的任意每个请求 HTTP 中间服务器）。`webshag` 的普通功能是：

- 端口扫描
- Web 爬虫
- Url 扫描
- 恢复域名列表
- 记录抓取

更多信息：http://www.scrt.ch/en/assault/downloads/webshag

**用法**: `n/a; GUI 工具`
**示例**: `n/a; GUI 工具`

### Websploit

### 描述
`WebSploit` 用于扫描和检查远程系统以追踪各种漏洞。该工具非常出色并支持多种漏洞。`WebSploit` 用于：社会工程攻击、扫描、爬虫和 Web 分析、自动利用器和支持网络攻击。

亮点：
- Autopwn - 继承 Metasploit 用于扫描和利用目标服务
- wmap - 来自 Metasploit wmap 模块的扫描、爬虫目标使用
- design infector - 将开关和绑定负载注入到文件设计中
- phpmyadmin 扫描器
- LFI 绕过
- Apache 用户扫描器
- 目录暴力破解
- 管理员定位器
- MLITM 攻击 - 人在中间，XSS 钓鱼攻击
- MITM - 中间人攻击
- Java Applet 攻击
- MFOD 攻击向量
- USB 感染攻击
- ARP Dos 攻击
- Web Killer 攻击
- 伪造更新攻击
- 伪造访问点攻击

**用法**: `n/a; GUI 设备`
**示例**: `n/a; GUI 工具`

### wpscan

### 描述
`WPScan` 是一个 WordPress 漏洞扫描器。

**用法**: `wpscan.rb – url [target ip] [options]`
**选项**: [http://wpscan.org/]
**示例**: `ruby wpscan.rb - - url www.example.com` (执行“无干扰”检查...)
**示例**: `ruby wpscan.rb - - url www.example.com - - wordlist darkc0de.lst - - strings 50` (在计数的客户端上使用 50 个线程对词表密钥野兽力量...)
**示例**: `ruby wpscan.rb - - url www.example.com - - wordlist darkc0de.lst - - username administrator` (仅对 'administrator' 用户名执行词表密钥野兽力量...)
**示例**: `ruby wpscan.rb - - url www.example.com - - list p` (列出引入的模块... )
**示例**: `ruby wpscan.rb - - url www.example.com – list` (运行所有计数工具...)

### xsser

### 描述
跨站“脚本编写器”（也称为 `XSSer`）是一个程序化结构，用于识别、利用和报告电子应用程序中的 XSS 漏洞。它包含了一些尝试绕过特定通道的选项，以及不同的代码注入策略。

**用法**: `xsser [OPTIONS] [-u |-I |-d ] [-g |-p |-c ] [Request(s)] [Vector(s)] [Bypasser(s)] [Technique(s)] [Final Injection(s)]`
**选项**: [http://xsser.sourceforge.net/]
**示例**: `python xsser.py - u http://host.com` (从 URL 注入)
**示例**: `python xsser.py - I "file.txt" - - intermediary "http://127.0.0.1:8118" - - referer "666.666.666.666"` (从文件注入，带有顶级中间件并伪造 HTTP Referer 头)
**示例**: `python xsser.py - u "http://host.com" - p index.php?target=search&subtarget=top&searchstring=" – s` (从 URL 注入，使用 POST，带有结果结果)
**示例**: `python xsser.py - u "host.com" – hash` (发送一个预查看哈希以检查目标是否会产生 虚假阳性结果)

### Zaproxy

### 描述





OWASP 攻击代理 (ZAP) 是一款简单易于使用的协调渗透测试工具，用于跟踪 Web 应用程序中的漏洞。它旨在供具有广泛安全经验的人员使用，因此非常适合新手渗透测试的设计师和实践分析师，同时也是资深渗透分析师工具包的宝贵扩展。更多信息：https://code.google.com/p/zaproxy/

用法：n/a；GUI 工具

示例：n/a；GUI 工具

# 第六章

## 密语攻击：GPU 工具

* `oclhashcat-light`
* `oclhashcat-plus`
* `pyrit`

### oclhashcat-light

### 描述
`oclhashcat-light` – 世界最快的 NTLM、MD5、SHA1、SHA256 和解密盐工具。`oclHashcat-light` 是一个针对破解增强的 GPGPU 工具。因此，它仅限于字典攻击、暴力破解和掩码攻击进行单哈破解。

用法：`oclhashcat-light [options]... hash [mask]` 参数 http://hashcat.net/wiki/doku.php?id=oclhashcat_lite

示例：`./oclHashcat-lite64.bin 9b957cc6ab97cbf88c4f6f0f146adafe`
示例：`./oclHashcat-lite64 - m 1900 - n 80 - 1 00010203040506070809 - - outfile=out.txt 21B1E417AF2DE6496772BCC2FE33D2593A9BB7A0:003515230478373400 ?1?1?1?1?1?1?1?1?1?1?1?1?1?1?1`
示例：`./oclHashcat-lite64.bin - m 1900 - n 800 - 1 00010203040506070809 - - outfile=351514044968571.txt - - session=35151404496857_1 514D1FCDE9231B61DAD191F7BC7675B87D8628B5:003515140449685700 ?1?1?1?1?1?1?1?1?1?1?1?1?1?1?1`
示例：`./oclHashcat-lite64.bin - m 1900 - n 800 - 1 00010203040506070809 - - outfile=355933045509554.txt - - session=35593304550955_1 B928680D8D7B1242BEBC8B7AC24FF2B90198E213:003559330455095500 ?1?1?1?1?1?1?1?1?1?1?1?1?1?1?1`

### oclhashcat-plus

### 描述
`oclhashcat-plus` - 世界最快的 md5crypt、phpass、mscash2 和 WPA/WPA2 盐工具，以及世界上唯一的基于 GPGPU 的标准引擎。`oclHashcat-in` 是基于 GPGPU 的多哈盐工具，利用了暴力攻击（作为掩护攻击执行）、组合攻击、字典引用攻击、半血种攻击、面纱攻击和基于规则的攻击。

用法：`oclhashcat-plus [options]... hash|hashfile|hccapfile [dictionary|mask|directory]...`

参数：http://hashcat.net/wiki/doku.php?id=oclhashcat_plus

示例：`oclhashcat-plus64.exe - m 2500 capture.hccap rockyou.txt`（字典攻击）
示例：`oclhashcat-plus64.exe - m 2500 - a3 capture.hccap ?d?d?d?d?d?d?d?d`（暴力攻击）
示例：`oclHashcat-plus64.exe - m 2500 - r rules/best64.rule capture.hccap rockyou.txt`（基于规则的攻击）

### pyrit

### 描述
`Pyrit` 允许创建巨大的数据集，在时空权衡中对 IEEE 802.11 WPA/WPA2-PSK 验证工作进行部分预。利用 ATI-Stream、Nvidia CUDA 和 `OpenCL` 通过多核及不同阶段的计算能力，它是目前针对全球使用最广泛的安全协议之一最强大的攻击工具。

用法：`pyrit [options] order`

参数：[https://code.google.com/p/pyrit/wiki/ReferenceManual]

示例：`pyrit - e NETGEAR confirm`
示例：`pyrit - r/temp/kismet_dump - o small_dump.pcap stripLive`
示例：`pyrit - r "large_dumps_*.pcap" - e MyNetwork - o tiny_compressed_dump_MyNetwork.dump.gz strip`
示例：`pyrit - r test.pcap - b 00:de:ad:be:ef:00 - I words.txt attack_passthrough`
示例：`pyrit - I dirty_words.txt.gz - e NETGEAR - o - passthrough | cowpatty - d - - r wpatestcapture.cap - s NETGEAR`
示例：`pyrit - u sqlite:////var/nearby/pyrit.db hand-off`
示例：`pyrit - u http://192.168.0.100:17934 group`

# 第十七章

## 离线攻击

* `cachedump`
* `chntpw`
* `cmospwd`
* `crunch`
* `dictstat`
* `hashcat`
* `hash-identifier`
* `john the ripper`
* `johnny`
* `lsadump`
* `oclhashcat-light`
* `oclhashcat-plus`
* `ophcrack`
* `ophcrack-cli`
* `policygen`
* `pwdump`
* `pyrit`
* `rainbowcrack`
* `rcracki_mt`
* `rsmangler`
* `samdump2`
* `sipcrack`
* `sucrack`
* `truecrack`

### cachedump

### 描述
`Cachedump` 特别适用于从 XP 机器恢复保留的 Active Directory 凭据。`CacheDump` 将创建一个 `CacheDump NT Service` 以获取 `SYSTEM` 权限并将其存入库中。随后，它将恢复 `LSA Cipher Key` 以解码(`rc4/hmac_md5 GloubiBoulga`) 存储的条目。已创建一个 `John The Ripper` 模块来攻击恢复的哈希值（计时与 `MD4( MD4( password|U(username) ) )` 相同）。

用法：如果你需要固定 John The Ripper，那么执行 `./john - format:mscash file.txt`

参数：[https://github.com/mcandre/fgdump/tree/ace/cachedump]

示例：`Cachedump: c:\cachedump.exe user:2d9f0b052932ad18b87f315641921cda:lab:lab.internal`

将结果复制到 `mscash.txt` 中

`c:\cachedump.exe – v`

未找到管理员。引入 CacheDump 服务 (`C:\cachedump.exe - s`)。CacheDump 管理已成功引入。管理开始。user:2d9f0b052932ad18b87f315641921cda:lab:lab.internals 服务当前动态。停止帮助... 管理已成功消除。John 插件：

```
./john - format:mscash ./mscash.txt
```
加载了 1 个密码哈希 (M$ Cache Hash [mscash]) 密码 (client)

### chntpw

### 描述
`chntpw` 是用于恢复 Windows 密码的卓越工具。`chntpw` 是一个 Linux 工具，用于重置 WinNT 或 Win2000 账户的密码，通过调整库中的加密密钥来设置 加密文件中的任何密码。在 SAM 数据库中工作。`chntpw` 工具。

用法：`chntpw [options] <systemfile> [securityfile]`

参数：`chntpw - h`（帮助）

示例：`Cachedump: c:\cachedump.exe user:2d9f0b052932ad18b87f315641921cda:lab:lab.internal`

### cmospwd

### 描述
`CmosPwd` 是一个 cmos 配置恢复工具。更多数据：http://www.cgsecurity.org/cmosp.txt

用法：`cmospwd [/d]`
用法：`cmospwd [/rlw] cmos_backup`
用法：`cmospwd/m0101`（执行）

### crunch

### 描述
`crunch` 是一个用于创建暴力破解字典列表的设备，用于检查密码强度。这些字典列表的大小并不小，但 `crunch` 可以利用示例缩小列表大小，并（从 2.6 版本起）目前包含有关将创建的列表大小的消息，如果大小对你来说太大，将提供 3 秒钟窗口来停止创建。

用法：`crunch [min length] [max length] [ character set] [options]`

示例：`./crunch [min length] [max length] [character set] [options] - o filename.txt`（写入记录）
示例：`crunch 8 8 abc + + \!\@\# - t TEST^%,@ - o test.txt`
示例：`crunch 1 1 - p bird feline canine`（创建单词组合）
示例：`crunch 6 6 0123456789ABCDEF`
示例：`./crunch 6 6 ABC\!\@\#\$`
示例：`crunch 6 6 0123456789 - b 1mb - o START`（按特定大小列表）
示例：`crunch 8 8 abcDEF123 - b 100mb - o START`（制作接近 100mb 的拆分列表）
示例：`crunch 6 6 0123456789 - c 200000 - o START`（创建接近 200000 行的记录）





示例：./crunch "123abcDEF " - t TEST@@@@`（记得在字符集中留一个空格，然后用引号包裹字符集）

### Dictstat

### 描述
`dictstat` Python 脚本是一个非常实用的工具，用于破解密码的结果检查或标准词列表调查。

更多数据：http://www.question-defense.com/2012/12/16/dictstat-backtrack-5-privilegeescalation-secret-phrase-disconnected-disconnected-dictstat

### 使用
`dictstat.py [options] passwords.txt`

### 选项
- `-variant`: 显示程序的适配版本并退出
- `-h`, `- -`: 显示帮助信息并退出
- `-l 8`, `- -`: 长度=8。密码长度通道
- `-c loweralpha`, `- -`: 字符集=loweralpha。密码字符集通道
- `-m stringdigit`, `- -`: 掩码=stringdigit。密码掩码通道
- `-o masks.csv`, `- -`: 输出掩码=masks.csv。将掩码保存到记录

### 示例
- 示例：./dictstat.py/root/wordlists/500-most noticeably terrible passwords.txt`
- 示例：./dictstat.py -l 4/root/wordlists/500-most noticeably terrible passwords.txt`（密码长度过滤）
- 示例：./dictstat.py -c numeric/root/wordlists/500-most noticeably terrible passwords.txt`（密码字符集过滤）
- 示例：./dictstat.py -m stringdigit -o stringdigit.txt/root/wordlists/500-most noticeably terrible passwords.txt`（密码掩码过滤）

### Hashcat

### 描述
`Hashcat` 是世界上最快的基于 CPU 的密钥恢复工具。虽然它没有它的 GPU 兄弟 `oclHashcat` 以及 `oclHashcat-light` 那么快，但通过良好的字典引用和对切换顺序的了解，可以轻松地将巨大的记录一分为二。

### 使用
`hashcat [options] hashfile [mask|wordfiles|directories]`

### 选项
http://hashcat.net/wiki/doku.php?id=hashcat

### 示例
- 示例：`hashcat-cli64.exe -a 3 – bf-cs-buf abcdefghijklmnopqrstuvwxyz – bf-pw-max 16 -m 0 – o yourfoundpasswords.txt -n 4 – eliminate yourhashlist.txt`（暴力破解）
- 示例：`hashcat-cli64.exe -a 0 -m 0 -o yourfoundpasswords.txt -n 4 – eliminate yourhashlist.txt C:\yourwordlist.txt`
- 示例：`hashcat-cli64.exe -a 0 -r rules\best64.rule -m 0 -o yourfoundpasswords.txt -n 4 – eliminate yourhashlist.txt C:\yourwordlist.txt`（规则）

### hash-identifier

### 描述
`hash-identifier` 是一款用于识别用于编码信息（特别是密码）的各种哈希的产品。更多数据：https://code.google.com/p/hash-identifier/

### 使用
输入你的哈希并获取可能性最大和最小的哈希类型

### 示例
启动程序：
```
python ./Hash_ID_v1.1.py
```
输入你的哈希：
```
e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855
```

### john the ripper

### 描述
`John the Ripper` (`JTR`) 是一个免费的密钥破解程序。它是最著名的密码测试和破解程序之一，因为它将各种密码盐值组合在一起，自动检测密钥哈希类型，并包含可调的规则。它可以很好地针对不同的杂乱密钥排列运行，包括不同 Unix 发行版中常见的几种密码哈希类型（考虑到 DES、MD5 或 Blowfish）、Kerberos AFS 以及 Windows NT/2000/XP/2003 LM 哈希。额外的模块扩展了它整合基于 MD4 的密钥哈希以及存储在 LDAP、MySQL 等处的密码的能力。

### 使用
`john [OPTIONS] [PASSWORD-FILES]`

### 选项
[http://www.osix.net/modules/article/?id=455]

### 示例
保存用户：`gyuJo098KkLy9` 到 `crackme.txt`
然后，使用任何帮助选项运行 `john`：
- `john -single crackme.txt`（单次破解模式）
- `john -wordfile:password.lst crackme.txt`（字典攻击）
- `john -incremental:alpha crackme.txt`（仅字母；稳进策略）
- `john -incremental:digits crackme.txt`（仅数字；稳进策略）
- `john -incremental:lanman crackme.txt`（字母、数字和一些特殊字符；渐进技术）
- `john -incremental:all crackme.txt`（所有字符；渐进策略）

### Johnny

### 描述
`Johnny` 是 `John the Ripper` 的图形界面。
所有基本功能运行良好：
- 通过剪贴板输出破解密码，
- 与办公套件协作（测试过 LibreOffice Calc），
- 客户端可以开始、暂停和恢复攻击（尽管全球范围内仅允许单个会议），
- 所有与攻击相关的选项均可工作，
- 所有的信息文档设计均保留（原始哈希、pwdump、passwd、混合），
- “明智”默认选项，
- 破解密码的精确结果，
- 工作流畅，例如没有卡顿，
- 配置是，例如没有。

### lsadump

### 描述
`lsadump` 是一个从 SAM 数据库提取 Windows 哈希的工具。





### Ophcrack

Ophcrack 是一款免费的开源（GPL 授权）程序，通过利用 LM 彩虹表破解 Windows 密码。该程序具备从各种配置导入哈希的能力，包括直接从 Windows 的 SAM 记录中卸载。在大多数 PC 上，`ophcrack` 可以在几秒内破解破解密码。假设你引入了 `ophrack-cli` 软件包，则无法访问图形界面。

用法：`ophcrack [options]`

选项：`[http://dev.man-online.org/man1/ophcrack-cli/]`

选项：`ophcrack - h`

示例：`ophcrack - g - d/way/to/tables - t xp_free_fast,0,3:vista_free - f in.txt` （在命令行中使用 `/way/to/tables/xp_free_fast` 中的表 0 和 3 以及 `/way/to/tables/vista_free` 中的所有表启动 `ophcrack`，并破解 `in.txt` 文件中的哈希）

### Policygen

### 描述
`PolicyGenerator` 根据指定的访问向量的权限，创建另一个策略模块或更新当前模块。它产生许可规则，以及模块需求声明和策略接口。默认情况下仅创建许可规则。`PolicyGenerator` 还可以根据产生该条目的审核消息，额外添加注释以说明为何允许特定的访问。

用法：`n/a`

示例：`n/a`

### Pwdump

### 描述
`pwdump` 用于导出 Windows 密钥哈希。`pwdump` 是不同 Windows 程序的名称，这些程序可以从安全账户管理器 (`SAM`) 生成本地客户端账户的 LM 和 NTLM 密钥哈希。要运行它，必须在管理员账户下运行，或者拥有访问要卸载哈希的 PC 上的管理员账户的权限。可以说 `Pwdump` 的使用是非常谨慎的，因为它可能允许怀意的管理员访问客户端的密码。

更多信息：`[http://www.foofus.net/~fizzgig/pwdump/]`

用法：`n/a`

示例：`pwdump - u AnAdministrativeUser [-p password] 192.168.0.10`

### Pyrit

### 描述
`Pyrit` 允许通过空间换时间的方法逐步预注册 IEEE 802.11 WPA/WPA2-PSK 验证，创建巨大的数据库。利用多核处理器以及通过 `ATI-Stream`、`Nvidia CUDA` 和 `OpenCL` 的计算能力，它是目前针对全球最广泛安全协议之一最强大的攻击工具。

用法：`pyrit [options] order`

选项：`[https://code.google.com/p/pyrit/wiki/ReferenceManual]`

示例：`pyrit - e NETGEAR confirm`

示例：`pyrit - r/temp/kismet_dump - o small_dump.pcap stripLive`

示例：`pyrit - r "large_dumps_*.pcap" - e MyNetwork - o tiny_compressed_dump_MyNetwork.dump.gz strip`

示例：`pyrit - r test.pcap - b 00:de:ad:be:ef:00 - I words.txt attack_passthrough`

示例：`pyrit - I dirty_words.txt.gz - e NETGEAR - o - passthrough | cowpatty - d - - r wpatestcapture.cap - s NETGEAR`

示例：`pyrit - u sqlite:////var/nearby/pyrit.db hand-off`

示例：`pyrit - u http://192.168.0.100:17934 bunch`

### Rainbowcrack

### 描述
`RainbowCrack` 是一个创建彩虹表用于破解密钥密码的 PC 程序。`RainbowCrack` 与“普通的”暴力破解不同，它利用了名为彩虹表的巨大预处理表，从根本上缩短了破解密钥密钥所需的时间。`RainbowCrack` 由朱硕磊创建，执行了一种始于 Philippe Oechslin 的 `Ophcrack` 的先进内存折中密码分析攻击。

用法：`rcrack rainbow_table_pathname - h hash`

用法：`rcrack rainbow_table_pathname - l hash_list_file`

用法：`rcrack rainbow_table_pathname - f pwdump_file`

选项：
`rainbow_table_pathname` 彩虹表路径，支持通配符(`*`, `?`)
`-h` 哈希，使用原始哈希作为信息
`-l` 哈希列表文件，使用哈希列表记录作为信息，每个哈希占一行
`-f` pwdump_file，使用 `pwdump` 文件作为信息，这将像处理 LAN Manager 哈希一样处理它

示例：`rcrack *.rt - h 5d41402abc4b2a76b9719d911017c592`

示例：`rcrack *.rt - l hash.txt`

示例：`rcrack *.rt - f hash.txt`

### rcracki_mt

### 描述
`Rcracki_mt` 可用于对哈希进行彩虹表攻击。它预期用于有序和最终的彩虹表，主要由项目 www.freerainbowtables.com 产生。

用法：`rcracki_mt [options] [hash]`

选项：`[http://sourceforge.net/project/shownotes.php?release_id=682650]`

示例：`rcracki_mt - h 5d41402abc4b2a76b9719d911017c592 - t 4 - o save.txt C:\md5`

示例：`rcracki_mt - r - s my_personal_hashes`

### Rsmangler

### 描述
`RSMangler` 将获取单词列表并对其进行不同的控制，类似于 John the Ripper 所执行的操作，并带有了一些额外项目。全新的元素是“更改模式”，它将列表中的每个单词与其他单词合并，以创建所有可能的阶段（不是混合模式，顺序很重要）。

用法：`rsmangler.rb [OPTIONS]`

选项：`[http://www.randomstorm.com/rsmangler-security-tool.php]`

示例：`./rsmangler.rb – record wordlist.txt > new_wordlist.txt`

### samdump2

### 描述
`samdump2` 导出 Windows 2k/NT/Vista 密钥哈希。

更多数据：`http://www.hackingdna.com/2012/05/learn-samdump-on-backtrack-5.html`

用法：`samdump2 samhive`

示例：`./samdump2 bootkey > hashes`

示例：`samdump2/mnt/Windows/System32/config/SAM syskey.txt`

示例：`samdump2/mnt/Windows/System32/config/SAM syskey.txt >hash.txt`

示例：`samdump2/mnt/Windows/System32/config/SAM syskey.txt >/root/pass1`

从 Windows 分区/dev/sda1 恢复 SAM 哈希的实例：
`# mkdir - p/mnt/sda1`
`# mount/dev/sda1`
`# bhive/mnt/sda1/Windows/System32/config/SYSTEM/tmp/savedkey.txt`

### Sipcrack

### 描述
`sipcrack` - 一用于嗅探和破解 SIP 协议内部验证的工具集。会发起协议 (SIP) 是由 IETF MUSIC 工作组创建的一种协议，是用于启动、更改和结束交互式客户端会议的建议标准，包括视频、语音、文本、网络游戏和增强现实等交互式媒体组件。

`sipcrack` 是一个 SIP 登录嗅探/破解工具，包含两个项目：`sipdump` 用于捕获摘要验证，`sipcrack` 使用单词列表或标准信息暴力破解哈希。

`sipdump` 导出 SIP 摘要验证。如果发现登录，嗅探到的登录将保留在日志文件中。查看 `sipdump - h` 获取选项。`sipcrack` 使用 `dump` 创建的日志文件暴力破解客户端的秘密密码。假设找到了秘密密码，嗅探并破解的登录将刷新在日志文件中。查看 `sipcrack - h` 获取选项。

用法：`sipcrack [options]<dump_file`

选项：
`-s` 使用标准输入作为密码
`-w` 包含所有尝试密码的单词列表文件。
`-p` 每隔 `n` 个密码打印一次破解过程（用于 `- w`）（注意：会大幅降低速度）

示例：
`sipdump - I eth0 logins.dump`

`sipcrack - w mywordlist.txt logins.dump`

### Sucrack

### 描述





### sucrack

sucrack 是一个多线程 Linux/UNIX 工具，用于通过 `su` 对动物动力邻域客户端账户进行暴力破解。在你不具备太多优势、反而处于劣势的框架下，这个工具被证明是非常实用的示例。多次执行 `su` 需要连接到伪终端以从客户端获取密钥。这就是为什么你无法利用基本的 shell 内容来完成这项工作的原因。该工具用 `c` 编写，性能极高，并能同时尝试多次登录。如果不麻烦，请注意：使用此设备将消耗大量的 CPU 资源并迅速填充日志。

| 规则 | 说明 | 原文 | 重写 |
| :--- | :--- | :--- | :--- |
| A | 所有字符转大写 | `myPassword` | `MYPASSWORD` |
| F | 第一个字符转大写 | `myPassword` | `MyPassword` |
| L | 最后一个字符转大写 | `myPassword` | `myPassworD` |
| a | 所有字符转小写 | `AnotherPASS` | `anotherpass` |
| f | 第一个字符转小写 | `AnotherPASS` | `anotherPASS` |
| l | 最后一个字符转小写 | `AnotherPASS` | `AnotherPASs` |
| D | 前置一个数字 (0..9) | `password` | `1password` |
| d | 后缀一个数字 (0..9) | `password` | `password1` |
| e | 单词 1337 化 | `password` | `p455w0rd` |
| x | 启用上述所有规则 | | |

用法: `sucrack [options]<wordlist.txt>`

选项: [`www.leidecker.info/projects/sucrack.shtml`](http://www.leidecker.info/projects/sucrack.shtml)

示例: `sucrack - s 10 - a wordlist.txt`

示例: `sucrack - c - a wordlist.txt`

示例: `sucrack -u myuser wordlist.txt`

示例: `sucrack -b 50 -w 10 wordlist.txt`

示例: `sucrack - r - l AFL wordlist.txt`

### Truecrack

DESCRIPTION

TrueCrack 是一款针对 TrueCrypt (版权所有) 卷文件的强力密钥破解工具。它针对 Linux 设计，并针对 Nvidia Cuda 创新进行了优化。

它支持：
- `PBKDF2`（在 PKCS5 v2.0 中定义），依赖于密钥导出能力：`Ripemd160`、`Sha512` 和 `Whirlpool`。
- 用于硬盘加密的 `XTS` 块模式，依赖于 `AES`。

TrueCrack 可以根据以下方式进行强力攻击：
- 字典引用：从密码列表文件中读取密码。
- 字母顺序：从给定的字符集中生成所有给定长度的密码。

TrueCrack 处理 `gpu` 和计算机芯片。在 `gpu` 中，TrueCrack 需要大量资源。我们建议在没有 Xserver 和 framebuffer 的远程会议中运行 TrueCrack。

用法：字典攻击：`truecrack – t<truecrypt_file> - k<ripemd160|sha512|whirlpool> - w<wordlist_file> [-b<parallel_blocks> ]`

用法：字母表攻击：`truecrack - t<truecrypt_file> - k<ripemd160|sha512|whirlpool>-c<charset> [-s<minlength> ] – m<maxlength> [-b<parallel_block> ]`

选项：[`code.google.com/p/truecrack/`](https://code.google.com/p/truecrack/)

示例：`./truecrack – t test_12345678 – w ../../pass.lst – v`

## 第十八章：在线攻击

- `burpsuite`
- `cewl`
- `cisco-inspecting apparatus`
- `dbpwaudit`
- `findmyhash`
- `hydra`
- `hydra-gtk`
- `medusa`
- `ncrack`
- `onesixtyone`
- `patator`
- `phrasendrescher`
- `thc-pptp-bruter`
- `webscarab`
- `zproxy`

### Burpsuite

DESCRIPTION

Burp Suite 是一个用于 Web 安全测试的集成平台。它的不同工具之间完美协作，帮助完成整个测试过程，从最初的规划和应用程序攻击面的调查，到发现和利用安全漏洞。Burp Suite 包含以下关键部分：
- 一个拦截 `Proxy`，允许你评估和调整你的程序与目标应用程序之间的流量。
- 一个感知应用程序的 `Spider`，用于爬取内容和实用性。
- 一个高级 Web 应用程序 `Scanner`，用于自动化识别各种漏洞。
- 一个 `Intruder` 工具，用于执行强大的自定义攻击以发现并利用异常漏洞。
- 一个 `Repeater` 工具，用于控制和重新发送单个请求。
- 一个 `Sequencer` 设备，用于测试令牌的随机性。
- 保存工作并在稍后恢复工作的能力。
- 可扩展性，允许你有效地编写自己的模块，在 Burp 内部执行复杂且高度定制化的任务。

更多数据：[`portswigger.net/burp/`](http://portswigger.net/burp/)

用法：不适用；GUI 设备

示例：不适用；GUI 工具

### Cewl

DESCRIPTION

CeWL 是一个 Ruby 应用程序，它会爬取给定的 URL 到预定义的深度，或者跟踪外部链接，并返回单词列表，这些单词可以用于 John the Ripper 等密钥破解工具。当然，CeWL 仅限于你指定的站点，并且深度为 2 个连接，此行为可以通过传递参数进行更改。如果设置了很大的深度并允许其离开站点，请小心，你可能会进入许多不同的空间。所有三个字符及以上的表达式都将输出到 `stdout`。此长度可以扩展，单词可以保留在文件中而不是屏幕上，以便程序自动化。

用法：`cewl [OPTION] ... URL`

选项：[`www.digininja.org/projects/cewl.php`](http://www.digininja.org/projects/cewl.php)

示例：`./cewl.rb - w passwords.txt http://www.digininja.org/projects/cewl.php`（从 http://www.digininja.org/projects/cewl.php 创建密钥记录，并将密钥文档保存在 passwords.txt 中）

### cisco-eval device

DESCRIPTION

Cisco Auditing Tool - 一个 Perl 脚本，用于过滤 Cisco 交换机的常见漏洞。检查默认密码、易猜测的局域名称以及 IOS 历史漏洞。集成了对模块的支持和各种主机的检查。

用法：`./CAT [options]`

选项：
- `-h hostname`（检查单个主机）
- `-f hostfile`（用于过滤不同的主机）
- `-p port #`（默认端口为 23）
- `-w (局域名称猜测的单词列表)`
- `-a passlist`（密钥猜测的单词列表）
- `-I [ioshist]`（检查 IOS 历史漏洞）
- `-l logfile`（记录到日志，默认屏幕）
- `-q mode`（静默模式，无输出）

示例：`./CAT - h 192.168.1.100 - w wordlist - a passwords - I`

示例：`./CAT - h 192.168.1.22 - a rundowns/passwords - w records/local area (审计 Cisco Telnet 密码和 SNMP 团体字符串)`

### Dbpwaudit

DESCRIPTION

DBPwAudit 是一个 Java 工具，允许你对许多数据库进行密码质量在线审查。应用程序配置通过简单地将新的 JDBC 驱动复制到 `jdbc index` 来添加额外的数据集驱动。设计分为两个部分：`aliases.conf` 文件用于规划驱动的别名和规则；`rules.conf` 让应用程序知道如何处理扫描中的错误信息。

该工具已测试并确认可用于：
- Microsoft SQL Server 2000/2005
- Prophet 8/9/10/11
- IBM DB2 Universal Database
- MySQL

用法：`dbpwaudit – s<server> - d<db> - D<driver> - U<users> - P<passwords> [options]`

选项：[`www.edwiget.name/2012/07/evaluating mysql-passwords-with-dbpwaudit/`](http://www.edwiget.name/2012/07/evaluating%20mysql-passwords-with-dbpwaudit/)

示例：`./dbpwaudit.sh - s localhost - d mysql - D MySQL - U ~/mysql-users.txt - P ~/mysql-password.txt`（假设我在 localhost 上有一个数据库服务器，并且在主目录的 mysql-users.txt 文件中保存了 MySQL 用户名列表，在主目录的 mysql-password.txt 文件中保存了要尝试的密码列表，此命令将对 MySQL 进行进行）

提示：运行此程序需要额外的插件：http://www.edwiget.name/2012/07/inspecting mysql-passwords-with-dbpwaudit/

### Findmyhash

DESCRIPTION

`findmyhash.py` 尝试利用免费的在线服务破解各种类型的哈希值。

用法：`python findmyash.py<algorithm> [OPTIONS]`





### findmyash.py

用法：`findmyash.py<algorithm> [OPTIONS]`

### 选项

- `-h<hash_value>`: 如果只需要破解一个哈希值，使用此选项确定其价值。
- `-f<file>`: 如果你有几个哈希值，可以每行使用一个哈希值确定一个文档。注意：所有哈希值必须是相似的类型。
- `-g`: 如果你的哈希无法被破解，在 Google 中搜索它并显示所有结果。注意：此选项仅配合 `- h`（单个哈希输入）选项有效。

### 示例

- `python findmyhash.py MD5 - h 098f6bcd4621d373cade4e832627b4f6`
- `python findmyhash.py MD4 - h "db346d691d7acc4dc2625db19f9e3f52"`
- `python findmyhash.py SHA224 - h "90a3ed9e32b2aaf4c61c410eb925426119e1a9dc53d4286ade99a809"`
- `python findmyhash.py LM - h "01fc5a6be7bc6929aad3b435b51404ee"`
- `python findmyhash.py CISCO7 - h "12090404011C03162E"`

---

### Hydra

### 描述

THC-Hydra 是一个极其快速（多线程）网络登录工具，支持多种协议：`afp`, `cisco`, `cisco-empower`, `cvs`, `firebird`, `ftp`, `http-get`, `http-head`, `http-intermediary`, `https-get`, `https-head`, `httpsform-get`, `https-structure post`, `icq`, `imap`, `imap-ntlm`, `ldap2`, `ldap3`, `mssql`, `mysql`, `ncp`, `nntp`, `prophet audience`, `pcanywhere`, `pcnfs`, `pop3`, `pop3-ntlm`, `postgres`, `rexec`, `rlogin`, `rsh`, `sapr3`, `taste`, `smb`, `smbnt`, `smtp-auth`, `smtp-authntlm`, `snmp`, `socks5`, `ssh2`, `svn`, `teamspeak`, `telnet`, `vmauthd`, `vnc`

### 用法

`hydra [[[-l LOGIN|-L FILE] [-p PASS|-P FILE]] | [-C FILE]] [-e ns] [-o FILE] [-t TASKS] [-M FILE [-T TASKS]] [-w TIME] [-f] [-s PORT] [-S] [-vV] server administration [OPT]`

### 选项

[`www.aldeid.com/wiki/Thc-hydra#Usage`](http://www.aldeid.com/wiki/Thc-hydra#Usage)

### 示例

- `hydra 127.0.0.1 mysql - l root - P/information/dictionnaires/test.txt - t 4`
- `hydra 192.168.1.26 ssh2 - s 22 - P pass.txt - L users.txt - e ns - t 10`
- `hydra 192.168.1.69 http-structure post "/w3af/bruteforce/form_login/dataReceptor.php:user=^USER^&pass=^PASS^:Bad login" - L users.txt - P pass.txt - t 10 - w 30 - o hydra-http-post-attack.txt`

---

### hydra-gtk

### 描述

THC-Hydra 是一个异常快速（多线程）网络登录工具，支持多种协议：`afp`, `cisco`, `cisco-empower`, `cvs`, `firebird`, `ftp`, `http-get`, `http-head`, `http-intermediary`, `https-get`, `https-head`, `httpsform-get`, `https-structure post`, `icq`, `imap`, `imap-ntlm`, `ldap2`, `ldap3`, `mssql`, `mysql`, `ncp`, `nntp`, `prophet audience`, `pcanywhere`, `pcnfs`, `pop3`, `pop3-ntlm`, `postgres`, `rexec`, `rlogin`, `rsh`, `sapr3`, `taste`, `smb`, `smbnt`, `smtp-auth`, `smtp-authntlm`, `snmp`, `socks5`, `ssh2`, `svn`, `teamspeak`, `telnet`, `vmauthd`, `vnc`。

同样是一个 GUI 界面。

### 用法

`hydra [[[-l LOGIN|-L FILE] [-p PASS|-P FILE]] | [-C FILE]] [-e ns] [-o FILE] [-t TASKS] [-M FILE [-T TASKS]] [-w TIME] [-f] [-s PORT] [-S] [-vV] server administration [OPT]`

### 选项

[`www.aldeid.com/wiki/Thc-hydra#Usage`](http://www.aldeid.com/wiki/Thc-hydra#Usage)

### 示例

- `hydra 127.0.0.1 mysql - l root - P/information/dictionnaires/test.txt - t 4`
- `hydra 192.168.1.26 ssh2 - s 22 - P pass.txt - L users.txt - e ns - t 10`
- `hydra 192.168.1.69 http-structure post "/w3af/bruteforce/form_login/dataReceptor.php:user=^USER^&pass=^PASS^:Bad login" - L users.txt - P pass.txt - t 10 - w 30 - o hydra-http-post-attack.txt`

---

### Medusa

### 描述

Medusa - 用于密码审计的开源软件“登录破解器”。它是一个快速、极度均衡且经过测量的登录怪兽，其模块可以帮助几乎任何允许使用秘密单词进行验证的助手：CVS, FTP, HTTP, IMAP, MySQL, POP3, SMTPAUTH, Telnet 和 VNC。Medusa 的设计旨在通过基于字符串的测试（而非 Hydra 的基于循环的测试）来尝试同时登录各种主机或客户端，从而运行比 Hydra 更快。

更多数据：`http://www.foofus.net/jmk/medusa.html#how](http://www.foofus.net/jmk/medusa.html#how)

### 用法

`[-h host|-H file] [-u username|-U file] [-p password|-P file] [-C file] - M module`

### 选项

[`www.irongeek.com/i.php?page=backtrack-r1-pages/medusa`](http://www.irongeek.com/i.php?page=backtrack-r1-pages/medusa)

### 示例

要使用 Medusa，请指定：
- 使用 `-h` 关联主机 `192.168.1.1`
- 使用 `-u` 关联客户端名称 `administrator`
- 使用 `-P` 指定包含目标密码的文本文件
- 使用 `-M` 指定用于协助的模块（在此情况下为 http）

`medusa - h 192.168.1.1 - u "administrator" - P wordlist.txt - M http`

---

### Ncrack

### 描述

ncrack — 网络验证破解工具。旨在通过一种可以适应各种情况的独特引擎进行高高速破解。Ncrack 可以针对特殊情况进行广泛调整，但默认边界已足够涵盖绝大多数情况。它基于测量的工程设计，可以简单地扩展以支持额外的协议。Ncrack 的设计目的是让安全专家能够快速、稳健地检查大型机构的默认密码。它还可以用于针对特定管理实施精细且升级的攻击。

### 用法

`ncrack [<Options>] {target specification}`

### 选项

[`nmap.org/ncrack/man.html`](http://nmap.org/ncrack/man.html)

### 示例

- `ncrack 10.0.0.130:21 192.168.1.2:22`
- `ncrack scanme.nmap.org 192.168.0.0/8 0.0.0,1-7.- p22`（Ncrack 可以在命令行上识别各种主机详情）
- `ncrack scanme.nmap.org 192.168.0.0/8 0.0.0,1-7.- p22:21,ftp:telnet`（全局帮助）





### phrasendrescher

### 用法
- `Dictionary mode: phrasendrescher - d wordlist key-document`
- `Dictionary mode: phrasendrescher - d wordlist index containing-keys` (如果你指定的是注册表而非单个键文件，则将读取并尝试多个键)

### 示例
`./phrasendrescher - vd wordlist.txt my.key`

### thc-pptp-bruter

### 描述
一个用于中和 pptp vpn 节点的暴力破解程序。该工具的使用非常直观：只需将密码字典记录通过管道输入 `thc-pptp-bruter`，并确定你正在攻击的用户名和主机。请注意，在与该工具交互后，你将看到有关所关联主机的简要数据，例如，“Hostname ˜c2611wooter, Vendor ˜Cisco Systems, Inc., Firmware: 4608。”这对于远程应用层指纹识别非常有用的策略。

更多信息：http://flylib.com/books/en/3.418.1.83/1/

### 用法
`thc-pptp-animal [options] <remote ip>`

## 
- `-v` 详细结果/调试输出
- `-W` 禁用 Windows 破解 [默认: 启用]
- `-u <user>` 用户 [默认: administrator]
- `-w <file>` 密码字典记录 [默认: stdin]
- `-p < >` PPTP 端口 [默认: 1723]
- `-n < >` 相同尝试次数 [默认: 5]
- `-l < >` 限制每秒密码数 [默认: 100]

### 示例
`thc-pptp-bruter - u g0tmi1k - n 99 - l 999 10.0.0.3`

### Webscarab

### 描述
WebScarab 是一个用于检查 HTTP 和 HTTPS 协议应用程序的框架。它用 Java 编写，对于许多阶段非常方便。WebScarab 有由各种模块执行的活动模式。在最常用的情况下，WebScarab 作为阻塞中间件工作，允许管理员在请求发送到服务器之前检查并修改程序发出的请求，并在程序接收服务器响应之前审计并更改这些响应。WebScarab 可以同时捕获 HTTP 和 HTTPS 通信。管理员还可以审计通过 WebScarab 的会话（请求和响应）。

更多信息：https://www.owasp.org/index.php/WebScarab_Getting_Started

### 用法
n/a；GUI 工具

### 示例
n/a；GUI 工具

### Zaproxy

### 描述
OWASP Zed Attack Proxy (ZAP) 是一种易用的集成应用程序测试工具，用于跟踪 Web 应用程序中的漏洞。它旨在具有广泛安全经验的人员使用，因此非常适合新接触渗透测试的工程师和实战分析师，也可以作为资渗透测试人员工具箱的有力扩展。

更多信息：https://code.google.com/p/zaproxy/

### 用法
n/a；GUI 工具

### 示例
n/a；GUI 设备

