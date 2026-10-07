
Kernel Params: `msMaxMessageSize`:65536 `msgMaxQueueIds`:65536

`smsMaxSegmentSize`:16 `max`:922337203685475807

`smsIlds`:4096 `semMap`:256000 `semNumIDs`:1024

`semump`:256000 `semundo`:256000 `semNumPeriod`:250 `demops`:32

`semUndoSize`:250 `max`:32767 `semAdjustOnExit`:32767

此记录中的信息仅在文件文件创建时有效（请参见此记录的时间戳）

每当你使用 `db2set` 设置或删除 DB2 配置文件变量时，如果 `DBLEVEL` 为 1 或更高，DB2 就会在 `db2diag` 中记录一条消息。如示例 7-16 所示，在执行以下命令后你将看到一条消息：

```
db2set DB2COMM=TCP
```

当你怀疑 DB2 引擎无法写入 `db2diag.log` 时，可以考虑使用此方法检查。

示例 7-16 关于设置 DB2 配置文件变量的消息

```
2008-02-14-10.18.46.710519-480 11285E292 LEVEL: Event
PID : 32098 TID : 47944161495904 PROC : db2set
INSTANCE: db2inst1 NODE : 000
FUNCTION: DB2 UDB, oper system services, db2set_main, probe:40
CHANGE : CFG DB2COMM: From: "TCPIP" To: "TCPIP"
```

示例 7-17 显示了从 `db2diag.log` 中提取的日志消息。当运行以下 DB2 命令时，该消息会被写入日志文件：

```
db2 update cfg for ITSDB using NEWLOGPATH /db2log
```

此消息显示 `SQLCODE` 为 5099，带有令牌 `"/db2log NEWLOGPATH 9"`，这些令牌在我们的示例中被**加粗**显示。使用 `db2 ? sql5099` 命令可以检查 SQL5099 的含义。该代码告诉你原因 9 意味着“无法访问路径”。在我们的示例中，无法访问该路径是因为 `/db2log` 的写权限仅分配给了 `root` 用户。用户 `db2inst` 不允许在 `/db2log` 下创建子目录。以 `root` 用户执行 `db2adm /db2log` 后，问题得到解决。

示例 7-1 关于设置 NEWLOGPATH 的消息

```
2008-02-14-10.32.19.9084-480 I1578E25 LEVEL: Error
PID : 25392 TID : 4773566839097 PROC : db2sysc
INSTANCE: db2inst1 NODE : 000
```

在 Linux 上运行 DB2

```
HDL : -07433
APPID : *N0.db2inst.1084832
AUTHID : DB2INST
EDUID : 1129
UNAME: db2agent (instance)
FUNCTION: DB2 UCB, config/install, db2Cfg, probe:923
DATA #1 : SQLCA, PD_DB2_TYPE_SQLCA, 136 bytes
sqlaid = SQLCA:136
sqlrml: -5099
sqlrmec: /db2log NEWLOGPATH 9
sqlerrp = SQL09950
sqlerrd = (1) 000000000 (2) 000000000 (3) 000000000 (4) 000000000 (5) 000000000 (6) 000000000
sqlwarn = (1) (2) (3) (4) (5) (6) (7) (8) (9) (10) (11)
sqlstate:
```

## 7.4.3 操作系统日志

Linux 操作系统提供了支持系统日志和内核消息拦截的工具。在这些工具中，`syslog` 是许多程序使用的日志类型。由 `syslog` 记录的每条消息至少包含时间和程序字段。位于 `/etc` 目录下的 `syslog` 文件是 `syslog` 的配置文件。它指定了 `syslog` 的日志规则。这是一个文件，你可以使用任何喜欢的编辑器使其适用于你的环境，或者直接使用 Linux 安装期间设置的默认值。

