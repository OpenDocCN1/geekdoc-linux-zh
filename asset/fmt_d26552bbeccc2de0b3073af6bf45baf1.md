
## T-SQL 配置

本节中的剩余配置将在 T-SQL 语句在服务器级别完成。如所述，也可以使用 `sqlcmd` 工具或任何可以向数据库引擎提交 T-SQL 语句的客户端工具在服务器级别完成。在这里我们将使用 SQL Server Management Studio。（在下一节中，我将介绍可用性组的用户界面，它需要 SQL Server Management Studio。）

启动 AlwaysOn 健康扩展事件会话。AlwaysOn health 是一个预配置的扩展事件会话，非常有用且方便，可以帮助你检测并排除可用性组的潜在问题。使用 `ALTER EVENT SESSION` 启动会话，如下：

```sql
ALTER EVENT SESSION AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON)
```

> **注意**
> 有关 AlwaysOn_health 扩展事件会话的更多详细信息，请参阅 https://msdn.microsoft.com/en-us/library/dn135324(v=sql.110).aspx。

# Linux 上的 Microsoft SQL Server 2017

接下来，创建一个用于可用性组配置的登录名和用户名。为此密码以及本章要求的其他密码指定一个强密码：

```sql
CREATE LOGIN ag_login WITH PASSWORD = 'Pa$$sword!';

CREATE USER ag_user FOR LOGIN ag_login
```

对于 SQL Server 可用性组配置，我们需要一个证书来验证镜像端点（endpoints）之间的通信。对于 SQL Server 2017，使用证书是支持的身份验证，但 Windows 身份验证将在未来的版本中启用。此步骤基本上要求创建一个主密钥（master key）和一个证书。主密钥是一个对称密钥，用于保护证书的私钥以及数据库中存在的非对称密钥。`CREATE CERTIFICATE` 语句向 SQL Server 数据库中添加证书。最后，`BACKUP CERTIFICATE` 用于导出证书和私钥。在我们的情况下，证书将保存到 `/var/opt/mssql/data/ag_certificate.cer`。此外，证书的私钥将导出到 `/var/opt/mssql/data/ag_certificate.pvk`。

在主副本上运行以下语句来创建并备份证书：

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Pa$$sword!';

CREATE CERTIFICATE ag_certificate WITH SUBJECT = 'ag';

