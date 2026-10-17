
```
oracle@ottillii:~ > exp userid-test/test compress=Y file=tst9.dmp
```

# 升级对象或数据库

还可以使用这些工具将数据库或对象从一个版本升级到另一个版本。如果这样使用工具，会对表或数据库进行导出，然后使用升级后的版本将其导入新数据库。

# 现实场景

## 将数据从一个数据库移动到另一个

导出和导入工具也可将数据从一个数据库移动到另一个。导出过程创建的二进制 dump 文件可以通过 FTP 从一个服务器发送到另一个服务器，然后加载到新数据库中。

# 使用导出和导入工具

（注：此部分似乎是源代码中的重复/延续）

# 导出和导入的概念与结构

如本章引言所述，导出工具可创建 Oracle 数据库的逻辑备份。导入工具可以恢复这些逻辑备份。导出有两种类型：常规路径导出和直接路径导出。

常规路径导出是导出工具的默认模式。对于大型对象或导出，这种方法可能非常耗时。但它对于日常使用良好。

直接路径导出通过在命令行中输入 `DIRECT=Y` 启用。这种导出选项明显快于常规路径导出。直接路径导出跳过了 SQL 评估层，因为它重新生成存储在二进制 dump 文件中的命令。这就是性能提升的地方。图 14.1 显示了每种导出的执行路径。

Export 工具对表执行全量 `SELECT` 操作，并将数据转储到一个名为“dump文件”的二进制文件中。（该文件具有 `.dmp` 扩展名，默认名为 `expdat.dmp`。）

Export 工具通过重现备份表的数据定义语言（DDL）来创建表和索引。这些信息随后可以由 Import 工具进行回放，以重建对象及其底层数据。

要显示所有可用的导出选项，请执行 `EXP -HELP` 命令行。

```
oracle@octilli:db01/oracle/tst9 > exp -help
```

```
Export: Release 9.0.1.0 - Production on Fri Oct 5 23:09:00 2001
(c) Copyright 2001 Oracle Corporation. All rights reserved.
```

你可以通过输入 `EXP` 命令后跟你的用户名/密码来让 Export 提示你输入参数：

示例：`EXP SCOTT-TIGER`

或者，你可以通过输入 `EXP` 命令后跟各种参数来控制 Export 的运行。要指定参数，你可以使用关键字：

```
Format: EXP KEYWORD=value 或
KEYWORD=(value1,value2,...,valueN)
示例: EXP SCOTT-TIGER GRANTS=Y
TABLES=(EMP,DEPT,MGR)
或 TABLES=(T1:P1,T1:P2),
如果 T1 是分区表
```

`USERID` 必须是命令行上的第一个参数。

## 导出与导入概念结构 423

| 关键字 | 描述 (默认值) |
| :--- | :--- |
| USERID | 用户名/密码 |
| BUFFER | 数据缓冲区的大小 |
| FILE | 输出文件 (EXPAT.DMP) |
| COMPRESS | 导入到一个扩展区 (Y) |
| GRANTS | 导出权限 (Y) |
| INDEXES | 导出索引 (Y) |
| ROWS | 导出数据行 (Y) |
| CONSTRAINTS | 导出约束 (Y) |
| LOG | 屏幕输出的日志文件 |
| DIRECT | 直接路径 (N) |
| FEEDBACK | 每隔 x 行显示一次进度 (0) |
| FILESIZE | 每个 dump 文件的最大大小 |
| QUERY | 用于导出表子集的 select 子句 |
| VOLSIZE | 写入每个磁卷的字节数 |
| FULL | 导出整个文件 (N) |
| OWNER | 所有者用户名列表 |
| TABLES | 表名列表 |
| RECORDLENGTH | IO 记录长度 |
| INCTYPE | 增量导出类型 |
| RECORD | 跟踪增量导出 (Y) |
| PARFILE | 参数文件名 |
| CONSISTENT | 跨表一致性 |
| STATISTICS | 分析对象 (ESTIMATE) |
| TRIGGERS | 导出触发器 (Y) |
| FEEDBACK | 每隔 x 行显示一次进度 (0) |
| FILESIZE | 每个 dump 文件的最大大小 |
| FLASHBACK_SCN | 用于设置会话快照回的 SCN |
| FLASHBACK_TIME | 用于获取最接近指定时间的 SCN |
| QUERY | 用于导出表子集的 select 子句 |
| RESUMABLE | 遇到空间相关错误时挂 (N) |
| RESUMABLE_NAME | 用于标识可恢复语句的文本字符串 |
| RESUMABLE_TIMEOUT | 可恢复的等待时间 |
| TTS_FULL_CHECK | 为 TTS 执行全量或部分依赖检查 |
| VOLSIZE | 写入每个磁带的字节数 |
| TABLESPACES | 要导出的表空间列表 |
| TRANSPORT_TABLESPACE | 导出可传输的元数据 (N) |
| TEMPLATE | 调用 IAS 模式导出的模板名称 |

