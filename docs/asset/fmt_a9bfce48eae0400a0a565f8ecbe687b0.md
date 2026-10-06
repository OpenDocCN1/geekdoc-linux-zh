
`mod_autoindex` 模块动态创建目录列表。列表将以用户友好的方式渲染，类似于 ftp 内置 ls 命令提供的列表。

## `mod_cgi`

`mod_cgi` 允许在服务器上执行 CGI 程序。CGI 程序是位于 `/var/www/cgi-bin` 目录的可执行文件，用于为远程浏览器动态生成数据（通常是 HTML）。

## `mod_dir` and `mod_env`

`mod_dir` 用于确定用户尝试访问目录时自动返回的文件。默认是 `index.html`。如果你的用户在 Windows 系统上创建 Web 页，你可能还想包含 `index.htm`，如下：

```
Directory index.html index.htm
```

`mod_env` 控制环境变量如何传递给 CGI 和 SSI 脚本。

## `mod_expires`

`mod_expires` 通过向 HTTP 响应添加 `Expires` 标头为网站内容添加过期日期。浏览器或缓存服务器将不再缓存内容。

## `mod_headers`

`mod_headers` 用于处理服务器响应的 HTTP 标头。你可以根据需要替换、添加或删除标头。该模块提供了 `Header` 指令来实现。`Header` 指令的顺序非常重要。对于同一个 HTTP 标头，`set` 后面跟着 `unset` 将完全删除该标头。你可以在配置文件的任何位置放置 `Header` 指令。这些指令按以下顺序处理：

+ 1. 核心服务器
+ 2. 虚拟主机
- 3. `<Directory>` 和 `.htaccess`
- 4. `<Location>`
- 5. `<Files>`

# `mod_imap`

`mod_imap` 模块提供了在服务器端处理 imagemap 文件的功能。可点击区域定义在 `.map` 文件中。`.map` 文件共有六个指令可供使用。这些指令用于描述可点击区域的布局以及它们指向的 URL。

# `mod_include`

`mod_include` 允许在你的服务器上使用服务端包含（SSI）。关于如何使用 SSI 的更多信息，请参阅章节后面的“动态内容”部分。

# `mod_info` and `mod_log_config`

`mod_info` 提供有关你服务器配置的全面信息。例如，它将显示所有已安装的模块以及配置文件中使用的所有指令。

`mod_log_config` 定义了日志文件的格式。有关该主题的更多信息，请参阅“日志”部分。

# `mod_mime` and `mod_mime_magic`

`mod_mime` 模块尝试根据文件的扩展名确定其 MIME 类型。

`mod_mime_magic` 模块尝试通过检查内容部分来确定文件的 MIME 类型。

# `mod_negotiation`

使用 `mod_negotiation` 模块，可以选择最适合客户端能力的多个文档版本之一。有多个选项可以选择在协商过程中使用哪些标准。例如，你可以在不同的语言、图形格式和压缩方法之间进行选择。

# `mod_proxy`

`mod_proxy` 为 Apache 服务器实现了代理缓存功能。它可以代理并缓存 FTP、CONNECT、HTTP/0.9 和 HTTP/1.0 请求。对于拥有大量用户且对代理和缓存要求极高的网站来说，这并不是理想的解决方案。然而，对于少数用户来说，它是绰绰有余。

# `mod_rewrite`

`mod_rewrite` 是 URL 操作的“瑞士军刀”。它允许你使用强大的正则表达式对 URL 进行任何难以想象的操控。它提供了重写、重定向、代理等功能。使用此模块几乎没有什么是你无法完成的。

> 提示
> 请访问 `http://localhost/manual/misc/rewriteguide.html` 查看食谱，它将为你详细解释 `.mod_rewrite` 模块的能力。

# `mod_setenvif`

`mod_setenvif` 允许操作环境变量。使用正则表达式，可以条件地更改环境变量的内容。`SetEnvIf` 指令在配置文件中出现的顺序非常重要。在同一个环境变量上使用时，每个 `SetEnvIf` 指令可能会重置早前的 `SetEnvIf` 指令。在使用此模块的指令时，务必记住这一点。

# `mod_spelling`

`mod_spelling` 用于修正 URL 中的轻微拼写错误。如果没有文件匹配请求的 URL，此模块将构建请求目录中的文件列表，并提取出最匹配的文件。它只会尝试纠正一个拼写错误。

# `mod_status`