当你遇到问题且不确定是否与系统设置时，检查系统日志（如果没有更改默认配置，文件可能名为 `/var/log/messages`）是一种良好的做法。有关如何设置 `syslog` 以及如何解释系统日志的更多信息，请参考 Linux 特定文档。

注意：不是 `syslog` 包，SUSE Linux 10 默认安装 `syslog-ng` 包。`syslog-ng.conf` 是主配置文件，位于 `/etc/syslog-ng`。

## 7.5 故障排除工具

DB2 产品包含几个帮助你监控和排除 DB2 系统问题的工具。我们介绍了其中几个有用工具并提供了使用示例。

### 7.5.1 db2diag

`db2diag.log` 文件包含运行 DB2 系统的信息。你需要定期查看此日志。你可以使用 `db2diag` 分析来过滤格式化 `db2diag.log` 文件。作为使用 `db2diag` 的替代方案，可以使用文本编辑器查看怀疑故障机器上的日志文件。最近的记录位于文件末尾。

注意：管理和诊断日志会持续增长。当它们变得太大时，请进行备份并删除文件。系统下次需要时会自动生成一组新文件。

在这里，我们说明带选项使用 `db2diag` 的示例：

- 不带选项运行 `db2diag` 命令：

`db2inst1@ms:~db2diag`

如果你不带任何参数使用 `db2diag` 命令，该工具将处理当前目录下的 `db2diag.log` 文件并将其打印到屏幕。如果在当前目录未找到文件，则搜索由 `DIAGPATH` 变量设置的目录。

- 在控制台运行时观察 `db2diag.log` 文件：

要查看 `db2diag.log` 文件的增长，请使用：

`db2diag -f`

此命令显示到目前为止写入 `db2diag.log` 文件的所有记录，显示将持续，直到你按下 Ctrl+C 停止。

- 查看特定间隔内的日志：

要显示时间戳 `2008-02-14-10.00`（包含）之后记录的所有消息，请输入此命令：

`db2diag -t 2008-02-14-10.00`

将 `2008-02-14 12.00.30` 到 `2008-02-14` 下午 3 点之间的所有条输出到名为 `db2diag_082014noon.log` 的输出文件中，输入：

`db2diag -t 2008-02-14-12.00.30:2008-02-14-15 -o db2diag_082014.log`

日期和时间的格式为 `YYYY-MM-DD-hh.mm.ss.nnnnnn`；然而，你不需要使用完整的时间戳。

要显示过去三天的条目，输入：

`db2diag -H 3d`

#### 查看特定数据库的日志

如果你在 DB2 实例中拥有多个数据库，并且只想查看某个特定数据库的 `db2diag.log` 条目，可以使用：

```
db2diag -g db1TS008
```

`-g` 选项提供了类似 `grep` 的过滤功能，用于处理逗号分隔的字段-模式对。另一个示例是：

```
db2diag -db1SAMPLE,level=Event,pid=5971
```

此命令显示进程 ID 5971 的所有与 SAMPLE 数据库无关的事件。

字段名不区分大小写，而搜索模式（输入字段）区分大小写。要获取所有可用字段名的列表，请使用 `db2diag -h` 命令。

#### 分区数据库

在分区数据库环境中，`db2diag.log` 文件包含所有数据库分区的条目。每个数据库分区都会将其消息写入同一个文件中。你可以对输出结果进行过滤：

- 仅显示数据库分区 2 的日志记录：

`db2diag -n 002`

- 显示数据库分区 0 和 2 中所有仅包含错误的日志记录：

`db2diag -node "0, 2" -l "Error, warning"`

#### 归档 db2diag.log 文件

如果你想存档当前的 `db2diag.log` 文件并启动一个新的日志文件，请输入：

```
db2inst1@ms:/dbhome/db2inst1> db2diag -A
db2diag: Moving "/dbhome/db2inst1/sqllib/db2dump/db2diag.log"
to "/dbhome/db2inst1/sqllib/db2dump/db2diag.log_2008-02-14-16.36.67"
```

