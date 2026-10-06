
`UPDATE DBM CFG USING INTRA_PARALLEL YES`

> 注意：`INTRA_PARALLEL` 参数在 SMP 机器上的默认值为 YES，在单处理器机器上的默认值为 NO。

如果将并行度设置为 ANY，则优化器将为每个 SQL 查询决定并行度。例如，在一台四四路 SMP 机器上，简单的插入语句在跨 CPU 并行运行时将无法获得任何优势，使用 ANY 设置将导致此类语句仅在单个 CPU 上运行（并行度为 1）。

### SQL 监控

在单处理器环境中，将 DBM 配置参数 `MAX_QUERYDEGREE` 设置为 2 可以略微提高 I/O 性能。这是因为单处理器在处理新查询之前可能不需要等待输入或输出任务完成，从而提高了 I/O 密集型应用程序的性能。

嵌入式 SQL 应用程序和 CLI 应用程序可以使用各种选项覆盖默认并行度。下表概述了可以在 DB2 中启用并行的参数和选项。

### 表 12-1 DB2 并行参数

| 参数 | 取值 |
| --- | --- |
| `INTRA_PARALLEL` (数据库管理器配置) | - YES/NO。<br>- 在单处理器机器上默认值为 NO。<br>- 在 SMP 机器上默认值为 YES。<br>- 如果发生更改，已有的程序包在下次执行时将自动重新绑定。 |
| `MAX_QUERYDEGREE` (数据库管理器配置) | - 1-32767, ANY。<br>- 默认值为 ANY - 允许优化器根据成本选择并行度。<br>- 在此实例数据库上执行的任何 SQL 其并行度不能高于此值。 |
| `DFT_DEGREE` (数据库配置) | - 1-32767, ANY。<br>- 默认值为 1（无并行）。<br>- 为以下提供默认值：<br>- `CURRENT DEGREE` 特殊寄存器。<br>- `DEGREE` 绑定选项。<br>- 此数据库中任何 SQL 的最大值。 |
| `CURRENT DEGREE` (特殊寄存器) | - 1-32767, ANY。<br>- 为动态 SQL 设置并行度。<br>- 默认值为 `DFT_DEGREE`。 |
| `DEGREE` (预编译或绑定选项) | - 1-32767, ANY。<br>- 为静态 SQL 设置并行度。<br>- 默认值为 `DFT_DEGREE`。<br>- 修改方法：`PREP STATIC.SQL DEGREE 2`。 |

### 表 12–1 DB2 并行参数（续）

| 参数 | 取值 |
| --- | --- |
| `RUNTIME DEGREE` (`SET RUNTIME DEGREE` 命令) | * 1-32767, ANY。<br>* 为运行中的应用程序设置并行度。<br>* 修改（将处理程序号为 100 的应用程序并行度设置为 4）：`SET RUNTIME DEGREE FOR (100) to 4`<br>* 修改（将处理程序号为 100 的应用程序并行度设置为 4）：`SET RUNTIME DEGREE FOR (100) to 4`<br>* 仅对执行 `SET RUNTIME` 后发出的查询有效。 |
| `DB2DEGREE` (CLI 配置文件) | * 1-32767, ANY。<br>* 默认值为 1。<br>* 为 CLI 应用程序设置并行度。<br>* CLI 应用程序在连接数据库后发出 `SET CURRENT DEGREE` 语句。 |

活动应用程序的最大查询并行度使用 `SET RUNTIME DEGREE` 命令指定。应用程序可以使用 `SET CURRENT DEGREE` 语句设置自己的运行时并行度。实际使用的运行时并行度是以下者的较低值：
- `MAX_QUERYDEGREE` DBM 配置
- 应用程序运行时度
- SQL 语句度

关于 DB2 通用数据库并行性的更多信息请参阅《DB2 UDB Administration Guide》。

### 性能调优场景

现在检查一个简单的 DB2 性能调优场景。数据库用户打电话说，每天下午 2:00 应用程序比其他时间慢得多。响应缓慢，有时用户必须等待。你假设这种情况是由于下午 2:00 有许多应用程序访问数据库。因此，你决定使用性能监控收集该时间段的信息。你决定监控的资源是缓冲池活动和升级次数。你在下午 2:00 之前、期间和之后每 30 秒获取一次快照。你发现缓冲池命中率下降到 50% 以下，升级次数增加，平均等待时间在下午 2:00 左右增加。