你可以使用 `mod_status` 创建一个包含大量运行中 Apache 服务器信息的 Web 页面。该页面将包含内部状态信息以及运行中的 Apache 进程的统计数据。当你尝试配置服务器以获得最大性能时，这是一个非常大的帮助。它也是判断 Apache 服务器何时出现问题的良好指标。

# `mod_ssl`

`mod_ssl` 为 Apache 提供安全套接层（版本 2 和 3）和传输层安全（版本 1）支持。至少有 30 个处理加密选项和客户端授权的指令可以与此模块配合。

# `mod_unique_id`

`mod_unique_id` 为每个入站请求生成唯一的请求标识符。此标识符将被放入 `UNIQUE_ID` 环境变量中。

# `mod_userdir`

`mod_userdir` 允许将每个用户主目录下的子目录映射到你的 Web 树。该模块提供了多种实现此点的方法。

# `mod_usertrack`

`mod_usertrack` 用于为用户会话生成 cookie。这可以跟踪用户在 Web 树内的点击流。你必须启用自定义日志将此 cookie 记录到日志文件中。

# `mod_vhost_alias`

`mod_vhost_alias` 支持动态配置的大批量虚拟主机，这对于拥有许多虚拟主机的服务提供商非常有用。然而，对于普通用户来说，Apache 普通的虚拟主机支持已经完全足够了。

在 Apache 服务器上托管虚拟主机有两种方法。你可以拥有一个带有多个 CNAME 的 IP 地址，也可以拥有多个 IP 地址且每个地址一个名称。Apache 有若干指令来处理这些每个选项。（你将在本章的下一节学习更多关于 Apache 虚拟主机的知识）。

再次，Apache 模块的可用选项和功能多到无法在本章中完全描述。你可以在 Fedora 随附的服务器在线文档或 Apache 组的网站上找到关于 Apache 模块的完整信息。

# 虚拟主机

Web 服务器提供的最流行的服务之一是托管虚拟域名。虚拟域名也被称为虚拟主机，是一个具有自己域名的完整网站，就像是一台独立的机器一样，但它托管在与其他网站相同的物理机器上。Apache 通过 `httpd.conf` 配置文件中的指令以简单的方式实现了这一功能。

Apache 现在通过你在本章上一节中读到的 `mod_vhost_alias` 模块动态托管虚拟服务器。该模块主要用于 ISP 以及托管大量虚拟站的类似站点。

# 基于地址的虚拟主机

在你为 Linux 机器配置了多个地址后，设置 Apache 服务这些地址非常简单。你只需要为每个想要独立的地址在 `httpd.conf` 文件中放置 `VirtualHost` 指令即可：

```apache
<VirtualHost 212.85.67>
ServerName gnulix.org
DocumentRoot /home/virtual/public_html
CustomLog logs/access_log
ErrorLog logs/error_log
</VirtualHost>
```

在 `<VirtualHost>` 标签中使用 IP 地址而不是主机名。你可以在 `<VirtualHost>` 标签内指定任何配置指令。例如，你可能为虚拟主机设置与主服务器不同的 `AllowOverrides`。任何未指定的指令将默认使用主服务器的设置。

# 基于名称的虚拟主机

基于名称的虚拟主机允许你在同一个 IP 地址上运行多个主机。你必须将额外的名称添加到相关机器的 DNS CNAME 中。当 HTTP 客户端（浏览器）向你的服务器请求文档时，它会发送指示请求文档的服务器名称变量。根据此变量，服务器确定应该提供哪个虚拟主机。

> 注意
> 某些旧浏览器无法查看基于名称的虚拟主机，因为这是 HTTP 1.1 的功能，而旧浏览器严格遵守 HTTP 1.0 标准。然而，许多其他旧浏览器部分兼容 HTTP 1.1，而这是 HTTP 1.1 中大多数浏览器支持了一段时间的部分。

基于名称的虚拟主机比基于地址的虚拟主机多了一个步骤。你必须首先指示哪个 IP 地址拥有多个 DNS 名称。这是通过 `NameVirtualHost` 指令完成的：

```apache
NameVirtualHost 212.85.67
```

然后你必须为该地址上的每个名称设置部分，设置该名称的配置。与基于 IP 的虚拟主机一样，你只需要设置必须与主机不同的配置。你必须设置 `ServerName` 指令，因为它是区分不同主机的唯一依据。

## 第16 章 Apache Web 服务器管理

