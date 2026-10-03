
确保每个 `LOG_ARCHIVE_DEST_N` 和 `LOG_ARCHIVE_DUPLEX_DEST` 位于不同的物理设备上。这些新参数的主要目的是允许在磁盘崩溃时，文件的副本能够保持完好。

## 总结

Oracle 的备份和恢复功能是健壮的。它提供了许多支持各种备份和恢复情况的选择。在本章中，你了解了如何配置 Oracle 数据库进行备份和恢复。你学习了在 `ARCHIVELOG` 模式与 `NOARCHIVELOG` 模式之间运行的影响，反之亦然，这种选择会影响备份和恢复过程。你看到了 `init.ora` 参数如何控制归档日志的目标和自动化的示例。最后，你通过了一个启用了数据库 `ARCHIVELOG` 模式和日志自动归档的示例。

对归档日志过程的深入理解是备份和恢复过程的基础。启用归档日志的决定对 DBA 恢复数据库的能力有重大影响。此外，在后续章节中将涵盖某些恢复选项取决于你是否启用了 `ARCHIVELOG` 模式。确保你理解启用或不启用归档日志过程的原因，这些知识将在 OCP 测试期间以及现实情况中对你有益。

## 考试要点

- 识别 `ARCHIVELOG` 和 `NOARCHIVELOG` 模式之间的差异。你应该知道数据库生成归档日志与不生成归档日志之间的区别。确保你意识到 `ARCHIVELOG` 和 `NOARCHIVELOG` 模式对备份和恢复过程的影响。
- 知道如何在 `ARCHIVELOG` 模式下配置数据库。能够解释如何配置数据库使其生成归档日志。你还应该能够识别涉及此过程的命令和初始化参数。
- 知道如何配置数据库进行自动归档。能够识别初始化参数 `LOG_ARCHIVE_START = TRUE`，它用于启用自动归档。
- 演示如何执行手动归档。知道如何使用所需的命令手动生成归档日志。
- 理解如何配置数据库多个归档目标。知道两种不同的初始化参数方法：`ARCHIVE_DEST_LOG_N` 和 `ARCHIVE_LOG_DEST_DUPLEX`。你还应该理解这些方法之间的区别，例如远程归档日志和位置数量。
- 理解如何配置多个归档进程。要配置多个归档进程，你必须熟悉配置数据库使用多个归档日志进程的初始化参数。
- 理解涉及远程归档的命令和初始化参数。你应该熟悉影响远程归档的命令，例如 `MANDATORY`、`OPTIONAL` 和 `REOPEN` 参数，以及 `ARCHIVE_MIN_SUCCEED_DEST`，以及它们如何影响远程归档过程。

## 关键术语

在参加考试之前，确保你熟悉以下术语：

| ARCHIVELOG 模式 | 介质故障 |
| :--- | :--- |
| 自动归档 | NOARCHIVELOG 模式 |
| LOG_ARCHIVE_DEST | 在线（热）备份 |
| LOG_ARCHIVE_START | 单点故障 |
| 手动归档 | |

## 复习题

1. 数据库需要处于什么种状态才能启用归档？

- A. 已打开 (Opened)
- B. 关闭 (Closed)
- C. 已挂载 (Mounted)
- D. 未挂载 (Unmounted)

2. 当数据库在 `ARCHIVELOG` 模式下运行时，DBA 应该注意哪些问题？

- A. 是否具有恢复的能力
- B. 是否具有关闭数据库的能力
- C. 是否具有不完全恢复的能力
- D. 这种模式是否增加了磁盘利用率

3. 下列哪些是你可以更改归档日志目标的方法？

- A. `LOG_ARCHIVE_DEST` 参数。
- B. 修改控制文件。
- C. `LOG_ARCHIVE_` 参数。
- D. `LOG_ARCHIVE_DUMP` 参数。

4. 支持的最大归档目标数量是多少？

- A. 1
- B. 2
- C. 5
- D. 10

5. 哪种类型的备份需要关闭数据库？

- A. ARCHIVELOG
- B. NOARCHIVELOG
- C. 在线备份（热）
- D. 冷备份（离线）

6. 确定数据库处于 `ARCHIVELOG` 模式的方法有：

- A. 查询 `V$DATABASE` 视图。
- B. 查看 `ARC` 进程是否在运行。
- C. 检查 `LOG_ARCHIVE` 的值。
- D. 查看 `ARCHIVE LOG` 命令的结果。