导出成功，无警告。`oracle@octilli:db01/oracle/tst9 >`

Oracle 9 的导出功能变化较少。变化如下：为了适应 Java 虚拟机，在全量模式下不再导出 sys 架构下的触发器，同时也不再支持增量/累计导出（INCREMENTAL/CUMULATIVE），以及从 Oracle 9 数据库创建 7.x 导出文件的过程。请阅读 Oracle 文档以获取这些更改的完整细节。

# 执行简单的导出和导入操作

让我们看看 DBA 如何执行简单的导出和导入。我们将使用交互式方法运行 Export 和 Import 工具。这意味着用户将对工具的每个提示做出响应。

首先，我们将导出表 t1。然后我们将导入同一个表。此外，我们还将演示如何使用 `PARFILE` 运行导出，以便其不需要用户交互。这种导出可以在命令行运行，并且既可以是脚本化的也可以调度的。`PARFILE` 是参数文件，将导出参数分组在一个文件中，因此 DBA 就不需要在命令行上输入每个参数。该过程将在接下来的导出过程之后演示。让我们逐一完成这些示例。

## 执行简单的导出

在这个交互式导出示例中，你将对用户 TEST 拥有的表 t1 进行全量导出。以下是执行导出的步骤：

1. 执行 `exp` 行来启动 Export 工具。在 Unix 中，你应该先设置 `ORACLE_SID` 环境变量指向你正尝试连接的数据库。可以通过在命令行执行 `export ORACLE_SID = tst9` 来。或者，你也可以通过显式定义目标数据库的 tnsora 条通过 SQL*Net 连接。

```
oracle@octilli:db01/oracle/tst9 > exp
Export: Release 9.0.1.0.0 - Production on Fri Oct 5 23:09:00 2001
(c) Copyright 2001 Oracle Corporation. All rights reserved.
连接到: Oracle Database Release 9.0.1.00 - Production Edition - Universal Use
用户名: test
密码:
```

2. 输入适当缓冲区大小。如果你想要默认的 64KB，请按..缓冲区大小: 4096

3. 下一个提示 dump 文件的文件名。导出文件: expdat.d

4. 下一个提示指定用户或表: t1

5. 下一个提示是否导出数据。

6. 下一个提示是否压缩扩展区。例如，如果你选择否，则扩展区将保留。压缩扩展区 (yes/no): yes

7. 下一个提示指定要导出的表。在示例中，你选择了 t1。导出完成后，将提示另一个表。如果你已完成，按回车。

导出字符集为 US7ASCII

正在通过常规路径导出指定的表

```
Table(T) or Partition(T:P) to be exported:
(RETURN to quit) > t1
. . exporting table
T1
3 rows exported
Table(T) or Partition(T:P) to be exported:
(RETURN to quit) >
```

导出完成。

## 执行简单的导入 (Import)

