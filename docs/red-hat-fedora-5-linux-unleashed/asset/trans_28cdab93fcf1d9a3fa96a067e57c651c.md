

# mod_setenvif

mod_setenvif 允许操作环境变量。使用被称为正则表达式的小段文本匹配代码，你可以有条件地改变环境变量的内容。SetEnvIf 指令在配置文件中出现的顺序很重要。当用于同一环境变量时，每个 SetEnvIf 指令都可以重置之前的 SetEnvIf 指令。在使用此模块的指令时，请务必牢记这一点。

# mod_speling

mod_speling 用于启用对 URL 中轻微拼写错误的纠正。如果没有文件与请求的 URL 匹配，此模块会构建请求目录中的文件列表，并提取最接近匹配的文件。它只尝试纠正一个拼写错误。

# mod_status

你可以使用 mod_status 创建一个包含大量关于正在运行的 Apache 服务器信息的网页。该页面包含内部状态信息以及关于正在运行的 Apache 进程的统计数据。当你试图将服务器配置为最大性能时，这可以是一个很大的帮助。它也是你检测 Apache 服务器是否出现问题的良好指示器。

# mod_ssl

mod_ssl 为 Apache 提供安全套接字层（版本 2 和 3）和传输层安全性（版本 1）支持。至少存在 30 个指令用于处理加密和客户端授权选项，并且可以与此模块一起使用。

# mod_unique_id

mod_unique_id 为每个传入请求生成唯一的请求标识符。该 ID 被放入 UNIQUE_ID 环境变量中。

# mod_userdir

mod_userdir 模块启用将每个用户主目录中的子目录映射到你的 Web 树中。该模块提供了几种实现此目的的方法。

# mod_usertrack

mod_usertrack 用于为每个用户会话生成一个 Cookie。这可用于跟踪用户在你的 Web 树内的点击流。你必须启用一个自定义日志，将此 Cookie 记录到日志文件中。

# mod_vhost_alias

mod_vhost_alias 支持动态配置的大规模虚拟主机，这对于拥有许多虚拟主机的互联网服务提供商（ISP）非常有用。然而，对于普通用户来说，Apache 的普通虚拟主机支持应该已经足够了。

在 Apache 服务器上托管虚拟主机有两种方式。你可以拥有一个 IP 地址和多个 CNAME，或者你可以拥有多个 IP 地址，每个地址对应一个名称。Apache 有不同的指令集来处理这些选项中的每一个。（你在本章的下一节中会了解更多关于 Apache 虚拟主机的知识。）

同样，Apache 模块的可用选项和功能太多，无法在本章中完全描述。你可以在 Fedora 附带的服务器在线文档或 Apache 软件基金会的网站上找到有关 Apache 模块的完整信息。

## 虚拟主机

Web 服务器提供的一项更流行的服务是托管虚拟域名。也称为*虚拟主机*，虚拟域名是一个具有自己域名的完整网站，就像它是一台独立的机器一样，但它与其他网站托管在同一台机器上。Apache 通过 `httpd.conf` 配置文件中的指令以简单的方式实现此功能。

Apache 现在可以使用你在本章前一小节中阅读过的 `mod_vhost_alias` 模块动态托管虚拟服务器。该模块主要面向托管大量虚拟站点的 ISP 和类似的大型站点。此模块面向更高级的用户，因此超出了本入门章节的范围。相反，本节专注于托管虚拟服务器的传统方式。

### 基于地址的虚拟主机

当你用多个 IP 地址配置了 Linux 机器后，设置 Apache 将它们作为不同的网站提供服务很简单。你只需要为每个你想要作为独立网站的地址在 `httpd.conf` 文件中放置一个 `VirtualHost` 指令：

```
<VirtualHost 212.85.67.67>
ServerName gnulix.org
DocumentRoot /home/virtual1/gnulix/public_html
TransferLog /home/virtual1/gnulix/logs/access_log
ErrorLog /home/virtual1/gnulix/logs/error_log
</VirtualHost>
```

在 `VirtualHost` 标签中使用 IP 地址，而不是主机名。

你可以在 <VirtualHost> 标签内指定任何配置指令。例如，你可能希望为虚拟主机设置不同于主服务器的 `AllowOverrides` 指令。任何未指定的指令都将默认为主服务器的设置。