#### 格式化 db2diag 输出

以下命令可以格式化 `db2diag` 的输出，仅显示时间戳、数据库分区号、消息级别和文本：

```
db2diag -fmt "Time: %{ts} Partition: %node Message Level: %{level} \nMessage: @{msg}\n"
```

内部错误返回码

#### DB2 内部错误代码

要获取 DB2 内部错误代码 `0x860F000A` 的描述：

```
db2diag -rc 0x860F000A
```

要显示所有可用的 DB2 ZRC 返回码列表，请输入：

```
db2diag -rc zrc
```

你可以组合这些选项。还有许多可用选项。使用命令 `db2diag -h` 查看 `db2diag` 的所有选项。输出如示例 7-18 所示。要查看更多细节和示例，请使用命令 `db2diag -h tutorial`。

#### 示例 7-18 db2diag -help 的输出

```
db2inst1@msa:> db2diag -help
```

`db2diag` - 用于过滤和格式化 `db2diag.log` 的分析工具

命令语法：

```
-----------------------
 V | V 
>>db2diag--+-------+-->>
|      +---+       |
|      --option-- --filename--
```

命令参数：

- `- filename` - 一个或多个用空格分隔的诊断日志路径名

- `-help, -h, ?` - 帮助信息。获取关于帮助的帮助，请尝试 "`db2diag -h h`"

- `-filter, -g` - 对字段-模式列表进行区分大小写的搜索

- `-gi` - 对字段-模式列表进行不区分大小写的搜索

- `-gv` - 区分大小写的反向匹配

- `-gvi, -gilv` - 反转所有过滤选项的匹配方向

- `-invert, -e` - 记录字段必须存在才能被处理

- `-pid` - 查找进程 ID 列表的所有记录

- `-tid` - 查找线程 ID 列表的所有记录

- `-edudiv` - 查找 EDU ID 列表的所有记录

- `-node, -n` - 查找节点列表的所有记录

- `-error, -l` - 查找错误列表的所有记录

- `-level, -H` - 查找严重性级别列表的所有记录

- `-history, -` - 显示在指定时间段内日志记录的历史记录

- `-time, -` - 显示特定时间段内的所有记录

- `-count, -c` - 显示匹配记录的计数

- `-verbose, -V` - 显示所有包含（或不包含）数据的字段

- `-strict` - 使用单个字段显示记录：每行一个“值”值对

- `-cbe` - 以通用基础事件 (CBE) 格式显示记录

- `-fnt` - 使用格式字符串格式化工具的输出

- `-output, -` - 将输出保存到文件

- `-follow, -f` - 随着文件增长连续显示追加的记录

- `-archive, -A` - 归档诊断日志文件

- `-readfile` - 从文件读取并忽略终端输入（用于脚本）

- `-rc` - 显示 DB2 错误代码、ZRC 或 ECF 的描述

- `-ecfid` - 显示从数字 ECF ID 中提取的函数信息

- `-facility, -fac` - 显示来自特定设施的消息

"`db2diag -h <option1,[option3..]>`" - 为选项列表列表中指定的一个或多个选项显示额外的帮助和用法示例

"`db2diag -h brief`" - 在不带示例的情况下所有选项的帮助

"`db2diag -h examples`" - 显示几个入门示例

"`db2diag -h tutorial`" - 显示涵盖所有功能的高级示例

"`db2diag -h notes`" - 显示用法说明和限制

"`db2diag -h all`" - 以最完整的形式显示关于所有选项的帮助

可以在故障排除指南、DB2 Linux、UNIX 命令参考中获取更多信息。

### 7.5. db2pd

你可以使用 `db2pd` 工具从 DB2 系统内存获取锁（latches）并快速返回结果。如果不使用任何选项，它将以交互模式启动。示例 7-19 显示了方法。

