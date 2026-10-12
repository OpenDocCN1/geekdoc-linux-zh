
指令用于描述可点击区域的布局以及它们所链接的 URL。

## mod_include

mod_include 允许在您的服务器上启用服务器端包含（SSI）。有关如何使用 SSI 的更多信息，请参阅本章后文的“动态内容”部分。

## mod_info 和 mod_log_config

mod_info 提供有关服务器配置的全面信息。例如，它会显示所有已安装的模块，以及配置文件中使用的所
有指令。

mod_log_config 定义了日志文件的显示方式。有关此主题的详细信息，请参阅“日志记录”部分。

## mod_mime 和 mod_mime_magic

mod_mime 模块试图通过文件的扩展名来确定其 MIME 类型。

mod_mime_magic 模块试图通过检查文件内容的片段来确定其 MIME 类型。

## mod_negotiation

使用 mod_negotiation 模块，您可以选择最适合客户端能力的几种文档版本之一。在协商过程中，有几种选项可以选择使用哪些标准。例如，您可以选择不同的语言、图形文件格式和压缩方法。

## mod_proxy

mod_proxy 为 Apache 服务器实现了代理和缓存功能。它可以代理和缓存 FTP、CONNECT、HTTP/0.9 以及 HTTP/1.0 请求。对于拥有大量用户因而对代理和缓存要求较高的网站来说，这不是一个理想的解决方案。然而，对于少量用户而言，它已经绰绰有余。

## mod_rewrite

mod_rewrite 是 URL 操作的多功能工具。它允许您使用强大的正则表达式对 URL 进行任何可以想象的操作。它提供了重写、重定向、代理等功能。使用此模块，几乎没有什么事情是你做不到的。

> **提示**
> 请参见 http://localhost/manual/misc/rewriteguide.html，这是一本食谱，详细解释了 .mod_rewrite 模块的功能。

## mod_setenvif

mod_setenvif 允许操作环境变量。通过使用被称为正则表达式的小型文本匹配代码片段，您可以有条件地更改环境变量的内容。配置文件中 SetEnvIf 指令出现的顺序很重要。当针对同一环境变量使用时，每个 SetEnvIf 指令都可以重置先前的 SetEnvIf 指令。在使用此模块中的指令时，请务必牢记这一点。

## mod_speling

mod_speling 用于启用对 URL 中轻微拼写错误的更正。如果没有任何文件匹配请求的 URL，该模块将构建请求目录中文件的列表，并提取最接近匹配的文件。它只尝试纠正一个拼写错误。

## mod_status

您可以使用 mod_status 创建一个包含正在运行的 Apache 服务器大量信息的网页。该页面包含内部状态信息以及有关正在运行的 Apache 进程的统计数据。当您试图将服务器配置为最高性能时，这将是一个巨大的辅助工具。它也是指示 Apache 服务器出现问题的良好指标。

## mod_ssl

mod_ssl 为 Apache 提供安全套接字层（版本 2 和 3）和传输层安全性（版本 1）支持。至少存在 30 个与加密选项和客户端授权相关的指令，并且可以与该模块一起使用。

## mod_unique_id

mod_unique_id 为每个传入请求生成一个唯一的请求标识符。此 ID 会被放入 UNIQUE_ID 环境变量中。

## mod_userdir

mod_userdir 模块允许将每个用户主目录中的子目录映射到您的 Web 树中。该模块提供了多种实现方式。

## mod_usertrack

mod_usertrack 用于为每个用户会话生成一个 cookie。这可以用于跟踪用户在您的 Web 树中的点击流。您必须启用自定义日志，以便将此 cookie 记录到日志文件中。

## mod_vhost_alias

mod_vhost_alias 支持动态配置的大规模虚拟主机托管，这对于拥有许多虚拟主机的互联网服务提供商（ISP）非常有用。然而，对于普通用户而言，Apache 的常规虚拟主机支持已经足够。

在 Apache 服务器上托管虚拟主机有两种方式。您可以拥有一个 IP 地址配合多个 CNAME，或者拥有多个 IP 地址，每个地址对应一个名称。Apache 拥有不同的指令集来处理这些选项中的每一种。（您将在本章的下一节中更多地了解 Apache 中的虚拟主机托管。）

再次说明，Apache 模块的可用选项和功能过多，无法在本章中完全描述。您可以在随 Fedora 提供的服务器在线文档或 Apache Group 的网站上找到有关 Apache 模块的完整信息。

# 虚拟主机托管

使用 Web 服务器提供的一项更受欢迎的服务是托管虚拟域。也称为*虚拟主机*，虚拟域是一个拥有自己域名的完整网站，好像它是一台独立机器一样，但它与托管在同一机器上的其他网站共享资源。Apache 通过 httpd.conf 配置文件中的指令以简单的方式实现了此功能。

Apache 现在可以通过使用本章前文所述的 *mod_vhost_alias* 模块动态托管虚拟服务器。该模块主要面向托管大量虚拟站点的 ISP 及类似大型网站。此模块面向更高级的用户，因此超出了本章入门内容的范围。相反，本节将专注于传统的虚拟服务器托管方式。

## 基于地址的虚拟主机

当您使用多个 IP 地址配置好 Linux 机器后，设置 Apache 以不同的网站身份提供这些服务就变得很简单了。您只需为希望使其成为独立网站的每个地址在 httpd.conf 文件中放入一个 `VirtualHost` 指令即可：

```
<VirtualHost 212.85.67.67>
ServerName gnulix.org
DocumentRoot /home/virtual/gnulix/public_html
TransferLog /home/virtual/gnulix/logs/access_log
ErrorLog /home/virtual/gnulix/logs/error_log
</VirtualHost>
```

在 `VirtualHost` 标签中，请使用 IP 地址，而不是主机名。

您可以在 `<VirtualHost>` 标签内指定任何配置指令。例如，您可能希望对虚拟主机设置与主服务器不同的 AllowOverrides 指令。任何未指定的指令都将默认使用主服务器的设置。

## 基于名称的虚拟主机

基于名称的虚拟主机允许您在同一 IP 地址上运行多个主机。您必须将这些名称添加到您的 DNS 中，作为相关机器的 CNAME。当 HTTP 客户端（Web 浏览器）向您的服务器请求文档时，它会随请求发送一个变量，指示其请求文档的服务器名称。基于此变量，服务器确定应从哪个虚拟主机提供内容。

> 注意
> 一些旧式浏览器无法识别基于名称的虚拟主机，因为这是 HTTP 1.1 的特性，而旧式浏览器严格遵循 HTTP 1.0 标准。然而，许多其他旧式浏览器部分支持 HTTP 1.1，而 HTTP 1.1 的这一部分也是大多数浏览器支持已久的功能。

基于名称的虚拟主机比基于 IP 地址的虚拟主机多一步。您必须首先指示哪个 IP 地址拥有多个 DNS 名称。这是通过 NameVirtualHost 指令完成的：

```
NameVirtualHost 212.85.67.67
```

然后，您需要为该地址上的每个名称创建一个部分，并设置该名称的配置。与基于 IP 的虚拟主机一样，您只需设置那些对于该主机必须不同的配置。您必须设置 ServerName 指令，因为它是区分一个主机与另一个主机的唯一标识：

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

> 提示
> 如果您在内网或内部网络上托管网站，用户很可能会使用机器的短名称而不是 FQDN（完全限定域名）。例如，用户可能在浏览器地址栏中输入 http://bugserver/index.html，而不是 http://bugserver.gnulix.org/index.html。在这种情况下，Apache 将无法识别这两个地址应该指向同一个虚拟主机。您可以通过为 bugserver 和

