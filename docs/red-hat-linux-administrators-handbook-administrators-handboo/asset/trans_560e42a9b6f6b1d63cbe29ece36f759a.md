
| 标识符 | 描述 |
|---|---|
| %a | 根据当前区域设置缩写的星期几名称 |
| %A | 根据当前区域设置完整的星期几名称 |
| %b | 根据当前区域设置缩写的月份名称 |
| %B | 根据当前区域设置完整的月份名称 |
| %c | 当前区域设置的首选日期和时间表示形式 |
| %d | 月份中的日期，十进制数（范围 01 到 31） |
| %H | 使用 24 小时制的小时，十进制数（范围 00 到 23） |
| %I | 使用 12 小时制的小时，十进制数（范围 01 到 12） |
| %j | 一年中的第几天，十进制数（范围 001 到 366） |
| %m | 月份，十进制数（范围 01 到 12） |
| %M | 分钟，十进制数 |
| %p | 根据给定时间值或区域的上午或下午 |
| %S | 秒，十进制数 |
| %w | 星期几的十进制数，星期日为 0 |
| %x | 当前区域设置不含时间的首选日期表示形式 |
| %X | 当前区域设置不含日期的首选时间表示形式 |
| %y | 不含世纪的年份，十进制数（范围 00 到 99） |
| %Y | 包含世纪的年份，十进制数 |
| %Z | 时区名称或缩写 |
| %% | 字面上的 % 字符 |

如果变量的值不可用，则将其打印为 "(none)"。打印的任何日期均受当前配置的 timefmt 约束。例如，

```
<!--#config timefmt="%m/%d/%Y" -->
<!--#echo var="DATE_LOCAL" -->
```

由于指定的 timefmt 字符串，会打印一个日期，例如 05/20/1998。

## exec
exec 命令使您能够执行外部程序，该程序可以是 CGI 程序或任何其他类型的可执行文件，例如 shell 脚本或原生二进制文件。语法如下：

```
exec [cgi="path/to/cgi/program"]
[cmd="path/to/other/program "]
```

如果为 Options 指令使用 IncludesNOEXEC 值，则 exec 命令将被禁用。exec cgi 命令将命名程序作为 CGI 脚本运行，而 exec cmd 命令使用 sh (/bin/sh) shell 将命名程序作为外部程序运行。

## fsize
fsize 命令打印指定文件的大小。语法如下：

```
fsize [ file="path" ] [ virtual="URL" ]
```

使用第一种语法（file="path"）时，路径假定相对于正在解析的当前 SSI 文档所在的目录。路径中不能使用 ./，也不能使用绝对路径。这种方式无法访问 CGI 脚本。但是，您可以访问另一个被解析的文档。例如：

```
<!--#fsize file="download.zip"-->
```

如果使用第二种语法（virtual="URL"），则虚拟路径假定为（%-编码的）URL 路径。如果路径不以斜杠（/）开头，则视为相对于当前文档。必须通过这种方式访问普通文件，但不能通过这种方式访问 CGI 脚本。

## flastmod
flastmod 命令打印指定文件的最后修改日期。语法如下：

```
flastmod [ file = "path" ] [ virtual="URL" ]
```

输出受 timefmt 格式规范的约束。例如：

```
<!--#flastmod file="free_software.zip"-->
```

```
<!--#flastmod virtual="/download/free_software.zip"-->
```

如果您对语法差异不明确，请参阅有关 fsize 命令的上一节作为示例。要控制修改日期的打印方式，请参阅 config 命令的早期描述。

## include
include 指令将文档的文本插入正在处理的 SSI 文档中。语法如下：

```
include [ file = "path" ] [ virtual="URL" ]
```

请参阅 fsize 命令的先前描述，了解 file 和 virtual 模式之间的差异说明。

任何包含的文件均受通常的访问控制约束。如果包含解析文件的目录设置了 IncludesNOEXEC 选项，并且包含该文档会导致程序执行，则不会包含该文档。这可以防止 CGI 脚本的执行。否则，CGI 脚本将按正常方式调用，使用命令中给出的完整 URL，包括任何查询字符串。例如，

