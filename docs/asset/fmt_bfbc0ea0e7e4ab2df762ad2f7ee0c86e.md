
如果一个网站有 50 或 60 个 Web 页面，每个页面都有相同的图像或文本标题，你应该考虑实施 SSI。这种技术允许你创建一个带有标题的 HTML 文档，然后将其包含在所有文档中。如果任何标题被更改，更改将反映在所有文档中。

其中一个命令是 `include`，它访问文件并将内容添加到嵌入命令的地方。通过这种类型的命令，假设网站的 Web 页面开发者可以创建一个 HTML 文件，并使用 SSI 包含在网站的每个 Web 页面中。开发者避免了重复相同的语句，而且在标题中进行更改非常容易。

使用 SSI 有多困难？SSI 命令的格式为：

```html
<!-- #SSI_command arguments="values" -->
```

这就是全部，以及 SSI 为何如此流行。

# 设置服务器端包含的环境

服务器端包含并非在所有 Web 服务器中都实现，但在 NCSA 中已实现，并且对于 CERN 服务器有一个变通方法。

## 第 7 章 -- Perl 和 CGI 中的动态交互式 HTML 内容

设置网站需要修改文件 `SRM.CONF`，这是服务器配置文件。通过在以下内容之后添加一行，添加将要解析的 HTML 文件扩展名：

```perl
AddType text/x-server-parsed-html .shtml
```

通过此行，任何扩展名为 `.HTML` 的文件都将被 Web 服务器解析以查找 SSI 指令。最常用的扩展名是 `.shtml`。此扩展名可以防止服务器解析任何 `.html` 扩展名的文件，这可能会降低不包含 SSI 指令的 HTML 文档的性能。

需要在 `ACCESS.CONF` 文件中添加一行来启用 SSI。要使用 `exec` 命令选项启用 SSI，请添加以下行：

```
Options Includes
```

若要在不使用 `exec` 命令的情况下启用 SSI，请添加以下内容：

```
Options IncludesNoExec
```

要启用 CERN Web 服务器，使用一个名为 `FAKESSILPL` 的文件进程。该文件允许服务器模拟服务端包含。安装此文件后，服务器可以处理 `exec SSI` 中 `cmd` 选项以外的所有内容。要安装它，请将其复制到 `/CGI-BIN` 子目录，并更改其权限使其可执行。在 `HTTPD.conf` 文件中（位于系统定义的 Web 配置文件子目录中），添加以下行：

```perl
Exec /*.shtml /users/www/cgi-bin/fakessipl.pl
```

重启服务器后，SSI 指令将变为可用。

## 理解命令

SSI 指令有：

- `include`
- `config`
- `lastmod`
- `fsize`
- `echo`
- `exec`

SSI 指令的格式为：

```html
<!command arg="value" -->
```

注意此命令中的空格至关重要。在前两个横线与命令之间不能有空格，在值与最后两个横线之间必须有一个空格。

**`include` 命令** 有两个参数：`virtual` 和 `file`。使用 `file` 允许开发者指定当前目录的子目录，HTML 文档就包含在该子目录中。该命令的示例是：

```html
<!#include file="support/top_main.html" -->
```

使用 `virtual` 参数时，命令变为：

```html
<#include virtual="/main_grp/top/support/top_main.html" -->
```

`virtual` 参数定义了相对于服务器根目录的路径。

包含的文件可以是 CGI 应用程序，也可以是包含 CGI 应用程序引用的 HTML 文档。图 7.6 显示了一个包含 SSI 的示例。图中显示的网页包含一个 HTML 文档，该文档包含一个包含在所有文档中的通用头部。

**图 7.6：** 此 HTML 文档包含一个 SSI include，它反过来调用了一个包含头部信息的 HTML 文档。

主 HTML 文件名为 `MAIN`。`.SHTML` 扩展名是为 SSI 定义的。列表 7.10 显示了该文档的源代码。

- 列表 7.10 包含 `include` 命令的服务端包含 HTML 文档 (`main.shtml`)

```html
<HTML>
<HEAD><TITLE>Some Software Company - Main Page </TITLE>
</HEAD>
<!--#include file="support/top_main.html" -->
<p>
Welcome to our web page!
</p>
BODY
</HTML>
```

包含的文件包含 BODY 部分的开头，该部分还定义了页面颜色、头部和图形。列表 7.11 显示了此文档的 HTML。

- 列表 7.11 包含头部部分的 HTML 文档 (`top_main.html`)

```html
<BODY BACKGROUND="#FEBCED" TEXT="#8B4513">
<H1>Welcome to Some Software Company!</H1>
<p>
<IMG SRC="../images/garden2.jpg">
<p>
```

**`config` 命令** `config` SSI 指令用于修改其他 SSI 指令的结果。以下命令行修改了 SSI 在指令结果时返回的错误：

```html
<!--#config errrmsg="We're sorry but we are temporarily having difficulty opening this page." -->
```

另一个使用 `config` 命令的示例是 `sizefmt`。以下命令修改了当 SSI `filesize` 时返回的尺寸格式：

```html
<!--#config sizefmt="bytes" -->
```

此命令返回 `fsize` 对象的的结果，显示文件的完整字节数。另一个可选参数是 `sizefmt="abbrev"`，它返回四舍五入到最近千字节的文件大小。

使用 `config` SSI 的最后一个参数是 `timefmt`，它使用 `lastmod` 命令格式化返回的结果。`lastmod` 命令返回文档的最后修改日期。这是该命令的示例，它以斜杠分隔的缩写小数显示星期和日期：

```html
<!--#config timefmt="%A %m/%d/%y" -->
```

**`lastmod` 命令** 此 SSI 指令显示 HTML 文档最后修改的日期。`include` 和 `lastmod` 命令可以使用 `file` 参数或 `virtual` 参数指定。图 7.7 显示此命令的示例。

[图 7.7；此 HTML 文档包含三个 SSI 指令。]

列表 7.12 显示了生成此文档的 HTML 语句。

- 列表 7.12 包含三个 SSI 指令的 HTML 文档 (`main2.html`)

```html
<HTML>
<HEAD><TITLE>Some Software Company - Main Page </TITLE>
</HEAD>
<!--#include file="support/top_main.html" -->
<p>
Welcome to our web page!
</p>
BODY
</HTML>
```

注：由于原文中存在大量重复段落，译文已根据要求“不要重复输出原文”，仅保留核心逻辑与翻译。

```perl
open(COUNTER, "> access-counter") || die "BUSY";

print COUNTER $value;

close(COUNTER);

#
print $value;

exit(0);
```

接下来，使用 `exec SSI` 命令访问 CGI 应用程序。列表 7.15 显示相关的 HTML 语句。

# **列表 7.15** 包含多个 SSI 命令的文档 (`main4.html`)

```html
<HTML>
<HEAD><TITLE>某软件公司 - 主页 </TITLE>
</HEAD>
<!--include file="support/top_main.html" -->
<p>
欢迎来到我们的网页！
<p>
此文档最后修改于：
<!--#config timefmt="%A %m/%d/%y" -->
<!--#lastmod file="main3.shtml" -->
<p>
此页面上图片的尺寸为：
<!--#fsize file="garden2.jpg" -->
<p>
此文档位于：
<!--#echo var="document_uri" -->
<p>
本网站已被访问 <!#exec cgi="accesses.cgi" --> 次。
</BODY>
```

</HTML>

# 章节 -- Perl 和 CGI 中的动态交互式 HTML 内容

每当访问 HTML 文档时，就会调用 CGI 应用程序 `accesses.cgi`。该应用程序增加计数并返回给 HTML 文档。

| 文件锁定 |
