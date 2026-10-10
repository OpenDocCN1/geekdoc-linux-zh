

启用SSI（Server-Side Includes，服务器端包含）最常见的方式是指示服务器在提供具有特定文件名扩展名（通常是 .shtml）的文件时对其进行解析。这可以通过在 `srvm.conf` 文件中取消以下行的注释来实现：

```
# To use server-parsed HTML files
# AddType text/html .shtml
# AddHandler server-parsed .shtml
```

通过取消注释 `AddType` 和 `AddHandler` 行，你可以告诉服务器解析所有 `.shtml` 文件中的SSI指令。

启用SSI较少使用的方式是通过 `XBitHack` 指令。`XBitHack` 可以设置为 on、off 或 full，并可以在服务器配置、每个 `<Directory>`、每个 `<VirtualHost>` 或 .htaccess 文件中设置。如果 `XBitHack` 指令处于开启状态，则表示所有设置了用户执行位的文件都应被解析以查找SSI指令。这有两个主要优点。其一，你无需仅仅因为想添加少量动态内容就重命名文件并更改指向该文件的所有链接。另一个原因更偏向外观——查看你网页内容的用户无法通过文件名看出你正在动态生成页面——因此你的“魔术”显得略微令人印象深刻。如果 `XBitHack` 设置为 full，Apache 还会测试组执行位。如果该位开启，它将返回包含文件最后修改时间的 `Last-Modified` 标头；否则，它不会生成 `Last-Modified` 标头。允许生成 `Last-Modified` 标头使得数据可以被缓存。

除了这些指令外，对于你希望允许SSI的目录，还必须指定 `Options Includes` 指令。这可以在服务器的 `access.conf` 文件或 .htaccess 文件中设置。

# 基本SSI指令

SSI指令看起来类似于HTML注释标签。语法如下：

```
<!--#element attribute=value attribute=value ... -->
```

`element` 可以是以下其中之一：

- `config`: 此指令允许你设置关于如何处理文档解析的各种配置选项。由于页面是从上到下解析的，因此 `config` 指令应出现在HTML文档的顶部。可以通过此命令设置三种配置：
    - `errormsg`: 允许你设置在解析文档过程中发生错误时返回给客户端的错误消息。这通常是 `[an error occurred while processing this directive]`，但你可以通过此指令将其设置为任何内容。
      示例：`<!--#config errormsg='[It's broken, dude]'-->`
    - `sizefmt`: 允许你设置用于显示文件大小的格式。你可以将值设置为 bytes 以显示确切的字节大小，或设置为 abbrev 以 KB 或 MB 显示大小。
      示例：`<!--#config sizefmt="bytes"-->`
    - `timefmt`: 允许你设置用于显示时间的格式。该值的格式与C（以及Perl）中用于显示日期的 strftime 函数使用的格式相同，如以下表格所示。

| 格式 | 描述 |
| :--- | :--- |
| %% | 百分号 |
| %a | 星期缩写 |
| %A | 星期 |
| %b | 月份缩写 |
| %B | 月份 |
| %c | ctime格式：Sat Nov 19 21:05:57 1994 |
| %d | 月份中的数字日期 |
| %e | DD |
| %D | MM/DD/YY |
| %h | 月份缩写 |
| %H | 小时，24小时制，前导0 |
| %I | 小时，12小时制，前导0 |
| %j | 一年中的第几天 |
| %k | 小时 |
| %l | 小时，12小时制 |
| %m | 月份编号，从1开始 |
| %M | 分钟，前导0 |
| %n | 换行符 |
| %o | 华丽的日期，如 1st, 2nd, 或 25th |
| %p | a.m. 或 p.m. |
| %r | 时间格式：09:05:57 p.m. |
| %R | 时间格式：21:05 |
| %s | 秒，前导0 |
| %t | Tab |
| %T | 时间格式：21:05:57 |
| %U | 周数；周日作为每周第一天 |
| %u | 星期数字：周日 = 0 |
| %V | 周数；周一作为每周第一天 |
| %x | 日期格式：11/19/94 |
| %X | 时间格式：21:05:57 |
| %y | 年份（两位数字） |
| %Y | 年份（四位数字） |
| %z | 时区ASCII表示，例如 PST |

- `echo`: 显示下列包含变量中的任意一个。时间将按照 timefmt 指定的时间格式显示。要显示的变量通过 var 属性指示。
    - `DATE_GMT`: 格林威治标准时间的当前日期。
    - `DATE_LOCAL`: 本地时区的当前日期。
    - `DOCUMENT_NAME`: 用户请求文档的文件名（不包括目录）。
    - `DOCUMENT_URL`: 用户请求文档的（%-解码）URL路径。注意，在嵌套包含文件的情况下，这不是当前文档的URL。
    - `LAST_MODIFIED`: 用户请求文档的最后修改日期。