Import 工具用于执行 Oracle 数据库的逻辑恢复。该工具读取由 Export 工具生成的转储文件。如前所述，Export 工具将表中的数据转储出来，并使用必要的 DDL 命令重新创建表。随后，Import 工具会回放这些命令，重新创建表，并插入存储在二进制转储文件中的数据。本节将提供该过程工作原理的逐步步骤概述。

Import 工具还具有许多选项。要显示所有可用的导入选项，请在命令行中执行 `IMP -HELP` 命令。

```
oracle@octilli: ~ imp -help
Import: Release 9.0.1.0 - Production on
Fri Oct 5 23:24:45 2001
> (c) Copyright 2001 Oracle Corporation.
All rights reserved.
```

你可以通过输入 `IMP` 命令并后跟你的用户名/密码来让 Import 提示你输入参数：

示例：`IMP SCOTT/TIGER`

或者，你可以通过输入 `IMP` 命令后跟各种参数来控制 Import 的运行方式。要指定参数，你需要使用关键字：

```
Format: IMP KEYWORD=value or
KEYWORD=(value1,value2,...,valueN)
Example: IMP SCOTT/TIGER IGNORE=Y
TABLES=(EMP,DEPT) FULL=N
or TABLES=(T1:P1,T1:P2),
if T1 是分区表
```

`USERID` 必须是命令行上的第一个参数。

| 关键字 | 说明 (默认值) |
| :--- | :--- |
| USERID | 用户名/密码 |
| BUFFER | 数据缓冲区的大小 |
| FILE | 输入文件 (EXPDAT.DMP) |
| SHOW | 列出文件内容 (N) |
| IGNORE | 创建错误 (N) |
| GRANTS | 导入权限 (Y) |
| INDEXES | 导入索引 (Y) |
| ROWS | 导入数据行 (Y) |
| LOG | 屏幕输出日志文件 |
| DESTROY | 覆盖表空间数据文件 (N) |
| INDEXFILE | 将表/信息写入指定文件 |
| SKIP_UNUSABLE_INDEXES | 跳过不可用索引的维护 (N) |
| FEEDBACK | 每隔 x 行显示进度 (0) |
| TOID_VALIDATE | 跳过指定类型 ID 的验证 |
| FILESIZE | 每个转储文件的最大大小 |
| STATISTICS | 导入预计算的统计信息 (always) |
| RESUMABLE | 遇到空间相关错误时暂停 (N) |
| RESUMABLE_NAME | 用于标识可恢复语句的文本字符串 |
| RESUMABLE_TIMEOUT | 可恢复的等待时间 |
| COMPILE | 编译过程、包和函数 (Y) |
| VOLSIZE | 磁带上文件每个卷的字节数 | |

以下关键字仅适用于可传输表空间 (transportable tablespaces)：

| 关键字 | 说明 |
| :--- | :--- |
| TRANSPORT_TABLESPACE | 导入传输表空间元数据 (N) |
| TABLESPACES | 要传输到数据库的表空间 |
| DATAFILES | 要传输到数据库的数据文件 |
| TTS_OWNERS | 拥有传输表空间中数据的用户 |

```
Import terminated successfully without warnings.
oracle@octilli:~ >
```

以下步骤指示了如何使用 Import 工具执行表的恢复。在这里，Import 工具处于交互模式。

1. 要恢复数据库，你必须验证应该恢复的内容。在这种情况下，请使用前文名为“执行简单导出”章节中针对 `t1.dmp` 的导出文件。在这里，你正在导出整个 t1 表，该表包含四行数据。

```
SQL> select * from t1;
C1
```

| 1 这是一个测试 - 热备之前 |
| 3 这是一个测试三 - 热备之后 |
| 2 这是一个测试二 - 热备之后 |
| 4 这是一个测试四 - 完整导出之后 |

已选择 4 行。

```
SQL>
```

2. 截断表以模拟表中数据的完全丢失。

```
SQL> truncate table t1;
Statement processed.
SQL>
```

3. 从导出的转储文件的工作目录，执行 `IMP` 命令并连接到用户 TEST。

