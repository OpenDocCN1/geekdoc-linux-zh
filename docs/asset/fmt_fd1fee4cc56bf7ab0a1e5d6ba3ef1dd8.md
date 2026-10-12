
- 基于 Linux v2.6 内核的 SLES9 操作系统以及所有与 SLES9 的服务
- 最新 Novell 企业 Linux 服务 (Novell Enterprise Linux Services)
- 允许两个操作系统无缝共存和管理的通用管理工具

鉴于 NetWare 和 Linux 是非常不同的操作系统，两个平台之间的可用服务存在某些程度的差异并不意外。然而，Novell 在为两个平台提供一套通用核心服务方面取得了令人赞叹的工作，但由于每个平台提供的某些服务不同，仍然存在特定的差异。表 1.1 列出了大多数 OES 服务及其提供的平台。如您所见，大多数服务在两个平台上都可用，因此组织可以根据其特定环境在最合适的平台上选择这些服务。此表还引用了书中讨论每项服务的所对应章节。

### 表 1.1 OES 服务的平台支持情况

| OES 服务 | 提供平台 | 注释 |
| :--- | :--- | :--- |
| **第一部分：Open Enterprise Server 概览** | | |
| iManager | 都 | 基于 Web 的 OES 管理控制台。 |
| Novell Remote Manager | 都 | 基于 Web 的 NetWare 和 Linux 操作系统管理控制台。 |
| iMonitor | 都 | 基于 Web 的目录监控和维护控制台。 |
| Novell Client | 都 | 用于访问 NetWare 和 Linux NCP 服务的客户端工具。 |
| Identity | 都 | 提供透明的 eDirectory 身份验证。 |
| NetDrive Client | 都 | 文件重定向器，用于在不安装完整 Novell Client 的情况下映射本地驱动器。 |
| NICI Client | 都 | Novell 国际加密基础设施。提供访问 eDirectory 中强大的加密和安全功能的权限。 |
| NMAS Client | 都 | Novell 模块化身份验证服务。为一组强大的身份验证和安全方法提供桌面支持。 |
| Package Management ConsoleOne | Linux, NetWare | 通过 YaST 管理的 OES 组件。基于 Java 的 NetWare 管理控制台。提供 Linux 版本下载。 |
| Native File Access Native eDirectory | NetWare | 为 Windows、Apple 和 UNIX 客户端提供对 NetWare 服务器资源的连接。Linux 通过 NFS 和 Samba 提供此服务。 |
| **第二部分：Open Enterprise Server 基础设施** | | |
| Novell | 都 | 全面的、支持 LDAP 的目录服务。 |
| DNS/DHCP 服务 | 都 | IP 地址管理工具套件。 |
| Nsure Identity Manager | 都 | 用户配置服务。 |
| Novell Storage Services (NSS) | 都 | 健壮的日志文件系统。 |
| 集群支持 | 都 | 关键网络资源的高可用管理。 |
| 多处理器支持 | 都 | 利用多处理器硬件，其线程架构允许进程在多个处理器上同时运行。 |
| 控制台工具 | 都 | 在 NetWare 和 Linux 控制台上提供的细粒度配置和管理选项。 |
| NICI | 都 | Novell 国际加密基础设施。eDirectory 强大安全功能的基础。 |
| NMAS | 都 | Novell 模块化身份验证服务。为一组强大的身份验证和安全方法提供桌面支持。 |
| Open WBEM CIMOM | Linux | 基于 Web 的 Linux 管理基础设施。 |
| Linux 用户管理 | Linux | 支持 eDirectory 的 Linux 用户管理。 |
| NCP Server | Linux | Linux 上 NetWare 核心协议服务。NetWare 的核心组件。 |
| Nsure Audit | NetWare | 跨平台审计服务。 |
| **第三部分：Open Enterprise Server 用户访问** | | |
| iPrint | 都 | 基于互联网打印协议 (IPP) 的打印管理。 |
| iFolder | 都 | 个人的基于服务器的文件存储和同步服务。 |
| 存储管理服务 (SMS) | 都 | 高级备份、恢复和数据迁移服务。 |
| iSC 支持 | 都 | 基于 IP 的 SCSI 存储网络。 |
| FTP 服务器 | 都 | 文件传输协议。访问 Net 上文件的传统方法。 |
| NetStorage | 都 | 安全的文件存储和基于互联网的访问。 |
| Samba | Linux | Microsoft SMB/CIFS 协议的开源实现。NetWare 通过原生文件访问提供此服务。 |

