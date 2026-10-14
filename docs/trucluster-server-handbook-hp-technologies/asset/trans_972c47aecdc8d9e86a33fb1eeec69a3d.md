

由于该命令会产生大量事件，我们可能希望将搜索范围限制为仅网络相关事件。

使用 V5.0A，执行 `evmwatch -i -f "[name *.net]" | evmshow`。
使用 V5.1（及更新版本），执行 `evmwatch -A -i -f "[name *.net]"`。

```text
# evmwatch -A -i -f "[name *.net]"
NIFF: node sheridan detected a failed network connection on network via interface
NIFF: node sheridan has detected an available network connection on network via interface
NIFF: node sheridan has declared a connectivity alert with network via interface
NETRAIN: node sheridan detected a failed network connection on network via interface
NETRAIN: node sheridan has detected an available network connection on network via interface
NETRAIN: node sheridan has declared a connectivity alert with network via interface
```

好的，这样我们缩小了范围，但如果我们想查看事件的名称而不是格式文本呢？`EvmEvent(5)` 参考页定义了可用于创建“show-template”的“标准数据项”。“show-template”可通过 `-t` 开关为 evmget、evmshow、evmsort 和 evmwatch 命令创建（或者如果使用相同的 show-template，可以使用你喜欢的格式设置 `EVM_SHOW_TEMPLATE` 环境变量）。

使用 V5.0A，执行：`evmwatch -i -f "[name *.net]" | evmshow -t "@name"`
使用 V5.1（或更新版本），执行 `evmwatch -A -i -f "[name *.net]" -t "@name"`

```text
# evmwatch -A -i -f "[name *.net]" -t "@name"
sys.unix.hw.net.niff.down
sys.unix.hw.net.niff.up
sys.unix.hw.net.niff.alert
sys.unix.hw.net.netrain.down
sys.unix.hw.net.netrain.up
sys.unix.hw.net.netrain.alert
```

### 8.7.2 如何等待事件发生？

使用不带 `-i` 开关的 `evmwatch` 命令即可轻松实现等待系统或集群上事件发生。

使用 V5.0A（或更新版本）：

```text
# evmwatch | evmshow
```

### 8.7.4 如何查看已配置的通道？

```text
# evmoinfo -lc
syslog
binlog
misclog
evmlog
```

### 8.7.5 如何获取来自特定通道的事件？

你可以使用 `-C` 标志限制 `evmget` 搜索的范围到特定通道。此功能在 *Tru64 UNIX* 版本 5.1 中添加到 EVM。

```text
# evmget -A -C binlog -f "[age < 1d]" -t "@timestamp @name @@"
28-Mar-2001 07:36:13 sys.unix.binlog.op.timestamp System timestamp
28-Mar-2001 07:37:41 sys.unix.binlog.hw.scsi SCSI event
28-Mar-2001 07:37:41 sys.unix.binlog.hw.scsi SCSI event
28-Mar-2001 07:37:41 sys.unix.binlog.hw.scsi SCSI event
28-Mar-2001 16:17:42 sys.unix.binlog.op.timestamp System timestamp
```

要从多个通道检索信息，请使用多个 `-C` 开关。

```text
# evmget -A -C binlog -C syslog -f "[age < 1d]" -t "@timestamp @name @@"
```

### 8.7.6 如何格式化从事件接收到的“timestamp”？

如你所见，你可以使用 `@timestamp` 过滤器检索时间和日期，但这会同时给出时间和日期。如果你只想要时间戳的特定部分，可以使用 `evmshow` 并通过 `-T` 开关指定时间格式。你使用的格式与 `date(1)` 命令使用的格式相同。

```text
# evmget -f "[prio >> 700]" | evmshow -T "%A (%D) %H:%M"
Thursday (03/22/01) 09:22 Correctable error reporting state changed
Thursday (03/22/01) 09:30 Correctable error reporting state changed
```

### 8.7.7 如何发送事件？

你可以使用 `evmpost` 命令发送（或发布）事件。`evmpost` 命令从输入流（或文件）接收输入，将输入转换为 EVM 的二进制格式，然后将事件发送到 EVM 守护进程以分发给订阅者。

```text
# echo "event { name tcrhb.timeEvent.overDue }" | evmpost
```

这只是使用事件模板文件中定义的默认值将 `tcrhb.timeEvent.overDue` 事件发布到 EVM（有关更多信息，请参阅第 8.4 节）。

你还可以将变量传递给事件，这些变量在事件的模板中定义。例如，在 `tcrhb.timeEvent.overDue` 事件中，我们定义了变量 `dueDate`，它被定义为字符串，默认值是 "Today"。

```text
event {
  name        tcrhb.timeEvent.overDue
  format      "TCR Handbook: this book is overdue. $dueDate is the due date."
  priority    400
  var         {name dueDate type STRING value "Today"}
}
```

为了使用 `dueDate` 变量的替代值发布事件，我们可以执行以下操作：

```text
# echo "event { name tcrhb.timeEvent.overDue var (name dueDate value `date`)}" \
| evmpost
```

如果你不想在命令行上输入事件来发布它，可以将其放在文件中，让 `evmpost` 读取该文件。

```text
# evmpost myEvent
```

你也可以使用 `-a`（管理员）和 `-u`（用户）开关向 EVM 发布简单消息。

```text
# evmpost -a "Starting the upgrade for the C++ compiler" -p 201
# evmpost -u "I am here!"
```

