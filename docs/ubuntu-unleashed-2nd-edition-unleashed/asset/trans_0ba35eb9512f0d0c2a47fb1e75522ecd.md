

## mod_usertrack

mod_usertrack 用于为每个用户会话生成一个 cookie。 这可用于跟踪用户在你的网站树内的点击流。 你必须启用一个自定义日志，将此 cookie 记录到日志文件中。

## mod_vhost_alias

mod_vhost_alias 支持动态配置的大规模虚拟主机托管，这对于拥有大量虚拟主机的互联网服务提供商（ISPs）很有用。 然而，对于普通用户来说，Apache 的普通虚拟主机支持应该已经足够了。

在 Apache 服务器上托管虚拟主机有两种方式。 你可以有一个 IP 地址配多个 CNAME，也可以有多个 IP 地址，每个地址一个名称。 Apache 有不同的指令集来处理这两种选项。 （你将在本章下一节中了解有关 Apache 中虚拟主机的更多信息。）

再次说明，本章无法完整描述 Apache 模块的可用选项和功能。 你可以在 Ubuntu 附带的服务器在线文档中或 Apache 组的网站上找到有关 Apache 模块的完整信息。

## Virtual Hosting

使用 Web 服务器提供的最受欢迎的服务之一是托管虚拟域。 也称为虚拟主机，虚拟域是一个拥有自己域名、仿佛是独立机器的完整网站，但它托管在与其他网站相同的机器上。 Apache 通过 apache2.conf 配置文件中的指令以简单的方式实现了此功能。

Apache 现在可以通过上一节中提到的 mod_vhost_alias 模块动态托管虚拟服务器。 该模块主要面向 ISP 和类似的大型站点，这些站点托管大量虚拟站点。 该模块面向更高级的用户，因此超出了本入门章节的范围。 相反，本节集中于托管虚拟服务器的传统方式。

## Address-Based Virtual Hosts

在为 Linux 机器配置了多个 IP 地址后，将 Apache 设置为以不同网站的形式提供服务就很简单了。 你只需在 apache2.conf 文件中为每个要作为独立网站的地址放置一个 VirtualHost 指令即可：

```
<VirtualHost 212.85.67.67>
ServerName gnulix.org
DocumentRoot /home/virtual/gnulix/public_html
TransferLog /home/virtual/gnulix/logs/access_log
ErrorLog /home/virtual/gnulix/logs/error_log
</VirtualHost>
```

在 VirtualHost 标签中使用 IP 地址，而不是主机名。

你可以在 <VirtualHost> 标签内指定任何配置指令。 例如，你可能希望为虚拟主机设置与主服务器不同的 AllowOverrides 指令。 未指定的任何指令都默认为主服务器的设置。

## Name-Based Virtual Hosts

基于名称的虚拟主机使你能够在同一个 IP 地址上运行多个主机。 你必须将名称添加到你的 DNS 中，作为相关机器的 CNAME。 当 HTTP 客户端（Web 浏览器）向你的服务器请求文档时，它会随请求发送一个变量，指示其请求文档的服务器名称。 服务器根据此变量确定应从哪个虚拟主机提供内容。

> **NOTE**
> 一些较旧的浏览器无法看到基于名称的虚拟主机，因为这是 HTTP 1.1 的功能，而较旧的浏览器严格遵守 HTTP 1.0。 然而，许多其他较旧的浏览器部分兼容 HTTP 1.1，而这正是 HTTP 1.1 中大多数浏览器已支持一段时间的功能之一。

基于名称的虚拟主机只需要比基于 IP 地址的虚拟主机多一步。 你必须首先指示哪个 IP 地址具有多个 DNS 名称。 这是通过 NameVirtualHost 指令完成的：

```
NameVirtualHost 212.85.67.67
```

然后你必须为该地址上的每个名称设置一个部分，为该名称设置配置。 与基于 IP 的虚拟主机一样，你只需设置与主机不同的配置即可。 你必须设置 ServerName 指令，因为它是区分一个主机与另一个主机的唯一因素：

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
```

