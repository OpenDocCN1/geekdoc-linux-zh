
## SSI

服务器端包含指令直接写入在 HTML 页面中，服务器在发送页面时对其进行解析。SSI 可包含其他文件、程序输出或环境变量。

你可以通过 `XBitHack` 指令启用 SSI。`XBitHack` 可以设置为 `on` 或 `off`，并可以在配置文件或 `.htaccess` 中设置。如果 `XBitHack` 指令为 `on`，表示所有具有用户执行权限的文件都应该被解析 SSI 指令。这有两个优点。优点是你不需要仅仅因为添加了一点动态内容就重命名文件并更改指向它的所有链接。另一个原因是美观：查看你网页内容的用户看不到你动态生成的文件名，因此你的魔术看起来更有趣。

使用 `XBitHack` 的另一个副作用是它允许控制缓存如何缓存你的页面。包含 `Last-modified` HTTP 头部的页面不会被代理或浏览器缓存。如果你启用了 `XBitHack`，文件的组执行位将控制是否生成 `Last-modified` 头部。它被设置为与文件最后修改时间相同的值。请确保仅对真正需要缓存的文件使用此。

使用 SSI 的另一种方法是指示具有特定文件名扩展（通常为 `.shtml`）的文件在提供服务时由服务器解析。这是通过在 `httpd.conf` 中添加以下行实现的：

```
# 使用服务器解析的 HTML 文件
#
#AddType text/html .shtml
#AddHandler server-parsed .shtml
```

如果你取消 `AddType` 和 `AddHandler` 行的注释，将告诉服务器解析所有 `.shtml` 文件以查找 SSI 指令。除了这些指令外，对于你想要允许 SSI 的目录，还必须指定以下指令：
`Options Includes`

这可以在服务器配置文件或 `.htaccess` 文件中设置。

### 基础 SSI 指令

SSI 指令看起来非常像 HTML 注释标签。其语法如下：
`<!---element attribute=value attribute=value ... -->`

该元素可以是多个指令之一，包括：

- `config`
- `echo`
- `exec`
- `fsize`
- `lastmod`
- `include`
- `printenv`
- `set`

接下来的章节将描述这些指令中的每一个及其用途。

#### config
`config` 指令允许你设置各种配置选项，以确定如何处理文档解析。由于页面是从上到下解析的，`config` 指令应该出现在 HTML 文档的顶部。此命令可以设置三项配置：

- `errmsg`—如果在解析文档时发生错误，设置返回给客户端的错误消息。默认消息是 [处理此指令时发生错误]，但你可以使用此指令将消息设置为任何文本。例如：

```
<!--#config errmsg="It's broken, dude" -->
```

- `sizefmt`—设置用于显示文件大小的格式。你可以将值设置为 `bytes` 以以字节显示精确的文件大小，或将其设置为 `abbrev` 以 KB 或 MB 为单位显示大小。例如，

```
<!#config sizefmt="bytes" -->
```

- `timefmt`—设置用于显示时间的格式。该值的格式与 C（以及 Perl）用于显示日期的 `str` 函数相同，如下列表所示：

- `%%` Percent
- `%a`—星期缩写
- `%A`—星期
- `%b`—月份缩写
- `%B`—月份
- `%c`—时间格式：Sat Nov 19 21:05:57
- `%d`—月份中的数字几
- `%e`—DD
- `%D`—MM/DD/YY
- `%h`—月份缩写
- `%H`—小时，24 小时制，带前导零
- `%I`—小时，12 小时制，带前导零
- `%j`—星期
- `%k`—小时
- `%l`—小时，12 小时制
- `%m`—月份数字，从 1 开始
- `%M`—分钟，带前导零
- `%n`—换行
- `%o`—月份中的序数—1st, 2nd, 25th 等
- `%p`—AM 或 PM
- `%r`—时间格式：09:05:57 PM
- `%R`—时间格式：21:05
- `%S`—秒数，带前导零
- `%t`—制表符
- `%T`—时间格式：21:05:57
- `%U`—周数：星期日为每周的第一天
- `%w`—星期，数字；星期日 = 0
- `%W`—周数：星期一为每周的第一天
- `%x`—日期格式：11/19/94
- `%X`—时间格式：21:05:57
- `%y`—年（两位）
- `%Y`—年（四位）
- `%Z`—ASCII 时区，例如 PST