7. 你是一家制造公司的 DBA，数据库每天运行 24 小时处理订单、调整库存和发货。你应该执行哪种类型的备份？

- A. `ARCHIVELOG` 模式下的热备份
- B. `ARCHIVELOG` 的冷备份
- C. `NOARCHIVELOG` 模式下的在线备份
- D. `ARCHIVELOG` 模式下的在线备份

8. 哪个 `init.ora` 参数允许两个以上的归档目标？

- A. `ARCHIVE_DEST_LOG_N`
- B. `ARCHIVE_LOG_DEST_DUPLEX`
- C. `LOG_ARCHIVE_DEST_DUPLEX`
- D. `LOG_ARCHIVE_DUPLEX_DEST`

9. 哪个 `init.ora` 参数允许最多 10 个归档目标？

- A. `ARCHIVE_DEST_LOG_N`
- B. `ARCHIVE_LOG_DEST_DUPLEX`
- C. `LOG_ARCHIVE_DEST_DUPLEX`
- D. `LOG_ARCHIVE_DUPLEX_DEST`
- E. `LOG_ARCHIVE_DEST_N`

10. 哪个 `init.ora` 参数允许远程归档日志目标？

- A. `ARCHIVE_LOG_DEST`
- B. `ARCHIVE_LOG_DEST_DUPLEX`
- C. `LOG_ARCHIVE_DEST_N`
- D. `LOG_ARCHIVE_DUPLEX_DEST`

11. 执行手动归档需要哪个命令？

- A. MANUAL ARCHIVE ALL
- B. ARCHIVE MANUAL
- C. LOG ARCHIVE LIST
- D. ARCHIVE LOG ALL

12. 手动归档数据库需要什么？

- A. 数据库在 `ARCHIVELOG` 模式下。
- B. `LOG_ARCHIVE_START` 设置为 TRUE。
- C. `MANUAL_ARCHIVE` 设置为 TRUE。
- D. 无。

13. 执行手动归档需要哪个命令？

- A. ARCHIVE LOG NEXT
- B. ARCHIVE LOG LIST
- C. ARCHIVE ALL LOG
- D. ARCHIVE ALL

14. 如果启用了 `ARCHIVELOG` 模式，但 `LOG_ARCHIVE_START` 命令未设置为 TRUE，数据库会发生什么？（选择所有适用项）

- A. 数据库运行出现问题。
- B. 数据库将挂起，直到手动归档存档日志。
- C. 数据库将因为配置不当而无法启动。
- D. 在所有在线重做日志填满之前，数据库将正常工作。

15. 关于 `NOARCHIVELOG` 模式，以下哪项是正确的？

- A. 备份必须完全关闭数据库。
- B. 备份前必须将表空间离线状态。
- C. 备份时数据库必须处于运行状态。
- D. 备份时数据库可以运行，但不是必须的。

16. 哪个初始化参数决定了在写入在线重做日志之前，必须成功写入多少个归档日志目标？

- A. ARCHIVE_MINIMUM_SUCCEED
- B. LOG_ARCHIVE_MIN_SUCCEED
- C. LOG_ARCHIVE_MIN_SUCCEED_DEST
- D. ARCHIVE_MIN_SUCCEED_DEST

17. 如果归档日志未到达日志归档目标，哪个参数将允许数据库继续处理？

- A. REOPEN
- B. MANDATORY
- C. OPTIONAL
- D. UNSSUCCESSFUL

18. 哪个参数会导致失败的归档日志传输在指定的间隔时间内重试？

- A. MANDATORY
- B. OPTIONAL
- C. REOPEN
- D. RETRY

19. 如何识别数据库是否处于 `ARCHIVELOG` 模式？（选择所有适用项）

- A. 你可以使用 `ARCHIVE LOG LIST` 命令。
- B. 你可以从 `V$DATABASE` 中查询 *。
- C. 你可以使用 `ARCHIVELOG LIST` 命令。
- D. 你可以从 `V$LOG` 中查询 *。

20. 当数据库满足什么种条件时，可以执行完全恢复？

- A. 它处于 `ARCHIVELOG` 模式。
- B. 它处于 `NOARCHIVELOG` 模式。
- C. 启用了手动归档日志。
- D. 启用了自动归档日志。

## 复习题答案

