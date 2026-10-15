

当在同一个环境变量上使用时。请在使用本模块的指令时务必牢记这一点。

## mod_speling

mod_speling 用于启用对 URL 中轻微拼写错误的纠正。如果没有文件与请求的 URL 匹配，该模块会构建请求目录中的文件列表并提取最接近匹配的文件。它只尝试纠正一个拼写错误。

## mod_status

你可以使用 mod_status 创建一个包含有关正在运行的 Apache 服务器的丰富信息的网页。该页面包含有关内部状态的信息以及有关正在运行的 Apache 进程的统计信息。当你尝试为服务器配置最大性能时，这可以成为很好的帮助。它也是 Apache 服务器出现问题时很好的指示器。

## mod_ssl

mod_ssl 为 Apache 提供安全套接字层（版本 2 和 3）和传输层安全（版本 1）支持。至少有 30 条指令涉及加密选项和客户端授权，可以与此模块一起使用。

## mod_unique_id

mod_unique_id 为每个传入请求生成唯一的请求标识符。此 ID 会放入 UNIQUE_ID 环境变量中。

## mod_userdir

mod_userdir 模块可将每个用户主目录中的子目录映射到你的 Web 树中。该模块提供了几种实现此功能的方法。

## mod_usertrack

mod_usertrack 用于为每个用户会话生成 cookie。这可用于跟踪用户在你的 Web 树中的点击流。你必须启用一个自定义日志，将此 cookie 记录到日志文件中。

## mod_vhost_alias

mod_vhost_alias 支持动态配置的大规模虚拟主机托管，这对于拥有大量虚拟主机的互联网服务提供商（ISP）非常有用。然而，对于普通用户而言，Apache 的普通虚拟主机支持应该已经足够了。

在 Apache 服务器上托管虚拟主机有两种方式。你可以有一个 IP 地址配多个 CNAME，也可以有多个 IP 地址，每个地址一个名称。Apache 有不同的指令集来处理这两种选项中的每一种。 （你在本章下一节中将更多地了解 Apache 中的虚拟主机。）

再次，Apache 模块的可用选项和功能太多，无法在本章中完全描述。你可以在随 Ubuntu 提供的服务器在线文档中或 Apache 组的网站上找到有关 Apache 模块的完整信息。

## Virtual Hosting

提供 Web 服务器的最受欢迎的服务之一是托管虚拟域。也称为虚拟主机，虚拟域是一个拥有自己域名、仿佛是独立机器的完整网站，但它托管在与其他网站相同的机器上。Apache 通过 apache2.conf 配置文件中的指令以简单的方式实现了此功能。

Apache 现在可以通过你在本章前一节中阅读的 mod_vhost_alias 模块动态托管虚拟服务器。该模块主要面向 ISP 和类似的大型站点，这些站点托管大量虚拟站点。该模块面向更高级的用户，因此超出了本入门章节的范围。相反，本节集中于托管虚拟服务器的传统方式。

### Address-Based Virtual Hosts

在为 Linux 机器配置了多个 IP 地址后，将 Apache 设置为以不同网站的形式为其提供服务非常简单。你只需在 apache2.conf 文件中为每个要作为独立网站的地址放置一个 VirtualHost 指令：

```
<VirtualHost 212.85.67.67>
ServerName gnulix.org
DocumentRoot /home/virtual/gnulix/public_html
TransferLog /home/virtual/gnulix/logs/access_log
ErrorLog /home/virtual/gnulix/logs/error_log
</VirtualHost>
```

在 VirtualHost 标签中使用 IP 地址，而不是主机名。

你可以在 <VirtualHost> 标签内指定任何配置指令。例如，你可能希望为虚拟主机设置与主服务器不同的 AllowOverrides 指令。未指定的任何指令都默认为主服务器的设置。

### Name-Based Virtual Hosts

基于名称的虚拟主机使你能够在同一个 IP 地址上运行多个主机。你必须将名称添加到你的 DNS 中，作为相关机器的 CNAME。当 HTTP 客户端（Web 浏览器）从你的服务器请求文档时，它会随请求发送一个变量，指示其请求文档的服务器名称。服务器根据此变量确定应从哪个虚拟主机提供内容。

