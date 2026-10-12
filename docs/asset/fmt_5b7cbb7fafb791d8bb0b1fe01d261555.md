
# Unix 和 Linux 上的 Oracle DBA

## iAS 之前存在什么

在 iAS 之前，Oracle 有一个名为 `OAS` `Oracle Application Server` 的产品。该工具主要运行 `PL/SQL`，但也支持 `Java`。该产品正在从 4.0 版本被淘汰。尽管 `OAS` 和 `iAS` 在目的上相似，但 `iAS` 在内部有所不同且更先进。Oracle 提供了到 `iAS` 的升级路径，不需要对现有应用程序进行大量修改。

![](img/0735bb12e1d45128c662b4b409eb1bf1_487_0.png)

图 18.3

关键 IAS 组件。

## 模块

模块（或 `mods`）是 `IAS` 中 `OAS` 匣件的等价物。这些本质上是 Web 服务器的插件，允许其处理每种类型的客户端请求。每个请求都会路由到与其相关的 `mod`。以下列表描述了最常见的 `mod`：

- `mod_plsql`：等同于 `OAS` 的 `PL/SQL` 匣件。它将 `PL/SQL` 和存储 `Java` 过程的请求路由到数据库。
- `mod_jserv`：处理 `servlets` 和 `JSPs` 等 `Java` 请求。它将其路由到 Apache `JServ`。
- `mod_perl`：由此 `mod` 处理 `Perl` 请求。

## Oracle Forms, Reports 和 Discover

`DBA` 和 `PL/SQL` 开发人员应该熟悉这些工具中的每一个。`Oracle Forms` 长期以来一直是 Oracle 的关键应用工具，几乎不需要介绍。`Reports` 用于创建和显示管理报告，传统上与 `Forms` 捆绑在一起。`Discover` 是一个查询创建工具，允许你轻松地从数据库提取信息。传统上，这些工具独立于数据库存在。在 `IAS` 中，这些工具被捆绑在应用程序服务器内部。

## Oracle Portal

`Oracle Portal` 是 `WebDB` 的下一代产品，将在第 17 节“WebDB/Oracle Portal”中介绍。这种基于 `PL/SQL` 的工具最初用作数据库 Web化的快速方法。然而，现在此工具已成为设计动态互联网应用程序的强大方式。它现在与 `iAS` 捆绑。

## PSPs 和 JSPs

`iAS` 支持 `PL/SQL` 页面 `PSPs` 和 `Java` 页面 `JSPs`。这些基本上是带有嵌入代码标签的 HTML 页面，用于生成动态内容。当这些代码在浏览器上启动时，它们会在服务器端进行编译和执行（而不是在浏览器内部）。

## iFS

Internet 文件系统 `iFS` 是 Oracle 将普通文件存储在数据库而非普通文件系统的方法。以这种方式存储的文件看起来像是在映射的网络驱动器上，而不是在数据库中。用户可以正常访问此类文件，但 `iFS` 提供了锁定和版本控制等附加功能。此外，由于文件在数据库内部，可以对其进行索引以实现快速访问和保护，这由 Oracle 经证明的索引以及备份恢复方法提供。最后，通过将文件存储在数据库中，开发者可以使用 `XML` 对其进行操作。

## Oracle 8 JVM

这就是你在 `Oracle 8` 数据库中看到的 `Java` 虚拟机，它具有相同的作用：运行 `Java` 程序。通过此功能，`Java` 使 `iAS` 能够运行 `EJBs`、`CORBA` 服务器、`Java` 页面、`servlets` 和 `Java` 过程。更多信息请参阅第 16 节。

## 数据库缓存和 Web 缓存

Oracle 意识到通过缓存数据库信息、查询以及 Web 信息（如 `URL`），可以获得巨大的性能提升。到达 Web 服务器的许多请求通常需要通过 `SQL` 或 `PL/SQL` 访问数据库。通常，这些请求必须中继到数据库处理然后返回。然而，数据库缓存可以在中间层保留只读数据库信息，从而减少对实际数据库的访问。`Web Cache` 用于缓存 Web 信息（如 `URL`）。这些缓存减少了网络流量以及数据库和 Web 应用程序服务器的负载。

这些是 `iAS` 的高级功能。还有许多令人兴奋的功能，例如其无线选项，允许与手机和 `PDA` 通信（超出本书范围）。此外，每个新的 `iAS` 版本都比上一个版本有更多功能。因此，你需要跟进文档和发布说明，以避免错过新功能。

