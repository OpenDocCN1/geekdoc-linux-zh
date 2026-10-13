
服务端包含（SSI）是直接插入 HTML 页面中的指令，服务器在页面提供给 Web 客户端对其进行解析。SSI 可用于包含其他文件、程序输出或环境变量。

你可以通过 `XBitHack` 指令启用 SSI，`XBitHack` 可以设置为 `on` 或 `off`，并可以在你的配置文件或 `.htaccess` 文件中设置。如果 `XBitHack` 指令为 `on`，则表示所有具有用户执行位的文件都应该被解析 SSI 指令。这有两个主要优势：其一你不需要为了给文件添加一点动态内容就重命名文件并更改指向该文件的所有链接。另一个原因更是为了美观：查看你 Web 内容的用户无法通过文件名判断你正在动态生成页面，因此你的向导看起来更高级了一点。

使用 `XBitHack` 的另一个积极副作用是它允许你控制客户端如何缓存你的页面。包含 SSI 语句的页面通常不包含 `Last-modified` HTTP 头。因此，它们不会被代理或 Web 浏览器缓存。如果你启用了 `XBitHack`，文件的组执行位将控制是否生成 `Last-modified` 头。它将被设置为与文件最后修改时间相同的值。请确保仅对应该被缓存的文件使用。

启用 SSI 的另一种方法是指定具有特定文件扩展名（通常为 `.shtml`）的文件在提供时由服务器解析。这通过在你的 `httpd.conf` 文件中使用以下行实现：

```apache
# 要使用服务器解析的 HTML 文件
#
#AddType text/html .shtml
#AddHandler server-parsed .shtml
```

## 第 16 章 Apache 服务器管理

如果你取消了 `AddType` 和 `AddHandler` 行的注释，你将告诉服务器解析所有的 `.shtml` 文件以查找 SSI 指令。

除了这些指令外，对于想要允许 SSI 的目录，必须指定以下指令：

`Options Includes`

这可以在服务器配置文件或 `.htaccess` 文件中设置。

### 基础 SSI 指令

SSI 指令看起来很像 HTML 注释标签。语法如下：

```html
<!--element attribute=value attribute=value ... -->
```

该元素可以是几个指令之一，包括：

- `config`
- `echo`
- `exec`
- `fsize`
- `lastmod`
- `include`
- `printenv`
- `set`

接下来的章节描述了这些指令中的每一个及其用途。

### config

`config` 指令允许你设置各种配置选项来确定如何处理文档解析。由于页面是从上到下解析的，`config` 指令应该出现在 HTML 文档顶部。使用此命令可以设置三个配置：

- `errmsg`—设置当解析文档出错时返回给客户端的错误消息。默认消息是 `an error occurred while processing this directive`，但你可以设置它。例如，

```html
<!--config errmsg="It's broken, dude" -->
```

- `sizefmt`—设置显示文件大小的格式。你可以将值设置为 `bytes` 以显示精确大小，或者 `KB` 或 `MB`。例如，

```html
<!--config sizefmt="bytes" -->
```

- `timefmt`—设置显示时间的格式。值的格式与 C（以及 Perl）显示日期的格式相同，如下所示：

```html
<!--config ... -->
```

### echo

`echo` 指令显示下列表中任何一个包含变量。时间按 `timefmt` 指定的格式显示。使用 `var` 属性来指示要显示的变量。

- `DATE_GMT`—格林尼治时间的当前日期。
- `DATE_LOCAL`—本地时区的当前日期。
- `DOCUMENT_NAME`—请求文档的文件名（不包括目录）。
- `DOCUMENT_URI`—请求文档的（解码后的）URL路径。注意在嵌套包含文件的情况下，这不是当前文档的 URL。
- `LAST_MODIFIED`—请求文档的最后修改日期。

### exec

`exec` 指令根据你提供的参数执行 shell 命令或 CGI 程序。有效的属性是 `cgi` 和 `cmd`。

