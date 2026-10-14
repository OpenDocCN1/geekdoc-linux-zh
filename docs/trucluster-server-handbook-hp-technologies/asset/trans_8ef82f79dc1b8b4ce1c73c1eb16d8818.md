

你可以在指定目录的每个文件中使用以下命令查看所有过滤器：

```
# evf -d /usr/share/svm/filters
```

如果你只想查看几个文件，请用空格分隔它们。

```
# evf syslog binlog
```

evf 命令也接受标准 shell 通配符作为文件规范，前提是该文件规范用双引号 (" ) 括起来。以下示例将在 EVF_DIR_PATH 中搜索所有以 "log" 结尾的过滤器文件，所有以 "c" 开头后跟 "l" 或 "a" 再后跟 "u" 或 "a" 的过滤器文件，以及任意四个字母的过滤器文件。

```
# export EVF_DIR_PATH="/var/svm/adm/filters /var/share/svm/filters"
# evf -v *"log" *"c[la][ua]" ?????"
```

有关 evf 命令的更多信息，请参阅 evf.tar.gz 工具包中包含的 evf(1) 参考页。

## 8.7.11 如何查看过滤器文件中过滤器的格式？

如果您正在使用过滤器文件中的过滤器，并且想查看它实际过滤的内容，您可以查看过滤器文件（如果您知道其位置），或者您可以要求 evmshow 为您显示。

```
# evmshow -f @binlog:scsi -F
( { name sys.unix.binlog.hw.scsi } )
```

## 8.7.12 如何检查我创建的模板的语法？

如果您是管理员，可以使用 "evmreload -n" 命令。

```
# evmreload -n
```

如果您是用户，可以使用 evmpost。

```
# cat New_Events.evt | evmpost -r -M | evmshow -D
```

## 8.7.13 如何对事件进行排序？

由于事件可能来自各种通道，因此显示的顺序并不总是您期望看到的顺序。此外，您可能希望按不同的数据项对事件进行排序。evmsort 命令就是为此任务而设计的。

### NOTE:

从 Tru64 UNIX 版本 5.1 开始，evmget 命令在使用 "-A" 开关时会自动调用 "evmsort -A" 命令。

要对事件进行排序，请使用 "-s" 开关，后跟 "Sort-Spec"。 "Sort-Spec" 定义为 EVM 数据类型的冒号 (:) 分隔字符串。排序顺序是通过在 "Sort Spec" 中的 EVM 数据类型后放置 "+" 或 "-" 来确定的（"+" 表示升序排序，而 "-" 表示降序排序）。如果您未指定排序顺序，则默认为升序。

例如：

```
@timestamp+:@name:@priority-
```

这会按时间戳（升序）对每个事件进行排序，然后按名称（升序），然后按优先级（降序）排序。

以下示例将产生相同的结果。

```
# evmget | evmsort -s "@timestamp+:@name:@priority-" | \
> evmshow -t "@timestamp [@priority] @name"
```

或：

```
# evmget | \
> evmsort -A -s "@timestamp+:@name:@priority-" -t "@timestamp [@priority] @name"
```

或：

```
# evmget -A -s "@timestamp+:@name:@priority-" -t "@timestamp [@priority] @name"
```

返回：

```
27-Mar-2001 02:00:01 [200] sys.unix.evm.chmgr.cleanup_done
27-Mar-2001 02:00:39 [500] sys.unix.syslog.mail
28-Mar-2001 07:37:41 [200] sys.unix.sysman.station.update_object.HOST.elroy
28-Mar-2001 07:37:43 [300] sys.unix.hv.dev_base_name_changed.tape._hwd1.123
28-Mar-2001 07:37:43 [300] sys.unix.hv.dev_base_name_changed.tape._hwd1.124
29-Mar-2001 18:02:41 [200] sys.unix.evm.nark
29-Mar-2001 18:15:41 [500] sys.unix.syslog.mail
29-Mar-2001 18:17:44 [200] sys.unix.binlog.op.timestamp
```

如果您发现自己经常使用相同的格式，您可能希望在 EVM_SORT_SPEC 环境变量中定义排序顺序。如果例如 EVM_SHOW_TEMPLATE 和 EVM_SORT_SPEC 都已定义，那么您的 evmget 命令可以简化为：

```
# export EVM_SHOW_TEMPLATE="@timestamp [@priority] @name"
# export EVM_SORT_SPEC="@timestamp+@name+@priority"
# evmget -A
```

## 8.7.14 如何找到有关我检索到的事件的更多信息？

evmshow 命令有三个选项可以返回有关事件的附加信息（如果可用）：

- "-d" 从通道的 "fn_details" 例程返回事件的详细信息。
- "-x" 从通道的 "fn_explain" 例程返回事件的解释。
- "-D" 返回事件完整内容的格式化转储。

假设您从系统中检索了一系列事件。其中一个看起来很有趣，您决定想要更多信息。以下是使用每个开关的示例：

```
# evmget -x '{id = 4817}' | evmshow
29-Mar-2001 12:44:36 [200] sys.unix.syslog.auth
```

```
# evmget -x '{id = 4817}' | evmshow -x

Syslog authorization events are posted by Security Integration
Architecture (SIA) components to report actions such as granting of
superuser privileges to a user through the "su" command, or refusal
to grant access.

Authorization events should be monitored by the System
Administrator.
```

