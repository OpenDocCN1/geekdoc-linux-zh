
*term* 字段指定了源如何终止日志消息。零表示日志消息以空终止符终止。来自 syslog 的消息在源端使用 `read()` 接收一条完整的消息。这种终止方式用于 UDP 套接字，例如。二表示以换行符终止消息。换行符终止用于 `tail -f` 类型的源。

MUx 表具有只读的字段，其中存储了使用统计数据、错误统计数据以及源的文件描述符。如需了解有关这些字段的更多信息，请使用 RTA 表编辑器在运行中的 Laddie 设备上对其进行检查。

另外两个 logmux 实例与消息输入处理相关。Rawlog 表是一个 FIFO，用于存储最近的 10 条消息。它在调试过滤器或监控向日志器的原始输入时非常有用。Accept 表存储了接受的 TCP 连接和 Unix 套接字所需的文件描述符和其他信息。Rawlog 或 Acpt 中均没有可配置字段。

## logmux 过滤器与重写

使用 logmuxd 的主要原因之一是它可以重写消息并将其转发到另一个进程。例如，当用户在区域内设置警报时，laddie 会发送消息“User set alarm on zone n, zone_name”（其中 *n* 和 *zone_name* 被替换为区域编号和用户分配的名称）。我们希望这条日志消息出现在前面的 LCD 显示屏；LCD 显示屏只能显示 16 个字符，因此我们使用 logmuxd 的重写功能将消息重写以适应 LCD 显示。原始消息从如下形式重写：

```
Aug 12 22:28:31 Ladd[3820]: User set alarm on zone 5, Refrigerator
```

变为如下形式：

```
22:28 Usr set 5
```

用于识别和重写日志消息的所有配置数据都包含在 Filters 表中。该表包含目的地的类型和名称、用于匹配的正则表达式，以及用于重写消息的 *sprintf()* 格式化字符串。让我们逐一查看这些每个字段。

Laddie 事件处理 95

有两个字段用于指定目的地：*destype* 和 *destname*。每种类型的目的地都有一个单独的表。这是必要的，因为例如，电子邮件目的地需要比 SNMP trap 目的地不同的配置信息。目的地的类型和其目的地表由 destype 字段设置。共有 9 种有效的目的地类型。类型 1 和 2 的类型未包含在表 7-3 中，因为它们严格来说是源。

### 表 7-3: 九种目的地类型

| destype | 目的地表 | 含义 |
| --- | --- | --- |
| 0 | None | 无目的地（用于收集统计数据） |
| 3 | NetDest | 接受的 TCP 连接 |
| 4 | NetDest | 发出的套接字连接 |
| 5 | NetDest | UDP 套接字目的地 |
| 7 | FileDest | 文件（包括 FIFO 和普通文件） |
| 8 | PdbDest | PostgresSQL（或 RTA 表） |
| 9 | SmpDest | SNMP trap 目的地 |
| 10 | MailDest | 电子邮件目的地 |
| 11 | TblDest | logmbox 用于输出消息的内部表 |

每个目的地表中可以描述多个目的地。每个目的地在其中一个目的地表中都有其唯一的名称（*destname*）。例如，如果你有两个不同的 SNMP 目的地，你可以将其中一个命名为 *allsnmp*，另一个命名为 *laddiesie*。通过给它们赋予不同的名称，你可以为它们定义不同的路由和重写规则。要将 Filters 表中的过滤器链接到特定的目的地，你需要同时指定目的地类型和目的地名称。

Logmbox 根据消息的设施（facility）、日志级别（level）以及文本模式匹配来路由消息。Filters 表中的这三个字段分别是 *facility*、*level* 和 *regex*。这些设施和日志级别与 syslog 的定义相同。regex 模式是用于模式匹配和子模式匹配的正则表达式。regex 库是模式匹配和提取的良好选择，因为模式可以预编译以提高匹配速度，且 regex 让你能够轻松提取子模式。在使用 Logmbox 时，我们发现不需要过多了解 regex 模式。

