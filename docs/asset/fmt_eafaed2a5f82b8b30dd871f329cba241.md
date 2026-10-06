
# 92 第7节：表格

2004年9月

## 企业级 Linux

| | Debian Debian GNU/Linux | Mandrakesoft Mandrakelinux Corporate Server 2.1 | Novell SUSE Linux Enterprise Server 8.0 | Red Hat Red Hat Enterprise Linux AS |

|---|---|---|---|-|

| **韧性** | | | | |

| 韧性 | 99.999% 系统可用性保证 | 不在 Debian 考虑范围内 | - | Y |

| | 处理器的在线添加/删除 | | | | Y |

| | 内存的在线添加/删除 | | | | Y |

| | I/O 适配器的在线添加/删除 | | | - | Y |

| | 热的热更换 | Y | 取决于硬件 | Y | Y |

| | 备内核安装 | | Y（但无实时切换） | Y | Y |

| | 动态内核补丁 | | N | | Y |

| | 动态应用补丁 | | | - | Y |

| | 灾难恢复功能 | | | | Y |

| | 系统韧性功能 | | | 内核/用户态分离 | Y |

| 恢复 | 处理器在线自动重配置 | | | | Y |

| | 内存在线自动重配置 | | | | Y |

| | 磁盘 I/O 适配器在线自动重配置 | | | | Y |

| | 网络适配器在线自动重配置 | | | | Y |

| | 链路聚合保护 | | | | Y |

| | 文件系统恢复 | | Y | Y | Y |

| | 容错文件系统 | | Y (reiserfs, ext3, xfs, jfs) | | Y |

| | 内核转储分析设施 | | Y (ksyms) | Y | Y |

| | 动态核心文件生成 | | | | Y |

| | 多模式启动 | | Y (lilo) | Y | Y |

| | 供应商故障预测 | | | N | 使用 Cluster Suite |

| | 自动挂起检测和解决设施 | | | 软件包保护 | Y |

| | 自动系统恢复设施 | | | 启动时自动 fsck | Y |

| | 交互式系统恢复设施 | | | 带有 fsck 的恢复系统 | Y |

| | 配置备份/恢复 | | Y | Y | Y |

| | 配置备份/恢复 | | Y | Y | Y |

| | 数据备份/恢复软件 | | Y | Y | Y |

| | 其他恢复功能 | | | - | Y |

列出的功能基于供应商对 Butler Group 问卷的回答。'-' 并不表示缺少某功能。

## 企业级 Linux

| | Debian GNU/Linux | Mandrakesoft - Mandrakellinux Corporate Server 2.1 | Novell - SUSE LINUX Enterprise 8.0 | Red Hat Red Hat Enterprise Linux AS |

|---|---|---|---|---|n|

| 互操作性 | 集成 Web 服务器 | | | | |

| 互联网和 Web 应用程序服务 | 集成代理服务器 | Y | Y | Y | Y |

| | 集成时间服务器 | Y | Y | Y | Y | Y |

| | 支持的协议 | HTTP | Y | Y | Y | Y |

| | SSL | Y | Y | Y | Y |

| | SMTP | Y | Y | Y | Y |

| | FTP | Y | Y | Y | Y |

| | NNTP | Y | Y | Y | Y |

| | POP | Y | Y | Y | Y |

| | IMAP | Y | Y | Y | Y |

| | XML | | Y | Y | Y |

| | JVM | | Y | Y | Y |

| | IPv6 | | Y | Y | Y |

| | VLAN | | Y | Y | Y |

| | IKE | | Y | Y | Y |

| | 高级 Socket API | - | - | - |

| | C/C++ | P+S | Y | P+S |

| | 语言提供/支持 (N / S / P+S) | PERL | P+S | Y |

| | Python | P+S | Y | Y |

| | VB | N | - | P+S |

| | Java | S | Y | Y |

| | Java Servlets | S | Y | P+S | Y |

| | 托管 ( |) | P | | | Y |

 | | | | | Script | P |S | Y | Y |

| | Active Server Pages | P+S | - | Y |

| | FrontPage Extensions | P+S | Y | - |

| | ODBC Support | P+S | Y | - |

| | JDBC Support | S | - | Y | Y |

| | TCP 优化功能 | | | ECN & cookies | Y | Y |

| | Mobile 支持 | | | | Y |

| | RADIUS 支持 | | | | Y |

| 互互操作性 | 消息队列服务 | Y | | Y | - |

| | 事务管理服务 | - | - | - |

| | 集成文件/打印服务器 | Y | Y | Y |

| | Microsoft Windows 支持 | Y | Y | Y |

列出的功能基于供应商对 Butler Group 问卷的回答。'-' 并不表示缺少某功能。

## 互操作性（续）

| | Debian - Debian GNU/Linux | Mandrakesoft - Mandraklinux Corporate Server 2.1 | Novell - SUSE Linux Enterprise 8.0 | Red Hat - Red Hat Enterprise Linux |

