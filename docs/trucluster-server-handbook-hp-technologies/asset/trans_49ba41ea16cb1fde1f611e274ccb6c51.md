

例如：

```
[name *.evm] AND [prio <= 500] AND NOT [before 2001:03:24:00:00:00]
```

返回所有在 2001 年 3 月 24 日之前优先级小于或等于 500 的 "evm" 事件。

为了确保复杂过滤器的正确顺序，您也可以使用括号 "(" 和 ")" 将过滤器包含在内。

```
([name *.evm] | [name ?.??.?]) & [age <= 2d]
```

返回所有 "evm" 事件或包含三个组件且年龄小于或等于两天的任何事件。

要使用过滤器，您可以在 evmget、evmwatch、evmshow(1) 或 evmsort(1) 命令上使用 "-f" 开关。例如：

```
# evmget -f "([name *.evm] | [name ?.??.?]) & [age <= 2d]"
```

有关更多信息，请参阅 EvmFilter(5) 参考页。

## 8.5.2 事件过滤器文件

除了事件关键字之外，还有一种方法可以创建复杂过滤器并将其存储以供重复使用（有点像环境变量）。这些可重复使用的过滤器可以存储在过滤器文件中。

Tru64 UNIX 和 TruCluster Server 包含多个过滤器文件。这些过滤器文件位于 /usr/share/evm/filters 中。事件过滤器文件的扩展名为 ".evf"。表 8-5 显示了过滤器文件目录及其搜索顺序。

要覆盖文件搜索顺序，您可以定义 EVM_FILTERDIR 环境变量。

### 事件过滤器文件目录

| 目录 | 搜索顺序 * | 描述 |
|---|---|---|
| 当前工作目录 | 1 | |
| $HOME/.sysman/evmfilters | 2 | 用户定义的过滤器文件应放置在此目录中。 |
| /var/evm/adm/filters | 3 | 站点特定的过滤器文件应放置在此目录中。 |
| /usr/share/evm/filters | 4 | Tru64 UNIX 和 TruCluster Server 提供的过滤器文件位于此目录中。 |
| * - 可以通过 EVM_FILTERDIR 环境变量覆盖 |

表 8-5：EVM 过滤器文件目录

事件过滤器文件具有以下语法：

```
filter {
  name        filter_name
  value       filter_value
  include     filter_element
  exclude     filter_element
  title       filter_title
}
```

filter_name 是您的过滤器的名称。filter_value 是一个关键字过滤器字符串。用于 "include"（逻辑 OR）和 "exclude"（逻辑 AND NOT）属性的 filter_element 是关键字过滤器字符串，您可以使用它来进一步细化您的过滤器。最后，filter_title 属性是对过滤器的描述。例如：

```
filter {
  name  'scsi'
  value "[name @SYS_VP8.binlog.hw.scsi]"
  title "Binlog SCSI events"
}
```

此过滤器来自位于 /usr/share/evm/filters 目录中的 binlog.evf 文件。要使用此过滤器，您将使用以下语法："@filter_file:filter_name"。要使用 binlog 过滤器文件中的 scsi 过滤器，请使用："@binlog:scsi"。请注意，此过滤器不包含 "include" 或 "exclude" 属性。每个过滤器定义可以有任意数量的 "include" 或 "exclude" 属性。

```
filter
{
  name      net
  value     "[name @SYS_VP8.hw.net]*"
  include   "[name @SYS_VP8.clu.clua]*"
  exclude   "[prio < 200]*"
  exclude   "[age > 1w]*"
}
```

这是一个示例，定义了一个名为 "net" 的过滤器，它将检索名称匹配 sys.unix.hw.net 或 sys.unix.clu.clua 的事件，只要事件的优先级大于 200 并且事件发生时间不超过一周。

换句话说，您可以创建一个过滤器文件并使用此命令：

```
$ evmget -A -f @myfilterfile:net
```

或输入此命令：

```text
# evmget -A -f "[name *.hw.net] | [name *.clu.clua] & [prio < 200] & [age > 1w]"
```

# NOTE:

@SYS_VP@ 值是一个宏，定义了“厂商”和“产品名称”。该宏解析为什么？

```text
# evminfo -vp
SYS.unix
```

您应该使用此值而不是使用实际值。这将完成两项任务：

- 1. 它使您的过滤器文件具有可移植性。
- 2. 它给予厂商更改其产品名称的自由，而无需您做更多工作。

有关事件过滤器文件的更多信息，请参阅 `evmfilterfile(5)` 参考页。

## 8.6 其他 EVM 主题

### 8.6.1 EVM 安全

`/etc/evm.auth` 文件定义了哪些用户和/或组有权发布、订阅（监视）或检索特定事件。`evm.auth` 文件包含两种类型的条目：

- `event_rights`
- 

此条目定义了特定事件类的权限。每个 `event_rights` 条目包含三个字段：

```text
event_rights {
              class  event_class
              post   rights_list
              access rights_list
              }
```

class 字段包含事件类（例如 @SYS_VP@.evm.msg.admin）。事件必须具有基本模板。有关更多信息，请参阅第 8.4 节。

