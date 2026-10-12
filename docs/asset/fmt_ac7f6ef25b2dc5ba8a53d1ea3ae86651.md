
## 8.5 部署高可用集群

Red Hat Linux Servers 和 SUSE Enterprise Servers 都为其各自的 Linux 操作系统提供了附加产品，可提供高可用（HA）故障转移集群。这些产品可以被部署，以增加 LinuxONE 上工作负载的可用性和可靠性。在导致一个集群节点故障的灾难性事件期间，运行在该节点上的应用程序可以由集群的其他成员之一自动启动，且无感知的停机时间。SUSE Enterprise Server High Availability Extensions 提供了地缘分布集群，允许从远程站点重启数据库或应用程序。

## 8.6 部署 MediaWiki 和 MySQL

MediaWiki 是一个流行的应用程序，它是一个源自 Wikipedia 的通用 wiki 平台。它用 PHP 编写，并使用 MySQL 作为后端数据库。这种配置通常被称为 LAMP 服务器，意味着该应用采用了 Linux、Apache、MySQL 和 PHP。Web 2.0 是 LinuxONE 的理想工作负载。

x86 上的 Linux 环境与 LinuxONE 上的环境一样大，极少数例外。x86 上的配置文件位置与你在 LinuxONE 上的 Linux 镜像位置相同，除非你选择将它们放在不同的地方。在这里，例如 MySQL 配置通常只需要从 x86 服务器复制到 LinuxONE 服务器，并放在文件系统的相同位置（`/etc/my.cnf`）。

在执行迁移到生产环境之前，迁移到 LinuxONE 应该先在测试环境中进行测试。

在本示例中，MySQL 数据库包含在外部 SCSI 磁盘的独立分区上。同样，Apache Web 服务器的 DocumentRoot 也存储在自己的外部 SCSI 磁盘上，与存储 MySQL 数据库的 LUN 不同。

在当今的数据中心中，以这种方式在外部磁盘上存储数据是常见的。这种做法使得服务从一个主机移动（迁移）到另一个主机变得更容易。它将操作系统和各种服务商品化。这是工业界处理此类任务的首选做法：

- 使用配置管理工具维护操作系统和服务的配置
- 使用云工具或外部应用程序（如 Puppet、Chef 或 caffeine-hx）将操作系统和服务的配置部署到虚拟机上

基础设施可以轻松调整和扩展以满足需求，同时确保数据从主存储系统中随处可用。

在本示例中，应用程序数据存储在外部磁盘上。虽然可以备份数据、将数据从一个主机传输到另一个主机并将数据重新导入到新的运行服务中，但这种方法非常慢。这里演示的方法是完成迁移任务的一种更快的方法。

### 8.6.1 分析与规划

遵循第 43 页第 4 章“迁移过程”以及第 55 页第 5 章“迁移分析”中的概述和建议，在进行这些迁移活动之前应进行适当的规划和分析。识别如何分配和组织虚拟资源的检查清单。

对于此场景，Linux 镜像已经就绪并安装了最小化的 Linux 操作系统。Linux 虚拟机称为 LSUNDB2，运行的是 SUSE Linux Enterprise 11 SP3，配备一个虚拟 CPU 和 1 GB 虚拟内存。假设已经设置了可用的包管理（RPM）仓库作为安装源，用于安装应用程序软件。

### 8.6.2 安装 LAMP 栈

可以通过 SUSE Linux Enterprise 11 的 YaST 完成应用程序软件的安装。为了更好地说明 LAMP 在 SUSE Linux Enterprise 和 RHEL 上的通用性，这些指令使用了命令行界面（CLI），并提供了适用于 SUSE Linux Enterprise 和 RHEL 的示例命令。

#### 在 SUSE Linux Enterprise Server 上安装 LAMP

首先，确保 SUSE Linux Enterprise Server 拥有用于 LAMP 服务器的模式（相关包的集合）。使用 `zypper info -t pattern lamp_server` 查看与 LAMP 服务器关联包。

示例 8-28 显示了运行以下命令 `zipper info -t pattern lamp_server` 时 LAMP 显示有用信息：