- `exec`: 根据提供的参数执行shell命令或CGI程序。有效属性为 cgi 和 cmd。
    - `cgi`: 要执行的CGI程序的URL。该URL必须是本地CGI，而不是位于另一台机器上的。CGI程序会接收最初传递给请求文档的 QUERY_STRING 和 PATH_INFO，因此指定的URL不能包含这些信息。你最好使用 include virtual 而不是此指令。
    - `cmd`: 要执行的shell命令。结果将显示在HTML页面上。
- `fsize`: 显示由 file 或 virtual 属性指定的文件的大小。大小将按照 sizefmt 指令指定的方式显示。
    - `file`: 文件的路径（文件系统路径），如果值以 / 开头，则相对于根目录；否则相对于当前目录。
    - `virtual`: 文件的相对URL路径。
- `flastmod`: 显示文件的最后修改日期。所需文件的指定方式与 `fsize` 指令相同。
- `include`: 包含文件的内容。文件通过 file 和 virtual 属性指定，方式与 `fsize` 和 `flastmod` 相同。如果指定的是CGI程序且未设置 IncludesNoExec，则该程序将被执行并显示结果。应优先使用此指令而非 *exec* 指令。你可以使用此指令传递 QUERY_STRING，而这是 *exec* 指令无法做到的。
- `printenv`: 显示所有现有变量。没有属性。
    - 示例：`<!--#printenv -->`
- `set`: 设置变量的值。属性为 var 和 value。
    - 示例：`<!--#set var="animal" value="cow" -->`

> **注意**
> 所有定义的CGI环境变量也可以作为 *include* 变量使用。

> **注意**
> 在你的 *配置* 文件中（或在 .htaccess 中），你可以指定 Options IncludesNoExec 来禁止 *exec* 指令，因为这是SSI指令中安全性最低的。当Web用户能够创建内容（如留言簿或讨论板）且这些选项被启用时，请格外谨慎！

这些变量可以在以下某些指令的其他位置使用。

# 流程控制

使用通过 *set* 指令设置的变量以及各种环境变量和 *include* 变量，你可以使用有限的流程控制语法在服务器解析页面上生成一定量的动态内容。

*if/else* 函数的语法如下：

```
<!--#if expr="test_condition" -->
<!--#elif expr="test_condition" -->
<!--#else -->
<!--#endif -->
```

*expr* 可以是一个字符串，如果非空则被视为真；也可以是两个字符串之间的多种比较。可用的比较运算符为 =、!=、<、<=、> 和 >=。如果第二个字符串的格式为 /string/，则字符串将通过正则表达式进行比较。可以使用 &&（AND）和 ||（OR）将多个比较串联起来。出现在 if/elsif/else 指令之间的任何文本都将在生成的页面上显示。

如下所示的这种流程结构的示例：

```
<!-- #set var="agent"  value="$HTTP_USER_AGENT"  -->
<!-- #if expr="agent = /Mozilla/" -->
Mozilla!
<!-- #else -->
Something else!
<!-- #endif -->
```

如果你使用将 Mozilla 作为其 USER_AGENT 字符串一部分的浏览器，这段代码将显示 Mozilla!；否则，将显示 Something else!。

# 启动和停止服务器

至此，你的Apache服务器已安装并按需配置完毕。是时候第一次启动它了。

服务器 httpd 有几个命令行选项，你可以使用它们来设置一些默认值，指定 httpd 将从哪里读取其配置指令。Apache httpd 可执行文件理解以下选项：

```
httpd [-d directory]  [ -f file]
     [ -C "directive" ] [ -c "directive" ]
     [ -V ] [ -v ] [ -h ] [ -l ] [ -L ] [ -8 ] [ -t ]
```

-d 选项覆盖 *ServerRoot* 目录的位置。它设置 *ServerRoot* 变量（Apache服务器查找其文件的目录）的初始值为你指定的任何路径。此默认值通常从 *httpd.conf* 中的 *ServerRoot* 指令读取，在 OpenLinux 中设置为 /etc/httpd/apache。

-f 标志指定主配置文件 *httpd.conf* 的位置。它在启动时读取并执行 *configurationFile* 中发现的配置命令。如果 *configurationFile* 不是绝对路径（不以 / 开头），则假设其位置相对于 *httpd.conf* 中 *ServerRoot* 指令指定的路径。默认情况下，此值设置为 */etc/httpd/apache/conf/httpd.conf*。

-v 选项打印Apache服务器的发展版本并终止进程。

-V 选项显示服务器编译时生效的所有设置。

-h 选项打印服务器的以下用法信息：

