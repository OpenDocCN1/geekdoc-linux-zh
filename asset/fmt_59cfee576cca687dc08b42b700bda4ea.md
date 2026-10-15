
一些旧版浏览器无法识别基于名称的虚拟主机，因为这是 HTTP 1.1 的功能，而那些旧浏览器严格遵守 HTTP 1.0 标准。然而，许多其他旧浏览器部分兼容 HTTP 1.1，而这是 HTTP 1.1 中大多数浏览器已支持了一段时间的部分。

基于名称的虚拟主机比基于 IP 地址的虚拟主机多出一个步骤。您首先需要指示哪个 IP 地址拥有多个 DNS 名称。这是通过 `NameVirtualHost` 指令完成的。

```
NameVirtualHost 192.101.204.24
```

然后，您需要为该地址上的每个名称设置一个节，并为该名称设置配置。与基于 IP 的虚拟主机一样，您只需要设置那些对主机来说不同的配置。您必须使用 `Server` 指令，因为这是区分一个主机与另一个主机的唯一因素：

```
<VirtualHost 192.101.204.24>
ServerName bugserver.databam.com
ServerAlias bugserver
DocumentRoot /home/bugserver/htdocs
ScriptAlias /home/bugserver/cgi-bin
TransferLog /home/bugserver/logs/access_log
</VirtualHost>
```

```
<VirtualHost 192.101.204.24>
ServerName pts.databam.com
ServerAlias pts
DocumentRoot /home/pts/htdocs
ScriptAlias /home/pts/cgi-bin
TransferLog /home/pts/logs/access_log
ErrorLog /home/pts/logs/error_log
</VirtualHost>
```

> 提示

如果您在内网中托管网站，日志格式可能会显示主机的短名而不是限定域名名。通过设置 `ServerAlias` 指令可以避免这个问题：

`ServerAlias bugserver`

## 注意

如果您计划在您的系统上运行大量虚拟主机，应考虑将所有信息发送到标准日志文件而不是单独文件，因为您可能会达到文件描述符限制（通常为 64 个进程）。

# 日志

Apache 提供了记录您可能感兴趣的任何信息。服务器运行时会生成两个标准文件：`access_log` 和 `error_log`。您可以使用 `CustomLog` 指令指定日志文件的位置和格式：

```
CustomLog logs/access_log common
```

如果没有指定绝对路径，则日志文件的位置假设相对于 `ServerRoot`。常用日志格式是创建自定义格式的起点。

以下变量适用于 `LogFormat`：

- `%a`：远程 IP 地址。
- `%HEADER}i`：发送到服务器的请求头部行内容。
- `%l`：远程日志名（来自 ident，如果提供）。
- `%NOTE}n`：来自另一个模块的 Note 内容。
- `%HEADER}o`：响应的头部行内容。
- `%p`：提供请求的服务器规范端口。
- `%P`：处理请求的子进程 ID。
- `%r`：请求的第一行。
- `%s`：状态。对于内部重定向的，这是原始请求的状态。
- `%t`：常用日志格式的时间。
- `%format}t`：按照 format 给出的时间，其格式应该是 `strftime(3)` 格式。
- `%T`：处理请求所需的时间，以秒为单位。
- `%u`：授权的远程用户；如果状态 `%s` 为 401，则可能是假的。
- `%U`：请求的 URL 路径。
- `%v`：提供请求的服务器规范 `ServerName`。

![](img/fbfff30e42d507bc7531108a281d6cf4_304_0.png)

在每个变量中，您可以放置一个条件来决定该变量是否显示。如果不显示，则将显示 `-`。这些条件以数值返回值的列表形式。例如，`%1401u` 在返回码为 401 的情况下将显示 `REMOTE_USER` 的值。

# CGI

默认情况下，你可以将任何 CGI 程序放在服务器上的 `ScriptAlias` 目录中。这些程序必须对运行服务器的用户具有可执行权限。这通常意味着你需要将文件模式更改为 755，以便 `nobody` 用户（服务器用户）可以执行它们。

```bash
chmod 755 program.cgi
```