假设你正在处理列车到达车站的事件，日志消息为 *Train from San Jose arriving on Track number*。为了重写这条消息，你提取了城市和列车号。捕获城市的 regex 模式是 *[A-Za-z-]+*。该模式匹配任何大写或小写字母字符、空格或连字符的组合。列车号的模式是 *[0-9]+*。诀窍在于：如果你在模式周围加上括号，regex 就会让该模式在输出中单独可用。以下是一个匹配城市和列车号的 regex 模式：

Train from ([A-Za-z-]+) arriving on Track number ([0-9]+)

Filter 表的 rewrite 字段包含用于重写日志消息的 snprintf() 格式化字符串。该格式包含你选择的文本，并可以包含从 regex 模式中提取的字符串。匹配项作为显式参数提供给 snprintf。

你可以从 CD 中复制源码并在你的开发系统上构建 logmuxd，也可以启动 Laddie CD 并使用其正在运行的 logmuxd 版本。不用担心更改 Laddie 上的 logmuxd 表，重启将把它们恢复到原始状态。如果你愿意，我们将使用 `psql` 来更新表。图 7-3 阐了此示例中的数据流。

![](img/a28f80056348678270f2ea0cfefd7891_122_0.png)

图 7-3：使用 telnet 的 logmuxd 示例

配置的基本步骤为：

- 配置 logmuxd 以接收来自 `/dev/log` 的 syslog 消息。验证设置。
- 配置 logmuxd 识别并重写“train arriving”（列车进站）消息。
- 配置 logmuxd 在端口 3333 上接受 TCP 连接。
- 使用 `logger` 和 `telnet` 验证消息是否已通过 TCP 端口 3333 分发到连接。

我们首先开始清除将用到的所有表中的配置。通过控制台或 telnet 登录到运行 logmuxd 的 PC（从书籍 CD 启动的 PC）。logmuxd 上的 RTA 接口监听在 8887 端口；当你启动 SQL 会话并使用这些命令清除表时：

```sql
psql -h localhost -p 8887
UPDATE MuxIn source = "", type =0;
UPDATE Filters destype = 0, destname = "", regex = ""
rewrite = "", time_fat = ""
UPDATE NetDest destname = "", dest = "", port = 0;
```

## MuxIn

在示例中，我们希望 logmux 替换 syslog，因此我们需要配置它监听 Unix 套接字 `/dev/log` 并按 syslog 格式读取日志消息。我们将将其指定为 `/dev/log`，类型指定为 6（syslog 格式），日志消息终止符指定为 0（消息之间的空字符）。

```sql
UPDATE MuxIn source = "/dev/log", type = 6, term = 0 LIMIT 1;
```

如果此时一切正常，该命令在 `/dev/log` 上打开了一个 Unix 套接字，MuxIn 表的显示应显示我们源的有效文件描述符。（`netstat` 命令也应该显示 `/dev/log` 套接字）。

```sql
SELECT source, fd FROM MuxIn;
```

如果我们现在正在监听 `/dev/log`，我们应该能看到通过 `logger` 发送的消息。打开另一个终端窗口并再次 telnet 登录到运行 logmuxd 的 PC。在新窗口中执行以下命令：

```bash
logger "Hello, world";
```

通过查看 Rawlog 表验证 logmuxd 是否接收了该消息。

```sql
SELECT source, log FROM Rawlog;
```

## Filters

继续该示例，我们将使用 Filters 表中的第一行，我们将一次更新一或两列，以便更好地解释这些列。

### destype

你可能记得 `destype` 是一个整数，它隐式地选择此过滤器将使用哪一个目标表作为其目标。`destype` 为 3 用于接受的 TCP 连接。

### destname

在一个目标表中可能有多个独立的目的地。我们需要某种方法来区分一个目的地和另一个，因此我们为每个目的地分配一个名称。Filter 表中的 `destype` 选择使用哪个目标表，而 `destname` 选择该表中的哪行。对于此示例，我们分配了名称 example_2。

```sql
UPDATE Filters SET destype = 3, destname = "example 2" LIMIT 1;
```

### regex