1. C. 数据库必须处于 MOUNT 模式才能启用归档日志。
2. D. 由于创建了归档日志，数据库将使用更多空间。
3. A. 归档目标由 `LOG_ARCHIVE_DEST` init.ora 参数以及在数据库运行时通过执行 `ALTER SYSTEM` 命令进行控制。
4. D. 最大归档目标数由 `LOG_ARCHIVE_DEST_N` init.ora 参数控制。它支持多达 10 个位置。
5. B, D. `NOARCHIVELOG` 模式的数据库不支持在不关闭的情况下进行备份，冷备份是在数据库离线或关闭时采取的备份。
6. A, B, D. `V$DATABASE` 视图显示数据库处于 `ARCHIVELOG` 还是 `NOARCHIVELOG` 模式，`ARC` 进程直接决定归档程序正在运行，`ARCHIVE LOG LIST` 命令显示是否已启用归档。检查 `LOG_ARCHIVE_DEST` 参数的值仅表示是否存在包含归档日志的目录，而不表示数据库是否处于 `ARCHIVELOG` 模式。
7. A, D. 热备份和在线备份同义。冷备份和离线备份同义。热备份只能在 `ARCHIVELOG` 模式下运行（因此答案 C 中的备份方法不存在）。热备份可以在数据库运行时运行；因此它不会影响数据库的可用性。因为此数据库必须 24 小时可用，热备份或在线备份是合适的。
8. D. `LOG_ARCHIVE_DUPLEX_DEST` 参数允许第二个归档目标。此外，此参数必须与第一个归档日志目标的 `LOG_ARCHIVE_DEST` 参数配合使用。
9. E. `LOG_ARCHIVE_DEST_N` 允许多达 10 个位置。
10. C. `LOG_ARCHIVE_DEST_N` 允许多达 10 个位置。位置可以是远程的，即不在服务器上。
11. D. `ARCHIVE LOG ALL` 命令负责手动生成归档日志。`LOG NEXT` 命令也会手动归档日志，但它只归档序列中的下一个归档日志，而不是所有的归档日志。数据库必须处于 `ARCHIVELOG` 模式。
12. A. 数据库以 `ARCHIVELOG` 模式运行是执行手动或自动归档的要求。这意味着数据库必须使用 `START MOUNT` 重启，然后执行命令 `ALTER DATABASE ARCHIVELOG`。数据库必须打开以正常使用。
13. A. `ARCHIVE LOG NEXT` 命令将归档下一组重做日志。
14. B, D. 在所有在线重做日志填满后数据库将挂起，但只要还有未填满的在线重做日志，它就能正常工作。

# 识别 Oracle 恢复管理器 (RMAN) 的特性

- 通过确定哪些块发生了变化并仅备份这些块来压缩备份：RMAN 通过压缩备份来提高性能的一种方法。RMAN 识别已变化的块并仅备份这些块。此外，不会备份空块。
- 执行增量备份：RMAN 具有执行增量备份和全备的能力。增量备份仅包含自上次备份以来发生的更改。这种备份类型允许您每周执行一次全备，而在其余时间执行增量备份，从而提高性能。
- 提供脚本能力以组合任务：RMAN 通过允许对 RMAN 命令进行脚本化来提高备份、恢复和重建操作的效率。脚本可以包含多个 RMAN 命令，并可以存储在恢复目录（`recovery catalog`）中。这些脚本可以被调用和执行，以完成重复任务。
- 记录备份操作：RMAN 能够记录备份进展过程中的状态。这些信息存储在日志和跟踪文件中。
- 与第三方磁带媒体软件集成：RMAN 工具具有许多第三方磁带媒体软件的 API。这些允许 RMAN 在其他非 Oracle 备份工具中执行，并集成到组织的通用备份策略中。
- 提供目录信息的报告和列表：存储在恢复目录中的备份信息可以通过 RMAN `LIST` 和 `REPORT` 命令进行查询。这些命令提供了显示信息的有用方法。
- 在 Oracle 数据库的目录中存储备份信息：备份信息存储在恢复目录中。这些信息可以在日后的某个日期或任何需要时检索。
- 提供性能优势，例如备份和恢复操作的并行处理：备份和恢复操作可以设置为并行执行。这可以将工作负载分配到不同的磁带头和磁盘设备，从而提高性能。
- 为测试和开发目的创建数据库：可以从 RMAN 备份创建复制数据库并用于测试。
- 测试备份能否成功恢复：RMAN 提供 `VALIDATE` 命令来检查备份是否有效。
- 确定备份在介质库中仍然可用：RMAN 提供 `CROSSCHECK` 命令来确定备份介质和目录信息是否匹配。

