

# NOTE:

如果您使用的是 csh shell，则需要转义 "!" 字符，像 "\!" 这样。这是为了能够打印出 "!" 字符。省略 "\" 将导致出现 "": Event not found." 错误。请注意，错误信息中的 "Event" 并不是指 EVM 事件，而是 C shell 表示您尝试调取的历史命令未找到的方式。"!" 是从历史列表中调取命令的方式。

## 8.7.8 How Can I Send an Event from a Script?

您可以通过在脚本中使用 evmpost 命令来从脚本中发布事件。evmpost(1) 参考页中也有一个脚本的简短摘录。

## 8.7.9 How Can I Format the Event Information I Receive?

可以使用 evmwatch、evmget 或 evmshow 命令的 "-t" 开关来格式化事件信息。"-t" 使您能够为命令创建 "show-template"。格式可以使用 EvmEvent(5) 参考页中定义的任何有效的 EVM 数据项。在 "show-template" 中使用数据项时，请以 "@" 为前缀。数据项在 EvmEvent(5) 参考页中以大写形式列出，但您可以使用小写。请注意 "@a" 是实际的事件文本，其中文本中引用的任何变量值都被替换为其引用。

```
# evmget -A -t "@pid [@priority] @name: @a" -f "[prio > 600]"
- [700] sys.unix.binlog.hw.correctable_rpt_switch: Correctable error reporting state changed
- [700] sys.unix.binlog.hw.correctable_rpt_switch: Correctable error reporting state changed
302 [700] sys.unix.hw.net.niff.down: NIFF: node sheridan detected a failed network connection on network 192.168.0.69 via interface tu0
```

如果您发现自己 constantly 使用相同的格式，您可能希望在 EVM_SHOW_TEMPLATE 环境变量中定义该格式。

```
# export EVM_SHOW_TEMPLATE="@pid [@priority] @name: @a"
# evmget -A -f "[name *.hw]"
21667 [300] sys.unix.hw.dev_base_name_changed.tape__hwid.123: Device base name changed from unknown to tape0 (HWID=123)
21667 [300] sys.unix.hw.dev_base_name_changed.tape__hwid.124: Device base name changed from unknown to tape1 (HWID=124)
```

从 V5.1A 开始，换行符 (\n) 和制表符 (\t) 可用于提高事件输出的可读性。例如，您可以通过使用 "\n" 在事件输出中插入换行符。

```
# evmget -A -f "[age < 1d]" \
> -t "%n%t%timestamp - %event_id [%priority]%n%name\n%" | more
26-Sep-2002 03:43:59 - 344680 [200]
sys.unix.clu.drd.server_leave_hwid.52
DRD: Removed (unmapped) DRD server molari
```

在过滤器关键字旁边使用 "s" 字符可以设置最小字段宽度。例如，要将 cluster_event 字段的最小字段宽度设置为五，您可以使用以下命令。

```
# evmget -A -f "[age < 1d]" \
> -t "@cluster_event%5 -@name" | more
True  - sys.unix.hw.net.niff.alert
False - sys.unix.evm.logger.log_closed
False - sys.unix.evm.logger.log_started
False - sys.unix.evm.mark
False - sys.unix.binlog.chan.binlog_size
False - sys.unix.binlog.hw.acsi
True  - sys.unix.clu.drd.server_leave_hwid.52
False - sys.unix.binlog.hw.acsi
True  - sys.unix.clu.drd.server_add_hwid.52
True  - sys.unix.clu.drd.new_accessnode_hwid.52
True  - sys.unix.clu.drd.new_accessnode_hwid.52
...
```

## 8.7.10 How Can I Find Out Which Filters are Available?

过滤器关键字在 EvmFilters(5) 参考页中定义。您可以在位于 /usr/share/evm/filters（系统）和 /var/evm/adm/filters（站点定义）目录的过滤器文件中找到过滤器。

```
$ ls /var/evm/adm/filters /usr/share/evm/filters
/usr/share/evm/filters:
binlog.evf  evm.evf    sys.evf    syslog.evf
/var/evm/adm/filters:
<no output>
```

此外，TruCluster Server Handbook 网站（请参阅附录 B 中的 URL）包含一个名为 evf(1) 的 Korn Shell 脚本，可用于查找过滤器文件中有哪些过滤器可用。

## evf [-v] [-d FilterFileDir] [file1 file2...filen]

evf 脚本如果未使用 "-d" 开关或 EVF_DIR_PATH 环境变量，将使用当前工作目录、/var/evm/adm/filters 和 /usr/share/evm/filters 作为默认搜索路径。

```
# evf binlog
/
[no event filter files found]
/var/evm/adm/filters
[no event filter files found]
/usr/share/evm/filters
binlog.evf
@binlog:binlog
@binlog:scsi
@binlog:lsm
@binlog:info
@binlog:msg
@binlog:startup
@binlog:shutdown
@binlog:panic
@binlog:timestamp
@binlog:unknown
```

在此示例中，使用了 "-d" 开关仅搜索 /usr/share/evm/filters 目录；"-v" 开关通过执行 "evmshow -f filter_exp -F" 显示过滤器的详细信息。

```
# evf -v -d /usr/share/evm/filters binlog
/usr/share/evm/filters
binlog.evf
@binlog:binlog      -> [name sys.unix.binlog]
@binlog:scsi        -> [name sys.unix.binlog.hw.scsi]
@binlog:lsm         -> [name sys.unix.binlog.sw.lsm]
@binlog:info        -> [name sys.unix.binlog.op.info]
@binlog:msg         -> [name sys.unix.binlog.op.info.ascii_msg]
@binlog:startup     -> [name sys.unix.binlog.op.startup]
@binlog:shutdown    -> [name sys.unix.binlog.op.shutdown]
@binlog:panic       -> [name sys.unix.binlog.op.panic]
@binlog:timestamp   -> [name sys.unix.binlog.op.timestamp]
@binlog:unknown     -> [name sys.unix.binlog.unknown_class]
```