```
<!--#include file="copyrights.html" -->
```

将当前文档中的 copyrights.html 文件包含在内。递归包含会被检测到，并在第一次传递后生成错误消息。

## printenv
printenv 命令打印所有现有变量及其值的列表。语法如下：

```
printenv
```

例如，以下内容打印所有可用的 Include 和 CGI 环境变量：

```
<!--#printenv -->
```

使用 <PRE> 标签对使输出更易读。还请注意，在公开可访问的页面中显示此命令的输出可能会泄露有关系统的一些敏感信息。因此，仅将此命令用于调试目的。

## set
set 命令设置用户定义变量的值。语法如下：

```
set var="name" value="something"
```

例如，

```
<!--#set var="home" value="index.shtml" -->
```

请注意，使用前述命令设置的任何变量都不是持久的。换句话说，每次加载使用 set 命令的页面时，所有变量都会被重置。

## Using SSI variables
SSI 模块为所有 SSI 文件提供一组变量，除 CGI 环境变量外，称为 include 变量。这些变量可由 SSI 命令（echo、if、elif 等）以及由 SSI 命令调用的任何程序使用。变量如下：

- DATE_GMT。格林威治标准时间的当前日期。
- DATE_LOCAL。本地时区的当前日期。
- DOCUMENT_NAME。当前 SSI 文件名。
- DOCUMENT_URI。文档的（%-解码）URL 路径。
- LAST_MODIFIED。当前文件的最后修改日期。日期受 config 命令的 timefmt 格式约束。

include 变量和 CGI 变量已预设并可供使用。任何预设的变量都可以用作其他命令的参数。使用已定义变量的语法如下：

```
<!--#command argument1="$variable1"
argument2="$variable2" . . . -->
```

变量名以 $ 符号为前缀。以下是另一个示例：

```
<!--#config errmsg="An error occurred in $DOCUMENT_NAME page." -->
```

在 var="variable" 字段中使用变量时，$ 符号不是必需的。例如：
<!--#echo var="DOCUMENT_NAME" -->
如果需要在变量的值中插入字面上的美元符号，可以使用反斜杠引用插入美元符号。例如，
<!--#set var="password" value="\$cheese" -->
<!--#echo var="password" -->
打印 $cheese 作为变量 "password" 的值。

此外，如果需要在可能被视为有效标识符的字符序列中间引用变量名，请在变量名周围使用一对大括号。例如，

```
<!--#set var="uniqueid" value="${DATE_LOCAL}_${REMOTE_HOST}" -->
```

根据 timefmt 设置，将 uniqueid 设置为类似 Tue May 20 06:47:48 1998_206.171.50.51 的内容。

## Using SSI flow control commands
如同编程语言一样，SSI 模块中提供了流程控制。通过使用流程控制命令，您可以有条件地创建不同的输出。最简单的流程控制（即条件）语句如下：

```
<!--#if expr="test_expression" -->
<!--#endif -->
```

test_expression 会被求值，如果测试结果为真，则直到 endif 命令为止的所有文本都将包含在输出中。test_expression 可以是一个字符串，如果字符串不为空则为真，或一个比较表达式，涉及两个字符串和比较运算符，例如 =（等于）、!=（不等于）、<（小于）、>（大于）、<=（小于或等于）或 >=（大于或等于）。以下是一个字符串本身的示例：

```
<!--#if expr="foobar" -->
This test is successful.
<!--#endif -->
```

这总是显示 "This test is successful"，因为当 test_expression 是一个非空字符串时表达式为真。但是，如果将 expr="foobar" 改为 expr="" 或 expr=""”，则 if-endif 块内的文本永远不会成为输出的一部分。

以下是一个字符串相等性测试的示例：

```
<!--#set var="quicksearch" value="yes" -->
<!--#if expr="$quicksearch = yes" -->
Quick search is requested.
