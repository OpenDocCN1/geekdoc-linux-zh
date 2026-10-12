

# mod_imap

此模块用于服务器端处理图像映射文件。可点击区域在 `.map` 文件中定义。`.map` 文件中可用六个指令。这些指令用于描述可点击区域的布局及其指向的 URL。

# mod_include

此模块启用您服务器上的服务器端包含（SSI）。有关如何使用 SSI 的更多信息，请参阅本章后面的“动态内容”部分。

# mod_info

**mod_info** 模块提供有关您服务器配置的全面信息。例如，它将显示所有已安装的模块，以及配置文件中使用的全部指令。

# mod_log_agent

此模块允许您记录 HTTP 请求中 **UserAgent** 头的内容。利用这些信息，您可以查看访问您网站的访客正在使用哪些 Web 浏览器。

# mod_log_config

此模块允许您定义日志文件的外观。有关此主题的更多信息，请参阅“日志记录”部分。

# mod_log_referer

此模块允许您记录 HTTP 请求中的 referer 部分。

> **注意**
> 从 Apache 1.3.5 开始，此模块已被弃用。请改用 CustomLog 指令。有关 CustomLog 的更多信息，请参阅日志记录部分。

# mod_mime

此模块尝试根据文件的扩展名确定其 MIME 类型。

# mod_mime_magic

此模块尝试通过检查文件内容的部分来确定文件的 MIME 类型。

# mod_mmap_static

此模块使用 `mmap()` 函数将静态页面映射到系统内存中。这用于减少由磁盘访问引入的服务器延迟。由于这些页面缓存在系统内存中，如果磁盘上的页面被更新，则必须重新启动服务器。

> **注意**
> 此模块仍被视为实验性功能！

# mod_negotiation

使用此模块，可以选择最适合客户端能力的几个文档版本之一。有几个选项可用于选择协商过程中使用的标准。例如，您可以在不同的语言、图形文件格式和压缩方法中进行选择。

# mod_proxy

此模块为 Apache 服务器实现代理和缓存功能。它可以代理和缓存 FTP、CONNECT、HTTP/0.9 以及 HTTP/1.0 请求。对于拥有大量用户因此对代理和缓存要求非常高的网站来说，这并不是理想的解决方案。但对于少量用户而言，这已经足够充足。

# mod_put

此模块实现了 HTTP/1.1 协议中的 PUT 和 DELETE 方法。

> **注意**
> 由于此模块授予用户写入权限，您必须确保将写入权限仅限于受信任的用户！

这是 Red Hat 添加的第三方模块之一。这些模块通常不属于 Apache 发行版的一部分。

# mod_rewrite

这是 URL 操作的瑞士军刀。它允许您使用强大的正则表达式执行任何想象中的 URL 操作。它提供重写、重定向、代理等功能。使用此模块，您几乎无所不能。

请访问 http://localhost/manual/misc/rewriteguide.html 获取一本“食谱”，这将为您很好地概述此模块的功能。

# mod_setenvif

此模块允许您操作环境变量。使用正则表达式，可以有条件地更改环境变量的内容。SetEnvIf 指令在配置文件中出现的顺序很重要。如果在同一个环境变量上使用，每个 SetEnvIf 指令都可能会重置之前某个 SetEnvIf 指令。在使用此模块的指令时，请务必牢记这一点。

# mod_spelling

此模块自动更正 URL 中的轻微拼写错误。如果没有文件匹配请求的 URL，此模块将构建请求目录中文件列表，并提取最接近匹配的那些文件。它只尝试纠正一个拼写错误。

# mod_status

此模块创建一个包含大量运行中 Apache 服务器信息的 Web 页面。该页面将包含关于内部状态的信息以及关于运行中的 Apache 进程的统计数据。当您试图将服务器配置为最大性能时，这会是一个巨大的帮助。它也是指示 Apache 服务器出现异常的良好指标。

# mod_throttle

此模块为您提供限制传入请求的功能，以便当请求过多时服务器不会过载。您可以对指向特定用户资料或特定虚拟主机的请求进行限制。

您可以在 `http://www.snert.com/Software/Throttle/` 访问此模块的文档。
这是 Red Hat 添加的第三方模块之一。这些模块通常不属于 Apache 发行版的一部分。

# mod_unique_id

此模块为每个传入请求生成唯一的请求标识符。此 ID 将被放入 `UNIQUE_ID` 环境变量中。

# mod_userdir

此模块允许您将每个用户主目录中的子目录映射到您的 Web 树中。该模块提供了几种不同的实现方式。

# mod_usertrack

此模块为每个用户会话生成一个 cookie。这可用于跟踪用户在您 Web 树中的点击流。您需要启用自定义日志，将此 cookie 记录到日志文件中。

# mod_vhost_alias

此模块为动态配置的批量虚拟主机支持提供了出色的支持。对于拥有大量虚拟主机的 ISP（互联网服务提供商）特别有用。然而，对于普通用户而言，Apache 的普通虚拟主机支持应该已经足够。
在 Apache 服务器上托管虚拟主机有两种方式。您可以使用一个带有多个 CNAME 的 IP 地址，或者使用每个地址对应一个名称的多个 IP 地址。Apache 有不同的指令集来处理这些选项。

# 虚拟主机

使用 Web 服务器提供的更流行的服务之一是托管虚拟域名，也称为虚拟主机。这是一个拥有自己域名的完整网站，就像一台独立的机器一样，但它与其他网站托管在同一台机器上。Apache 通过 `httpd.conf` 配置文件中的指令以简单的方式实现了此功能。

最近添加了一种动态托管虚拟服务器的新方法。这是通过使用 `mod_vhost_alias` 模块启用的。该模块主要面向 ISP 和类似托管大量虚拟站点的大型网站。这是一个用于更高级用途的模块，因此超出了本章简介的范围。相反，本节专注于传统的托管虚拟服务器方式。

# 注意

> 有关在 Linux 机器上设置多个 IP 地址或为 Linux 机器赋予多个 CNAME 的信息，请参阅第 14 章“域名服务（DNS）和动态主机配置协议（DHCP）”。

# 基于地址的虚拟主机

一旦您配置了具有多个 IP 地址的 Linux 机器，将 Apache 设置为将它们作为不同的网站提供服务就变得非常简单。您只需在 httpd.conf 文件中为每个希望作为独立网站的地址添加一个 VirtualHost 指令即可：

```
<VirtualHost gnulix.org>
ServerName gnulix.org
DocumentRoot /home/virtual/gnulix/public.html
TransferLog /home/virtual/gnulix/logs/access_log
ErrorLog /home/virtual/gnulix/logs/error_log
</VirtualHost>
```

建议在 VirtualHost 标签中使用 IP 地址，而不是主机名。

您可以在 <VirtualHost> 标签内指定任何配置指令。例如，您可能希望为虚拟主机设置与主服务器不同的 AllowOverides 指令。任何未指定的指令默认使用主服务器的设置。

无法在 VirtualHost 部分中设置的指令包括 ServerType、StartServers、MaxSpareServers、MinSpareServers、MaxRequestsPerChild、BindAddress、Listen、PidFile、TypesConfig、ServerRoot 和 NameVirtualHost。

# 基于名称的虚拟主机

基于名称的虚拟主机允许您在同一个 IP 地址上运行多个主机。您需要将额外的名称作为相关机器的 CNAME 添加到您的 DNS 中。当 HTTP 客户端（Web 浏览器）向您的服务器请求文档时，它会随请求发送一个指示其请求文档的服务器名称的变量。基于此变量，服务器确定应从哪个虚拟主机提供内容。

