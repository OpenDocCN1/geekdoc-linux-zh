

# Linux 系统管理：入门指南

| 属性名称 (propname) | 描述 |
|---|---|
| msg | 消息的 MSG 部分；实际的日志消息 |
| rawmsg | 与从套接字接收时完全相同的消息 |
| HOSTNAME | 消息中的主机名 |
| FROMHOST | 接收消息的系统主机名（不一定是原始发送者） |
| syslogtag | 消息中的 TAG |
| PRI-text | 文本格式的消息中的 PRI 部分 |
| syslogfacility | 数字格式的消息中的设施 (facility) |
| syslogfacility-text | 文本形式的消息中的设施 (facility) |
| syslogseverity | 数字格式的消息中的严重程度 (severity) |
| syslogseverity-text | 文本格式的消息中的严重程度 (severity) |
| timereported | 消息的时间戳 |
| MSGID | MSGID 字段的内容 |

表 8-7 rsyslog 消息属性名称

-   `/etc/rsyslog.conf` 文件中任何包含美元符号 ($) 的条目都是指令。
日志属性指的是任何日志消息中定义良好的字段。表 8-7 显示了常用属性示例。
百分比符号 (%) 用于编码日志消息属性。可以通过使用属性替换来修改属性。
任何以井号 (#) 开头的条目都是注释，并会被忽略。空行也会被忽略。

## rsyslog 模板 (Templates)
如所述，rsyslog 依赖于模板的使用，模板定义了日志消息的格式。模板的使用使得 rsyslog 能够生成与旧版传统的 syslog 生成的格式相似的日志文件。支持 syslog 日志格式的模板被硬编码在 rsyslog 中，并被默认使用。
这里有一个支持使用 rsyslog 消息格式的示例模板：

```
$template TraditionalFormat,"%timegenerated% %HOSTNAME% %syslogtag% %msg\n",<options>
```

# 第 8 章 核心系统服务

此示例模板的各个字段将在下面的列表和表 8-7 中进行解释。

-   **$template** 该指令意味着该行是一个模板定义。
-   **TraditionalFormat** 这是一个描述性名称。
-   **%timegenerated%** 这指定了 `timegenerated` 属性。
-   **%HOSTNAME%** 这指定了 `HOSTNAME` 属性。
-   **%syslogtag%** 这指定了 `syslogtag` 属性。
-   **%msg%** 这指定了 `msg` 属性。
-   **\n** 反斜杠是转义字符。在这里，`\n` 表示换行。
-   **<options>** 此条目可选可选。它指定了影响整个模板的选项。

# rsyslog 规则 (Rules)

可以在 rsyslog.config 中使用不同的过滤标准创建规则。当前可用的过滤标准见表 8-8。

| 过滤类型 | 描述 | 语法 | 示例 |
|---|---|---|---|
| 基于设施和优先级 | 使用传统的设施和优先级选择器 | facility.priority action_field | mail.info /var/log/messages |
| 基于属性 | 允许根据 rsyslog 定义的属性（如 HOSTNAME、syslog、programname）进行过滤 | :property,[] compare operation,"value" | :hostname, isequal,"fedora-server" |
| 基于表达式 | 使用 rsyslog 内置的脚本语言 RainerScript 构建过滤器 | if EXPRESSION then ACTION else ACTION | action(type="omfile" file="/var/log.log") else { if $msg contains 'look' then { action(type="omfile" file="/var/log/nolook.log") } |

**表 8-8 rsyslog 过滤标准**

# Linux 系统管理：入门指南

让我们深入研究一下传统的基于设施和优先级（Facility and Priority-based）的过滤类型规则。rsyslog.conf 文件中的此类过滤规则被分为一个选择器字段（facility:priority）、一个操作（action，字段或目标）以及一个可选的模板名称。在最后一个分号后指定模板名称将把相应的操作分配给该模板。每当缺少模板名称时，将使用硬编码的模板。当然，确保在引用模板之前已经定义了所需的模板是非常重要的。

以下是文件中每一行的格式：

```
selector_field action_field ; <optional_template_name>
```

这里有一个示例：

```
mail.info /var/log/messages; RSYLOG_TraditionalFormat
```

选择器字段 (Selector Field)：选择器字段指定了设施和优先级的组合。这里有一个选择器条目示例：

```
mail.info
```

在这里，mail 是设施 (facility)，info 是优先级 (priority)。

操作字段 (Action Field)：规则的操作描述了对消息要执行的操作。这种操作可以从简单的（如将日志写入文件）到稍微复杂的操作（如写入数据库表或转发到另一个主机）。这里有一个操作示例：

```
/var/log/messages
```

此操作描述了对消息要执行的操作。这种操作可以涵盖从简单的……：

| 操作字段 | 描述 |
|---|---|
| 常规文件 (例如 /var/log/messages) | 此操作将日志写入文件。其他操作值在表 8-9 中描述。 |
| 命名管道 (例如 /tmp/fifo) | 命名管道。rsyslog 允许在管道中运行。这种操作类型 必须以管道管道结尾的。 |

8-9 操作字段描述 (Action Field Descriptions)

| 操作字段 | 描述 |
|---|---|
| 远程主机 (@) | 远程主机。使用单个 @ 符号表示通过 UDP 传输。使用双符号 @@ 表示通过 TCP 传输。 |
| 丢弃 (-) | 丢弃。此操作意味着将丢弃日志消息。 |
| 用户列表 (*) | 用户列表。使用星号 * 表示发送到所有登录用户。 |
| 数据库 (>host,dbname,user) | 数据库。指定的 > 符号必须遵循严格顺序：> 之后是数据库主机 (host)，逗号，数据库名 (dbname)，再次是数据库用户 (user)，然后是数据库密码 (password)。可选的模板 (demplate) 可以在分号后指定。 |

