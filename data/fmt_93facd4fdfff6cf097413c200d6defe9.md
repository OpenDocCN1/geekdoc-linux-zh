
## SQL Server 配置

本节介绍了最重要的 SQL Server 配置设置。这里涵盖的内容同时适用于 Windows 和 Linux 安装。我在本节早前的 `mssql-conf` 部分中讨论过如何配置 SQL Server 内存。在本节中，我将开始描述一种在配置 Linux 安装的可用内存时应该注意的 Linux 行为。

## Linux 内存溢出杀手 (Out-of-Memory Killer)

如果你是熟悉 Windows 世界的 SQL Server 管理员，你需要注意的 OOM 是一种 Linux 内核行为：当服务器内存不足时，内核开始杀死进程以释放内存并保持运行。这种行为由名为“内存溢出杀手”（OOM Killer）的机制控制，原则上，它是为了让内核更好地利用应用程序分配的内存而设计的优化。由于许多应用程序会预先分配内存且通常不会利用所有分配的内存，Linux 内核被设计为具有“过度提交”（overcommit）的能力，分配比实际可用更多的内存，以使内存使用更加高效。

在这种设计下，当应用程序确实使用所有分配的内存时，就会发生明显的问题。对于 SQL Server 实现，SQL Server 将是使用内存最多的应用程序，因此很可能是被杀掉的进程。

如果 SQL Server 进程被杀死且你知道可能有内存问题，请首先查看 `/var/log/messages` 中的 Linux 系统日志。OOM Killer 算法在 `/linux-mm.org/OOM_Killer` 中有记录，它旨在考虑几个因素来估计 OOM 分数，这包括尝试杀死最少的进程（最好只杀死一个）、恢复大量内存以及尽可能减少已完成工作的损失。

> 关于 SQL Server 进程被 OOM Killer 杀死的故障排除案例，请参见文章：https://blogs.msdn.microsoft.com/psql/2017/10/17/how-to-safeguard-sql-server-on-linux-from-killer/

避免 SQL Server 进程被 Linux 内核杀死的方法是正确配置内存服务器，为 SQL Server、操作系统以及可能运行在同一服务器上的任何其他进程分配适当的内存。你可以像本节之前解释的那样，使用 `mssql-config` 工具为 SQL Server 分配所需的内存。此外，如前文所述，妥善配置交换文件（swap file）也有帮助。你可以在启动时的错误日志中查看 SQL Server 的可用内存，如下所示：

```text
12/20/2017 5:12:16 AM Server Detected 6374 MB of RAM. 这是一个信息性消息，不需要用户操作。
```

## tempdb 配置

据我所知，正确配置 `tempdb` 是所有版本 SQL Server 的性能考虑因素之一。SQL Server 2016 带来了一些改进，例如在产品设置期间根据系统可用处理器的数量自动创建多个数据文件，或者默认的 `tempdb` 配置（它集成了跟踪标志 1117 和 1118 的行为）。由于 Linux 版 SQL Server 目前还没有在设置期间自动创建多个 `tempdb` 数据文件的功能，手动配置这仍然是一个重要要求。

`tempdb` 在很大程度上与经典的性能问题有关：`tempdb` 冲突。短时间内创建大量用户对象会导致锁冲突（latch contention）。

## Linux 版 Microsoft SQL Server 2017

![](img/0a5d3f27ca07081d5ee426b77bb624b8_131_0.png)

图 4-2 在 tempdb 上配置多个数据文件

此处显示了 SSMS 创建的相关 Transact-SQL 语句：

```sql
USE [master]
GO
ALTER DATABASE [tempdb] MODIFY FILE ( NAME = N'tempdev', SIZE = 4193404KB, FILEGROWTH = 104856KB )
GO
ALTER DATABASE [tempdb] ADD FILE ( NAME = N'tempdev2', FILENAME = N'/var/opt/mssql/data/tempdev2.ndf', SIZE = 4193404KB, FILEGROWTH = 104856KB)
GO
ALTER DATABASE [tempdb] ADD FILE ( NAME = N'tempdev3', FILENAME = N'/var/opt/mssql/data/tempdev3.ndf', SIZE = 4193404KB, FILEGROWTH = 104856KB)
GO
ALTER DATABASE [tempdb] ADD FILE (NAME = N'tempdev4', FILENAME = N'/var/opt/mssql/data/tempdev4.ndf', SIZE = 4194304KB, FILEGROWTH = 1048576KB)
GO
ALTER DATABASE [tempdb] MODIFY FILE (NAME = N'templog', SIZE = 4194304KB, FILEGROWTH = 1048576KB)
GO
```

### 跟踪标志 1117 和 1118

由于 SQL Server 使用 GAM（全局分配映射）页处理包含至少一个页的混合扩展区，解决 GAM 竞争的一种可能方法是避免使用混合扩展区，转而专门使用专用扩展区。跟踪标志 1117 自 SQL Server 2000 以来即可用于此目的。通过共享页分配并转而使用专用扩展区，你可以减少 GAM 页上的竞争。跟踪标志 1118 的缺点是每个对象将使用一个专用扩展区；如果对象小到仅能容纳一个页，这将浪费 64KB。另一个缺点是该配置在实例级别生效，也会影响数据库。

跟踪标志 1117 与 SQL Server 如何通过启用所有文件的增长来增加数据库文件的大小有关。另外两个建议是创建相同大小的 tempdb 数据文件，并且不要依赖自动增长设置。SQL Server 使用的算法会考虑文件组层面的数据库文件当前大小，并确定哪些文件被使用，同时以轮询方式分散分配。然而，当文件大小不相同时，它不会在所有文件之间分散 GAM 分配，而是会倾向于使用最大的文件。

跟踪标志 1117 允许你通过实例同时增长所有 tempdb 文件，从而避免此问题。然而，在跟踪标志 1118 的情况下，它适用于整个实例，在用户数据库的文件组级别上工作。

最后，不要依赖默认的自动增长配置，但如果将其作为最后的选择，请保持其开启状态并配合适当的文件配置。生产环境可能为 tempdb 准备了专用驱动器，为数据文件准备了专用驱动器，并为事务日志准备了另一个驱动器。如果你处于这种情况下，只需为 tempdb 分配所有可能的空间（可能受可用阈值限制），将有助于避免在生产操作期间增长文件，同时尽可能减少数据库碎片。

## 进程亲和性 (Process Affinity)

Microsoft 建议当 SQL Server 在 Linux 操作系统运行时，为所有 NUMA 节点和 CPU 设置进程亲和性。你可以使用 `ALTER SERVER CONFIGURATION` 语句配合 `PROCESS AFFINITY` 选项来实现此。你可以使用 `CPU` 或 `NUMANODE`，后者是最简单的选择。使用 `CPU` 选项允许你指定分配线程的 CPU 或 CPU 范围。使用 `NUMANODE` 选项允许将线程分配给指定 NUMA 节点或节点范围的所有 CPU。

`PROCESS AFFINITY` 允许硬件线程与 CPU 关联，有助于维护高效的 Linux 调度。即使你的系统只有一个 NUMA 节点，也设置进程亲和性。例如，以下命令为具有四个节点的系统的所有 NUMA 节点设置进程亲和性：

```sql
ALTER SERVER CONFIGURATION
PROCESS AFFINITY NUMANODE = 0, 3
```
