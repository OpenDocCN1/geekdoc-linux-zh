
`mod_env` 控制传递给 CGI 和 SSI 脚本的环境变量。

# `mod_expires`

`mod_expires` 用于通过向 HTTP 响应添加 `Expires` 标头为你的网站内容添加过期日期。浏览器和缓存服务器不会缓存内容。

# `mod_headers`

`mod_headers` 用于操作服务器的 HTTP 标头。你可以根据需要替换、添加或删除标头。该模块提供了 `Header` 指令来实现此。`Header` 指令的顺序非常重要。对于同一个 HTTP 标头，一个 `set` 后跟一个 `unset` 将完全删除该标头。你可以将 `Header` 指令放置在配置文件的任何位置。这些指令的处理顺序如下：

1. 核心服务器
2. 虚拟主机
3. `<Directory>`
4. `<Location>`
5. `<Files>`

# `mod_include`

`mod_include` 允许在服务器上使用服务器包含（SSI），这在 PHP 接管该部分市场之前非常流行。

# `mod_info` 和 `mod_log_config`

`mod_info` 提供有关你服务器配置的全面信息。例如，它会显示已安装的模块，以及配置文件中使用的指令。

`mod_log_config` 定义了日志文件的格式。关于此主题的更多信息，请参阅本章稍后的“日志（Logging）”部分。

# `mod_mime` 和 `mod_mime_magic`

`mod_mime` 模块尝试通过检查扩展名来确定文件的 MIME 类型。

`mod_mime_magic` 模块尝试通过检查文件内容的部分来确定文件的 MIME 类型。

# `mod_negotiation`

使用 `mod_negotiation` 模块，你可以从多个最适合客户端能力的文档版本中选择一个。有多个选项可以选择在协商过程中使用哪些标准。例如，你可以在不同的语言、图形文件格式和压缩方法之间进行选择。

# `mod_proxy`

`mod_proxy` 为 Apache 服务器实现了代理和缓存功能。它可以代理 FTP、CONNECT、HTTP/0.9 和 HTTP/1.0 请求。对于拥有大量用户因此对代理和缓存有高要求的网站来说，这不是一个理想的解决方案。然而，对于少数用户来说，它绰绰有余。

# `mod_rewrite`

`mod_rewrite` 是 URL 操作的“瑞士军军刀”。它允许你使用正则表达式对 URL 进行任何想象所及的操作。它提供了重写、重定向、代理等等功能。使用该模块几乎没有你无法完成的任务。

> 提示
> 如果你安装并运行了 Apache，请查看 `http://localhost/manual/misc/modrewrite.html` 获取菜谱指南，该指南将为你详细解释 `mod_rewrite` 模块的功能。

# `mod_setenvif`

`mod_setenvif` 允许操作环境变量。通过使用短小的文本匹配代码段作为正则表达式，你可以条件地更改环境变量的内容。`SetEnvIf` 指令在配置文件中出现的顺序非常重要。每个 `SetEnvIf` 指令都可以重置之前在同一环境变量上使用的早期 `SetEnvIf` 指令。在使用此模块的指令时，务必记住这一点。

# `mod_spelling`

`mod_spelling` 用于启用修正 URL 中的细微拼写错误。如果没有文件匹配请求的 URL，此模块将构建请求目录中的文件列表，并提取出最匹配的文件。它只尝试纠正一个拼写错误。

# `mod_status`

你可以使用 `mod_status` 创建一个网页，其中包含关于运行中的 Apache 服务器的海量信息。该页面包含了内部状态信息以及运行中的 Apache 进程的统计数据。当你尝试配置服务器以获得最大性能时，这是一个极大的帮助。它还可以作为你的 Apache 服务器何时出现问题的良好指标。

# `mod_ssl`