你决定为 DB2 捕获当前活动应用程序的快照。如下所示，使用 `db2 LIST APPLICATIONS` 命令可以列出所有连接到数据库的活动应用程序。

| 身份 ID | 应用程序名称 | 句柄 | 应用程序 ID | DB 名称 | 代理 |
|---|---|---|---|---|---|
| DB2CERT | db2bp_r | 51 | 0903107704490021385 | DB2CERT | 1 |
| DB2CERT | db2CC_exe | 53 | 0903107704F00061533 | DB2CERT | 1 |
| DB2CERT | db2BP_exe | 58 | 0903107704F00061443 | DB2CERT | 1 |
| RNICOL | db2bp_exe | 59 | 0903107304D500061401 | DB2CERT | 1 |
| RNICOL | db2bp_exe | 60 | 0903107304D70006184 | DB2CERT | 1 |
| DB2USER | DB2CERT_exe | 61 | 0903108004E100021595 | DB2CERT | 1 |

图12-30 `LIST APPLICATIONS` 输出

你注意到抱怨性能的用户 `DB2USER` 使用输出最后一行显示的 `DB2CERT` 应用程序。根据每个其他应用程序的锁快照，你发现 `DB2USER` 拥有大量的行锁，并使用了大部分由于 `LOCKLIST` 数据库参数分配的内存。

根据语句 `APPL_ID*LOCAL.db2cert.0002115285` 拍摄快照，发现该应用程序正在 `TEST` 表上执行大量插入。你决定增加分配给锁内存，因为应用程序耗尽可用锁时会出现锁升级。

锁内存定义在数据库配置文件。可以使用 CLP、命令中心或控制中心修改该值。获取当前数据库设置的 CLP 命令为：

```
GET DATABASE CONFIGURATION for dbcert
```

图 12-38 显示了一些重要的数据库配置参数。解决锁问题的第一步是增加 `LOCKLIST` 的大小和 `MAXLOCKS` 的值。你可以执行以下 CLP 命令进行更新：

```
UPDATE DB CF for dbcert USING LOCKLIST 250 MAXLOCKS 3000
```

| 参数 | 取值 |
| --- | --- |
| 并行度 | (`DFT_DEGREE`) = 1 |
| 默认查询优化类 | (`DFT_QUERYOPT`) = 5 |
| | (`DBHEAP`) = 1200 |
| 目录缓存大小 (4KB) | (`CATALOGCACHE_SZ`) = 128 |
| 日志缓冲区大小 (4KB) | (`LOGBUFS`) = 8 |
| 工具类堆大小 (4KB) | (`UTIL_HEAP`) = 5000 |
| 缓冲池大小 (4KB) | (`BUFFHEAPS`) = 16000 |
| 扩展存储段大小 (4KB) | (`ESTORE_SEG_SZ`) = 0 |
| 扩展存储段数量 | (`NUM_ESTORE_SEGS`) = 0 |
| 锁列表最大存储空间 (4KB) | (`LOCKLIST`) = 100 |
| 最大应用程序控制堆大小 (4KB) | (`APP_CTL_HEAP_SZ`) = 128 |
| 排序列表堆 (4KB) | (`SOTHEAP`) = 256 |
| SQL 语句堆 (4KB) | (`STMTHEAP`) = 128 |
| 默认应用程序堆 (4KB) | (`PKCACHESIZE`) = (`MAXAPPLS*8`) |
| 程序包缓存大小 (4KB) | |
| 统计堆大小 (4KB) | (`STATHEAP_SZ`) = 1 |
| 每个应用程序的锁列表百分比 | (`MAXLOCKS`) = 10 |

| 参数 | 取值 |
| --- | --- |
| 更改页面阈值 | (`CHNGPOS_THRESH`) = 60 |
| 异步页面清理程序 | (`NUM_IOCLEANERS`) = 1 |
| I/O 服务数量 | (`NUM_SERVS`) = 3 |
| 顺序检测标记 | (`SEQDETECT`) = YES |
| 最大活动应用程序数 | (`MAXAPPLS`) = 40 |
| 平均活动应用程序数 | (`MINAPPLS`) = 1 |
| 组提交计数 | (`MINCOMMIT`) = 1 |
| 每个应用程序最大打开数据库文件数 | (`MAXFILE`) = 6 |

