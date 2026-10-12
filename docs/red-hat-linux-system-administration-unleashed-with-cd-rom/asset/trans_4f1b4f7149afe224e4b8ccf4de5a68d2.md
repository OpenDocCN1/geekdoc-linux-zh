
DocumentRoot。如果访问您服务器的用户未指定任何文件名，则将访问默认文件名，通常是 index.html。

## ServerRoot
ServerRoot 指令用于指定存放服务器所有配置文件所在的目录。在 Red Hat Linux 下的默认值是 /etc/httpd。

两个您可能想要配置的其他重要指令是 User 和 Group 指令。User 指令指定服务器响应请求时使用的用户 ID，而 Group 指令用于指定服务器响应请求时使用的组 ID。User 和 Group 指令只有在 Apache 由 root 启动时才会生效。以下是同时使用 User 和 Group 的示例：

```
User nobody
Group nobody
```

您可以在 User 和 Group 指令中指定任何有效用户或组；然而，出于安全目的，通常使用 nobody。

使用这些基本指令，您可以启动并运行一个基本的 Apache 服务器。事实上，很多时候在您安装并启动 Apache 后它就能立即工作。然而，让 Apache 按您想要的方式运行的关键在于正确配置它。我们所介绍的指令只是搭建一个可工作的 Apache 服务器的最低要求。

## 设置基于目录的指令
Apache 配置很大程度上涉及为特定目录设置访问控制指令，因此就有了 Directory 指令来完成此任务。使用 Directory 指令，您可以设置一组仅适用于特定目录的指令。通过 Directory 指令应用的任何指令也适用于父目录的任何子目录。

Directory 指令的语法如下：

```
<Directory dir_name>
Directive
Directive
...
</Directory>
```

指定 dir_name 时，您可以提供目录的完整路径，也可以使用通配符字符串。通配符字符如下：

- ? — 匹配单个字符
- * — 匹配任意数量的字符
- [...] — 匹配方括号内包含的任意一个字符

使用通配符时，请务必记住通配符不会匹配 / 字符。

在 Directory 指令内部，您可以使用多种不同的指令。其中最常见的是 Options 指令。Options 指令用于指定在指定目录中应启用哪些服务器选项，其语法如下：

```
Options [+|-]option [+|-]option ...
```

您可以在 Options 指令后指定任意数量的选项，加号 (+) 将启用指定的选项，而减号 (-) 将禁用指定的选项。可用的选项有多种，包括以下内容：

- All — 涵盖除 MultiViews 之外的所有选项。
- ExecCGI — 允许执行 CGI 脚本。
- FollowSymLinks — 如果服务器遇到符号链接，它将跟随该链接。
- Includes — 允许使用服务器端包含。
- IncludesNOEXEC — 允许使用服务器端包含，但排除 #exec 和 #include 命令。
- Indexes — 如果客户端请求某个目录时该目录不包含 index.html 文件，则会向客户端输出目录列表。
- MultiViews — 允许使用内容协商的 MultiViews。
- SymLinksIfOwnerMatch — 当服务器遇到符号链接时，只有当链接的目标由与链接相同的用户 ID 拥有时才会跟随它。

如果未指定任何选项，则默认选项 All 将被启用。

另一个常用于 Directory 指令中的指令是 AllowOverride 指令，它允许您指定在目录内部可以从服务器默认值覆盖哪些指令。当您希望在服务器上的各个目录内以不同方式配置特定指令时，这很有用。

## 设置基于文件的指令
您还可以根据文件名定义访问控制指令。这与 Directory 指令非常相似，称为 Files 指令。正如您所知，Directory 指令允许您根据目录以不同的方式设置指令；Files 指令的工作方式相同，只是基于文件而不是目录。事实上，您甚至可以将 Files 指令与 Directory 指令嵌套，以进一步限制指令的作用范围。Files 指令的语法如下：

```
<Files filename>
Directive
Directive
...
</Files>
```