`ScriptAlias /home/bugserver/cgi-bin`

`TransferLog /home/bugserver/logs/access_log`

`<VirtualHost>`

```
<VirtualHost 212.85.67>
ServerName pts.gnulix.org
ServerAlias pts
DocumentRoot /home/pts/htdocs
ScriptAlias /home/pts/cgi-bin
TransferLog /home/pts/logs/access_log
ErrorLog /home/pts/logs/error_log
</VirtualHost>
```

> 如果你在局域网或内部网络上托管网站，那么用户很有可能会使用机器的短名称而不是完全限定域名名。例如，用户在浏览器的地址栏中输入 `http://bugserver/index.html` 而不是 `http://bugserver.gnulix.org/index.html`。在这种情况下，Apache 将无法识别出这两个地址应该指向同一个虚拟主机。你可以通过为 `bugserver` 和 `bugserver.gnulix.org` 分设置 `VirtualHost` 指令来实现这一点，但简单的方法是使用 `ServerAlias` 指令，它列出了该机器的所有别名：

`ServerAlias bugserver`

有关 `VirtualHost` 的更多信息，请参阅 `http://localhost/_manual` 上的帮助系统。

## 日志（Logging）

Apache 提供了你可能感兴趣的任何 Web 访问信息的记录功能。记录可以帮助你：

- 通过跟踪使用情况进行系统资源管理
- 通过记录恶劣的 HTTP 请求进行入侵检测
- 通过记录处理请求过程中的错误进行诊断

当你运行 Apache 服务器时，会生成两个标准日志文件：`access_log` 和 `error_log`。它们可以在 `/var/log/httpd` 目录下找到。（其他还包括 SSL 日志 `ssl_access_log`、`ssl_error_log` 和 `ssl_request_log`。）除了 `error_log` （在默认情况下，它是 `access_log`）之外，所有日志都是按照 `CustomLog` 和 `LogFormat` 指令指定的格式生成的。这些指令出现在你的 `httpd.conf` 文件中。

可以使用 `LogFormat` 指令定义新的日志格式：

## `LogFormat %h %u %t "%r* %>s %b" common`

常用日志格式是创建你自定义日志格式的良好起点。请注意，大多数可用的日志分析工具都假设你使用的是常用日志格式或组合日志格式——这两种格式都在默认配置文件中定义。

以下变量用于 `LogFormat` 语句可用：

- `%a` 远程 IP 地址。
- `%A` 本地 IP 地址。
- `%b` 发送的字节数，不包含 HTTP 头。显示在 Apache 的组合日志格式 (CLF) 中。对于没有任何数据内容的请求，将显示 `-` 而不是 `0`。
- `%B` 发送的字节数，不包含 HTTP 头。
- `%{VARIABLE}e` 环境变量 `VARIABLE` 的内容。
- `%f` 输出日志的文件名。
- `%h` 远程主机。
- `%H` 请求协议。
- `%{HEADER}i` `HEADER` 的内容；发送到服务器的请求中的 `HEADER` 头部（行）。
- `%l` 远程日志名（如果提供了 identd）。
- `%m` 请求方法。
- `%{NOTE}n` 来自另一个模块的 note `NOTE` 内容。
- `%{HEADER}o` `HEADER` 的内容；响应中的 `HEADER` 头部（行）。
- `%p` 提供请求服务的服务器的规范端口。
- `%P` 服务请求的子进程 ID（PID）。
- `%q` 查询字符串的内容，前面带有一个 `?` 字符。如果没有查询字符串，这将评估为空字符串。
- `%r` 请求的第一行。
- `%s` 状态。对于内部重定向的请求，最后一个显示为 `->%s`。
- `%t` 时间，常用日志时间格式。
- `%{format}t` 以 `format` 给出的格式的时间，该格式应为 `strftime(3)` 格式。请参阅本章节后面的“基本 SSI 指令”部分获取可用格式选项的完整列表。
- `%T` 服务请求消耗的秒数。
- `%U` 经认证的远程用户；如果返回状态 (`%s`) 为 `401`，则可能是伪造。
- `%U` 请求的 URL 路径。
- `%V` 根据 `UseCanonicalName` 指令的服务器名称。
- `%V` 提供请求服务的服务器的规范 `ServerName`。

你可以在每个变量前面放置一个条件，以确定该变量是否显示。如果变量未显示，则将显示 `-`。这些条件以数值返回值的列表形式存在。例如，`%!401u` 将在返回码不为 `401` 的情况下显示 `REMOTE_USER` 的值。

