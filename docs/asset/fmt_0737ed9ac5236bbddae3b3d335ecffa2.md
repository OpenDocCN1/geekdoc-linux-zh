
```
# evmget -A -f "[name *.hw]" AND [prio > 400]" -t "@timestamp [priority] @name @@"
22-Mar-2001 09:22:56 [700] sys.unix.binlog.hw.correctable_rpt_switch Correctable
error reporting state changed
22-Mar-2001 09:30:16 [700] sys.unix.binlog.hw.correctable_rpt_switch Correctable
error reporting state changed
```

### 8.7.4 如何查看配置了哪些通道？

```
# evminfo -lc
syslog
binlog
mislog
evmlog
```

### 8.7.5 如何从特定通道获取事件？

你可以使用 `evmget` 的 `"-C"` 标志将搜索范围限制到特定通道。这是在 Tru64 UNIX 5.1 版本添加到 EVM 的。

```
# evmget -A -C binlog -f "[age < 1d]" -t @timestamp @name @@
28-Mar-2001 07:36:13 sys.unix.binlog.hw.correctable_rpt_switch Correctable
error reporting state changed
22-Mar-2001 09:22:56 [700] sys.unix.binlog.hw.correctable_rpt_switch Correctable
error reporting state changed
22-Mar-2001 09:30:16 [700] sys.unix.binlog.hw.correctable_rpt_switch Correctable
error reporting state changed
```

从 V5.1A 开始，换行符 (`\n`) 和制表符 (`\t`) 字符可提高事件输出的可读性。例如，你可以使用 `"\n"` 在事件输出中插入换行。

```
# evmget -A -f "[age < 1d]"
-t "\n@timestamp -event_id [priority]\n@name@" | more
26-Sep-2002 03:43:59 - 344680 [200]
sys.unix.clu.drd.server_leave.._hwid.52
DRD: Removed (unmapped) DRD server molari
```

在过滤关键字旁使用 `""` 字符允许你设置最小字段宽度。例如，要设置 `cluster_event` 字段的最小字段宽度，可以使用以下命令。

```
# evmget -A -f "[age < 1d]"
-t "@cluster_event%5 @name" | more
True - sys.unix.hw.net.alert
False - sys.unix.evm.logger.log_closed
False - sys.unix.evm.logger.log_started
False - sys.unix.evm.mark
False - sys.unix.binlog.chan.binlog_size
True - sys.unix.clu.drd.server_leave.._hwid.52
False - sys.unix.binlog.hwid.scsi
True - sys.unix.drd.server_add.._hwid.52
True - sys.unix.clu.drd.new_accessnode.._hwid.52
True - sys.unix.clu.drd.new_accessnode.._hwid.52
```

## 8.7.10 如何找到哪些可用的过滤器？

过滤关键字定义在 `EvmFilters (5)` 参考页面中。你可以在位于 `/usr/share/evm/filters`（系统级）和 `/var/evm/adm/filters`（站点定义）目录下的过滤文件中找到这些过滤器。

```
# ls /var/evm/adm/filters /usr/share/evm/filters
/usr/share/evm/filters:
binlog.evf evm.evf syslog.evf
/var/evm/adm/filters:
<no output>
```

TruCluster Handbook 网站（URL 参见附录 B）包含一个名为 `evf (1)` 的 Korn Shell 脚本，用于查找过滤文件中哪些过滤器。

## `evf [-v] [-d FilterFileDir] [file1 file2...filen]`

在不使用 `"-d"` 关或 `EVF_DIR_PATH` 环境变量的情况下，`evf` 脚本将使用当前工作目录 `/var/evm/adm/filters` 和 `/usr/share/evm/filters` 作为默认搜索路径。

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

在此示例中，使用 `"-d"` 选项仅搜索 `/usr/share/evm/filters` 目录；`"-v"` 选项通过执行 `"evmshow -f filter_exp -P"` 显示过滤器的详情。

```
# evf -v -d /usr/share/evm/filters binlog
/usr/share/evm/filters
binlog.evf
@binlog:binlog      -> [name sys.unix.binlog.hw.scsi]
@binlog:scsi        -> [name sys.unix.binlog.sw.lsm]
@binlog:lsm         -> [name sys.unix.binlog.info]
@binlog:info        -> [name sys.unix.binlog.info.ascii_msg]
@binlog:msg         -> [name sys.unix.binlog.op.startup]
@binlog:startup     -> [name sys.unix.binlog.op.shutdown]
@binlog:shutdown    -> [name sys.unix.binlog.op.panic]
@binlog:panic       -> [name sys.unix.binlog.op.timestamp]
@binlog:timestamp   -> [name sys.unix.binlog.unknown_class]
@binlog:unknown     
```

第 8 章

你可以使用以下命令查看指定目录中每个文件中所有的过滤器：

```
# evf -d /usr/share/evm/filters
```

如果你只想看几个文件，请用空格将它们隔开。

```
# evf syslog binlog
```

`evf` 命令还接受标准 shell 通配符作为文件规范，前提是文件规范包含在双引号（`""`）中。以下示例将在 `EVF_DIR_PATH` 中搜索所有以 `"log"` 结尾的过滤器文件、所有以 `"c"` 开头并后跟 `"l"` 或 `"a"` 且其后跟 `"u"` 或 `"a"` 的过滤器文件，以及任何四个字母的过滤器。

```bash
# export EVF_DIR_PATH="/var/evm/adm/filters /usr/share/evm/filters"
# evf -v "log" "clua*"
```

有关 `evf` 命令的更多信息，请参阅 `evf.tar.gz` 中包含的 `evf(1)` 参考页面。

## 8.7.11 如何查看过滤文件中过滤器的格式？

如果你正在使用过滤文件中的过滤器并想查看它实际过滤了什么，你可以查看过滤文件（如果你知道它的位置），或者你可以要求 `evmshow` 为你显示。

```
# evmshow -f @binlog:scsi sys.unix.binlog.hw.scsi
```

## 8.7.12 如何检查模板的语法？

如果你是管理员，可以使用 `evmreload -n`。

```
# evmreload -n
```

如果你是用户，可以使用 `evmget`。

## 8.7.13 我可以排序事件吗？