### 基于名称的虚拟主机

基于名称的虚拟主机允许你在同一个 IP 地址上运行多个主机。你必须将这些名称作为目标机器的 CNAME 添加到你的 DNS 中。当 HTTP 客户端 Web 浏览器向你的服务器请求文档时，它会随请求发送一个变量，指示它正在从中请求文档的服务器名称。基于此变量，服务器确定应该从哪个虚拟主机提供内容。

> 注意
> 一些旧的浏览器无法看到基于名称的虚拟主机，因为这是 HTTP 1.1 的功能，而旧的浏览器严格符合 HTTP 1.0 标准。然而，许多其他旧浏览器部分符合 HTTP 1.1，而这是大多数浏览器已支持了一段时间的 HTTP 1.1 的一部分。

基于名称的虚拟主机比基于 IP 地址的虚拟主机多一步。你必须首先指示哪个 IP 地址拥有多个 DNS 名称。这是通过 `NameVirtualHost` 指令完成的：

```
NameVirtualHost 212.85.67.67
```

然后，你必须为该地址上的每个名称设置一个部分，以设置该名称的配置。与基于 IP 的虚拟主机一样，你只需要设置那些必须对主机不同的配置。你必须设置 `ServerName` 指令，因为这是区分一个主机和另一个主机的唯一方式：

```
<VirtualHost 212.85.67.67>
  ServerName bugserver.gnulix.org
  ServerAlias bugserver
  DocumentRoot /home/bugserver/htdocs
  ScriptAlias /home/bugserver/cgi-bin
  TransferLog /home/bugserver/logs/access_log
</VirtualHost>

<VirtualHost 212.85.67.67>
  ServerName pts.gnulix.org
  ServerAlias pts
  DocumentRoot /home/pts/htdocs
  ScriptAlias /home/pts/cgi-bin
  TransferLog /home/pts/logs/access_log
  ErrorLog /home/pts/logs/error_log
</VirtualHost>
```

**提示**

如果你在内网或内部网络上托管网站，用户很可能会使用机器的简写名称而不是 FQDN（完全限定域名）。例如，用户可能在浏览器地址栏中输入 http://bugserver/index.html，而不是 http://bugserver.gnulix.org/index.html。在这种情况下，Apache 不会认识到这两个地址应该去往同一个虚拟主机。你可以通过为 bugserver 和 bugserver.gnulix.org 都设置 VirtualHost 指令来绕过这一点，但简单的方法是使用权所有有效别名的 **ServerAlias** 指令：

```
ServerAlias bugserver
```

有关 **VirtualHost** 的更多信息，请参阅 http://localhost/_manual 上的帮助系统。

## 日志记录

Apache 几乎可以记录你可能感兴趣的任何 Web 访问信息。日志记录可以帮助：

- 通过跟踪使用量进行系统资源管理
- 通过记录不良 HTTP 请求进行入侵检测
- 通过记录处理请求中的错误进行诊断

运行 Apache 服务器时会生成两个标准日志文件：`access_log` 和 `error_log`。它们位于 `/var/log/httpd` 目录下。（其他包括 SSL 日志 `ssl_access_log`、`ssl_error_log` 和 `ssl_request_log`。）除 `error_log`（默认情况下，这只是 `access_log`）外的所有日志都以由 **CustomLog** 和 **LogFormat** 指令指定的格式生成。这些指令出现在你的 `httpd.conf` 文件中。

可以使用 **LogFormat** 指令定义新的日志格式：

```
LogFormat "%h %l %u %t "%r" %>s %b" common
```

通用日志格式是创建你自己定制日志格式的好起点。请注意，大多数可用的日志分析工具假设你使用的是通用日志格式或组合日志格式——两者都在默认配置文件中定义。

以下变量可用于 **LogFormat** 语句：

| 变量 | 描述 |
|---|---|
| `%a` | 远程 IP 地址。 |
| `%A` | 本地 IP 地址。 |
| `%b` | 发送的字节数，不包括 HTTP 头部。这在 Apache 的组合日志格式（CLF）中显示。对于没有数据内容的请求，显示 - 而不是 0。 |

