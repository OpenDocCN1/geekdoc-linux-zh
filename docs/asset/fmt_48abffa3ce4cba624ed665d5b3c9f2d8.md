
图 8-1 显示了来自 curses 界面的事件查看器的屏幕截图，而图 8-2 显示了 CDE GUI。更多信息请参见 `evmviewer(8)` 参考页。

![](img/a0df85c2e542a8d6c913113908553aa4_204_0.png)

图 8-1：EVM curses 风格界面

![](img/a0df85c2e542a8d6c913113908553aa4_205_0.png)

图 8-2：EVM CDE GUI

# 8.3 EVM 优先级与 syslog 和 binlog 优先级

事件优先级显示在表 8-3 中。EVM 优先级范围为 0-700，其中 700 intended 为最高优先级，而 syslog 优先级范围为 7-0，其中 (0) 为最高。binlog 优先级范围仅有三个有效优先级，粒度远不如前者。

| Event Priorities |  |  |  |
|---|---|---|---|
| Name | EVM | syslog | binlog |
| process-to-process | 0 | — | — |
| debug | 1–99 | 7 | low (5) |
| information | 100–199 | 6 |  |
| notice | 200–299 | 5 |  |
| warning | 300–399 | 4 | high (3) |
| error | 400–499 | 3 |  |
| critical | 500–599 | 2 |  |
| alert | 600–699 | 1 | severe (1) |
| emergency | 700 | 0 |  |

表 8-3：事件优先级

EVM 优先级为零保留给不希望任何人查看的事件。这些低优先级事件可用于应用程序之间的通信，例如另一个进程发出的心跳事件以保持自身存活（正如您将在 NetRAIN 事件部分 [第 9 章，第 9.2.3 节] 中看到的，所有注册的事件优先级均为零）。默认情况下，优先级低于 200 的事件不会被 EVM 记录器记录。

`EvmEvent(5)` 参考页列出了 EVM 优先级及其预期用途。

# 8.4 事件模板

我们已经讨论了事件是什么以及事件如何处理，但没有讨论事件如何定义。为了发布事件，事件必须被定义。

随 Tru64 UNIX 和 TruCluster Server 提供的事件模板文件按事件类型将事件分组到模板文件中；例如，硬件网络事件位于 `hw.net.ev` 文件中，ADFS 文件系统事件位于 `fs.adfs.evt` 文件中。

模板文件具有以下格式：

```
event {

        name             event_name

        format           format_specifier

        priority         priority

        cluster_event    true | false

        i18n_catalog     i18n_cat

        i18n_set_id      i18n_set

        i18n_msgid       i18n_msg

        reference        reference_string

        var {

                name     variable_name

                type     variable_type

                value    variable_value

        }

}
```

- `name`

每个事件必须具有由至少三个组件组成的名字属性。组件由句点 (`.`) 分隔。例如：

`tcrhb.timeEvent.overdue`

- `format`

`format` 属性是事件的文本。例如：

“TCR Handbook: this book is overdue”

### priority

优先级是 0（零）到 700 之间的任意值。请参阅 `EvmEvent(5)` 参考页以了解优先级定义。

### cluster_event

`cluster_event` 属性用于定义事件的范围。如果 `cluster_event` 为 "true"，则如果该事件在集群中的任何成员上发生，集群中的每个成员都会看到它。如果 `cluster_event` 为 "false"，则只有生成该事件的成员才会看到该事件。正如前面的示例所示，`hw.evt` 模板文件中的所有事件默认 `cluster_event` 值为 "true"。

### i18n_catalog, i18n_set_id, i18n_msg_id

如果您使用消息目录，则 "i18n" 属性可用于索引事件文本的目录消息。更多信息请参阅 `evmtmpl(5)` 参考页。

### reference

这是一个文本字符串，将由事件通道的解释函数使用。该字符串的格式由事件通道定义。

### var

您还可以通过定义 "var" 块向事件传递变量。变量有三个属性：`name`、`type` 和 `value`。"`name`" 属性是变量的名称，"`type`" 属性可以是 `EvmEvent(5)` 参考页中定义的几种不同类型之一。类型 "`STRING`" 为默认值。"`value`" 属性是您希望变量具有的默认值。

下面是包含变量的虚构事件的模板：

```
event {

  name        tcrhb.timeEvent.overDue

  format      "TCR HB: this book is overdue. $dueDate is the due date."

  priority    400

  var         {name dueDate type STRING value "Today"}

}
```

将事件模板输入到文件中。

```
# cd /usr/share/evm/templates/local ; mkdir tcrhb ; cd tcrhb
```

```
# cat > tcrhb.evt
event {

    name        tcrhb.timeEvent.overDue

    format      "TCR HH: this book is overdue. $dueDate is the due date."

    priority    400

    var         {name dueDate type STRING value "Today"}

}
^D
```

设置所有者和权限。

```
# chown root tcrhb.evt
# chmod 540 tcrhb.evt
```

检查模板文件的语法错误。

```
# evmrload -n
```

告诉 EVM 关于新的模板。

```
# evmreload
```

发布新的事件。

```
# echo "event { name tcrhb.timeEvent.overDue }" | evmpost
```

检查事件是否已发布。

```
# evmget -A -f "[name tcrhb]*"
TCR Handbook: this book is overdue. Today is the due date.
```

再次发布事件。这次，传递一个值给 "`dueDate`" 变量。

```
# print "event
> { name tcrhb.timeEvent.overDue
>  var {name dueDate value "\${date}"} }" | evmpost
```

检索事件。这次你应该看到两个事件，因为这是我们第二次发布事件。

```
# evmget -A -f "[name tcrhb]*"
TCR Handbook: this book is overdue. Today is the due date.
TCR Handbook: this book is overdue. Mon Mar 26 05:34:29 EST 2001 is the due date.
```

最后，你可以通过将属性条目放在事件定义之外，来为模板文件中的所有事件定义默认属性值。事件定义内的属性将覆盖“全局”属性值。以下是 `hw.evt` 模板文件中的摘录，说明了这一点：

```
================ Hardware event defaults =================
cluster_event   true
priority         200
ref              cat:evexmp.cat:800
================ Hardware event templates =================
event {
    name        @SYS_VP0.hw.deregistered
    priority    400
```
