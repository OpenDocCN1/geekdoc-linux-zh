
## 11.4.2 Oracle 客户端

WIN/XP 上的 Oracle 客户端需要选择并安装高级安全选项（Advanced Security Option），以便从 Oracle 客户端进行 RADIUS 身份验证。

使用 Oracle Net Manager 配置 Oracle 客户端使用 RADIUS 进行验证。从第 215 页图 11-1 所示的本地窗口，在下拉菜单中选择 Oracle Advanced Security，选择“验证”（Authentication）选项卡，并将 RADIUS 从“可用方法”（Available Methods）面板移动到“已选方法”（Selected Methods）面板。

![](img/5b458d26d6ded58c4d2c82af59a3d71c_236_0.png)

图 11-1 Oracle Advanced Security 窗口

这将通过向 `SQLNET.AUTHENTICATION_SERVICES` 参数添加 RADIUS 来更新客户端的 `sqlnet.ora` 文件：

```
# sqlnet.ora 网络配置文件：
C:\pt849\rawin\NETWORK\ADMIN\sqlnet.ora
# 由 Oracle 配置工具生成。
SQLNET.AUTHENTICATION_SERVICES= (RADIUS,NTS)
NAMES.DIRECTORY_PATH=(TNSNAMES, EZCONNECT)
```

## 11.4.3 LDBM 中的用户名和 SDBM 中的密码的 Oracle 客户端连接

此时，Oracle 用户 `icucser2` 可以与 Oracle 数据库服务器进行正常连接，并由 z/VM LDAP 作为 FreeRADIUS 服务器的后端进行身份验证。所使用的 `radius.conf` 文件位于第 209 页的示例 11-2 或第 210 页的示例 11-3，取决于是否允许匿名绑定。在此处的窗口中显示了 `icucser2`，它是为 z/VM LDAP 原生身份验证设置的，这意味着它的密码在 RACF 中，而不是在 LDBM 目录中。`icucser1` 也有相同的窗口，其密码在 LDBM 目录中。

![](img/5b458d26d6ded58c4d2c82af59a3d71c_237_0.png)

在输入用户名、有效密码和 Oracle 连接字符串后，用户连接到 Oracle 数据库，如图 11-3 所示。

![](img/5b458d26d6ded58c4d2c82af59a3d71c_237_1.png)

如果 `icucser2` 输入了错误的密码，将出现第 217 页图 11-4 所示的窗口。

![](img/5b458d26d6ded58c4d2c82af59a3d71c_238_0.png)

## 11.4.4 SDBM 中的用户名和密码的 Oracle 客户端连接

Oracle 用户 `icracf1` 和密码 `ldapxx` 位于 RACF SDBM 数据库中。Oracle 客户端连接数据库时的唯一区别是使用了 `icracf1/ldapxx` 代替 `icuser1/icuser1x`。主要区别在于启动 FreeRADIUS 时需要一个 `radius.conf` 文件，如第 210 页的示例 11-4 所示。该文件中的参数设置允许 FreeRADIUS 使用 RACF SDBM 后端绑定到 zVM LDAP，并在 RACF 中搜索 `icracf1` 进行用户身份验证。

## 11.4.5 外部身份验证的 Oracle 参考

- Oracle Database Security Guide 10g Release 2, B14266-01, 2005年6月
- Oracle Database Advanced Security Administrator's Guide, B14268-02, 2005年11月

# 缩写与术语

| 缩写 | 描述 | 缩写 | 说明 |
|---|---|---|---|
| ADF | Application Development Framework | ONS | Oracle Notification Service |
| API | Application Programming Interface | OTN | Oracle Technical Network |
| AS | Application Server | OUI | Oracle Universal Installer |
| ASM | Automated Storage Manager | RAC | Real Application Clusters |
| BIEE | Business Intelligence Enterprise Edition | RPM | Red Hat Package Manager |
| BPEL | Business Process Execution Language | SID | System Identifier |
| CRS | Cluster Ready Services | SOA | Service-Oriented Architecture |
| CVU | Cluster Verification Utility | SQL | Structured Query Language |
| CW | Cluster/Ware | SR | Oracle Cluster Request |
| DB | Database | VIP | Virtual Cluster IP addresses |
| EBS | E-Business Suite | VM | Virtual Machine |
| GSD | Global Services Daemon | | |
| HTTP | Hypertext Protocol | VNC | Virtual Computing |
| IBM | International Business Machines | JDK | Developer Kit |
| IM | Identity Manager | XML | Extensible Language |
| ITSO | International Technical Support | | |
| J2EE | Java Enterprise Edition | | |
| JDK | Java Developer Kit | | |
| JMS | Java Message Service | | |
| LDAP | Lightweight Directory Protocol | | |
| LVM | Logical Volume Manager | | |
| OCF2 | Oracle File System | | |
| OCR | Oracle Registry | | |
| OEM | Oracle Enterprise Manager | | |
| OFA | Optimum Architecture | | |