作为 `DBA`，你应该与 IT 员工的不同部门协作，以确定如何最有效地使用 `iAS`。例如，与你的 HTML Web 设计师协调，以确定 `Oracle Portal` 如何制作 Web 门户。毫无疑问，你的 `PL/SQL` 和 `Java` 开发人员应该包含在关于如何以及何处开发和部署应用程序的讨论中。他们对 Web 环境下的 `Forms`、`Reports` 和 `PL/SQL` 以及各种现有的 `Java` 组件将有宝贵的见解。不要忘记与 `SA`（系统分析师）人员沟通，以便他们知道在自己的服务器上运行 `iAS` 时会有什么预期。特别是由于 `iAS` 可以（并且应该）存在于与数据库独立的服务器上，并且由于它可以具有容错性，因此需要严谨的架构规划。

## 安装

本节概述了在 `Red Hat Linux` 上简单安装 `iAS 1.0.2.0` 的方法。服务器上已经安装了 `8.1.6` 数据库，但 `iAS 1.0.2.0` 软件版本是 `8.1.7`。出于测试目的，数据库和 `iAS` 将位于同一台物理机器上，但通常应避免这种配置。

在进行任何软件安装之前，请先阅读安装和配置指南 `ICG`。以下步骤用于安装 `iAS`：

1. 根据你安装的产品，Oracle `iAS` 需要大量的磁盘空间。企业版的安装可能超过 `3G`。请确保标准安装至少有 `2G` 可用空间。

```bash
[oracle@mikehat~$] df -m
Filesystem      1M-blocks Used Available% Mounted on
/dev/hda13      7875      66% /u01
[oracle@mikehat~$] 
```

2. 取消 `LD_LIBRARY_PATH` 环境变量。

```bash
[oracle@mikehat~$] unset LD_LIBRARY_PATH
```

3. 为 `iAS` 创建并设置一个新的 `ORACLE_HOME`。像所有最近 Oracle 产品一样，你必须使用独立的 `ORACLE_HOME`。

```bash
[oracle@mikehat~$] export ORACLE_HOME=/u01/app/oracle/ias10.2
```

4. 像在进行任何软件安装之前一样，阅读安装和配置指南 `ICG`。以下步骤用于安装 `iAS`：

11. 下一个屏幕要求你提供 `Oracle Portal` 将使用的 `DAD`（数据库访问描述符）、架构名称和数据库 `tnsname` 别名。如图 18.9 所示，接受默认值。数据库为 `rhdev1`，因此它将是 `TNS` 连接字符串。

![](img/0735bb12e1d45128c662b4b409eb1bf1_493_0.png)

图 18.9

`Oracle Portal` 的 `DAD`、架构和数据库。

12. 安装程序将要求你输入之前相同的信息，但这次是针对单登录选项。接受 `porta130_sso` 的默认值并输入你的数据库名称，如图 18.10 所示。

![](img/0735bb12e1d45128c662b4b409eb1bf1_493_1.png)

图 18.10

单登录 `DAD`、架构和数据库。

13. Oracle 将要求你提供用于企业 `Java` 引擎 `EJE` 的数据库全局数据库名称 `SID`。这是重命名后的 `Oracle 8i JVM`。Oracle 在手册中指出数据库在 `IAS ORACLE_HOME` 中创建，且应仅用于 `EJE`。如图 18.11 所示，使用默认 `SID` `ias1021` 和全局数据库名称 `ias1021.mike.com`。

![](img/0735bb12e1d45128c662b4b409eb1bf1_494_0.png)

图 18.11

提供 `EJE` 全局数据库名称和 `SID`。

14. 接下来，你被要求输入 `JDK 1.1.8` 的位置。在我的案例中，它位于 `/u01/app/oracle/jre/1.1.8`。如图 18.12 所示输入你的位置。

![](img/0735bb12e1d45128c662b4b409eb1bf1_494_1.png)

图 18.12

输入 `JDK 1.1.8` 位置。

15. 接下来会请求 `Portal-to-go` 仓库信息。在这里你需要输入主机名、监听器端口号、`SID`。如图 18.13 所示。

![](img/0735bb12e1d45128c662b4b409eb1bf1_495_0.png)

# 图 18.13

输入 `Portal-to-Go` 仓库信息。

16. 下一个屏幕提示你输入 `Portal-to-Go` 仓库的所有者。如图 18.14 所示，选择一个好记的用户名（如 `PTG_MANAGER`）和一个密码。