```
db2inst1@msa:/home/db2inst1$ db2pd
db2pd> 你正在交互模式运行。
db2pd> 如果你需要命令行模式，请带有有效选项重新运行 db2pd。
db2pd> 输入 -h 或 -help 获取帮助。
db2pd> 输入 q 退出。
db2pd> --memsets
```

```
db2inst@ms:/dbhome/db2inst> export DB2PDOPT="agents"
db2inst@ms:/dbhome/db2inst> db2pd
```

数据库分区 0 -- 激活 -- 已运行 0 23:49

- 代理:

当前代理: 6

空闲代理: 0

激活代理: 4

激活总: 4

池化代理: 2

池化总: 2

| Name | Size(Kb) | Unrsv(Kb) | Used(Kb) | Cmt(Kb) |

|---|---|---|---|---|

| DBMS | | | | |

| BP | 0x0000002000000041235219 | 29568 | 0xF197AE61 | 0 | |

| FMP | 7360 8000 21568 | 0x000002100000041238528 | 22592 | 0x0 | 2 |

| Trace | 320 22592 0 | 0x00000000000000412319750 | 39227 | 0xF197AE74 | 0 | -1 |

| FCM | 39227 0 | 0x00000022000000412418057 | 238592 | 0xF197AE62 | 0 | 11 |

| FCM | 204032 34560 204032 | | | |

```
db2inst@ms:/dbhome/db2inst> db2pd -osinfo
```

#### 操作系统信息:

- OSName: Linux

- NodeName: mensa

- Version: 2

- Release: 6

- Machine: x86_64

| CPU 信息 | OnlineCPU | ConfigCPU | Speed(MHz) | HMTDegree |

|---|---|---|---|---|

| | 2 | 2 | 600 | 1 | 2 |

| 物理内存和交换分区 (MB): | TotalMem | AvailMem | TotalSwap | FreeSwap |

|---|---|---|---|---|

| | 3753 | 209 | n/a | 8198 | 8192 |

| 虚拟内存 (MB): | Total | Reserved | Available | Free |

|---|---|---|---|---|

| | 11951 | n/a | n/a | 8401 |

| 消息队列信息: | MsgSeg | MsgMax | MsgMap | MsgMni | MsgTql | MsgMnb | MsgSsz |

|---|---|---|---|---|---|---|

| n/a | 65536 | 65536 | 1024 | 65536 | 65536 | 16 |

#### 共享内存信息:

| ShmMax | ShmMin | ShmIds | ShmSeg |

|---|---|---|---|

| ShmMap | SemMni | SemMns | SemMnu | SemSls | SemOpm | SemUme |

| SemUz | SemVmx | SemAem | | | | |

| 92237023685477581 | | | | | | |

| 20 | 1024 256000 256000 250 32 | n/a | | |

| 32767 | | | | |

#### CPU 负载信息:

- 短 | 中 | 长

- 0.160000 | 0.140000 | 0.080000

#### CPU 使用率信息:

Total Usr Sys Wait Idle

0.080000 n/a 0.920000 n/a

你可以使用 `DB2PDOPT` 环境变量为 `db2pd` 设置默认选项。

在示例 7-20 中，将默认设置为 "`agents`" 以获取有关运行的信息。

```
db2inst1@msa:/home/db2inst1$ db2pd
db2pd> 你正在交互模式运行。
db2pd> 如果你需要命令行模式，请带有有效选项重新运行 db2pd。
db2pd> 输入 -h 或 -help 获取帮助。
db2pd> 输入 q 退出。
db2pd> --memsets
```

```
db2inst@ms:/dbhome/db2inst> export DB2PDOPT="agents"
db2inst@ms:/dbhome/db2inst> db2pd
```

数据库分区 0 -- 激活 -- 已运行 0 23:49

- 代理:

当前代理: 6

空闲代理: 0

激活代理: 4

激活总: 4

池化代理: 2

池化总: 2

| Address | AppHandle [nod-index] | AgentEUID Priority | Type | State |
