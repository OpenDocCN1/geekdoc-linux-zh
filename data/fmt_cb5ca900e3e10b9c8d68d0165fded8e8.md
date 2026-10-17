
并将其保存到 `/var/opt/mssql/secrets/passwd`。将权限更改为仅限 root 用户可读：

```bash
sudo chown root:root /var/opt/mssql/secrets/passwd
sudo chmod 400 /var/opt/mssql/secrets/passwd
```

最后，创建可用性组资源。运行以下命令：

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=agl-master meta notify=true
```

基本上，这是在使用 `pcs` 来管理集群资源。在这种情况下，它创建了一个新资源 `ag_cluster`。`mssql` 是一个定义的资源提供者。由于使用了 `master` 选项，因此创建了一个主/从资源。

## 运行在 Linux 上的 SQL Server 2017

与我们的红帽企业版 Linux 的过程类似，运行以下命令为集群创建一个虚拟 IP 资源。你需要指定一个有效的静态 IP 地址：

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=13.91.249.38
```

接下来，添加关联约束以确保可用性组主副本和虚拟 IP 资源运行在同一台主机上：

```bash
sudo pcs constraint collocation virtualip ag-cluster-master INFINITY --with-rsc-role=Master
```

最后，运行以下命令确保先启动可用性集群资源，然后启动虚拟 IP 资源：

```bash
sudo pcs constraint order promote ag-cluster-master then start virtualip
```

## 第 7 章：高可用与灾难恢复

第二步需要你移除位置约束：

```bash
sudo pcs clear ag-cluster-master
sudo pcs constraint --full
```

## Linux 版 Microsoft SQL Server 2017

![](img/0a5d3f27ca07081d5ee426b77bb624b8_265_0.png)

- 分组 (Group by)
- sqllinux1 AdventureWorks 同步无数据丢失
- sqllinux2 AdventureWorks 同步无数据丢失
- sqllinux3 AdventureWorks-3 同步无数据丢失

图 7-13 手动故障到 sqllinux2

## 总结

本章介绍了 Linux 上 SQL Server 高可用性和灾难恢复的基础知识。虽然讨论了多个功能，但本章大部分集中在 Always On 可用组上。

Windows 和 Linux 上的可用性组可用于高可用灾难恢复配置，并用于迁移和升级，甚至用于扩展一个或多个数据库的可读副本。

Windows 和 Linux 上可用性组的区别在于，在 Windows 中，Windows Server 故障转移集群（WSFC）是内置在操作系统中的，且 SQL Server 可用组是感知集群。在 Linux 中，可用性组依赖于 Pacemaker 而不是 WSFC。由于 Linux 不提供内置集群解决方案，所有三个支持 SQL Server 的 Linux 发行版都使用了它们自己的版本的 Pacemaker。SQL Server 高可用包（也称为 Pacemaker 的 SQL Server 资源代理）是一个可选包，在 Linux 上实现高可用解决方案时必须安装它。

有关 Windows 上可用性组的更多细节，请参阅 SQL Server 文档 https://docs.microsoft.com/en-us/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server。

有关 Linux 上可用性组的更多信息，请访问 https://docs.microsoft.com/en-us/linux/sql-server-linux-availability-group-overview。

请查看 Red Hat 高可用性附加组件文档：https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/high_availability_add-on/reference/index。

SUSE 企业高可用扩展文档可在 www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html 获取。

# 第 8 章

## 安全

本章

- SQL Server 安全简介
- 透明数据加密 (TDE)
- 始终加密 (Always Encrypted)
- 行级安全 (Row-Level Security)
- 动态数据掩码 (Dynamic Data Masking)
- 总结

![](img/0a5d3f27ca07081d5ee426b77bb624b8_268_0.png)

## Linux 版 Microsoft SQL Server 2017

本章介绍了 SQL Server 安全，适用于 Windows 和 Linux 环境。它涵盖了 SQL Server 安全如何分层工作，例如保护数据本身、控制对数据的访问以及监控访问。本章还详细介绍了在产品最新版本中引入的一些最新 SQL Server 安全功能，包括透明数据加密 (TDE)、始终加密 (Always Encrypted)、行级安全 (Row-Level Security) 和动态数据掩码 (DDM)。

Windows 上提供的所有安全功能在 Linux 上均可用，但 Active Directory 除外，后者将在未来的更新中包含。

- **透明数据加密**：此功能旨在保护数据库数据和事务日志文件免受对物理介质的未经授权的访问。它在页级别执行实时 I/O 加密，尽管数据在内存中或通过其他通信通道时不会被加密。

