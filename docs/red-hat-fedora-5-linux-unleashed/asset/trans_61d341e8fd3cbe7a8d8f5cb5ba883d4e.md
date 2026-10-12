
## 日志格式变量

-   `%h`
    -   发送的字节数，不包括 HTTP 头。
-   `%(VARIALE)e`
    -   环境变量 `VARIABLE` 的内容。
-   `s`
    -   输出日志的文件名。
-   `co`
    -   远程主机。
-   `ar`
    -   请求协议。
-   `%(HEADER)i`
    -   `HEADER` 的内容；即发送到服务器的请求中的头行。
-   `%i`
    -   远程日志名称（如果提供了 `identd`，则取自其中）。
-   `%m`
    -   请求方法。
-   `%(module)N`
    -   来自其他模块的注释 `NOTE` 的内容。
-   `%(HEADER)O`
    -   `HEADER` 的内容；即响应中的头行。
-   `%p`
    -   处理请求的服务器的规范端口。
-   `%P`
    -   处理请求的子进程的进程 ID。
-   `%q`
    -   查询字符串的内容，前面加上 `?` 字符。如果没有查询字符串，则此值为空字符串。
-   `%r`
    -   请求的第一行。
-   `%s`
    -   状态。对于内部重定向的请求，这是原始请求的状态——最后一个请求的状态为 `%s`。
-   `%t`
    -   时间，采用通用日志时间格式。
-   `%(format)t`
    -   时间，形式由 `format` 指定，应采用 `strfTime(3)` 格式。本章后面“基本 SSI 指令”部分列出了所有可用的格式化选项。
-   `%T`
    -   处理请求所花费的秒数。
-   `%u`
    -   来自 `auth` 的远程用户；如果返回状态（%s）为 401，此值可能无效。
-   `%U`
    -   请求的 URL 路径。
-   `%V`
    -   根据 `UseCanonicalName` 指令确定的服务器名称。
-   `%v`
    -   处理请求的服务器的规范 `ServerName`。

您可以在每个变量前添加条件，以决定是否显示该变量。如果变量不显示，则改为显示 `-`。这些条件的形式是一个数字返回值的列表。例如，`%{%401}u` 会显示 REMOTE_USER 的值，除非返回代码为 401。

然后，您可以使用 `CustomLog` 指令指定日志文件的位置和格式：

```
CustomLog logs/access_log common
```

如果未指定为绝对路径，则假设日志文件的位置是相对于 `ServerRoot` 的。

## 动态内容

在网站上提供动态内容最常见的方式是使用 CGI 程序。CGI 是一种规范，定义了服务器进程（例如生成动态文档的程序）与服务器本身之间的通信方式。SSI 允许将 CGI 程序或其他程序的输出插入到现有的 HTML 页面中。

向网站添加动态内容的另一种方式是使用 PHP（PHP HYPertext Preprocessor [该名称是递归的]）。PHP 是一种专为 Web 使用而设计的 HTML 嵌入式脚本语言。Apache 的 PHP 模块是其中最流行的第三方模块之一。

### CGI

默认情况下，您可以将任何 CGI 程序放在由 `ScriptAlias` 指令定义的目录中。CGI 程序可以用任何语言编写。用于 CGI 编程最流行的语言是 Perl 和 C。第 30 章“使用 Perl”提供了更多关于使用 Perl 脚本语言的信息。

这些程序必须对默认的 Apache 用户具有可执行权限，这意味着您必须将文件的模式更改为 555，以便 Apache 用户可以执行它们。默认情况下，Apache 在 Fedora 中作为一个名为 `apache` 的用户运行：

```
chmod 555 program.cgi
```

要在 `ScriptAlias` 目录之外执行 CGI 程序，您必须为该目录启用 `ExecCGI` 选项。这可以在您的 `httpd.conf` 文件中的该目录或在目录中的 `.htaccess` 文件中完成。

要测试您的 CGI 配置是否正确，请尝试运行清单 21.1 中的 CGI 程序。该程序使用 Perl 编写，并显示 HTTP 环境变量的值。

