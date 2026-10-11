
| NMAS (Novell 认证服务) | 无功能差异。 |

### 表 1-3 服务说明和参考

| 服务 | 说明和参考 |
| --- | --- |
| Novell 客户端 (Linux 和 Windows) 与 NCP 无功能差异。 |
| Novell 聚类服务 | 访问 Linux 版 OES Novell 聚类服务 1.8.2 管理指南 (`cluster_admin_lx.pdf`) 第 9 页的“产品功能”。<br>访问 NetWare 版 OES Novell 聚类服务 1.8.2 管理指南 (`cluster_admin.pdf`) 第 9 页的“产品功能”。 |
| Novell 许可服务 | Linux 不可用。 |
| NSS (Novell 存储服务) | 访问 OES 存储服务文件系统指南 (`nss_enu.pdf`) 第 73 页的“共存与迁移问题”。 |
| Nsure 审计 | Linux可用。 |
| NTPv3 | 访问 Novell OES，“时间同步”，5-4。 |
| OpenSSH | 访问 OpenSSH 管理指南 (`openssh.pdf`) 第 10 页的“平台特性”。 |
| PAM (插件认证模块) | NetWare 不可用。认证与 eDirectory 完全集成。 |
| Pervasive.SQL | 访问 Pervasive.SQL 的在线文档：`http://www.pervasive.com/support/technical/online_manuals.asp` |
| PKI (公共密钥基础设施) | 无功能差异。 |
| 打印 | 访问 iPrint。 |

## 集成 Linux 的 Novell Open Enterprise Server

| 服务 | 说明和参考 |
| --- | --- |
| RADIUS | 无功能差异 (NMAS)。 |
| QuickFinder | 访问搜索。 |
| Samba | Linux 解决方案，NetWare 使用原生文件协议。 |
| 搜索 (QuickFinder) | 在索引文件系统时，QuickFinder 引擎仅索引它有权访问。在 NetWare 上，它对所有挂载卷具有完全访问权限。在 Linux 上，它仅权访问 www 组中 dell 用户的文件。更多信息请参阅 Novell QuickFinder Server 4.2 管理指南 (`qserver.pdf`) 第 156 页的“安全特性”和第 81 页的“为 Linux-NSS 卷生成索引”。 |
| 服务资源管理 (eDirectory) | NetWare  eDirectory 管理资源。例如，你可以查看和修改系统信息、管理 NetWare 卷上的文件和文件夹、清理删除的文件、分配卷空间以及创建对象以方便管理。更多信息请参阅 Novell eDirectory 8.7.3 管理指南 (`edir873.pdf`) 第 87 页的“管理对象”。当前 Linux 版 eDirectory 不支持服务器资源管理。 |

## 表 1-3 服务说明与参考

| 服务 | 解释与参考 |
|---|---|
| SLP (Novell SLP) (OpenSLP) | 请参阅《Novell SUSE Server Administration Guide》(`sles_admin.pdf`) 第 308 页的“SLP Support in SUSE LINUX”。<br>访问网页 `http://www.novell.com/documentation/edir87/edir87/data/a2iimc.html` 查阅“Implementing the Service Location Protocol”。<br>另请访问网页 `http://www.openslp.com` 查看 OpenSLP 项目主页。<br>默认情况下，NetWare 使用 Novell SLP，该服务在位于 eDirectory 上下文（context）中的目录代理（DAs）之间提供同步。这提供了超越本地网络范围的服务信息。<br>或者，您也可以为 eDirectory 实现 OpenSLP。但请注意，OpenSSL 不支持 DA 同步。<br>Linux 上的 OpenSLP 未经过定制以提供 DA 同步功能。 |
| 软件 RAID RAID | 请参阅《OES Novell Storage Services File System Administration Guide》(`nss_enu.pdf`) 第 117 页的“Understanding Software RAID Devices”。 |
| 存储管理服务 (SMS) | 无功能差异。 |
| TCP/IP | 无功能差异。 |
| Timesync | Linux 不可用，但两个 OES 平台均支持 NTPv3。 |
| Tomcat | 请访问网页 `http://www.novell.com/documentation/oes/web_tomcat/data/ahydran.html#ahydran` 上的“Administration Instance vs. Public Instance of Tomcat on NetWare”。 |
| NetWare 传统文件系统 | Linux 不可用。 |
| 虚拟办公室（协作） | 无功能差异。 |
| WAN 流量管理器 | 请参阅《Novell eDirectory 8.7.3 Administration Guide》(`endir873.pdf`) 第 229 页的“WAN Traffic Manager”。 |

### 目标 3

## 规划您的 OES 方案

一旦了解了 Novell OES 中可用的组件并决定了安装哪些服务，就可以开始规划您的 OES 实施方案。

以下是您成功实施 Novell OES 应该遵循的关键规划步骤：

- 规划 eDirectory
- 为每台服务器准备现有的 eDirectory 树
- 为每台服务器确定用途
- 评估服务器需求
- 评估用户限制和 Linux 用户管理
- 在开始之前考虑共存和迁移
- 在开始前检查您的安装选项
- 如何通过升级保护获取 OES

有关安装和升级到 Novell OES 的详细信息，请参阅《Novell OES SP2 Planning and Implementation Guide》(`implpgde.pdf`) 第 55 页的“Installing OES”和第 61 页的“Upgrading to OES”。

您可以通过 `http://www.novell.com/documentation/oes` 或从您的 3077 课程光盘中的 `OES_Docs` 目录 访问该指南。

## 规划 eDirectory

Novell eDirectory 是 OES 网络服务和安全的内核。在规划 eDirectory 时，您需要考虑以下指南：

- 安装到现有树中
- 创建新的 eDirectory 树

### 安装到现有树中

- 共存问题
- 迁移问题

## 共存问题

下表列出了 OES NetWare 和 OES Linux 经过测试（并发现兼容）的操作系统和 eDirectory 版本：

| 平台 | eDirectory 版本 |
|---|---|
| NetWare 6.5 SP2 | eDirectory 8.7.3 IR2 (eDirectory 8.7.3.2) |
| NetWare 6.0 SP5 | eDirectory 8.6.2 |
| NetWare 5.1 SP8 | eDirectory 8.7.3 |
| NetWare 5.1 SP7 | eDirectory 8.7.3 |
| NetWare 5.1 | NDS 8 (必须具有最新版本的 NDS 8 和 eDirectory 8.7 架构扩展) |
| NetWare 4.2 | NDS 6 (6.21 或更高版本) |
| SLES 9 | eDirectory 8.7.3 |
| SUSE LINUX Professional 9.1 | eDirectory 8.7.3 |
| Red Hat AS 3.0 | eDirectory 8.7.3 IR 3 (eDirectory 8.7.3.3) |
| Windows 2003 Server | eDirectory 8.7.3 IR 3 (eDirectory 8.7.3.3) 或更高版本 |
| Windows 2003 Server | Active Directory（通过 Identity Manager 同步用户） |
| Windows 2000 Advanced Server | eDirectory 8.7.3 IR 3 (eDirectory 8.7.3.3) 或更高版本 |

### 表 1-4 平台 eDirectory 版本

| 平台 | eDirectory 版本 |
|---|---|
| Windows NT | NT Domain（通过 Identity Manager 同步用户） |
