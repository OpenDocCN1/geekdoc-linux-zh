
此此命令以默认方式显示日志文件的报告，即：它获取每个事件的数据格式，使用所引用的任何变量的值对其进行扩展，并显示出来。变量的引用通过美元符号（`$`）识别。因此，`my_events`文件包含一个格式化数据项为`AdvFS: AdvFS domain sdomain is full`的事件，该事件还包含一个值为`root_domain`的变量`domain`，相应的输出行是：

```
AdvFS: AdvFS domain root_domain is full
```

这些信息告诉您发生了什么，但没有告诉您何时发生的，或者事件的重要性。您可以使用`-t`选项指定显示模板（show-template），修改`evmshow`命令的输出以包含事件中的任何数据项，包括其时间戳和优先级。显示-模板是一个文本字符串，指示您想要为事件显示哪些数据项，以及您希望如何显示它们。

以下示例说明了如何使用显示-模板显示带有时间戳、优先级和格式化事件消息的事件。在显示-模板中，要显示的项名称均由符号`@`引导。两个符号`@@`表示事件的格式项应该被扩展并显示。第二行显示了域 full 的输出。在输出中，事件的优先级被方括号括起来，消息文本之间有两个空格，完全按照显示-模板中指定的格式。

```bash
# cat my_events | evmshow --timestamp [priority] @@ | more
22-Jun-2020 11:22:27 [600] AdvFS: AdvFS domain root_domain is full
```

您可以设置自己的显示-模板，以任何格式显示对您重要的项。所有数据项列表请参阅`EvmMEvent(5)`。在确定了偏好的样式后，您可以在环境变量`EVM_SHOW_TEMPLATE`中创建默认显示-模板，并在命令行中使用更少的按键。以下 Kernel shell (`ksh`) 命令与上例中的命令等效：

```bash
# export EVM_SHOW_TEMPLATE="timestamp [priority] @@"
# cat my_events | evmshow | more
```

如果您想获取有关事件的更多信息，可以使用带有`-d`选项的`evmshow`命令请求详细显示，包括内容的和转储。以下示例显示了 AdvFS domain full 的详细数组：

```bash
# cat my_events | evmshow -d |
EVM event name: sys.unix.fs.advfs.domain.full
```

此事件由 AdvFS 文件系统发布，用于通知 AdvFS 域已满。没有更多可用空间进行写入。

==============================

格式化消息：

AdvFS: AdvFS domain root_domain is full

事件数据项：

| 事件名称 | sys.unix.fs.advfs.fdmn.full |

| :--- | :--- |

| 集群事件 | True |

| 优先级 | 600 |

| PID | |

| 时间戳 | 22-Jun-2020 11:22:27 |

| 主机 IP 地址 | 0.0.0.0 |

| 主机名称 | example.com |

| 用户名称 | root |

| 格式 | AdvFS: AdvFS domain is full |

| 引用 | |

变量项：

`domain` (`string`)

第 13.3.1 节了解如何显示事件。

此事件由 AdvFS 文件系统发布，用于通知 AdvFS 域已满。没有更多可用空间进行写入。

大多数系统会产生大量事件，其中许多报告正常运行。使用事件过滤器将显示限制为您感兴趣的事件集。

## 13.3.2 引入事件过滤器

本节介绍事件过滤器并将其关联 `evmshow` 命令。过滤在后面的章节中被更广泛使用，那些章节描述了事件检索和监控技术。

Event Manager 过滤器是一个字符串，告诉 Event Manager 您想要检索哪些事件。例如，过滤器 `[priority > 600]` 选择优先级为 600 或更高的事件。过滤器可以非常简单，但过滤语言非常强大，通过一些练习，您可以轻松构建并存储过滤器表达式，精确定义您想要监控的事件集。过滤器被多个 Event Manager 命令、Event Manager 日志器以及系统守护进程和应用程序使用。

`evmshow`、`evmget` 和 `evmwatch` 支持 `-f` 选项，您可以使用它过滤字符串。您可以从 `my_events` 文件选择要显示的事件，如下所示：