为了在 `ScriptAlias` 目录之外执行 CGI 程序，你需要为该目录启用 `ExecCGI` 选项。这可以在你的 `httpd.conf` 文件（1.3.4 之前的版本为 `access.conf`）或目录下的 `.htaccess` 访问文件中完成。

CGI 程序可以使用任何语言编写。用于 CGI 编程的最流行的语言是 Perl 和 C。你可能想想找一本关于 CGI 编程的好书，例如《CGI Programming With Perl, Second Edition》，因为这本书并不是一本专门讲解 CGI 的书。

要测试你的 CGI 配置是否正确，请尝试以下用 Perl 编写的 CGI 程序，它会显示 HTTP 环境变量的值。

```perl
#!/usr/bin/perl
print "Content-type: text/html\n";
print "<html><head><title>Simple CGI program</title></head><body>\n";
for (keys %ENV) {
    print "$_ = $ENV{\$_}<br>\n";
}
print "</body></html>\n";
```

如果你打算用 Perl 编写 CGI 程序，你可能想查看 Perl 自带的 CGI 模块。

# SSI

服务器端包含（SSI）是直接写入 HTML 页面中的指令，当页面发送到 Web 客户端时，服务器会处理它们。它们可以用于包含其他文件、程序的输出或环境变量。

启用 SSI 最常见的方法是指定具有特定扩展名（通常为 `.shtml`）的文件在提供时由服务器解析。这通过你的 `httpd.conf` 文件（1.3.4 之前的版本为 `srm.conf`）中的以下行实现：

```apache
# To use server-parsed HTML files
#
#AddType text/html .shtml
#AddHandler server-parsed .shtml
```

## 配置服务

第二部分

通过取消 `AddType` 和 `AddHandler` 行的注释，你可以告诉服务器解析所有 `.shtml` 文件中的 SSI 指令。

另一种不常用但在我看来更好的 SSI 启用方法是使用 `XbitHack` 指令。`XbitHack` 可以设置为 `on` 或 `off`，并可以在你的配置文件或 `.htaccess` 文件中设置。如果 `XbitHack` 指令开启，则表示所有设置了用户可执行位的文件都应该被解析 SSI 指令。

这有两个主要优势。其一是是你不需要为了仅仅给文件添加一点动态内容，就重命名文件并更改所有指向该文件的文件链接。另一个原因更多是视觉上的——查看你 Web 内容的用户无法通过文件名判断出你正在动态生成页面，因此你的“魔术”会更令人印象深刻一点点。

除了这些指令外，在你想要允许 SSI 的目录中，必须指定以下指令：

```apache
Options Includes
```

这可以在服务器配置文件或 `.htaccess` 文件中设置。

# SSI 指令

SSI 指令看起来非常像 HTML 注释标签。其语法如下：

```html
<!--element attribute=value attribute=value -->
```

元素可以是以下之一：

| 元素 | 描述 |
| :--- | :--- |
| config | 这允许你设置有关如何处理文档解析的各种配置选项。由于页面是从上到下解析的，`config` 指令应该出现在 HTML 文档顶部。使用此命令可以设置三种配置： |
| errormsg | 设置当解析文档时出现问题时返回给客户端的错误消息。这通常是 [处理此指令时发生错误]，但可以使用此指令将其设置为任何内容。 |
| sizefmt | 设置用于显示文件大小的格式。你可以将值设置为 `bytes` 以以字节显示精确的文件大小，或设置为 `abbrev` 以 KB 或 MB 显示大小。 |

示例： `<!--#config errormsg='It's broken, dude!' -->`

示例： `<!--#config sizefmt='bytes' -->`

# Apache 服务器

第9章

`timefmt` 设置用于显示时间的格式。该值的格式与 C（以及 Perl）中用于显示日期的 `strftime` 函数格式相同，如下表所示。

| 格式 | 描述 |
| :--- | :--- |
| `%a` | 星期缩写。 |
| `%b` | 星期 |
| `%c` | 月份缩写。 |
| `%d` | 日期 |
| ctime format | Sat Nov 19 21:05:57 1994 |
| `%e` | 月份数字日期 |