图 8.1 展示了 RMAN 与前面的章节中自定义备份脚本和命令之间的某些区别。

## 图 8.1 备份脚本与 RMAN 工具之间的差异

![](img/a183fd041839741f5ab6df3caffc6b52_291_0.png)

| OS 命令 | RMAN 工具 | 脚本 | 恢复目录 |
| :--- | :--- | :--- | :--- |
| Unix 中的 `cp`, `tar`, `cpio` | 命令 | | 备份并恢复数据库文件 |
| `ALTER TABLESPACE` | | | 备份数据库文件 |
| `[BEGIN/END] BACKUP` | | | 备份并恢复数据库文件 |
| `ALTER DATABASE` | | | 执行热备和冷备 |
| `BACKUP CONTROL FILE TO TRACE` | | | 记录备份信息 |
| `ARCHIVE LOG ALL` | | | 验证备份 |
| | | | 与第三方磁带媒体硬件集成 |
| | | | |
| 结合 OS 命令和 SQL 以制作热备和冷备自定义备份脚本 | | | | |

# 探索 RMAN 组件

RMAN 的主要组件是 GUI 或命令行访问、可选的恢复目录、RMAN 命令和脚本，以及磁带媒体连接。这些组件允许 DBA 自动化和标准化备份与恢复过程。每个组件描述如下：

**GUI 或命令行访问方法** 此方法提供了对恢复管理器的访问，恢复管理器进而提供了对 RMAN 的访问。GUI 方法启动连接到目标数据库的服务器会话——即通过 RMAN 进行备份或恢复操作的数据库。GUI 访问通过 Oracle Enterprise Manager (OEM) 工具提供，这是一个 DBA 工具，可以执行备份、导入/导出、数据加载、性能监控/调优、作业和事件调度以及状态管理等。命令行访问可以在标准的 Unix Telnet 或 X Windows 会话中运行，也可以在 Windows 环境下的 DOS shell 中运行。

**可选的恢复目录** 这种特殊的备份信息字典存储在一组表中，方式与字典存储数据库信息的方式相同。恢复目录提供了一种存储备份、恢复和重建信息的方法。这些信息提供了备份成功或失败、OS 备份、数据文件副本、表空间、控制文件、归档日志副本、全数据库备份以及数据库物理结构的状态更新。

**RMAN 命令** 这些命令允许执行不同的操作，以促进数据库的备份和恢复。这些命令可以逻辑地组织成脚本，然后存储在恢复目录数据库中。脚本用于其他备份，保持不同目标数据库备份之间的一致性。

**磁带媒体连接** 此组件提供了一种与不同的第三方磁带硬件供应商接口的方法，以便在自动磁带库 (ATL) 中存储和跟踪备份。ATL 是一个大型磁带柜，存储许多磁带并可以同时写入多块磁带以提高性能。ATL 使用机械臂加载、卸载和存储磁带。默认情况下，Oracle 为管理 ATL 设备的 Legato Storage Management (LSM) 软件提供了媒体管理库 (MML)。

图 8.2 显示了 RMAN 工具组件如何组合形成一个完整的备份和恢复包。

## 图 8.2 RMAN 的组件

![](img/a183fd041839741f5ab6df3caffc6b52_293_0.png)

# 使用 RMAN 仓库和控制文件存储信息

RMAN 工具使用两种方法来存储有关备份的目标数据库的信息。每种方法被称为 RMAN 仓库。当 RMAN 使用第一方法时，它访问一个可选的备份信息 RMAN 目录。在第二方法中，它访问目标数据库控制文件中必要的备份信息。如果不使用可选的恢复目录数据库，则使用目标数据库的控制文件作为 RMAN 仓库。RMAN 在恢复目录或目标数据库控制文件中运行所需的信息也被称为 RMAN 仓库。无论是否使用目录，目标数据库的控制文件始终会更新。在下一段中，我们将讨论将恢复目录作为存储信息的 RMAN 仓库，然后列出可以在这种方法中使用的命令。在列表之后，我们将关注使用控制文件作为 RMAN 仓库。

Oracle 建议将 RMAN 备份数据存储在恢复目录中，而不是目标数据库的控制文件中。如果您以此方式存储数据，RMAN 工具将具有完整功能。此恢复目录是另一个 Oracle 数据库，具有特殊的 RMAN 目录表，存储备份的元数据。使用此数据库时，可以执行检查备份和可用磁带等活动。此外，使用这种方法可以在恢复目录中创建并存储脚本供以后使用。该数据库也可以进行备份，以确保其包含的信息安全。我们将在第 13 章“恢复目录的创建与维护”中详细讨论恢复目录数据库。

