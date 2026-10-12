
在此之后是以下行：

`ErrorLog logs/error_log`

`ErrorLog` 指令定义 `httpd` 错误存储的位置。你可以使用完整路径或相对路径，如前面的代码片段所示。相对路径以 `ServerRoot` 设置的位置为起点。

### LogLevel

继续日志相关指令的是以下内容：

`LogLevel warn`

此指令根据第 9 章“In Depth”部分中“什么日志”一节中讨论的标准 `syslog` 级别设置记录多少信息。

### LogFormat

现在我们来到更多的日志设置。在此之前的部分设置了数据记录到的文件以及记录的数据类型，而这一部分利用 `LogFormat` 指令指定要记录的具体项目及其使用的格式：

`LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"" combined`

`LogFormat "%h %l %u %t \"%r\" %>s %b" common`

`LogFormat "%{Referer}i -> %U" referer`

`LogFormat "%{User-agent}i" agent`

为了理解上述行，你需要了解 `LogFormat` 使用的格式：

`LogFormat *format* *name*`

`LogFormat` 语句中的 `*format*` 部分有许多潜在参数，列在表 13.11 中。

前面 `LogFormat` 语句中的 `*name*` 项指的是你希望此数据进入的自定义日志的名称。如果你将 `CustomLog` 指令保留为以下格式，则使用 `LogFormat` 指令设置为以自定义格式记录的任何内容都会发送到单个日志文件：

```
CustomLog logs/access_log common
#CustomLog logs/referer_log referer
#CustomLog logs/agent_log agent
#CustomLog logs/access_log combined
```

> **注意：** 输入 `man strftime` 以获取可供你使用的长列表时间格式化选项。

#### 表 13.11 LogFormat 指令中可用的输出语句。

| 类型 | 结果 |
| :--- | :--- |
| `%a` | 标识发起请求的 `IP` 地址。 |
| `%A` | 标识请求到达的 `IP` 地址。 |
| `%B` | 标识发送的字节数，不包括 `HTTP` 头。 |
| `%{argument}e` | 标识列出的环境变量的内容。 |
| `%f` | 标识文件名。 |
| `%h` | 标识请求来源主机的名称。 |
| `%H` | 标识请求中使用的协议。 |
| `%I{argument}i` | 标识发送到服务器的指定头行的内容。 |
| `%l` | 标识由 `identd` 提供的远程登录名称（如果提供）。 |
| `%m` | 标识使用的请求方法。 |
| `%I{argument}n` | 标识来自其他模块的指定备注的内容。 |
| `%I{argument}o` | 标识服务器回复中发送的指定头行的内容。 |
| `%p` | 标识响应请求的服务器使用的规范端口。 |
| `%P` | 标识响应请求的子进程的 `PID`。 |
| `%r` | 标识请求的第一行。 |
| `%s` | 标识原始请求的状态（在内部重定向之后）。 |
| `%t` | 指定 `strftime` 格式的时间。 |
| `%T{format}t` | 指定以列出的格式显示的时间。有关更多信息，请参阅“立即解决方案”部分的“自定义你的日志”。 |
| `%T` | 指定处理请求花费了多少秒。 |
| `%u` | 标识远程用户。 |
| `%U` | 标识请求的 `URL`。 |
| `%v` | 标识处理请求的服务器使用的规范服务器名称。 |
| `%V` | 标识由 `UseCanonicalName` 设置的服务器名称。 |

### ServerSignature

在日志部分之后是：

```
ServerSignature On
```

`ServerSignature` 指令告诉 `Apache` 在其提供的所有文件底部放置页脚。

### Alias

接下来是：

```
Alias /doc /usr/doc
```

`Alias` 命令允许你在 `Web` 层级中创建一个别名，指向不在该层级中的文件。在此情况下，当用户尝试访问 `http://www.domain.extension/doc` 时，他们会看到 `/usr/doc` 的内容。

> **注意：** `Alias` 指令位置必须以斜杠开头，且任何目录必须以斜结尾。

### 用于图标的目录

现在，告诉 `Apache` 如何处理其基础图标层级：

```
<Directory "/home/httpd/icons">   
Options Indexes MultiViews
AllowOverride None
Order allow,deny
Allow from all
</Directory>
```

这里没有引入任何新内容。

### ScriptAlias

接下来是 `ScriptAlias` 指令：

```
ScriptAlias /cgi-bin/ /home/httpd/cgi-bin/
```

你以与 `Alias` 指令相同的格式使用它。这两个指令的区别在于，`ScriptAlias` 允许你指定存储特定类型脚本的位置。在此情况下，该指令告诉 `Apache` 去哪里查找其 `CGI` 脚本。

### 用于 CGI 的目录

以下是默认访问文件的下一部分：

```
<Directory /home/httpd/cgi-bin>
AllowOverride None
Options ExecCGI
</Directory>
```

大多数 `Web` 管理员希望控制在其系统上运行哪些 `CGI`。此 `<Directory>` 部分定义了中心 `CGI` 目录基础及其内部允许的内容。在此目录中应用的两条指令应该已经看起来很熟悉了。有关 `AllowOverride` 的更多信息见表 13.4，有关 `Options` 的更多信息见表 13.3，两者均出现在本章的前面部分。

### Redirect

虽然下一个部分作为说明的一部分被注释掉，但它很重要，所以我将其包含在此处：

```
# Format: Redirect fakename url
```

`Redirect` 命令允许你自动告知客户端页面已移动，并使该客户端请求新的 `URL`。我觉得被注释掉的语句令人困惑，所以这是我自己的版本：

```
Redirect *original_url* *new_url*
```

### IndexOptions

现在文件设置 `Apache` 如何处理目录和文件索引：

```
IndexOptions FancyIndexing
```

`IndexOptions` 指令有许多可用选项。这些选项概述在表 13.12 中。

#### 表 13.12 httpd.conf 中 IndexOptions 指令可用的值。

| 选项 | 目的 | 示例 |
| :--- | :--- | :--- |
| `DescriptionWidth` | 指定文件描述列的宽度（以字符计）。要自动调整此列的大小，请使用星号。 | `DescriptionWidth`=`*` |
| `FancyIndexing` | 指定启用索引处理。 | `FancyIndexing` |
| `FoldersFirst` | 指定在索引列表顶部列出目录，然后列出文件。 | `FoldersFirst` |
| `IconHeight` | 指定文件图标的高度（以像素计）。 | `IconHeight`=90 |
| `IconsAreLinks` | 指定用户可以单击类型图标以及文件名来访问文件。必须激活 `FancyIndexing`。 | `IconsAreLinks` |
| `IconWidth` | 指定文件图标的宽度（以像素计）。 | `IconWidth`=100 |
| `NameWidth` | 指定文件名列的宽度（以字节计）。要自动调整此列的大小，请使用星号。 | `NameWidth`=`*` |

## 表 13.12 httpd.conf 中 IndexOptions 指令可用的值（续表）。

| 选项 | 用途 | 示例 |
| :--- | :--- | :--- |
| `ScanHTMLTitles` | 指定从列出的任何 `HTML` 文件中提取 `<TITLE>` 标签的内容，并将其用作文件描述符。必须激活 `FancyIndexing`。 | `ScanHTMLTitles` |
| `SuppressColumnSorting` | 指定不使索引列表中的列头可点击。这将导致无法点击列头以反向排序内容。必须激活 `FancyIndexing`。 | `SuppressColumnSorting` |