- **始终加密**：这是一种客户端加密技术，旨在保护敏感数据，数据在数据库引擎中始终保持加密状态。

- **行级安全**：此功能根据执行查询的用户身份来控制对表中行的访问。该功能的优势在于，访问限制逻辑定义在 SQL Server 中，而不是定义在应用程序层级。

- **动态数据掩码**：此安全功能旨在通过对非特权用户进行掩码处理来限制敏感数据的暴露。

## SQL Server 安全简介

Linux 版 SQL Server 支持与 Windows 版 SQL Server 相同的企业级安全能力，且所有这些功能都已构建在产品中。微软分层定义了 SQL Server 安全，如图 8-1 所示。

第一层安全是关于保护和加密数据本身，例如使用静态地加密以在案例文件或磁盘被盗时保护数据。SQL Server 提供了静态加密功能，例如 TDE、备份加密和单元级加密。另一种类型的加密是传输中加密，它确保了 SQL Server 通信的安全，并基于传输层安全 (TLS) 协议。最后一种加密类型是客户端加密，也称为始终加密，它使数据在数据库引擎中始终保持加密状态，且仅在客户端可见。TDE 和始终加密在本文章中都有详细介绍。

![](img/0a5d3f27ca07081d5ee426b77bb624b8_270_0.png)

图 8-1 SQL Server 安全层级

SQL Server 的第二层安全是关于通过身份验证和授权过程控制对数据的访问。SQL Server 拥有非常细粒度的权限系统，允许你控制几乎每个 SQL Server 对象的特定访问。Windows 版 SQL Server 支持 SQL Server 和 Active Directory 身份验证。Active Directory 身份验证目前在 Linux 上可用，但计划在未来实现。此外，行级安全和动态数据掩码等功能提供了控制访问的额外方法，并在本文中中介绍。

最后一层通过记录用户操作来监控访问。SQL Server 提供了审核功能，允许你指定要跟踪哪些用户、操作和对象。最后，从 2018 年 5 月 25 日开始，通用数据保护条例 (GDPR) 将作为一项保护个人数据的法律引入。其中，个人有权访问其数据、修正错误并删除数据。另一方面，组织被要求使用适当的安全措施保护个人数据，并在泄露时提供通知。有关 GDPR 的更多详细信息请参考官方文档。

本文章其余部分将提供透明数据加密、始终加密、行级安全和动态数据掩码功能的概述。有关这些和其他功能的更多信息，请参阅 SQL Server 文档。

## 透明数据加密

透明数据加密（也称为静态加密）保护数据库数据和事务日志文件免受对物理介质的未经授权访问。当数据库配置 TDE 时，即使访问数据库文件或数据库备份也无法获取数据。TDE 通过在页级别执行实时 I/O 加密来工作，这意味着页在写入磁盘之前被加密，在从内存读取时被解密。注意，数据在内存中不加密，跨其他通信通道时也不加密。

尽管这意味着启用 TDE 后，未经授权的人无法恢复你的数据库，但这也意味着你需要拥有与证书相关的证书和私钥才能进行 TDE 配置，因此你应该立即对其进行备份。如果你想在不同的 SQL Server 实例上挂载或恢复数据库，将需要它们。在后面的“在另一个 SQL Server 实例上挂载或恢复 TDE 数据库”部分将显示如何操作的示例。

如果 SQL Server 实例中有一个加密数据库，tempdb 数据库将被加密。这有助于加密未加密数据库的性能。如果数据库用于数据库镜像、日志传送或可用性组配置，则所有相关的数据库（镜像、辅助或副本）也将将被加密。

让我们通过一个示例来展示 TDE 如何工作。首先，我们需要创建一个主密钥和一个证书，类似于我们在第 7 章中所做的，当时我们使用证书来验证镜像端点之间的通信。

```sql
USE master;
GO
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Pa$$ssword1!';
GO
CREATE CERTIFICATE MyCertificate WITH SUBJECT = 'My Certificate';
GO
```

## 第 8 章：安全性

数据库主密钥是一个对称密钥，用于保护数据库中存在的证书私有密钥和非对称密钥。`CREATE CERTIFICATE` 语句用于向 SQL Server 数据库中添加证书。`CREATE DATABASE ENCRYPTION KEY` 语句现在可用于创建数据库加密密钥并通过证书对其进行保护。运行以下语句：

```sql
USE AdventureWorks2012
GO
CREATE DATABASE ENCRYPTION KEY
WITH ALGORITHM = AES_128
ENCRYPTION BY SERVER CERTIFICATE MyCertificate;
GO
```