在详细讨论第二方法之前，请看这些命令。只有在在使用 RMAN 恢复目录作为 RMAN 仓库时，才允许这些命令。

- `CREATE CATALOG`
- `UPGRADE CATALOG`
- `DROP CATALOG`
- `CREATE SCRIPT`
- `DELETE SCRIPT`
- `REPLACE SCRIPT`
- `PRINT SCRIPT`
- `LIST STORED FILES`
- `LIST INCARNATION`
- `REGISTER DATABASE`
- `REPORT SCHEMA AT TIME`
- `RESET DATABASE`
- `RESYNC`

如前所述，RMAN 实用程序还允许您不使用此恢复目录数据库连接到目标数据库。虽然 Oracle 不推荐这种方法，但它确实有其用处。（例如，如果创建和维护恢复目录的开销对您的组织来说太大了，您可能会使用这种方法。）

如果您在没有恢复目录的情况下使用 RMAN，您将存储关于每个目标数据库控制文件的大部分必要信息，它作为 RMAN 仓库。因此，您必须管理目标数据库的控制文件以支持这些数据。`init.ora` 文件中的 `CONTROL_FILE_RECORD_KEEP_TIME` 参数决定了 RMAN 生成的信息在控制文件中保留多长时间。该参数的默认值为 7 天，但最多可以长达 365 天。数值越大，控制文件就越大，以便存储更多信息。控制文件的大小只能达到操作系统允许的程度，因此请注意这一点。存储在控制文件中信息存储在可重用区域中。如果 `CONTROL_FILE_RECORD_KEEP_TIME` 参数的值为 1 或更多，这些重用区域将会增长。可重用区域由以下类别组成：

- 归档日志 (Archived log)
- 备份数据文件 (Backup data file)
- 备份重做日志 (Backup redo log)
- 副本损坏 (Copy corruption)
- 删除的对象 (Deleted object)
- 离线范围 (Offline range)
- 备份损坏 (Backup corruption)
- 备份分 (Backup piece)
- 备份集 (Backup set)
- 数据文件副本 (Data file copy)
- 日志历史 (Log history)

## 描述通道分配

通道分配是您可以用于连接 RMAN 和目标数据库的方法。在执行此操作时，您还可以确定服务器进程执行备份或恢复操作时使用的 I/O 设备类型。图 8.3 显示此示例。I/O 设备可以是带或磁盘（在图 8.3 中，您可以看到两者）。

## 图 8.3 通道分配

![](img/a183fd041839741f5ab6df3caffc6b52_296_0.png)

通道可以手动分配或自动分配。手动通道分配在您发行 `ALLOCATE CHANNEL` 命令时执行，该命令会在目标数据库的服务器上启动一个服务器进程。要手动写入到磁盘文件系统，您将使用 `ALLOCATE CHANNEL <name> TYPE DISK` 命令。同样，要写入磁带备份系统，您将使用 `ALLOCATE CHANNEL <channel name> TYPE SBT_TAPE` 命令。这些是最常见的手动通道分配。

自动通道分配是在您 RMAN 命令提示符处设置 RMAN 配置时执行的。您通过使用 `CONFIGURE DEFAULT DEVICE` 或 `CONFIGURE DEVICE` 命令来实现。当您执行 `BACKUP`、`RESTORE` 或 `DELETE` 命令时，这种分配是自动的。通过使用 `CONFIGURE` 命令，您可以消除每次执行 `BACKUP`、`RESTORE` 或 `DELETE` 时使用 `ALLOCATE CHANNEL <name> TYPE DISK` 或 `SBT_TAPE` 命令的需求。自动通道分配命令的完整列表如下：

- `CONFIGURE DEVICE TYPE PARALLELISM`
- `CONFIGURE DEFAULT DEVICE TYPE`
- `CONFIGURE CHANNEL DEVICE TYPE`
- `CONFIGURE CHANNEL n DEVICE TYPE`

磁盘和磁带设备类型有一些默认命名规范——`ORA_MAINT_DISK_n` 和 `ORA_SBT_TAPE_n`。下面的示例显示默认设备类型设置为 `DISK`，并行度设置为 `1`。这意味着如果您不手动分配通道，您将获得下面列出的参数。

```
RMAN> show all;
RMAN 配置参数为：
```