### 清单 21.1 environment.pl

```
#!/usr/bin/perl -w

print <<EOF;
"Content-type: text/html"

<HTML>
<HEAD>
<TITLE>Simple CGI program</TITLE>
</HEAD>
<BODY>
EOF
for (keys %ENV) {
print " $ _ = $ENV{$_}<BR>\n";
}

print <<EOF;
</BODY>
</HTML>
EOF
```

如果您打算用 Perl 编写 CGI 程序，请花些时间研究 Perl 随附的 CGI 模块。一个广泛的 Perl 模块库包含了许多专为编写 CGI 而设计的模块，可在 http://www.cpan.org/ 访问。如果您使用许多用 Perl 编写的 CGI，请检查 `mod_perl` 模块。该模块在 Apache 服务器内嵌了一个 Perl 解释器。使用此模块可以加快 CGI 的执行速度，因为您不需要为每个请求启动一个新的 Perl 解释器。如果您从本书的 DVD 安装该模块，您可以在 `/usr/share/doc/mod_perl-1.31_12/docs/` 目录下找到关于使用 `mod_perl` 的信息。

> 注意：如果您使用其他用户或外部开发人员开发的 CGI，请务必检查安全更新和漏洞修复。更新不及时或实现/编写不当的 CGI 会给您的系统带来严重的安全威胁。

### SSI

服务器端包含（SSI）是直接写入 HTML 页面的指令，服务器在向 Web 客户端提供页面时会解析这些指令。SSI 可用于包含其他文件、程序输出或环境变量。

您可以使用 `XBitHack` 指令启用 SSI。`XBitHack` 可以设置为 `on` 或 `off`，并可以设置在配置文件或 `.htaccess` 文件中。如果 `XBitHack` 指令为 `on`，则表示应解析所有设置了用户执行位文件的 SSI 指令。这有两个主要优点。一是您无需仅因为想在文件中添加少量动态内容而重命名文件并更改指向该文件的所有链接。另一个原因更偏向于美观：查看您 Web 内容的用户无法通过查看文件名得知您正在动态生成页面，因此您的魔法会显得稍微厉害一点。

使用 `XBitHack` 的另一个积极副作用是，它允许您控制客户端应如何缓存您的页面。包含 SSI 语句的页面通常不包含 `Last-modified` HTTP 头。因此，它们不会被代理或 Web 浏览器缓存。如果您启用 `XBitHack`，文件的组执行位将控制是否应生成 `Last-modified` 头。它被设置为与文件最后修改时间相同的值。请确保仅对确实应该被缓存的文件使用此功能。

启用 SSI 的另一种方式是指示具有特定文件名扩展名（通常是 `.shtml`）的文件在服务时由服务器解析。这通过在您的 `httpd.conf` 文件中添加以下行来实现：

```
# To use server-parsed HTML files
#
#AddType text/html .shtml
#AddHandler server-parsed .shtml
```

如果您取消注释 `AddType` 和 `AddHandler` 行，则告知服务器解析所有 `.shtml` 文件中的 SSI 指令。除了这些指令外，对于允许 SSI 的目录，还必须指定以下指令：

```
Options Includes
```

这可以设置在服务器配置文件中，也可以在 `.htaccess` 文件中设置。

### 基本 SSI 指令

SSI 指令看起来很像 HTML 注释标签。语法如下：

```
<!--#element attribute=value attribute=value ... -->
```

元素可以是以下指令之一，包括：

-   config
-   echo
-   exec
-   fsize
-   lastmod
-   include
-   printenv
-   set

接下来的各部分将描述这些指令及其用途。

#### config

`config` 指令允许您设置各种配置选项，以确定文档解析的处理方式。由于页面是从上到下解析的，因此 `config` 指令应出现在 HTML 文档的顶部。可以使用此命令设置三种配置：

-   **errmsg**—设置解析文档过程中出错时返回给客户端的错误消息。默认消息是 [an error occurred while processing this directive]，但您可以使用此指令将消息设置为任何文本。例如：

```
<!--#config errmsg="[It's broken, dude]" -->
```

