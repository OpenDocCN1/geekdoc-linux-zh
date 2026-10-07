
格式或结合日志格式（combined log format），两者都在默认配置文件中定义。

以下变量适用于 LogFormat 语句：

- %a 远程 IP 地址。
- %A 本地 IP 地址。
- %b 发送的字节数，不包含 HTTP 头部。这显示在 Apache 结合日志格式 (CLF) 中。对于没有任何数据内容的请求，将显示 - 为 0。
- %B 发送的字节数，不包含 HTTP 头部。
- %(VARIABLE)e 环境变量 VARIABLE 的内容。
- %f 输出日志的文件名。
- %h 远程主机。
- %H 请求协议。
- %(HEADER)i HEADER 的内容；发送到服务器的请求中的头部行。
- %l 远程日志（来自 ident，提供）。
- %m 请求方法。
- %(NOTE)n 来自另一个模块的注释内容。
- %(HEADER)o HEADER 的内容；响应中的头部行。
- %p 服务该请求的服务器规范端口。
- %P 服务该请求的子进程进程 ID。
- %q 查询字符串的内容，以 ? 字符开头。如果没有查询字符串，这将为空字符串。
- %r 请求的第一行。
- %s 状态。对于经过内部重定向的请求，这是原始请求的状态，最后一个显示为 %s。
- %t 时间，采用通用日志格式的时间。
- %(format)t 以 format 给定的格式的时间，应符合 strftime(3) 格式。请参阅本章后面的“基本 SSI 指令”部分获取可用格式选项的完整列表。
- %T 服务请求所需的秒数。
- %u 来自认证的远程用户；如果返回状态 (%s) 为 401，则可能为此值。
- %U 请求的 URL 路径。
- %V 根据 UseCanonicalName 指令指定的服务器名称。
- %v 服务该请求的服务器的规范 ServerName。

# 第16 章 Apache Web 服务器管理

你可以在每个变量前加上一个条件，以确定该变量是否显示。如果变量未显示，则将显示另一种内容。这些条件的形式为数值返回值的列表。例如，%140iu 将显示 REMOTE_USER 的值，除非返回代码为 401。

然后你可以使用 CustomLog 指令来指定日志文件的位置和格式：
CustomLog logs/access_log common

如果未指定为绝对路径，则假设日志文件的位置相对于 ServerRoot。

# 动态内容

在 Web 站点上提供动态内容的常用方法是使用 CGI 程序。CGI 是服务器进程（如生成动态文档的程序）与服务器之间通信的规范。SSL 允许将 CGI 程序或其他程序的输出插入到现有的 HTML 页面中。

为 Web 站点添加动态内容的另一种方法是使用 PHP（PHP 超文本预处理器 [名称是递归]）。PHP 是一种嵌入 HTML 的脚本语言，专为 Web 使用设计。Apache 的 PHP 模块是最流行的第三方模块之一。

# CGI

默认情况下，你可以将任何 CGI 程序存放在由 ScriptAlias 指令定义的服务器目录中。

CGI 程序可以使用任何语言编写。用于 CGI 编程最流行的语言是 Perl 和 C。第 23 章“使用 Perl”提供了关于使用 Perl 脚本语言的更多信息。

这些程序必须允许默认的 Apache 用户执行，这意味着你必须将文件模式更改 555，以便 Apache 用户可以执行它们。Apache 在 Red Hat Linux 中以名为 apache 的用户运行。

```
chmod 555 program.cgi
```

若要在 ScriptAlias 目录之外执行 CGI 程序，你必须为该目录启用 ExecCGI 选项。这可以在你的 httpd.conf 文件或目录下的 .htaccess 文件中完成。

为了测试是否配置正确，请尝试 16.1 中的 CGI。该程序用 Perl 编写，并显示环境变量的值。

# 16.1 环境

```perl
#!/usr/bin/perl -w

print <<EOF;
"Content-type: text/html"

<HTML>
<HEAD>
<TITLE>Simple CGI</TITLE>
</HEAD>
<BODY>
for (keys %ENV) {
    print "$_: $ENV{$}\n";
}
</BODY>
</HTML>
EOF
```
（注：16.1 的 OCR 文本损坏严重；我根据标准 Perl 对其进行了重建。）

这种格式与 C（和 Perl）中用于显示日期的 strftime 函数格式一致，如下文列表所示。

为你的 Web 站点添加动态内容的另一种方法是使用 PHP（PHP 超文本预处理器 [名称是递归]）。PHP 是一种嵌入 HTML 的脚本语言，专为 Web 使用设计。Apache 的 PHP 模块是最流行的第三方模块之一。

# SSI

服务器端包含（SSI）是指令。你可以通过指定特定的扩展名（通常为 .shtml）来启用 SSI，服务器将会解析。这可以在 httpd.conf 或 .htaccess 文件中通过以下行实现：

```
# 使用 SSI
AddType text/html .shtml
AddHandler parse .shtml
```

除了这些指令，必须对允许 SSI 的目录指定以下指令：

Options Includes
这可以在服务器配置或 .htaccess 文件中设置。

# 基本 SSI 指令

SSI 指令看起来像 HTML 注释标签。语法如下：

```
<--Element attribute=value -->
```

元素可以是指令之一，包括：

- config
- echo
- exec
- fsize
- lastmod
- include
- printenv
- set

config 指令允许你设置各种选项来确定如何处理文档解析。由于页面从上向下解析，config 指令应出现在 HTML 文档的顶部。可以使用此命令设置三种配置：

- errmsg 如果解析文档出错返回给客户端的错误消息。默认消息是 [处理此指令时发生错误]，但你可以使用此指令将消息设置为任何文本。

```
<--config errmsg="It's broken, dude" -->
```

- sizefmt 显示文件大小的格式。你可以将值设置为 bytes 以按字节显示精确的文件大小，或设置为 abbrev 以 KB 或 MB 显示大小。例如：

```
<--config sizefmt="bytes" -->
```

- timefmt 显示时间的格式。值的格式与 C（和 Perl）中用于显示日期的 str 函数格式相同，如下列表所示：

```
%% PERCENT
%a 周几缩写
%A 周几
%b 月份缩写
%B 月份
%c ctime 格式: Sat Nov 19 21:05:57 1994
%d 月中的数字
%e DD
```