注意以下关于备份证书以及与证书相关的私钥的警告：

> 警告：用于加密数据库加密密钥的证书尚未备份。您应该立即备份该证书以及与其相关的私钥。如果证书不可用，或者您必须在另一个服务器上恢复或附加数据库，您必须同时拥有证书和私钥的备份，否则您将无法打开数据库。

因此，让我们遵循该建议，备份证书以及与证书相关的私钥：

```sql
USE master
GO
BACKUP CERTIFICATE MyCertificate
TO FILE = 'MyCertificate'
WITH PRIVATE KEY
(
FILE = 'SQLPrivateKeyFile',
ENCRYPTION BY PASSWORD = 'Pa$$ssword!'
)
```

`BACKUP CERTIFICATE` 语句用于将证书及其相关的私钥都导出到文件中。在我们的案例中，证书将保存在 `/var/opt/mssql/data/MyCertificate`，而与证书相关的私钥将导出到 `/var/opt/mssql/data/SQLPrivateKeyFile`。如果您使用的是 Windows 平台，两者都将保存在 `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA` 文件夹中。

现在我们准备好使用 `ALTER DATABASE SET ENCRYPTION` 语句将数据库设置为加密：

```sql
ALTER DATABASE AdventureWorks2012
SET ENCRYPTION ON
GO
```

此时，数据库正在使用 TDE（透明数据加密）。让我们进行一个快速测试，执行并恢复备份：

```sql
BACKUP DATABASE AdventureWorks2012 TO DISK = 'AdventureWorks2012.bak'
```

数据库备份将保存存在 `/var/mssql/data/AdventureWorks2012.bak`。现在尝试在 SQL Server 实例中使用新的数据库名称恢复备份文件：

```sql
RESTORE DATABASE [AdventureWorks2012New] FROM DISK = N'/var/mssql/data/AdventureWorks2012.bak' WITH FILE = 1, MOVE N'AdventureWorks2012' TO N'/var/opt/mssql/data/Adventure/AdventureWorks2012.mdf', MOVE N'AdventureWorks2012_log' TO N'/var/opt/mssql/data/AdventureWorks2012_log.ldf', NOUNLOAD, STATS = 5
```

运行以下查询将显示数据库已恢复并已加密。将列出三个数据库：AdventureWorks2012、AdventureWorks2012New，以及之前解释过的 tempdb。

```sql
SELECT name, is_encrypted FROM sys.databases WHERE is_encrypted = 1
```

尝试将此数据库恢复到另一个 SQL Server 实例将行不通，而是会返回“无法找到指纹对应的证书”的错误消息。下一节将解释如何在另一个 SQL Server 实例上使用 TDE 恢复数据库。

## 将 TDE 数据库附加或恢复到另一个 SQL Server 实例

遵循上一个示例，现在我向您展示如何将 TDE 恢复到另一个 SQL Server 实例。请记住，此时在 Linux 安装上您只能有一个 SQL Server 实例，但在 Windows 环境中您可以有多个实例。因此，在 Linux 安装上，这将涉及将文件复制到另一个服务器，并可能还需要更新其权限。

我们将开始复制数据库备份文件，将其移动到 `/var/opt/mssql/data` 目录，并确保 mssql 用户可以访问它。替换主机目标名称或 IP 地址以及用户和目录目标。此命令在原始服务器上执行，文件将复制到目标服务器的我的家目录：

```bash
sudo cp /var/opt/mssql/data/AdventureWorks2012.bak bvarez@23.99.83.158:~home/bvarez
```

现在在目标服务器上运行以下命令：

```bash
sudo cp AdventureWorks2012.bak /var/opt/mssql/data
# cd /var/opt/mssql/data
# chown mssql AdventureWorks2012.bak
# chgrp mssql AdventureWorks2012.bak
```

显然，您可以在 Windows 上使用相应的目录遵循完全相同的练习，例如 `C:\Program Files\Microsoft SQL Server\MSSQL14\MSSQLSERVER\DATA` 或其他位置。回到 SQL Server 管理 Studio，使用原始数据库名 AdventureWorks2012 恢复第二个服务器：

```sql
RESTORE DATABASE [AdventureWorks2012] FROM DISK = '/var/opt/mssql/data/AdventureWorks2012.Bak' WITH FILE = 1, MOVE N'AdventureWorks2012' TO N '/var/opt/mssql/data/AdventureWorks2012.mdf', MOVE N'AdventureWorks2012_log' TO N'/var/opt/mssql/data/AdventureWorks2012_log.ldf', NOUNLOAD, STATS = 5
```