|---|---|---|---|---|

| 互操作性（续） | Apple 客户端支持 | Y | Y | Y | Y |

| | Linux 客户端支持 | Y | Y | Y | Y |

| | Unix 客户端支持 | Y | | Y | Y |

| | 访问外部文件/打印服务器 | Y | | tcp or smb network | Y | Y |

| | 集成终端服务器 | | | | Y | Y |

| | 邮件服务器 | Y | | | Y | Y |

| | 邮件客户端 | Y | Y | Y | Y |

| | Web 应用程序服务器 | Y | | Y | Y |

| 系统管理接口 | 集成系统管理工具 | | | Y | Red Hat Network |

| | 命令行界面 | Y | | Y | Y |

| | GUI 界面 | | | Y | Y |

| | Web 界面 | | | Y | Y |

| | 远程访问工具 | | | Y | Y |

| | 单个控制台管理多个系统 | Y | | | | |

| | 通过 API 添加设施 | | | | | |

| | 作为 Web 服务发布的管理工具 | | Y | Y | |

| | 资源指标 | | Y | Y | |

| | 资源的动态发现： | | | Y (udev, devfs, hotplug) | Y |

| | 事件监控和告警管理设施 | | | N | |

| | 来自/来自第三方应用程序的代理 | | | N | |

| | 用户/组管理 | Y | | N | Y |

| | 网络管理 | Y | | Y | Y |

| | 打印机管理 | Y | | Y | Y |

| | 文件共享管理 | Y | | Y | Y |

| | 服务管理 | Y | | Y | Y |

| | 集群管理 | | | N | |

| | 分区管理 | Y | | | Y |

| | 按需容量功能 | | | | |

| | 配置复制管理 | | Y | Y | Y |

| | Debian - Debian GNU/Linux | Mandrakesoft - Mandrakelinux Corporate Server 2.1 | Novell - SUSE LINUX Enterprise Server 2.0 | Red Hat - Red Hat Enterprise Linux |

|---|---|---|---|---|

| 管理（续） | 存储配置和监控工具 | | Y | Y |

| 存储管理 | 存储分区 | | Y | Y |

| | 热备盘的配置与管理 | | | Y |

| | 识别热点并重新分配以平衡负载 | | | | |

| | 与系统管理工具集成的工具 | Y | | | |

| 管理 | 软件包管理工具 | Y (RPM + UPMI) | Y | Y |

| | 软件注册表/配置数据库 | | Y | Y |

| | 版本控制和两阶段提交 | | Y | | |

| | 单点管理多个服务器 | | Y | | |

| | 客户端配置管理 | | Y | | |

| | 与系统管理工具集成的工具 | | | | | |

| 工作负载管理 | 资源管理工具 | | | N | |

| | 于 SMP 和集群环境 | | Y | | |

| | 支持的分区 | | | | |

| | 基于权限或目标的资源管理工具 | | | | |

| 安装选项 | 操作系统提供 | Y | CDs | Y |

| | 预装选项 | | N | Y |

| | 预配置选项 | | Y | Y |

| | 安装自动化 | | AutoYAST2 | | |

| 通用安全 | | | | |

|---|---|---|---|---|

| 身份验证服务 | | Y | PAM | Y |

| | 加密服务 | | | ssh | Y |

| | 基于证书的验证 | | Y | | Y |

| | SSL 加密 | | Y | Yes | Y |

| | 访问控制 | | Y | POSIX | Y |

| | 基于 IP 的安全 | Y (ipsec, iptables) | Y iptables | Y | Y |

| | 系统区域网 | | | | Y |

| | VPN | | Y (ipsec, pptp) | Y | Y |

## 企业级 Linux

| 安全性对比 | Debian - Debian GNU/Linux | Mandrakesoft - Mandrelinux Corporate Server 2.1 | Novell - SUSE LINUX Enterprise Server 8.0 | Red Hat - Red Hat Enterprise Linux |

| :--- | :--- | :--- | :--- | :--- | :--- |

| 一般安全性对比 | 集成目录/身份验证服务 | | | Y | |

| 集成目录/DNS 服务 | | | | Y | |

| 集成目录/文件安全服务 | | | | Y | |

| 智能卡认证 | | | | Y | |

| “单点登录”支持 | | | Y | | |

| 目录和安全服务 (LDAP) | LDAP 验证用户身份 | 支持 | Y | Y | Y |

| LDAP 用户/组授权 | | 支持 | Y | Y | Y |

| 不符合规范的 LDAP 架构 | | | | Y | |

| 打印与 LDAP 集成 | | | | Y | |

| 邮件服务利用 LDAP 目录 | | 支持 | | Y | Y |

| Kerberos 与 LDAP 集成 | | 支持 | Y | | Y |

| 与 LDAP 的额外集成 | | 支持 | Y | Y | |