# 索引

符号
`/profile` 31
`/etc/hosts` 24
`/etc/init.d/oracasm` 83
`/etc/pam` 27
`/etc/profile` 26
`/etc/sysctl.conf` 24
`/etc/udev/permissions.d` 79

BIEE 95
块设备 76
简报阅读器 110
业务智能企业 95

数值
10.2.0.3 patchset 17
31-bit 88
3270 129
64-bit 88

C
C++ 运行时库 103
C/C++ 编译器 61
缓存缓冲区 88
缓存 144
客户端
断开 110
`clients.conf` 文件 213
克隆器 137
克隆 123
集群就绪服务 (CRS) 84
集群验证工具 (CVU) 83–84
集群软件 84
CMS 字节文件系统 (BFS) 203
命令

A
访问控制列表 (ACLs) 203
管理安全 154
高级安装 34
高级安全 4, 213
高级安全选项 (ASO) 208
分析 Web 116
归档 179
AS10g 96
ASCII 87
ASM 72, 93–94
ASM 内内核 81
ASLIB 80
ASMLib 82
属性 202
认证 201
目录 206
extern 212
自动存储管理 (ASM) 20, 39, 72
自动工作负载仓库 57
可用性 63, 169
AWR 94

`cat` 129
`cp` 130
`iconfig` 131
`netstat` 133
配置 87
配置助手 48
配置，磁盘 72
约束环境 90
冲突 91
控制器
profile 127
corav 51
CP 命令 94
CP 备用控制 144
CPU (CP) 分配 89
CPU 分配 87
`create_db.sql` 98
`cron` 90
CRS 84
CVU 83, 219

B
备份与恢复 179
备份 123, 142
热备份 146

D
数据挖掘 4

Data Pump 数据库 188
- 创建 98
- 性能 115
- 存储库 114
- DB 控制 AWR 94
- `DB_UNIQUE_NAME` 174
- `db2pwden` 205
- `dbca` 198
- `DBControl` 42, 56
- DBF 文件 179
- `dbhome` 51
- `dbora stop` 命令 144
- `dedicate` 语句 73
- DGMRL 170
- 目录认证 206
- 目录信息树 (DIT) 209
- DIRMAINT 137
- 断开的客户端 110
- 逻辑磁盘 10
- LUN 10
- 条带 94
- 磁盘配置 72
- 特异名称 (DN) 202
- distro 11
- DM 多路径 70
- DN 202
- DNS 22, 116
- 文档 30
- 下载 29
- DS CONF 203
- DTCVSW 127

FCP 93
光纤连接器 (FICON) 70
光通道协议 (FCP) 70
fICON 93
文件系统 74
闪回恢复区域 177
FlashCopy 123, 142
FreeRADIUS 208, 213
调试模式 212
FreeRADIUS 服务器 217
FTP 22
融合中间件 3

G
- GCC 102
GNU 编译器集合 102
黄金镜像 137
Grid 控制 42
`grouppadd` 命令 23

H
- HFS 194
高可用性 169
高带宽 133
HiperSocket 68-69
热备份 146
HTTP Web 服务器 152
虚拟机监控程序 88

I
- I/O 并发 71
I/O 考虑
磁盘 93
i/O 调优 87
VM 性能工具 94
身份管理器 3
IE 浏览器 56
`iconfig` 131
初始化参数 177
安装 12, 19, 96
高级 34
Oracle 136
Intel 88
IOCDS 连接 63
iSQL*Plus 48, 58–59

E
- EBCDIC 187
EBCDIC 转 ASCII 188
ECK 11
企业系统连接 (ESCON) 70
ESAM 94
ESCON 93
以太网 129
扩展存储 88
扩展计数键数据 (ECKD) 70
外部认证 212

F
故障转移 168, 183

J
JEE 151
Java 154
JDK 219
MIPS 89
监控性能 87

K
内核参数 14, 25

N
`netca` 182
Net 服务 4
网络安全 134
NIC 127
Novell 20

L
LAN 段 124
启动程序 153
`LD_LIBRARY_PATH` 31
LDAP 201
认证 201
Oracle 数据源 115
OEM 56
OEM Home 56
OFA 55
OLAP 4