BACKUP CERTIFICATE ag_certificate
TO FILE = '/var/opt/mssql/data/ag_certificate.cer'
WITH PRIVATE KEY (FILE = '/var/opt/mssql/data/ag_certificate.pvk', DECRYPTION BY PASSWORD = 'Pa$$sword!');
```

现在你可以验证文件是否已在 `/var/opt/mssql/data/` 创建：

```bash
$ ls -l /var/opt/mssql/data/ag*
-rw-r--r 1 mssql mssql 667 Jan 14 04:50 ag_certificate.cer
-rw-r--r 1 mssql mssql 1212 Jan 14 04:50 ag_certificate.pvk
```

现在让我们这些文件复制到其他服务器的相同位置，并授予它们与主副本（principal replica）相同的权限。实现此目标有方法。在第 1 节中，我们使用 PuTTY Secure copy 在 Windows 和 Linux 之间复制文件。在这种情况下，我们将使用 `scp`，这是用于在网络上复制文件的安全复制命令。

`scp` 命令可以使用以下格式复制文件：

```bash
scp username@servername:/directory
```

运行以下命令，替换目标主机（例如 `sqllinux2`）或 IP 地址，以及目标用户和目录。此命令在主副本上执行，文件将被复制到两个备用副本的主目录：

```bash
sudo scp /var/opt/mssql/data/ag* bnevarez@servername:/home/bnevarez
```

文件是以用户 bnevarez 身份复制的，我仍然需要将它们复制到正确的目录并赋予正确的权限。运行以下命令：

```bash
# cp /home/bnevarez/ag* /var/opt/mssql/data
# cd /var/opt/mssql/data
# chown mssql:mssql ag*
# chmod 600 ag*
```

## 验证可用性组

现在让我们验证可用性组的配置。在每个副本上运行以下查询语句：

```sql
SELECT * FROM sys.dm_hadr_availability_group_states;
```

# 第 7 章：高可用性与灾难恢复

接下来我们将在主副本 sqlonlinux1 上创建可用性组。`CREATE AVAILABILITY GROUP` 语句有许多选项。以下语句指定了几个项。`DB_FAILOVER` 值为 `ON` 表示可用性组中的数据库任何非 `ONLINE` 状态都会触发自动故障转移。如果选择 `OFF`，则意味着仅使用实例的健康状况来触发自动故障转移。

`CLUSTER_TYPE` 是 SQL Server 2017 的新功能，用于定义集群类型，值可以是 `WSFC`、`EXTERNAL` 和 `NONE`。`WSFC` 用于在 Windows 上使用 WSFC 配置可用性组。`EXTERNAL` 用于 Linux 上使用 Pacemaker 等外部集群管理器。`NONE` 用于未使用集群管理器的情况。最后这种选择对于作为只读副本用于迁移或升级的可用性组配置有用。在 Linux 上的 SQL Server 实例上，你只会看到 `EXTERNAL` 和 `NONE` 选项。

`AVAILABILITY_MODE` 定义了主副本在数据库上提交事务之前，是否需要等待备副本确认日志记录的写入，其取值为 `ASYNCHRONOUS_COMMIT` 和 `SYNCHRONOUS_COMMIT`。第三种选择是 SQL Server 2007 CU1 的新功能 `CONFIGURATION_ONLY`，它定义了一个仅配置的副本或用于可用性组配置元数据的副本。`CONFIGURATION_ONLY` 可适用于任何版本的 SQL Server，且不适用于 `CLUSTER_TYPE` 为 `WSFC` 的情况。它主要在不支持文件共享的 Linux 环境中作为见证。

`FAILOVER_MODE` 定义了故障转移模式，可以是 `AUTOMATIC`、`MANUAL` 或 `EXTERNAL`。对于 Linux 安装，它始终为 `EXTERNAL`。

`SEEDING_MODE` 定义了备副本如何进行初始引导，可以选择 `AUTOMATIC` 或 `MANUAL` 选项。`ENDPOINT_URL` 使用托管可用性副本的 SQL Server 实例上的数据库镜像端点路径。如下面的示例所示，`ENDPOINT_URL` 需要一个系统名、完全限定域名或 IP 地址，以唯一地标识目标计算机系统，以及与伙伴服务器实例的镜像端点相关的端口号。

以下语句创建了一个具有三个同步副本的可用性组。请将服务器、完全限定域名等替换为你自己的信息。为了简单起见，仅使用了服务器名——在你的情况下，请也加上完全限定域名。

```sql
USE master
GO
CREATE AVAILABILITY GROUP agl1
WITH (DB_FAILOVER = ON, CLUSTER_TYPE = EXTERNAL)
FOR REPLICA ON
N'sqlonlinux1'
WITH (
  ENDPOINT_URL = N'tcp://sqlonlinux1:5022',
  AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
  FAILOVER_MODE = EXTERNAL,
  SEEDING_MODE = AUTOMATIC
),
N'sqlonlinux2'
WITH (
  ENDPOINT_URL = N'tcp://sqlonlinux2:5022',
  AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
  FAILOVER_MODE = EXTERNAL,
  SEEDING_MODE = AUTOMATIC
),
N'sqlonlinux3'
WITH (
  ENDPOINT_URL = N'tcp://sqlonlinux3:5022',
  AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
  FAILOVER_MODE = EXTERNAL,
  SEEDING_MODE = AUTOMATIC
);
```

值得注意的是，如果你运行两次，你会收到一个与 Windows 相关的消息，我在其他错误中也看到过：

Msg 41171, Level 16, State 2, Line 31: Failed to create availability group 'ag1',因为名为指定名称的 Windows Server Cluster (WSFC) 组已存在。操作已成功回滚。要重试创建可用性组，请删除或重命名 WSFC 组，或指定不同的可用性组名称重试操作。

接下来，为可用性组授予 `CREATE ANY DATABASE` 权限——现在，仅针对主副本 sqlonlinux1：

```sql
ALTER AVAILABILITY GROUP ag1 GRANT CREATE ANY DATABASE;
```

在另外两个副本 sqlonlinux2 和 sqlonlinux3 上运行这些语句。`ALTER AVAILABILITY GROUP` 的 `JOIN` 选项用于本地服务器来托管指定可用性组中的备副本。与 sqlonlinux1 相同，也向可用性组授予 `CREATE ANY DATABASE` 权限。

```sql
ALTER AVAILABILITY GROUP ag1 JOIN WITH (CLUSTER_TYPE = EXTERNAL);
GO
ALTER AVAILABILITY GROUP ag1 GRANT CREATE ANY DATABASE;
```

此时，可用性组已完全配置完成。现在可以回到主副本向可用性组添加数据库了。你可以使用现有数据库，也可以现在创建一个数据库。数据库需要处于完全恢复模式并有一个初始备份。运行以下语句执行此操作：

```sql
CREATE DATABASE AdventureWorks
ALTER DATABASE AdventureWorks SET RECOVERY FULL
BACKUP DATABASE AdventureWorks
TO DISK = N'/var/opt/mssql/data/AdventureWorks.bak'
```

再次在主副本 sqlonlinux1 上，我们可以使用 `ALTER AVAILABILITY GROUP` 的 `ADD DATABASE` 选项向可用性组添加一个或多个用户数据库。运行以下语句：

```sql
ALTER AVAILABILITY GROUP ag1 ADD DATABASE AdventureWorks
```

由于可用性组配置时 `SEEDING_MODE` 为 `AUTOMATIC`，此时数据库应该已经在备副本上创建。通过以下语句验证数据库已创建：

```sql
SELECT * FROM sys.databases
GO
SELECT @@SERVERNAME, DB_NAME(database_id), synchronization_state_desc, synchronization_health_desc
FROM sys.dm_hadr_database_replica_states
```