- `cgi`—要执行的 CGI 程序的 URL。该 URL 必须是本地 CGI，而不是位于其他机器。CGI 程序将最初传递给请求文档的 `QUERY_STRING` 和 `PATH_INFO`，因此指定的 URL 不能包含这些信息。你应该使用 `virtual` 代替此指令。
- `cmd`—要执行的 shell 命令。结果将显示在 HTML 页面上。

### fsize

`fsize` 指令显示由文件或虚拟属性指定的文件大小。显示格式由 `sizefmt` 指令指定。

- `file`—指向文件的路径（系统路径），如果值以 `/` 开头，则相对于根目录；否则相对于当前目录。
- `virtual`—指向文件的相对 URL 路径。

### lastmod

显示文件的最后修改日期。目标文件的指定方式与 `fsize` 指令相同。

### include

`include` 指令包含一个文件的内容。与 `fsize` 和 `lastmod` 一样，通过 `file` 和 `virtual` 属性指定文件。

如果文件被指定为 CGI 程序且未设置 `Includes`，则将执行该程序并显示结果。这优于使用 `exec` 指令。你可以使用此指令传递 `QUERY_STRING`——这是使用 `exec` 指令时无法做到的。

### printenv

显示所有现有变量。没有属性。例如：

```
<!--#printenv -->
```

### set

设置变量的值。属性为 `var` 和 `value`。例如：

```
<!--#set var="animal" value="cow" -->
```

> NOTE
> 所有定义的 CGI 环境变量也允许作为包含变量。

> NOTE
> 在你的配置文件（或 `.htaccess`）中，你可以指定 `Options IncludesNOEXEC` 来禁用 `exec` 指令，因为这是所有 SSI 指令中安全性最低的。当 Web 用户能够创建内容（如留言板或讨论板）且启用了这些选项时，务必格外小心！

通过 `var` 和 `value` 属性设置的变量也可以配合以下某些指令用于其他。

## Flow Control

使用 `set` 指令设置的变量以及各种环境变量和包含变量，可以使用有限的流控制语法在服务器解析的页面上生成一定量的动态内容。

`if/else` 函数的语法如下：

```
<!#if expr="test_condition" --
<!#elif expr="test_condition" --
<!#else --
<!#endif -->
```

`expr` 可以是一个字符串，如果非空、`!=` 或两个字符串之间的各种比较成立，则被视为真。可用的比较运算符有 `=`、`!=`、`<`、`>` 和 `>=`。如果第二个字符串的格式为 `/string/`，则使用正则表达式对字符串进行比较。可以使用 `&&` (AND) 和 `||` (OR) 同时设置多个比较。出现在 `if/elif/else` 指令之间的任何文本将显示在生成的页面上。此类流控制结构的示例：

```
<!#set var="agent" value="HTTP_USER_AGENT" --
<!#if expr="$agent = /Mozilla/" --
Mozilla:
<!#else --
Something else!
<!#endif --
```

如果你使用的浏览器将 Mozilla 作为其 `USER_AGENT` 字符串的一部分传递，此代码将显示 Mozilla！否则显示 Something else!。

## Apache 图形界面配置

Apache 的某些基本行为可以使用 Red Hat 的 `redhat-config-httpd` 配置（Windows 系统的 GUI）。这可以提供一种简单的方法来配置设置，例如 Apache 的用户和组名、PID 和进程锁文件的位置，或性能设置（如最大连接数），而无需手动编辑配置文件。

> CAUTION
> 如果你使用 `redhat-config-httpd`，你不应该尝试手动编辑 `httpd.conf` 文件。如果你再次使用 `redhat-config-httpd`，手动更改将被 GUI 客户端覆盖！

通过使用 X 桌面面板的“服务器设置”“HTTP 服务器”菜单项，或从 X 终端窗口的命令行启动此客户端：

```
$ redhat-config-httpd &
```

按下回车键后，将要求你输入根密码。你将看到图 16.2 所示的主客户端窗口。

在 Main（主）选项卡中，你可以设置服务器名称、指定发送给 Web 管理员邮件地址，并设置 Apache 使用的端口。如果需要，你还可以配置特定的虚拟主机以监听不同的端口。

### 配置虚拟主机属性
