
读到这里的 SQL 纯粹主义者可能正用鞋子敲桌子并大喊：“`ORDER_BY`、`INSERT` 和 `DELETE` 都在哪里……还有……？”但那里并没有这些。记住，`RTA` 不是一个数据库——它是一个接口。我们只选择 `SELECT` 和 `UPDATE`。

## RTA 内置表介绍

`RTA` 库有几个内置表。附录 A 提供了完整细节，因此我们在这里介绍这些表。第一张表只有一行。

### `rta_dbg`

`rta_dbg` 表允许你控制日志的记录方式和记录内容。你可以通过将 `trace` 设置为 1 来开启 SQL 追踪，并通过将 `target` 分别设置为 0、1、2 或 3，将日志消息重定向到无、`syslog`、`stderr` 或两者。你还可以为 `syslog()` 指定 `priority`、`facility` 和 `ident` 值。从 `psql` 中：

```sql
# select * from rta_dbg;
syserr | rtaerr | sqlerr | trace | target | priority | facility | ident
+------+------+------+------+----+----+----------+------+
1 | 1 | 1 | 0 | 1 | 3 | 8 | rta
(1 row)
```

### `rta_stat`

`rta_stat` 表存储与调用 `RTA` 的统计信息。它包含了不同类型的错误计数、打开 `RTA` 的连接数，以及 `SELECT` 和 `UPDATE` 的数量。

```sql
# select * from rta_stat;
syserr | nrtaerr | nsqerr | nauth | nselect | npdate
+------+------+------+------+------+------+
0 | 0 | 1 | 3 | 6 | 7
(1 row)
```

### `rta_tables`

`rta_tables` 元数据是表定义结构的集合。为了向 `RTA` 中添加表，你必须填充一个带有该表描述的数据结构。该表定义结构集合本身就是 `RTA` 中的一张表。这是 `RTA` 的元表之一。

```sql
# select name, address, rowlen, nrows, ncol from rta_tables;
name | address | rowlen | nrows | ncol
rta_tables | 0 | 40 | 5 | 10
rta_columns | 0 | 36 | 5 | 9
rta_dbg | 1073986432 | 48 | 1 | 8
rta_stat | 1073988768 | 48 | 1 | 6
ztable | 134517280 | 28 | 5 | 3
(5 rows)
```

`RTA` 元表的 `address` 字段为 0，因为它们实际上是指针数组，所以它们使用迭代器函数。元表中的所有列都被标记为只读，因为所有值都是通过 `rta_add_table()` 调用设置的。

### `rta_columns`

`rta_columns` 元数据是列定义的集合。所有表的所有列定义都收集到 `rta_columns` 表中（该表实际上持有指向 `COLDEF` 结构的指针）。我们可以使用元表和 `WHERE` 子句查看某个表中包含哪些列。

```sql
# SELECT table, name FROM rta_columns WHERE table = ztable;
ztable | address
ztable | zalarm
table | zcount
(3 rows)
```

你认为如果我们将元表结合会得到什么？

## RTA 表编辑器

`RTA` 软件包有一个基于 `PHP` 的工具叫做表编辑器，它可以让你查看并编辑任何表。图 3-3 显示了该界面。你可以通过浏览器访问 `http://192.168.1.11/rta/tables.php?port=8885` 来启动它。

### rta 表

| 名称 | 描述 |
| --- | --- |
| rta_tables | 系统中的所有表。 |
| rta_columns | 所有列的列表。 |
| rta_dbg | 调试日志。通过修改 `target` 字段设置默认值。 |
| rta_stat | rta 软件包错误计数。 |
| ztable | 显示列标志 |

图 3-3：RTA 表编辑器

从顶部选择一个表会打开该表内容的网页。图 3-4 显示了 `ztable` 的示例。

| name | zalarm | zcount |
| --- | --- | --- |
| Front Door | 0 | 0 (编辑) |
| Back Door | 0 | 0 (编辑) |
| Garage | 0 | 0 (编辑) |
| Refrigerator | 0 | 0 (编辑) |
| 0 | 0 | 0 (编辑) |

图 3-4：示例表格显示

你可以从表格中选择一行进行编辑。图 3-5 显示了选择第 3 行后的视图。

![](img/a28f0056348678270fea0cfef7891_63_0.png)

图 3-5：示例行编辑界面

侵入。作为安全预防措施，某些守护进程如果无法打开并加载配置文件，它们将拒绝运行。

由于配置文件通常在命令行中指定，你的程序可能需要对它进行两次扫描：第一次是为了获取配置文件，第二次是在加载配置文件后解析命令行。命令行上的参数通常在调试时使用，因此它们的值会覆盖配置文件中的值。

让你的程序进行一次完整性检查（sanity check），验证配置的一致性，并在发现任何问题时确保其报告错误或退出。

# 进入后台

一旦加载了配置，下一步是让进程（可选地）进入后台运行，这样它就可以从控制终端中分离出来。这是通过调用 `fork()` 函数创建一个子进程来实现的。父进程应该在 `fork` 之后退出。

为了进入后台，子进程会关闭控制终端的文件描述符。结果是，我们拥有了一个没有附加到控制终端的后台进程。

你的代码看起来可能像这个示例，父进程 `fork` 并退出，留下子进程继续设置守护进程：

```c
pid_t dpid;                                //守护进程 PID
dpid = fork();
if (dpid < 0)                             // 错误？
    exit(-1);
if (dpid > 0)                             // 父进程？
    exit(0);
// 我们是子进程，继续设置守护进程
```

在两种情况下，你不应该将进程发送到后台：调试时（因为你希望终端保持为程序的的控制终端，以便你可以查看诊断信息并在需要时杀死程序），以及当你希望在程序崩溃时自动重新启动它时。在后一种情况下，守护进程应该保持在前台，这样当守护进程退出时（无论正常退出还是由于错误），父进程将接收控制权。

下面的示例 脚本展示了你如何自动重新启动守护进程。

```sh
#!/bin/sh
while true
do
    mydaemon
    logger "Restarting mydaemon"
done
```

脚本监控的两种常见替代方案是将你的守护进程添加到 `/etc/initab` 并让 `init` 进程重新启动它，或者编写一个自定义监控程序来重新启动设备上的各种守护进程。`/etc/initab` 方法可以节省内存和进程表中的条目，而且你不需要编写任何新软件。重启 `mydaemon` 的脚本可以替换为 `/etc/initab` 中的单行内容。如果默认级别为 3，该行可能显示为：

```
ap:3:respawn=:usr/local/bin/mydaemon
```

`respawn` 词告诉 `init` 程序在 `mydaemon` 崩溃时重启它。

# 成为进程和会话组组

Linux 内核将每个进程分配到一个进程组和一个会话，两者都用于信号的分发。在一个会话中，所有进程通常从 `xterm` 窗口或虚拟控制台登录启动。在一个进程组中，所有进程都在命令行管道中启动。每个进程只有一个从控制终端接收输入的进程组；该进程组被称为前台进程组。

例如，打开一个 `xterm` 或登录虚拟控制台，并输入这些命令：

```bash
cat | sort uniq | tr a &
cat | sort uniq | tr a d
```
