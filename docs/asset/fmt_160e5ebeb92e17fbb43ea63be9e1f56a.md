
如果你使用按目录访问控制文件（`.htaccess`）来启用 SSI 支持，请确保拥有此类操作的站点 `AllowOverride` 指令已设置。站点的 `AllowOverride` 指令也允许覆盖 `Options`。例如，如果站点的 `AllowOverride` 设置为 `None`，则不会发生任何 SSI 解析。

如果你在上述示例的 `Options` 行未使用 `+`，则除 `Includes` 之外的所有选项将被禁用。

## 使用 SSI 命令

SSI 命令以注释的形式嵌入在 HTML 页面中。基本命令结构看起来如下：

```
<#command argument1=value argument2=value argument3=value -->
```

值通常用双引号括起来；许多命令仅允许单个属性-值对。注意，注释终止符（`--`）前面应该有一个空格，以确保它不会被视为 SSI 命令的一部分。

现在，让我们检查 `config`, `echo`, `exec`, `fcgi`, `lastmod`, `include`, `printenv` 和 `set` SSI 命令。

### 第四部分：设置内网/互联网服务

```
config [errmsg="error message"] [sizefmt="bytes" | "abbrev"]
[timefmt-=format string]
```

`config` 命令允许你配置错误消息和输出格式。例如：

```
<--config errmsg="This is a custom SSI error message." -->
<--config errmsg_type="This is a custom error message." -->
```

第一个是有效的 `errmsg` 命令，它将错误消息设置为字符串 "This is a custom SSI error message."。第二个是无效的 SSI 命令，会导致解析错误；结果是显示错误消息 "This is a custom SSI error message,"。该消息出现在无效命令所在。在错误消息字符串中可以输入 HTML 标签甚至插入客户端脚本。

要配置文件大小的输出格式，请使用 `config sizefmt="bytes" | "abbrev"]` 命令。接受的格式指定符为 "bytes" 或 "abbrev"。例如：

```
<-- config sizefmt="bytes" -->
```

这以字节显示文件大小。要以千字节或兆字节显示文件，请使用：

```
<-- config sizefmt="abbrev" -->
```

要配置时间的显示格式，使用 `config timefmt-format string` 命令。格式字符串的常用值可以由以下标识符组成：

- `%a`: 根据当前本地设置的缩写星期几
- `%A`: 根据当前本地设置的全星期几
- `%b`: 根据当前本地设置的缩写月份
- `%B`: 根据当前本地设置的全称月份
- `%c`: 当前本地设置的首选日期和时间表示
- `%d`: 月份数字（范围 01到31）
- `%H`: 使用24小时时制的数字小时（范围 00到23）
- `%I`: 使用12小时时制的数字小时（范围 01到12）
- `%j`: 年中的（范围 001到366）
- `%m`: 月数字（范围 01到12）
- `%M`: 分数字
- `%p`: 根据给定的时间或本地设置的 a.m. 或 p.m.
- `%S`: 秒
- `%w`: 星期几，星期日为0
- `%x`: 当前本地设置的首选日期表示
- `%X`: 当前本地设置的首选时间表示
- `%y`: 不带世纪的年份数字（范围 00到99）
- `%Y`: 包含世纪的年份
- `%Z`: 时区名称或缩写
- `%q`: 字面字符 %

例如：

```
<--#config timefmt="%m/%d/%Y -->
```

这显示时间为 05/20/1998。

`echo var="variable name"` 命令打印一个 Include 变量或任何 CGI 环境变量。如果变量值已设置，则会被打印。

（注：后续重复的文本已根据要求省略，不再进行重复翻译）

```
<#--config errmsg="在 $DOCUMENT_NAME 页面中发生了错误。" -->
```

在 `var="variable"` 字段中使用变量时，不需要使用 `$` 符号。

例如：

```
<#--echo var="DOCUMENT_NAME" -->
```

如果你需要在变量的值中插入一个字面上的美元符号，可以使用反斜杠转义来插入美元符号。例如：

```
<#--set var="password" value="\cheese" -->
<#--echo var="password" -->
```

这会将 "password" 变量的值打印为 cheese。

此外，如果你需要在一个序列中间引用变量名，而该序列在其他情况下可能被视为有效的标识符，请在变量名周围使用大括号。例如：

```
<#--set var="uniqued" value="$(DATE_LOCAL)$(REMOTE_HOST)" -->
```

这会将 `uniqued` 设置为类似 `Tue May 20 06:47:48 1998_206.171.50.51` 的值，取决于 `timefmt` 的设置。

## 使用 SSI 流控制命令

作为编程语言，SSI 模块也提供了流控制功能。

使用流控制命令，你可以根据条件创建不同的输出。

最简单的流控制（即条件判断）语句是：

```
<#--if expr="test_expression" -->
<#--endif -->
```

会评估 `test_expression`，如果测试结果为真，则到 `endif` 命令为止的所有文本都将包含在输出中。`test_expression` 可以是一个字符串（如果字符串不为空则为真），也可以是一个涉及两个字符串和比较运算符的比较，例如 `==`（等于）、`!=`（不等于）、`<`（小于）、`>`（大于）、`<=`（小于或等于）或 `>=`（大于或等于）。让我们来看一个字符串测试的例子：

```
<#--if expr="foobar" -->
```

此测试是成功的。

```
<#--endif -->
```

这总是显示 "This is successful"，因为当字符串为非空字符串时，表达式为真。然而，如果将 `expr="foobar"` 改为 `expr=""` 或 `expr=''`，那么 `if-endif` 块中的文本将不会是输出的一部分。现在让我们来看一个字符串相等测试的例子：

```
<--set var="quicksearch" value="yes" -->
<--if expr="$quicksearch" value="yes" -->
Quick search is requested.
<--endif -->
```

在这里，变量 `quicksearch` 被设置为值 `yes`，稍后与 `yes` 进行比较。由于设置的值和比较值相等，"Quick search is requested" 这行将作为输出。如果你需要更复杂的流控制结构，可以使用以下形式：

```
<--if expr="test_condition1" -->
<--elif expr="test_condition2" -->
<--else -->
<--endif -->
```

`elif` 允许你创建一个 `else-if` 条件。例如：

```
<--if expr="$(HTTP_USER_AGENT) = /MSIE/" -->
<--set var="browser" value="IE" -->
<--include file="vbscript.html" -->
<--elif expr="$(HTTP_USER_AGENT) = /Lynx/" -->
<--set var="browser" value="Lynx" -->
<--include file="simple-html.html" -->
<--else -->
```

```
<--set var="browser" value="Navigator" -->
<--include file="javascript.html" -->
<--endif -->
```