您可能还会决定更改活动应用程序平均数，以匹配数据库活动。`AVG_APPLS` 参数将影响优化器认为的每个缓冲池的使用。根据 `LIST APPLICATIONS` 命令，目前只有五个应用程序正在使用数据库，因此将值设置为 8（允许几个额外的连接）。以下 CLP 命令将修改 `AVG_APPLS` 参数：

```
UPDATE DB CFG FOR db2cert USING AVG_APPLS 8
```

在完成所有这些修改后，您应该创建新的应用程序包（为任何静态 SQL 创建新的访问计划）。使用 `REBIND` 命令更新程序包信息。您也可以使用 `db2rbind` 实用程序来处理此工作。

现在，您应该验证这些更改是否有益。在例例中，您应该判断第二天是否会发生锁升级（lock escalations），并验证用户 (`db2user`) 是否获得了可接受的响应时间。记住，某些性能问题必须在应用程序或数据库设计本身中解决。

### 诊断与问题确定

DB2 Universal Database 提供了一系列工具，用于确定 DB2 系统中问题或错误的原因。常见问题包括：

- 操作系统特定的
- 硬件或 I/O 特定的
- 应用程序特定的
- 通信特定的

在复杂环境中，例如分布式 V7.1 DB2 数据库系统或高量 OLTP 数据库系统，可能会出现问题。在更严重的情况下，您可能想要确定系统崩溃的原因。这种故障排除需要尽可能快速、高效地进行。

## 错误消息和 SQL 代码

DB2 Universal Database 拥有大量的错误代码来解释数据库系统内部的问题。这意味着 DB2 不仅可以报告数据库内部的问题，还可以报告随 DB2 提供的任何工具和功能的问题。

这些消息分为几个不同的类别。每条消息都关联一个错误代码。错误代码的三字母前缀决定了错误代码所属的类别：

- `ASN` - DB2 复制支持消息
- `CCA` - 客户端配置助手消息
- `CLI` - ODBC/CLI 应用程序消息
- `DBA` - 控制中心或 DBA 实用程序消息
- `DBI` - DB2 安装消息
- `DB2` - CLP 或命令行中心消息
- `DWC` - 数据仓库中心消息
- `FLG` - 信息目录管理器消息
- `GSE` - 空间扩展（Spatial Extender）消息
- `SAT` - DB2 卫星版消息
- `SPM` - 同步点管理器（Syncpoint Manager）消息
- `SQJ` - Java 中的嵌入式 SQL (SQLJ) 消息
- `SQL` - SQL 消息

由于 DB 环境可能复杂，存在大量的错误消息。在 DB2 的安装和设置期间，管理员在熟悉新系统的可能会遇到一些 DBI、DBA 和 CCA 消息。另一个例子可能是用户对 DB2 数据库运行即时查询。他们可能因为 SQL 语法不准确或未获得某些表的访问权限而收到 SQL 错误。如果您有与错误相关的特定代码，可以通过两种方式查看错误消息：首先，查阅《DB2 消息参考》，该书籍详细列出了 DB2 中所有的错误代码；其次，使用 CLP 或命令行中心查询代码：

```
DB2 ? SQL0818
```

如果 SQL 语句执行失败，您将收到一个 SQL 错误代码以及一个 SQLSTATE 代码。SQLSTATE 是基于 ISO/ANSI SQL92 标准的标准代码。它在 DB2 家族的所有成员（包括主机系统上的 RDBMS）中保持不变。SQL 错误代码可能是 UNIX、Windows 和 OS/2 上的 DB2 Universal Database 特有的。

SQL 代码有两种格式：负代码（格式为 `SQLXXXX`）或正代码（格式为 `SQLXXXXW`）。负代码表示 SQL 错误，正代码表示 SQL 警告（SQL 代码为表示 SQL 成功完成）。

有时，SQL 代码在错误消息文中包含原因代码。这些原因代码通常提供更详细的信息来补充消息文本。原因代码的示例包括操作系统返回代码和通信协议代码。《DB2 UDB V7.1 消息参考》对常见原因代码提供了一些详细信息。然而，有时可能需要查阅其他系统文档。