| 安全网络 | 分布式安全应用 | | | Y | Y |

| SOCSS5 协议 | | | | | |

| 安全 Shell/脚本环境 | | | | Y | Y |

| 网络命令的安全版本 | Y | | | Y | Y |

| 入侵检测与防御功能 | | | Y (prelude, tripline) | saint, nessus | Y |

| IP 过滤工具 | Y | | | Y | |

| 管理员角色委派 | | | Y (libsafe) | | Y |

| 缓冲区溢出保护 | | | | | Y |

| 加密设施 | Y | Y (GPG) | | | | |

| 操作系统的安全合规性 | | | | Y | EAL3 & COE |

| 集成防火墙 | | | | Y | Y |

| 包含反病毒软件 | N | | | Y | |

| 额外的安全网络功能 | | | | | Ispec |

| 客户端功能 | 客户端产品 | Debian GNU/Linux 10.0 | Mandrakelinux | SUSE LINUX Desktop | Red Hat Desktop |

| :--- | :--- | :--- | :--- | :--- | :--- |

| 一般 | 文件服务 | Y (各种) | Y | Y | Y |

| 网络邻域集成 | | Y | Y | Y | Y |

| 打印 | | Y | | Y | |

| Active Directory 集成 | | Y | | Y | |

| 日历功能 | | | | OpenOffice, Star Office, 通过 Codewaver 使用的 MS Office | Y |

| 文件格式支持 | | 所有主要文件格式 | | 私有 | Y |

| 管理功能 | | 标准 Linux 管理工具 | | 远程管理 | |

列出的功能基于供应商对 Butler Group 问卷的回答。`*` 并不一定意味着某功能的缺失。

2004年9月

第 7 节：表格 97

## 企业级 Linux

| | Debian Debian GNU/Linux | Mandrakesoft Mandrelinux Corporate Server 2.1 | Novell SUSE LINUX Enterprise Server 8.0 | Red Hat Red Hat Enterprise Linux AS |

|---|---|---|---|---|---|

| 安全 | 认证服务 | LDAP, Kerberos, PAM 等 | Y | KDE 桌面 | Y |

| | 加密文件系统 | | 是 (所有文件系统均可加密) | Y | |

| | 密钥管理 | Y | Y (GPG) | | Y |

| | 加密接口 | | 多种 | Y (GPG) | | 内内核级！ |

| 接口 | 蓝牙 | Y | Y | | Y |

| | USB | Y | Y | | Y |

| | 红外线 | | Y | | Y |

| | 1394 | | Y | | Y |

| | 同步 | | Y | | Y |

| | 流媒体视频 | | Y | | Y |

| 移动 | 无线连接 | Y | Y | | Y |

| | 电源管理 | | Y | | Y |

列出的功能基于供应商对 Butler Group 问卷的回答。`~` 并不一定意味着某功能的缺失。

## 7.2 BUTLER GROUP 企业级 Linux 产品能力图

![](img/767d23264d3e5471ce58a1972dfd07dc_98_0.png)

![](img/767d23264d3e5471ce58a1972dfd07dc_98_1.png)

## 企业级 Linux

## Novell

SUSE LINUX Enterprise Server 8.0

企业级 Linux 特性

![](img/767d23264d3e5471ce58a1972dfd07dc_99_0.png)

## Red Hat

Red Hat Enterprise Linux AS

企业级 Linux 特性

![](img/767d23264d3e5471ce58a1972dfd07dc_99_1.png)

## 7.3 BUTLER GROUP 企业级 Linux 市场生命周期位置

Linux 发行版

| 表现卓越 | Novell SUSE LINUX Red Hat | Novell SUSE LINUX Red Hat |

| --- | --- | --- |

| 表现良好 | Novell SUSE LINUX Red Hat | Asianux* Mandrakeux Red Hat |

| 表现不佳 | Debian Asianux | Debian Mandrakeux |

| Linux 服务 | 表现卓越 | IBM |

| --- | --- | --- |

| 表现良好 | IBM | Novell Red Linux |

| 表现不佳 | IBM | Novell Red Linux |

| 早期采用期至2005 | 市场采用期2006-2009 | 市场成熟期2010年以后 |

## 企业级 Linux

## 关于 Butler Group 位置

垂直轴分为三组，每组对供应商和产品做出陈述。水平轴反映了市场成功情况。在每组内，按字母顺序排列，并不重要。

- * 表现卓越：供应商拥有成熟的市场地位，其解决方案被广泛认为是顶级的。

- * 表现良好：供应商定位良好，且营销到位。该解决方案具有竞争力的功能和性能。

- * 表现不佳：供应商定位不佳，时机不对，且未能有效进行营销。产品可能存在缺陷或过时。

- * 早期采用期：代表市场的早期阶段，通常由新进入者推动的新技术或标准被创新型公司采用。

- * 市场采用期：大多数技术发生的阶段，通常持续三四年。