> 示例 8-28 zypper 的 LAMP 模式输出
Insubd2:"$ `zypper info -t pattern lamp_server`
Loading repository data...
Reading installed packages...

pattern lamp_server 示例:
Repository: SLES_DVD
Name: lamp_server
Version: 11-38.44.33
Arch: s390x
Vendor: SUSE LINUX Products GmbH, Nuernberg, Germany
Installed: No
Summary: Web and LAMP Server
Description:
用于设置能够提供静态、动态和交互内容（如网商店）的服务器的软件。这包括 Apache HTTP Server、数据库管理系统 MySQL 以及 PHP、Python、Ruby on Rails 或 Perl 等脚本语言。
Contents:

| S | | Type | Dependency |
|---|---|---|---|
| mysql | | package |

注意：lamp_server 模式包含了 Apache 和 MySQL 组件，但缺少 PHP 组件。这是因为令人困惑的是，“LAMP”中的“P”代表的是“Ruby”，它通常被用作服务器端动态网页引擎。

通过执行以下命令安装 Apache 和 MySQL 包：
`zypper install -t lamp_server`

`zipper` 命令报告预计将安装哪些包，然后提示确认。按 y 和回车安装包。

通过执行以下命令安装剩余的 PHP 包：
`zypper install apache2-mod_php53 php53-mysql`

#### Red Hat Enterprise Linux上的 LAMP

虽然 RHEL 拥有与 SUSE Linux Enterprise Server 类似的机制来表示包集合，但 RHEL 没有名为 LAMP 的组。

#### 在 SUSE Linux Enterprise Server 上安装 LAMP

首先，确保 SUSE Linux Enterprise Server 拥有 LAMP 服务器的模式（相关包的集合）。使用 `zypper info -t pattern lamp_server` 查看与 LAMP 服务器关联包。

示例 8-28 显示了运行以下命令 `zipper info -t pattern lamp_server` 时 LAMP 显示的有用信息：

> 示例 8-28 zypper 的 LAMP 模式输出
Insubd2:"$ `zypper info -t pattern lamp_server`
Loading repository data...
Reading installed packages...

示例  lamp_server 示例:
Repository: SLES_DVD
Name: lamp_server
Version: 11-38.44.33
Arch: s390x
Vendor: SUSE LINUX Products GmbH, Nuernberg, Germany
Installed: No
Summary: Web and LAMP Server
Description:
用于设置能够提供静态、动态和交互内容（如网商店）的服务器的软件。这包括 Apache HTTP Server、数据库管理系统 MySQL 以及 PHP、Python、Ruby on Rails 或 Perl 等脚本语言。
Contents:

| S | | Type | Dependency |
|---|---|---|---|
| mysql | | package |

注意：lamp_server 模式包含了 Apache 和 MySQL 组件，但缺少 PHP 组件。这是因为令人困惑的是，“LAMP”中的“P”代表的是“Ruby”，它通常被用作服务器端动态网页引擎。

通过执行以下命令安装 Apache 和 MySQL 包：
`zypper install -t lamp_server`

`zipper` 命令报告预计将安装哪些包，然后提示确认。按 y 和回车安装包。

通过执行以下命令安装剩余的 PHP 包：
`zypper install apache2-mod_php53 php53-mysql`

#### Red Hat Enterprise Linux上的 LAMP

虽然 RHEL 拥有与 SUSE Linux Enterprise Server 类似的机制来表示包集合，但 RHEL 没有名为 LAMP 的组。

### 8.6.3 启动并测试组件

在迁移 MediaWiki 软件之前，配置并测试 Apache、PHP 和 MySQL 以确保它们正常工作。

此示例中的 Apache 和 MySQL 配置是简单的，而你的配置可能更复杂。迁移 Apache 和 MySQL 配置可能会增加调试变量。

显示版本的常用方法是运行 `apachectl -v` 命令，SUSE Linux Enterprise 和 RHEL 都是相同的。

示例 8-29 显示了在 SUSE Linux Enterprise 中执行此命令显示的 Apache 版本：
`apachectl -v`

> 示例 8-29 apachectl 的输出
Insubd2:~ # `apachectl -v`
Server version: Apache/2.2.12 (Linux/SUSE)
Server built: March 27 2013 18:57:40
```
