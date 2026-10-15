
Chunks

| address | chk/dbs offset | size | free | bpages | flags | pathname |
|---|---|---|---|---|---|---|
| 101ief8 | 1 | 0 | 10000 | 6971 | | PO- | `/opt/data/rootdbs` active, 2047 maximum |

为了继续我们最后的配置，你需要对你的 `$ONCONFIG` 进行几处更改，然后重启引擎。

# 第 4 章 • 在 Linux 上安装 Informix

> 注意
>
> 通过使用 `onstat` 命令可以获得 `onstat` 选项列表。请参阅管理员指南获取关于这些选项的完整讨论。书中包含了一些可以提供有关引擎更详细报告的工具。

## 停止你的引擎

现在引擎正在运行，如何关闭它？停止 Informix 引擎，请使用 `onmode -q`：

```
$ onmode -q
```

这将允许你对 `$ONCONFIG` 进行更改并重启引擎。`onmode` 命令包含了一系列附加功能。务必阅读管理员指南获取更多关于选项的信息。

## 最后配置

接下来是什么？你的引擎正在运行，但尚未就。下一阶段将使你的服务器变得有用，特别是对于终端用户。我们将为你的引擎设置最终配置，你可以根据需要进行更改。你需要确保你有执行以下操作的磁盘空间。如果你在本章初完成了分配，现在可以完成以下步骤。

## 回顾

让我们快速回顾一下在安装和数据库期间涵盖的一些 dbspaces：

- `rootdb`. 将包含物理日志；必须移出 `rootdb` 进入独立空间。
- `logdb`. 将包含逻辑日志；必须移出 `rootdb` 进入独立空间。
- `tempdb`. 默认到 `rootdb`，指向独立空间，用于排序、查询和临时表。
- `userdb`. 将包含数据库条目，但没有表条目。
- `tabdb01`. 将包含表。
- `indexdb01`. 将包含索引。

### Physdb

出于性能考虑，将物理日志移到独立空间是标准做法。物理日志是缓冲区或缓存，是写入数据库的活动。将其移到独立空间允许你在不影响 `rootdb` 的情况下扩展或缩小其大小，并提高性能。如前所述，`rootdb` 是你在此创建的每个实例的核心。你可以拥有多个 Informix 实例；每个实例都有自己的 `rootdb` 且与其他实例分开。最小化对 `rootdb` 的风险非常重要。迁移物理日志是我们确保 `rootdb` 仅用于活动——以及管理引擎的步骤之一。确保你的 Informix 引擎已启动运行。

```
$ onstat
```

如果引擎没有运行，使用不带选项的 `oninit` 程序启动它，或者至少使用 `-v` 选项（详细模式）：

不要在创建 `rootdb` 后使用 `-i` 选项运行 `oninit`。这样做等同于格式化你的硬盘。你可以使用的例外是 `oninit -v`，它在引擎启动时显示详细输出。一旦引擎启动运行，你可以先用 UNIX/Linux 命令创建 `physdb`，然后像创建 `rootdb` 一样用 Informix 命令。

## 创建 physds 文件

UNIX 和 Linux 允许你在执行 `>` 命令时创建一个零长度的文件。

```
$ cd /opt/data
$ touch physds
$ chown informix:informix physds
$ chmod 660 physds
```

这创建了文件，但里面完全为空。正如提到的，我们需要在单用户（single-user）或静止模式（quiescent mode）下执行大部分后续步骤。我们还将作为 DBA 使用两个工具——`onspaces` 和 `onparams`。`onspaces` 可以在多用户模式下使用，但 `onparams` 必须在引擎处于单用户模式运行时运行。进入单用户模式，运行命令 `onmode -s`。在此命令中添加 `s` 将移除以下问题：

```
rebel:root # onmode -s
```

这将执行执行机 GRACEFUL SHUTDOWN

Do you wish to continue (y/n)? y

```
rebel:root # onstat
```

Informix Dynamic Server Version 7.30.UC10 -- Quiescent-Up 00:22:36 -- 8888 Kbytes

| address | flags sessid user tty wait tout locks nreads nwrites |
|---|---|---|---|---|---|---|---|---|
| 1012014-P-D 1 | informix | | | | 0 | 0 | 0 | 11 | 5 |
| 101204c-P-F 0 | informix | | | | 0 | 0 | 0 | | 2 |
| 1012097c-P-W 9 | informix | | | | 0 | 0 | 0 | | 0 |
| 1012030-P-B 10 | informix | | | | 0 | 0 | 0 | | 0 |
| 101214c-P-D 13 | informix | | | | 0 | 0 | 0 | | 0 |

5 active, 128 total, 18 maximum concurrent

Profile

dskreads pagreads bufreads %cached dskwrits pagwrites bufwrites %cached

```
20 38 36 44.44 7 2 0.00
```

```
isamtot open start read rewrite delete commit rollbk
16 4 5 3 0 0 0 0
```

### 在 Linux 上安装 Informix • 第 4 章

| gp_read | gp_write | gp_rewrt | gp_del | gp_alloc | gp_free | gp_curs |
|---|---|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 | 0 | 0 |

| ovlock | uservithread | ovbuff | usercpu | syscpu | numckpts | flushes |
|---|---|---|---|---|---|---|
| 0 | 0 | | 2.95 | 0.09 | 1 | 10 |

| bufwaits | lokwaits | lockreqs | deadlocks | dltouts | ckpwits | compress | segscans |
|---|---|---|---|---|---|---|---|
| 0 | | 10 | | 0 | 0 | 0 | 0 |

| ixda-RA | idx-RA | da-RA | RA-pgsused | lchwaits |
|---|---|---|---|---|
| 0 | 0 | | 0 | 0 |

如果你查看第一行，你会发现 Informix IDS 现在处于静止状态（quiescent），或者说处于单用户模式。这是你可以运行 `onparams` 来执行某些更关键命令的唯一模式，例如将物理日志转出到另一个数据库空间（dspace）。在其他时间或其他平台上，`onparams` 必须在引擎完全关闭的情况下运行。

让我们创建一个 `physdbs`。为了做到这一点，我们必须首先使用 `onspaces` 命令创建一个 20MB 的 `physdbs` 数据库空间，然后使用 `onparams` 命令转出物理日志。本章剩余部分中的命令在代码示例中均已加粗处理，以便你能够轻松地识别出发生了什么。

```
rebel:root # onspaces -c -d physdbs -p /opt/data/physdbs -o 0 -s 20480
```

正在验证物理磁盘空间，请稍候 ...

空间添加成功。

> **警告** 需要对 Root DBSpace 进行层 0 归档。

```
rebel:root # ontape -s -L 0
```

到磁带设备 `/dev/null/` 的归档已完成。

程序结束。

```
rebel:root # on -1
```

Informix Dynamic Server Version 7.30.UC10 -- Quiescent-Up 00:46:17 -- 8888 Bytes

物理日志

Buffer bufused bufsize numpages writes/io

P-1 4 16 4 0 0.00%

| phybegin physize phpos phused used |
|---|---|---|---|---|
| 10003f | 500 | 223 | 4 | 0.80 |

### 逻辑日志