```bash
# export EVMW_TEMPLATE="$timestamp [priority] %#"
# cat my_events | evmshow -f "priority > 600" | more
```

（上例介绍于第13.3.1节）。在此示例中，`-f` 选项过滤并选择了优先级为 600 或更高的事件。该命令读取文件中的所有事件，但仅返回匹配过滤器字符串的事件。

如果您知道想要检索的事件名称，可以在过滤器中指定它们，如下所示：

```bash
# cat my_events | evmshow -f "[name sys.unix.fs.advfs.fdmn full]" 
```

您可以在名称组件中使用通配符字符，如下：

- 星号 (`*`) 匹配零个或多个完整组件

- 问号 (`?`) 匹配恰好一个完整组件

例如，使用以下命令可以缩短之前的示例命令：

```bash
# cat my_events | evmshow -f 'name *.advfs.fdmn.full' | more
```

通配符星号 `*` 匹配 `sys.unix.fs` 组件。为了避免 shell 用文件名扩展通配符字符的可能，请使用单引号而不是双引号括起字符串。在 shell 命令中使用特殊字符时，这始终是一个明智的预防措施。

当你按名称进行过滤时，事件管理器（Event Manager）假设名称字符串末尾有一个通配符 `*`，即使命令中没有包含它。因此，你可能会收到比你指定的包含更多组件的事件。以下两个命令是等价的，但第一个命令中最后的通配符 (`*`) 是必要的：

```bash
# cat my_events | evmshow -f 'name *.advfs'
# cat events | evmshow -f 'name'
```

在运行 `evmshow` 命令时，可以通过将 `name` 指定为显示窗口（show-window）的项之一来按名称查找事件。

使用过滤语法通过 `AND`、`OR` 和 `NOT` 关键字将多个条件组合到单个过滤器中，并可以使用括号对条件分组。下面的过滤示例选择了所有名称包含 `advfs` 且优先级大于或等于 600 的事件：

```bash
# cat my_events | evmshow -f '(name *.advfs) and (priority >= 600)'
```

以下命令还选择了 binlog 中的事件，无论优先级如何。在下面的示例中，关键字 `priority` 缩写为 `pri`，`name` 缩写为 `na`。大多数过滤关键字可以描述为 EventFilter(5)。

```bash
# cat my_events | evmshow -f '(name *.advfs) and (pri >= 600) or [na *.binlog]'
```

本节中的示例说明了最常用的过滤关键字。当你熟悉了 `evmshow` 命令的过滤器以及后续章节描述的事件管理器命令后，可以使用更高级的过滤功能来创建和保存实用的过滤器，并增强你选择最感兴趣事件的能力。高级过滤技术见第 13.3.12 节，完整语法见 EventFilter(5)。

## 13.3.3 使用 evmget 获取事件

系统日志以许多不同的格式和不同的详细程度存储事件，这使得很难使用传统的系统实用程序生成所有事件的有序视图。你可以使用 `evmget` 命令通过从各种日志文件中检索每个事件来生成有序视图，如果它们尚未成格式，则将其转换为事件管理器事件，并返回单个事件管理器事件流。随后使用 `evmshow` 命令，你可以将事件管理器事件流转换为显示格式。

下面的命令管道使用 `evmget` 命令检索所有事件系统，并将它们传递给 `evmshow` 命令进行显示：

```bash
# evmget | evmshow -t @timestamp @priority @message | more
```

`evmget` 命令对事件管理器守护进程建立服务连接，该守护进程会启动 `get-server` 程序的新副本 `/usr/bin/evmgetsrv`。`get-server` 程序读取配置文件，并为通道配置文件 `/etc/evmchannel.conf` 中配置的每个通道运行 `get` 函数（通常是一个 shell 脚本）。该配置文件在第 13.2.2 节中描述。

`get` 函数执行以下操作：

- 读取日志文件

- 将事件转换为 EVM 格式