filename 参数应由文件名组成，不过它也可以包含通配符。正则表达式也允许使用。请记住，与 Directory 指令不同，Files 指令不能在 .htaccess 文件中使用。

在 Files 指令内部，您可能也会使用 Options 和 AllowOverride 指令。

## 条件指令
您可以拥有仅基于条件语句才适用的指令。这称为条件指令，它允许您设置仅在某个参数为真时才会设置的指令。为此，您可以使用 IfDefine 指令。测试会传递给 IfDefine 指令，其内容只有在测试返回 true 时才会被处理。语法如下：

```
<IfDefine [!]parameter_name>
Directive
Directive
...
</IfDefine>
```

测试由以下两种形式之一组成：

- parameter_name
- !parameter_name

对于第一种形式，如果指定的 parameter_name 已定义，则 <IfDefine>...</IfDefine> 指令的内容将被处理。第二种形式则相反：只有在指定的 parameter_name 未定义时内容才会被处理。

parameter_names 在 httpd 启动时通过命令行使用 -D 选项传递来定义。

## 设置日志
运行 Web 服务器的一个关键部分是对其发生的活动进行日志记录。Apache 允许您对日志记录方式进行很大程度的控制，从 LogLevel 指令开始。

LogLevel 指令用于指定您希望 Apache 执行的日志记录量。Apache 可以运行多种不同的日志级别。此指令允许您精确指定希望 Apache 执行的日志记录量。以下是可用的日志级别：

- emerg — 仅记录紧急情况。
- crit — 仅记录严重问题。
- alert — 任何警报条件都会被记录。
- error — 记录所有错误——默认级别。
- warn — 记录所有错误和警告。
- notice — 任何重要情况都会被记录。
- info — 记录所有服务器信息。
- debug — 记录调试消息。

指定日志级别时，请记住它也会打开所有次要重要级别的日志记录。因此，将日志级别指定为 warn 也会打开 notice、info 和 debug。

您还需要指定错误将被记录到的文件名。这是通过 ErrorLog 指令完成的。例如：

```
ErrorLog logs/error_log
```

在此示例中，所有服务器错误都将记录到位于 logs 目录中的名为 error_log 的文件中。

每当对您的 Web 服务器发出任何请求时，Apache 都会在传输日志中记录这些请求。您可以使用 TransferLog 指令指定传输日志使用的文件名。以下是示例：

```
TransferLog logs/access_log
```

最后，当 httpd 启动时，它会将父 httpd 进程的进程 ID 存储到文件 logs/httpd.pid 中。您可以使用 PidFile 指令更改 pid 文件的名称。这是一个非常重要的文件，因为当您想要重启或终止 Apache 时，必须知道父进程 ID。以下是设置此文件的示例：

```
PidFile logs/httpd.pid
```

请务必记住，在配置虚拟主机时，您可以为每个虚拟主机指定不同的错误日志和传输日志。

## 错误处理
错误处理是管理 Apache 的重要部分。Apache 有多个错误代码，每个代码都有不同的含义。以下是常用错误代码：

- 400 — 坏请求
- 401 — 需要授权
- 403 — 禁止访问
- 404 — 未找到
- 500 — 内部服务器错误

设置 Apache 处理错误的方式有多种。默认设置只是让 Apache 显示一个包含发生错误代码以及相应错误消息的页面。

## 自定义错误处理
然而，您可以自定义 Apache 的错误处理功能。最简单的方法是使用 ErrorDocument 指令。ErrorDocument 指令用于将错误消息分配给特定错误代码。ErrorDocument 指令保存在 srm.conf 文件中。以下是使用自定义错误消息的示例：

```
ErrorDocument 403 "I'm sorry, you do not have access to this directory"

ErrorDocument 404 "I'm sorry but what you are looking for cannot be found"
```

请注意，在错误代码后只使用一个引号，错误消息末尾不需要闭合引号。