```
oracle@octilli:~ imp
Import: Release 9.0.1.0.0 - Production on
Fri Oct 5 23:31:44 2001
(c) Copyright 2001 Oracle Corporation.
All rights reserved.
```

4. 下一个提示是转储文件的文件名。你可以输入完全限定的文件名，或者如果你位于转储文件的工作目录，则只需输入文件名。

Import file: expdat.dmp > t1.dmp

5. 下一个提示是导入数据加载的缓冲区大小。选择最小，即 8KB。

Enter insert buffer size (minimum is 8192) 30720 > 8192

6. 下一个提示询问是否列出转储文件的内容，而不是实际执行导入。默认是否；在本示例中选择该选项。

Export file created by::V09.00.01

done

List contents of file (yes/no): no > n

7. 下一个提示询问是否由于对象存在而忽略错误。在本示例中选择是。

Ignore error due to (yes/no): yes > y

8. 下一个提示询问是否导入对象相关的权限。在本示例中选择是。

Import grants (yes/no): yes > y

9. 下一个提示询问是否导入表中的数据。在本示例中选择是。

Import data (yes/no): yes > y

10. 下一个提示询问是否导入导出文件。在这种情况下，选择默认值，即否。

Import file (yes/no): no > n

- 导入 TEST
- 表
- 已导入 4 行

```
Import terminated successfully without warnings.
oracle@octilli:~
```

11. 接下来，你需要验证导入是否成功恢复。对表进行查询以验证有四行数据。

```
SQL> select * from t1;
```

| 1 这是一个测试 - 热备之前 |
| 3 这是一个测试三 - 热备之后 |
| 2 这是一个测试二 - 热备之后 |
| 4 这是一个测试四 - 完整导出之后 |

![](183fd041189741f556c6b52_493_0)

# 使用导出和导入的指南

使用导出和导入工具的指南要求逻辑备份和恢复是可以接受的。此问题的另一种方法是：“数据可以从某个时间点恢复吗？”

对于导出，无法像完全恢复或不完全恢复那样向前回滚。导出中的数据是导出提取时的数据，并且无法更改。它是特定时间点的数据快照。

既然如此，导出和导入工具不是最好的备份和恢复解决方案。这些工具更多是作为良好物理备份策略的补充。

以下是使用导出和导入工具的一些指南：数据应该是静态的。被导出的数据是一致的，或者尽可能不要处于更新过程中。如果在导出期间发生了剧烈的 DML 活动，转储文件对于恢复目的将无用。

表之间的逻辑引用应有限。表具有具有的引用完整性约束。复杂的引用完整性会给导出工具带来问题。

本章演示了 Oracle 逻辑备份和恢复工具：Export 和 Import。在本章中，你练习了使用这些工具对数据库对象进行备份和恢复。你学习了如何显示导出和导入工具中所有可用选项，并看到了直接路径导出的示例，它比标准的常规路径导出快得多。

此外，你已经介绍了导出（Export）和导入（Import）工具适用的场景类型。你还熟悉了为了充分利用导出和导入工具而需要遵循的指导原则。

在大多数环境中，导出和导入工具并不作为主要的备份，而是作为物理备份的补充。然而，导出和导入工具提供了额外的保护，并消除了对某些物理恢复的需求。

本章涵盖的主题将是测试的重要部分，在工作中也同样有益。导出和导入工具是任何备份和恢复计划的宝贵补充。当数据库发生用户或开发者错误时，这些工具可以防止完全恢复并消除停机时间。

# 考试要点

- 理解导出和导入工具的用途。导出和导入工具可恢复数据库对象、重组数据库以获得最佳性能、升级数据库或将数据从一个数据库移动到另一个数据库。
- 理解如何执行导出。要执行导出，必须熟悉相关的命令。你还应该知道导出的两种方式：通过用户交互和使用 `PARFILE`。
- 理解如何执行导入。要执行导入，必须熟悉相关的命令。你还应该知道导入的两种方式：通过用户交互和使用 `PARFILE`。