#### echo
`echo` 指令显示下列表中的任何包含变量。时间按 `timefmt` 指定的格式显示。使用 `var` 属性来指定要显示的变量：

- `DATE_GMT`—格林尼治时间的当前日期。
- `DATE_LOCAL`—本地时区的当前日期。
- `DOCUMENT_NAME`—用户请求文档的文件名（不包括目录）。
- `DOCUMENT_URI`—用户请求文档的（经过解码的）URL 路径。注意，在嵌套包含文件的情况下，这不是当前文档的 URL。
- `LAST_MODIFIED`—用户请求文档的最后修改日期。

#### exec
`exec` 指令根据你提供的参数执行 shell 命令或 CGI 程序。有效的属性有 `cgi` 和 `cmd`：

- `cgi`—要执行的 CGI 程序的 URL。该 URL 必须是本地 CGI，不能是位于另一机器上的。CGI 程序将获得原始传递给请求文档的 `QUERY_STRING` 和 `PATH_INFO`，因此指定的 URL 不能包含这些信息。你应该包含 `virtual` 而不是此指令。
- `cmd`—要执行的 shell 命令。结果显示在 HTML 页面上。

## 第 21 章 Apache Web 服务器管理

#### fsize
`fsize` 指令通过 `file` 或 `virtual` 属性定义文件大小。大小按 `sizefmt` 指令指定的格式显示：

- `file`—文件的路径（文件系统路径），如果值以 `/` 开头，则相对于根目录；否则相对于当前目录
- `virtual`—指向文件的相对 URL 路径

#### fstatmod
显示文件的最后修改日期。指定文件的方式与 `fsize` 指令相同。

#### include
`include` 指令包含文件的内容。通过 `file` 和 `virtual` 属性指定文件，与 `fsize` 和 `fstatmod` 一。

如果指定的文件是 CGI 程序且未设置 `IncludesNOEXEC`，则执行该程序并显示结果。这应优于 `exec` 指令。你可以使用此指令传递 `QUERY_STRING`——这是使用 `exec` 指令无法做到的。

#### printenv
它显示所有现有变量，且没有属性。例如：

```
<--printenv -->
```

#### set
`set` 设置变量的值，其属性为 `var` 和 `value`。例如：

```
<--set var="animal" value="cow" -->
```

> 注意
> 所有定义的 CGI 环境变量也允许作为包含变量。

> 注意
> 在你的配置文件（或 `.htaccess`）中，你可以指定 `Options IncludesNOEXEC` 来禁用 `exec` 指令，因为这是 SSI 指令中安全性最低的。当 Web 用户能够创建内容（如留言板或讨论板）且这些这些选项时，要格外小心！

通过 `var` 和 `value` 设置属性的变量也可以在后续指令的其他地方使用。

### 流程控制
使用通过 `set` 指令设置的变量可以使用各种流程控制来生成动态内容。`if/else` 示例显示所示：

```
<#if="test_condition">

<#elif="test_condition">

<#else>

<#endif>
```

可用的运算符有 `=`、`<=` 和 `>=`。多个比较可以使用 `&&`（与）和 `||`（或）串联。`set` 的示例也显示了：

```
<#set var="animal" value="cow">
```

### Apache 的图形界面
Apache 的某些基本行为可以使用 `system-config-httpd`（一个 GUI 工具）进行配置。

警告
如果你使用 `system-config-httpd`，你不应该手动编辑 `httpd.conf` 文件。手动更改会被 GUI 覆盖。

![d4ad9a7c85702c925b428f587284a4f_598_0.png](FIGURE 21.2 system-config-httpd 主对话框提供了对基本配置的访问)

按下回车后，你会被要求输入 root 密码。然后你会看到主客户端窗口。

使用你的 X 桌面面板的“服务器设置”菜单或从命令行启动此客户端，如下：

```
$ system-config-httpd &
```