`mod_ssl` 为 Apache 提供了安全套接层（版本 2 和 3）和传输层安全（版本 1）支持。该模块至少有 30 个用于加密和客户端授权的指令选项可以使用。使用此模块要求你安装 OpenSSL 并生成购买证书。（这将在本章稍后的“HTTPS”部分介绍。）

# `mod_unique_id`

`mod_unique_id` 为每个入站请求生成唯一的请求标识符。此 ID 被置于 `UNIQUE_ID` 环境变量中。

# `mod_userdir`

`mod_userdir` 允许将每个用户 `/home` 目录下的子目录映射到你的 Web 树中。该模块提供了实现此点的几种方法。

# `mod_usertrack`

`mod_usertrack` 用于每个用户会话生成 cookie——例如，跟踪用户在你 Web 树内的点击流。你必须启用自定义日志，将此 cookie 记录到日志文件中。

# `mod_vhost_alias`

`mod_vhost_alias` 支持动态配置批量虚拟主机，这对于拥有许多虚拟主机的服务提供商（ISP）非常有用。然而，对于普通用户，Apache 普通的虚拟主机支持应该足够。

在 Apache 服务器上托管虚拟主机有两种方法。你可以拥有一个 IP 地址对应多个 CNAME，或者拥有多个 IP 地址对应一个名称地址。Apache 有不同的指令集来处理这些情况。（你将在本章的下一节学习更多关于 Apache 虚拟主机的知识。）

再次，Apache 模块的可用选项和功能太多，在本章中无法完全描述。你可以在 Ubuntu 自带的服务器在线文档或 Apache 项目网站上找到关于 Apache 模块的完整信息。

# 虚拟托管（Virtual Hosting）

Web 服务器提供的最流行的服务之一是托管虚拟域名。虚拟域名也被称为虚拟主机，是一个拥有自己独立域名的完整网站，就像一台独立的机器一样，但它与其他网站托管在同一台机器上。Apache 以一种简单的方式实现了这一功能，即通过 `apache2.conf` 配置文件中的指令。

Apache 现在可以使用你在本章上一节中读过的 `mod_vhost_alias` 模块动态托管虚拟服务器。该模块主要用于托管大量虚拟站的 ISP 和大型网站。此模块面向更高级的用户，因此超出了本介绍章节的范围。本节集中于托管虚拟服务器的传统方法。

## 基于地址的虚拟主机（Address-Based Virtual Hosts）

在你为 Linux 机器配置多个 IP 地址后，设置 Apache 将它们作为不同的网站提供是非常简单的。对于每个想要作为独立网站的地址，你只需要在 `apache2.conf` 文件中使用一个 `VirtualHost` 指令：

```
<VirtualHost 212.85.67.66>

ServerName example1.com

DocumentRoot /var/www/example1

</VirtualHost>

<VirtualHost 212.85.67.67>

ServerName example2.com

DocumentRoot /var/www/example2

</VirtualHost>
```

## 基于名的虚拟主机（Name-Based Virtual Hosts）

基于名的虚拟主机允许你在同一个 IP 地址上运行多个主机。当 HTTP 客户端（浏览器）向你的服务器请求文档时，它会发送一个指示服务器名称的变量。根据该变量，服务器确定提供哪个虚拟主机。

基于名的虚拟主机比基于地址的虚拟主机多需要一步。你必须首先标识哪个 IP 地址拥有名称。这是通过 `NameVirtualHost` 指令完成的：

```
NameVirtualHost 212.85.67.66
```

你必须为每个名称设置一个部分并为该名称设置配置。对于基于地址的主机，你只需要为主机设置配置。你必须设置 `ServerName` 指令，因为它是区分不同主唯一依据：

```
<VirtualHost 212.85.67.66>

ServerName example1.com

ServerAlias www.example1.com

DocumentRoot /var/www/example1

</VirtualHost>

<VirtualHost 212.85.67.67>

ServerName example2.com

ServerAlias www.example2.com

DocumentRoot /var/www/example2

</VirtualHost>
```
