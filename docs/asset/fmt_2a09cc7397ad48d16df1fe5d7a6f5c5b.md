
在为 Linux 机器配置了多个 IP 地址后，将 Apache 设置为以不同网站的形式为其提供服务非常简单。你只需在`apache2.conf`文件中为每个要作为独立网站的地址放置一个`VirtualHost`指令：

```
<VirtualHost 212.85.67.67>
ServerName gnulix.org
DocumentRoot /home/virtual/gnulix/public_html
TransferLog /home/virtual/gnulix/logs/access_log
ErrorLog /home/virtual/gnulix/logs/error_log
</VirtualHost>
```

在`VirtualHost`标签中使用 IP 地址，而不是主机名。

你可以在`<VirtualHost>`标签内指定任何配置指令。例如，你可能希望为虚拟主机设置与主服务器不同的`AllowOverrides`指令。未指定的任何指令都默认为主服务器的设置。

## Name-Based Virtual Hosts

基于名称的虚拟主机使你能够在同一个 IP 地址上运行多个主机。你必须将名称添加到你的 DNS 中，作为相关机器的 CNAME。当 HTTP 客户端（Web 浏览器）从你的服务器请求文档时，它会随请求发送一个变量，指示其请求文档的服务器名称。服务器根据此变量确定应从哪个虚拟主机提供内容。

### NOTE

一些较旧的浏览器无法看到基于名称的虚拟主机，因为这是 HTTP 1.1 的功能，而较旧的浏览器严格遵循 HTTP 1.0。然而，许多其他较旧的浏览器是部分 HTTP 1.1 兼容的，而这正是大多数浏览器已经支持一段时间了的 HTTP 1.1 的一部分。

基于名称的虚拟主机只需要比基于 IP 地址的虚拟主机多一步。你必须首先指出哪个 IP 地址上有多重 DNS 名称。这是通过`NameVirtualHost`指令完成的：

```
NameVirtualHost 212.85.67.67
```

然后你必须为该地址上的每个名称设置一个部分，为该名称设置配置。与基于 IP 的虚拟主机一样，你只需要设置对主机不同的配置。你必须设置`ServerName`指令，因为它是区分一个主机与另一个主机的唯一因素：

```
<VirtualHost 212.85.67.67>
ServerName bugserver.gnulix.org
ServerAlias bugserver
DocumentRoot /home/bugserver/htdocs
ScriptAlias /home/bugserver/cgi-bin
TransferLog /home/bugserver/logs/access_log
</VirtualHost>
```

```
<VirtualHost 212.85.67.67>
ServerName pts.gnulix.org
ServerAlias pts
DocumentRoot /home/pts/htdocs
ScriptAlias /home/pts/cgi-bin
TransferLog /home/pts/logs/access_log
ErrorLog /home/pts/logs/error_log
</VirtualHost>
```

#### TIP

如果你在局域网或内部网络上托管网站，用户可能会使用机器的简短名称而不是 FQDN。例如，用户可能会在浏览器位置字段中输入`http://bugserver/index.html`而不是`http://bugserver.gnulix.org/index.html`。在这种情况下，Apache 将无法识别这两个地址应指向同一个虚拟主机。你可以通过为`bugserver`和`bugserver.gnulix.org`都设置`VirtualHost`指令来解决这个问题，但简单的方法是使用`ServerAlias`指令，该指令列出了机器的所有有效别名：

```
ServerAlias bugserver
```

有关`VirtualHost`的更多信息，请参阅`http://localhost/manual`上的帮助系统。

## Logging

Apache 为你可能感兴趣的几乎任何 Web 访问信息提供日志记录。日志记录可以帮助

- 通过跟踪使用情况进行系统资源管理
- 通过记录不良 HTTP 请求进行入侵检测
- 通过记录处理请求时的错误进行诊断

当你运行 Apache 服务器时，会生成两个标准日志文件：`access_log`和`error_log`。它们位于`/var/log/apache2`目录下。（其他包括 SSL 日志`ssl_access_log`、`ssl_error_log`和`ssl_request_log`。）除了`error_log`之外（默认情况下只有`access_log`）的所有日志，其格式由`CustomLog`和`LogFormat`指令指定。这些指令出现在你的`apache2.conf`文件中。

可以使用`LogFormat`指令定义新的日志格式：

```
LogFormat "%h %l %u %t \"%r\" %>s %b" common
```

`common`日志格式是创建你自己的自定义日志格式的良好起点。请注意，大多数可用的日志分析工具假定你使用的是`common`日志格式或`combined`日志格式——两者都在默认配置文件中定义。

以下变量可用于`LogFormat`语句：

- `%a` 远程 IP 地址。
- `%A` 本地 IP 地址。
- `%b` 发送的字节数，不包括 HTTP 头。这显示在 Apache 的联合日志格式（CLF）中。对于没有数据内容的请求，会显示`-`而不是`0`。
- `%B` 发送的字节数，不包括 HTTP 头。
- `%{VARIABLE}e` 环境变量`VARIABLE`的内容。
- `%f` 输出日志的文件名。
- `%h` 远程主机。
- `%H` 请求协议。
- `%{HEADER}i` `HEADER`的内容；发送到服务器的请求中的`HEADER`头行。
- `%l` 远程日志名称（来自`identd`，如果提供）。
- `%m` 请求方法。
- `%{NOTE}n` 来自另一个模块的 note `NOTE`的内容。
- `%{HEADER}o` `HEADER`的内容；回复中的`HEADER`头行。
- `%p` 为请求提供服务的服务器的规范端口。
- `%P` 为请求提供服务的子进程的进程 ID。
- `%q` 查询字符串的内容，以`?`字符开头。如果没有查询字符串，则求值为一个空字符串。
- `%r` 请求的第一行。
- `%s` 状态。对于内部重定向的请求，这是原始请求的状态——`%>s`为最后一次。
- `%t` 时间，采用通用日志时间格式。
- `%{format}t` 时间，采用`format`给出的日志形式，`format`应为`strftime(3)`格式。有关可用格式化选项的完整列表，请参阅本章后面“Basic SSI Directives”部分。
- `%T` 为请求提供服务所花费的秒数。
- `%u` 来自 auth 的远程用户；如果返回状态（`%s`）为 401，则可能为假。
- `%U` 请求的 URL 路径。
- `%v` 根据`UseCanonicalName`指令的服务器名称。
- `%V` 为请求提供服务的服务器的规范`ServerName`。

你可以在每个变量前加上一个条件，以确定是否显示该变量。如果变量未显示，则显示`-`。这些条件采用数值返回值的列表形式。例如，`%!401u`在返回代码为 401 时除外，否则显示`REMOTE_USER`的值。

然后你可以使用`CustomLog`指令指定日志文件的位置和格式：

```
CustomLog logs/access_log common
```

如果未指定为绝对路径，则假定日志文件的位置相对于`ServerRoot`。

## Other Web Servers for Use with Ubuntu

要确定最适合你使用的 Web 服务器，请考虑你管理的网站的需求。它是否需要强大的安全性（用于电子商务）、多媒体（音乐、视频和图片），或轻松下载文件的能力？你愿意为软件花费多少钱？你需要易于维护和故障排除的软件，还是包含技术支持的软件？这些问题的答案可能会引导你选择除 Apache 之外的其他方案。

以下各节列出了一些比使用 Apache 作为 Web 服务器更受欢迎的替代方案。

### Sun ONE Web Server