当使用 DB2 自带的管理工具时，日志（Journal）会记录返回给用户的所有消息。例如，如果您尝试在正在离线备份时使用控制中心访问 `DB2CERT` 数据库，将弹出一个对话框通知您数据库正在使用。此消息将记录在日志中。图 12–39 给出了日志记录的消息示例。

![](img/06451013a7a38ae7d0597faa16c37ebb_686_0.png)

## 第 12 章 监控与调优

![](img/06451013a7a38ae7d0597faa16c37ebb_687_0.png)

图 12-39 日志中的消息

### 诊断和服务日志

DB2 允许您记录系统内的大多数管理任务。每个 DB2 实例都有诊断日志文件、随 DB2 带的管理工具有诊断日志、DB2 Governor 有报告日志以及记录 DB2 实例的日志。重点将放在每个 DB2 实例（包括管理服务器）的诊断日志上。

DB2 不记录任何数据定义语言 (DDL) 语句或数据操作语言 (DML) 语句。

## 第 12 章 监控与调优

## 深入理解 DB2DIAG.LOG

`db2diag.log` 中的信息易于阅读，但某些数据（例如十六进制转储和 DB2 内部代码）可能难以解释。`db2diag.log` 是一个包含系列消息目的 ASCII 文件。每个消息条目包含：

- 条目的的时间戳
- 报告错误的位置，可以是 DB2 应用程序、DB2 工具，甚至是数据库管理器内部的 DB2 函数
- 诊断消息，前缀为 DIA，用于解释错误原因
- 辅助数据，例如 `SQLCA` 数据结构和指向其他 FFDC 信息的指针

接下来的示例摘录描述了 `db2diag.log` 文件中条目的头部，这可以帮助您更轻松地解释其内容。

```
2000-06-05-14.38.03.57621 1 Instance:db2inst1 2 Node:000 3

PID:45698(db2sysc.exe) 4 ID: 372 Appid:LOCAL.db2inst1.00065193714 5

buffer_pool_services 6 sqlbMSDirectWrite 7 Probe:99 8 Database:DB2CERT 9 full.
```

在容器 0 上检测到 SMS 表 2(`USERSPACE1`)。

1. 错误的时间戳。
2. 发生错误的实例。
3. 发生错误的数据库分区号（适用于分区数据库环境）。在非分区数据库环境中，节点号始终为 000。
4. 进程 ID (`PID`) - 在具有独立进程的 UNIX 环境中更为适用。进程 ID 允许您识别是哪个进程返回了错误。然而，在 OS/2 和 Windows 环境中，DB2 多线程运行，因此进程 ID 通常标识主执行线程。
5. 应用程序 ID (`Appid`) - 标识进程正在处理的应用程序。要收集更多关于该应用程序的信息，可以使用 `LIST APPLICATIONS` 命令或使用快照监控器（Snapshot Monitor）。
6. 写入消息 DB2 组件。
7. 提供消息的函数名称。
8. 报告内部错误的位置。

### 诊断与问题确定

### 665

9. 发生 db2 错误的数据库。

在此示例中，此 `db2diag.log` 条目的消息文本易于阅读，错误也容易解释。然而，图 12–40 展示了一些记录的较不那么直观的错误。在此示例中，DB2 正在将数据加载到缓冲区时，SMS 表满了并停止了加载。

```
2000-06-05-14.03.057621 Instance:db2inst1 Node:000

PID:45698(db2sysc.exe) Appid:LOCAL.db2inst1.000605193714

buffer_pool_services sqlDIrectWrite Probe:99 Database:DB2CERT

SMS Tables 2 (USERSPACE1) is full. Detected on Container .

2000-06-05-14.03.096743 Instance:db2inst1 Node:000

PID:45698(db2sysc.exe) Appid:LOCAL.db2inst1.000605193714

buffer_pool_services sqlDIrectWrite Probe:99 Database:DB2CERT

SMS Tables 2 (USERSPACE1) is full. Detected on Container .

2000-06-05-14.03.096743 Instance:db2inst1 Node:000

PID:45698(db2sysc.exe) Appid:LOCAL.db2inst1.000605193714

buffer_pool_services sqlDIrectWrite Probe:825 Database:DB2CERT

DIA612C Disk was full.

ZRC=FFFF6C0

2000-06-05-14.03.32180 Instance:db2inst1 Node:000

PID:45698(db2sysc.exe) Appid:LOCAL.db2inst1.000605193714
```