# 什么是 Open Enterprise Server (OES)

OES 服务 | 提供平台 | 注释

## 第三部分：OPEN ENTERPRISE SERVER 用户访问

| OES 服务 | 提供平台 | 注释 |
|---|---|---|
| DFS | NetWare | 分布式文件系统。基于 eDirectory 的分布式 NetWare 文件结构访问。 |

## 第四部分：OPEN ENTERPRISE SERVER WEB 服务

| WEB 服务 | 提供平台 | 注释 |
|---|---|---|
| Apache Web Server | 都 | 极其强大且流行的开源服务器。 |
| Tomcat Servlet 引擎 | 都 | Web 容器，用于在 Apache Web Server 中提供 Java Servlet 和 Java Page 支持。 |
| Java 虚拟机 (JVM) | 都 | OES 基于 Web 的控制台使用的 Java 解释器。 |
| eGuide | 都 | 基于 Web 的 eDirectory 查询工具，通常用于基于目录的白页查询。 |
| 虚拟办公室 (Virtual Office) | 都 | 基于 Web 的工作组协作环境。 |
| 快速查找 (Quickfinder) | 都 | 网站索引服务器。 |
| MySQL 数据库 | 都 | 开源结构化查询语言 (SQL)数据库。 |
| OpenSSH | 都 | 用于远程访问的安全 Shell 服务器。 |
| Perl 和 PHP | 都 | 强大的脚本语言。 |

本书的其余部分将讨论表 1.1 中列出的每个支持 Linux 的服务。将提供每个服务的常用管理信息，包括安装、配置以及持续维护和故障排除。

## 瞬时访问 (Instant Access)

### 准备安装

- 确保您的服务器硬件符合 OES Linux 的最低要求：
  - 带有 Pentium II 或 AMD K7 450MHz 处理器的服务器级计算机（推荐 Pentium III、Pentium 4、AMD K8 或更高版本）
  - 512MB 内存（推荐 1GB）
  - 2GB 可用且未分区的硬盘空间（推荐 10GB；根据 OES 组件的实现情况，可能需要额外空间）
  - 4X CD-ROM 驱动器（推荐 48X）
- 在创建新的 OES Linux 环境之前，规划好 OES Linux 文件系统、eDirectory 树和网络配置。
- 在现有的 SLES9 服务器上实施 OES for Linux 之前，确保您已进行完整备份并验证可以从备份中恢复数据。

### 配置安装源

- 使用 `netInstall.sh` 配置基于网络的安装源。该脚本可以通过以下 URL 获取：http://www.novell.com/documentation/oes/script/netInstall.sh
- 使用网络协议（如 NFS、HTTP 或 FTP）导出您的安装源目录。
- 要安装带有 OES 的新 SLES9 服务器，将 OES CD1 CD-ROM 插入服务器的 CD-ROM 驱动器并重启服务器。按照后续安装提示操作。
- 确保 Linux 验证设置为使用本地文件进行验证——而不是基于 OpenLDAP 的 LDAP 验证。
- 确保已配置静态 IP 地址以及有效的主机名和域名（可在 DNS 中解析）。
- 通过将 OES CD1 CD-ROM 插入服务器的 CD-ROM 驱动器开始安装，然后使用 YaST 开始 OES 安装。

OES Linux 的安装是一个非常直接的过程。然而，投入一些时间进行规划将有助于确保安装尽可能顺利，并减少因误解需求（如网络或目录布局）而导致重复过程的概率。本章将讨论这些重要的准备步骤，这些步骤应该在安装 OES Linux 之前完成。

本章还将描述如何配置网络安装源，以减少多次安装的复杂性并提高安装过程的速度。最后，还讨论了 OES Linux 的安装过程以及将 SLES9 服务器升级到 OES Linux 的过程。