O
应用 3
服务 7
自动存储管理 (ASM) 72
自动存储管理 (ASM) 20
二进制文件 75
集群软件 65, 75
E 协作套件 3
E-业务套件 3
融合中间件 3
安装 12, 36
通用安装程序 3
管理工具 6
高级安全选项 (ASM) 202
自动存储管理 (ASM) 78
自动存储管理 (ASM) 20
BIEE 6
业务智能企业版 3
Oracle 业务智能 Javost 109
Oracle 业务智能演示服务 109
Oracle 业务智能调度进程 109
Oracle 业务智能服务器 109
Oracle 调用接口 (OCI) 4
企业中间件 3
Oracle 产品安装 15
Oracle RAC 75
面向服务的架构 3
Oracle SID 103
Oracle Store 7
技术网络 (OTN) 29
Oracle 用户界面 (OUI) 21
Oracle PeopleSoft 企业版 3
Oracle Siebel 应用 3
`ORACLE_BASE` 31
`ORACLE_HOME` 31, 51
`ORACLE_INVENTORY` 31
`ORACLE_OWNER` 51
`ORACLE_SID` 31
`oraeasm` 83
`oraun` 55
OSA 适配器 69
OSA express 126

M
内存 10, 94
MetaLink 190
备注 9, 11
迁移 89, 188
`midisk` 75, 124
Minidisk Cache (MDC), 禁用 92

P
分页空间 94
`pam` 15
`pam.d` 27
分区 4
密码管理 213
密码认证 201
补丁安装 16
`PATH` 31
性能 87
数据库 115
I/O 考虑 93
性能调优 64, 90
文件 177-178
PGA 10, 88
物理 CPU 90
物理备用数据库 168, 179
PL/SQL 58
安装后 19
主数据库 168
Pro*C/C++ 4
程序全局区域 (PGA) 88
`puTTY` 28, 50

Q
QDIO 68, 126

R
RADIUS 29
支持 212
RADIUS 服务器 211
`radius.conf` 209, 216
`radtest` 212
原始设备 76
设备语句 73
Real RAC 63
Red Hot 20
Red Hot 4
安装 85
Red Hot AS4 4
Red Hot 包 25
redo 日 172
复制 114
存储库 114
恢复 147
层 92
逻辑卷管理 (LVM) 72
逻辑分区 (LPAR) 23
逻辑备用数据库 168
逻辑卷管理 (LVM) 72
`niscript` 54
LVM 85, 219

L
监听 54
Net 服务名称 182
补丁 93
Publisher 桌面 110

S
架构 4
SCSI 设备 70
秘密文件 212
安全 134
服务名称 182
SGA 56
单实例 92
SLES10 17
SUSE Linux Enterprise 9
交换空间 11, 24
切换 167, 183
`sync` 命令 144
`sysctl.conf` 24
SYSDBA 56
系统全局区域 (SGA) 88

U
`ulimit` 参数 24

V
`VDISK` 75, 91
VIP 219
虚拟 LAN 68
虚拟化 134
虚拟化策略 142
VLANs 124
VNC 28
服务器 28, 33
卷组 77
投票磁盘 76
VSwitch 90, 123, 124, 126, 133

W
Web 应用 192
网站 7
WebSphere 服务器 151, 163
可写目录 196

X
窗口系统 28
接口 28
`xhost +` 33
XML 文件 151

Y
YAST2 102

Z
z/OS 187
z/VM 10, 124
虚拟机监控程序 88
分页 92
z/VM V2.2 20
zRACE 工具 89

# 在 System z Linux 上使用 Oracle 解决方案

# 为 Oracle Database 10gr2 设置虚拟机和 Linux

对于依赖 IBM 主机系统运行业务的客户，System z Linux 提供了许多优势。System z for Linux 利用了 System 硬件和 zVM 的服务特性，使其成为稳健的工业级 Linux。这为托管您企业中运行的 Oracle 解决方案提供了一个卓越的平台。

# 为 Data Guard 设置环境

本 IBM Redbooks 出版物描述了在安装和测试若干 Oracle 功能时获得的经验，例如：

# 为 Oracle 设置多个 Linux 客户机

- Oracle Data Guard
- IBM WebSphere Application Server 连接到 System z for Linux 上的 Oracle 数据库
- Oracle DB2 连接到适用于 System z 的 Oracle 数据库
- Oracle Data Pump

它包含了许多在带有 Linux 和 zVM 的 IBM System z 上运行 Oracle 产品的通用提示和技巧。

本书的读者群体包括数据库顾问、安装程序人员、管理员和系统程序员人员。它并非旨在替代 Oracle 的官方文档，这仅代表了我们安装和使用 Oracle 产品的经验。

# 国际技术支持组织

# 基于实战经验构建技术信息

IBM Redbooks 由 IBM 国际技术支持组织开发。来自全球的 IBM 客户和合作伙伴的专家根据真实场景创建及时信息。书中提供的建议旨在帮助在您的环境中更有效地实施 IT 解决方案。

更多信息请访问：`ibm.com/redbooks`