然后，你可以使用 `CustomLog` 指令指定日志文件的位置和格式：`CustomLog logs/access_log common`

如果未指定为绝对路径，则假设日志文件的位置相对于 `ServerRoot`。

## 动态内容（Dynamic Content）

在 网站上提供动态内容的常用方法是使用 CGI 程序。CGI 是服务器进程（例如生成动态文档的程序）与服务器之间通信的规范。SSI 允许将 CGI 程序或其他程序的输出插入到现有的 HTML 页面中。

为你的网站添加动态内容的另一种方法是使用 PHP（PHP Hypertext Preprocessor [该名称是递归的]）。PHP 是一种专门为 Web 使用设计的 HTML 嵌入式脚本语言。Apache 的 PHP 模块是最流行的第三方模块之一。

## CGI

默认情况下，你可以将任何 CGI 程序放在由 `ScriptAlias` 指令定义的服务器目录中。

CGI 程序可以使用任何语言编写。

CGI 程序可以使用任何语言编写。最流行的语言是 Perl 和 C。要使用 CGI，你必须为目录启用 `Execute` 选项。在 `httpd.conf` 中进行实现：

```
ExecCGI
```

要使用 CGI，你还必须为该扩展启用 `ScriptHandler`。在 `httpd.conf` 中进行实现：

```
AddHandler application/xd-cgi .cgi
```

如果你在使用 CGI，你必须确保文件是可执行的。可以使用 `chmod` 命令实现：

```bash
chmod 755 filename.cgi
```

## SSI

服务器包含（SSI）是直接写入 HTML 页面的指令，服务器在提供它们时会解析。SSI 可用于包含其他文件、程序输出或环境变量。

可以使用 `XBitHack` 指令启用 SSI。`XBitHack` 可以设置为 `on` 或 `off`，可以在你的配置文件或 `.htaccess` 文件中设置。如果 `XBitHack` 指令为 `on`，表示所有设置了用户位的文件都应该被解析 SSI。这有两个主要优势。其一是你不需要重命名文件并更改指向它的链接，仅仅是为了向其添加一点动态内容。另一个原因是外观上的：查看内容的用户无法通过文件名判断你正在动态生成页面，这让你的网站看起来更高端。

使用 `XBitHack` 的另一个积极副作用是它可以让你控制客户端如何缓存页面。包含 SSI 语句的页面不一定包含 `Last-modified` 头部。因此，它们不会被代理或浏览器缓存。如果你启用了 `XBitHack`，文件的组执行位将控制是否生成 `Last-modified` 头部。它将与文件的修改时间相同。确保只在确实需要的文件上使用它。

启用 SSI 的另一种方法是指定具有特定文件名扩展（通常为 `.html`）的文件在提供时由服务器解析。这是通过你的 `httpd.conf` 文件中的以下行实现的：

```
# 使用服务器解析的 HTML 文件
#
AddType text/html .html
AddHandler server-parsed .html
```

如果你注释掉这些指令（即 `AddType` 和 `AddHandler`），将告诉服务器解析 `.html` 文件中的 SSI 指令。

除了这些指令外，必须在允许 SSI 的目录中指定以下指令：

`Options Includes`

这可以在服务器配置文件或 `.htaccess` 文件中设置。

## 基本 SSI 指令

SSI 指令看起来像 HTML 注释标签。语法如下：

```
<!--#element attribute=value attribute=value ... -->
```

该元素可以是以下几个指令之一，包括：

- `config`
- `echo`
- `exec`
- `fsize`
- `lastmod`
- `include`
- `printenv`
- `set`

接下来的章节描述了这些指令中的每一个及其用法。

## `config`

`config` 指令允许你设置各种配置选项，以确定如何处理文档解析。由于页面是从上到下解析的，`config` 指令应该出现在 HTML 文档的顶部。通过此命令可以设置三个配置：

- **`errmsg`**—设置当解析文档时出现问题时返回给客户端的错误消息。默认消息为[处理此指令时发生错误]，但你可以使用此指令将消息设置为任何文本。例如：

```html
<!--#config errmsg='It's broken, dude' -->
```

- **`sizefmt`**—设置用于显示文件大小的格式。你可以将值设置为 `bytes` 以以字节显示精确的文件大小，或设置为 `abbr` 以以 KB 或 MB 显示大小。例如：
