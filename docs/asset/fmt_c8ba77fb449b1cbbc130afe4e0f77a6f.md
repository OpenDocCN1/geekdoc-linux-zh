
在这里，检查 `HTTP_USER_AGENT` 变量以查看它是否包含字符串 MSIE（Microsoft Internet Explorer 浏览器使用的字符串）。如果包含此字符串，则将 `browser` 变量设置为 "IE"，并在当前文档中插入名为 `vbscript.html` 的文件。相反，如果 `HTTP_USER_AGENT` 不包含 MSIE 字符串，则假设它是另一个浏览器（Netscape Navigator），因此将 `browser` 变量设置为 "Navigator"，并在当前文档中插入 `javascript.html` 文件。通过使用 `if-then-else` 结构，此示例为同一个变量设置了不同的值并加载了不同的文件。

# 托管虚拟站点

为每个 Web 服务器提供多个 Web 站点几乎是高端 Web 服务器的一项基本功能。Apache 支持两种类型的虚拟主机——基于 IP 的虚拟主机和基于名称的虚拟主机。无论你选择实现哪种类型的虚拟主机，适当的域名系统服务（DNS）都是前提。基于 IP 的虚拟主机配置需要每个虚拟主机具有唯一的 IP 地址，而基于名称的虚拟主机是使用 CNAME 记录创建的。由于 DNS 在第10章（DNS 服务）中有详细介绍，我将在此不讨论 DNS 的细节。我假设你已经如何在 DNS 数据库中创建 A 或 CNAME 记录。

# 虚拟主机的 Apache 配置

你可以通过两种方式配置 Apache 以使其支持多个主机（主服务器和虚拟服务器）。你可以运行多个守护进程，以便每个主机都有一个独立的 `httpd` 守护进程；或者你可以运行单个守护进程，它支持所有虚拟主机和主服务器。第二种方法在大多数情况下被广泛使用并首选。因此我将讨论它。

第二种方法是使用配置文件中的 `vhost` 块。这允许单个 `httpd` 进程根据主机或 IP 地址响应多个请求。第二种方法在大多数情况下被广泛使用并首选。因此我将讨论它。（注：原文中此处存在大量重复段落，翻译时已根据要求进行精简处理）

# 第四部分：设置内网/互联网服务

## 基于 IP 的虚拟主机的 Apache 配置

在单个主 Apache 服务器配置中设置虚拟主机非常简单。你只需要为每个虚拟 IP 地址创建一个 `<VirtualHost>` 容器即可。例如，若要创建一个名为 `vhost1.domain.com` (`192.168.0.50`) 的虚拟主机，并将 `/www/vhost1/` 作为文档根目录（`DocumentRoot`），你需要在 `httpd.conf` 文件中添加以下行：

```
<VirtualHost 192.168.0.50>
DocumentRoot /www/vhost1
ServiceName vhost1.domain.com
</VirtualHost>
```

## 基于名称的虚拟主机 Apache 配置

设置基于名称的虚拟主机也非常容易。第一步是将 `NameVirtualHost` 指令设置为基于名称的虚拟机的 IP 地址。该指令指定了应作为基于名称的虚拟主机目标的 IP 地址。例如，假设你想在一个监听 IP 地址 `192.168.0.50` 的 Apache 服务器上设置两个虚拟主机：`www.client1.com` 和 `www.client2.com`。以下是此类设置的配置示例：

`NameVirtualHost 192.168.0.50`

```
<VirtualHost 192.168.0.50>
ServiceName www.client1.com
DocumentRoot /www/client1
</VirtualHost>
```

```
<VirtualHost 192.168.0.50>
ServiceName www.client2.com
DocumentRoot /www/client2
</VirtualHost>
```

对于使用该 IP 地址的所有基于名称的虚拟主机，每个 IP 地址只需要一个 `NameVirtualHost` 指令。当符合 HTTP/1.1 标准的浏览器向其中一个虚拟主机发送请求时，Apache 将 `ServerName` 与请求头中 `Host` 的主机名进行匹配。因此，Apache 能够确定请求的是哪个虚拟主机。

一旦你创建了 Apache 的虚拟主机配置，就可以启动（或重启）Apache 服务器使配置生效。此外，不要忘记在重启 Apache 服务器之前，创建你在虚拟主机配置中可能用到的任何目录。

从 Apache 1.3.x 开始，你可以通过使用 `-s` 选项运行 Apache 来验证你的虚拟主机配置。

# 使用 Apache 作为代理服务器

Apache 的代理支持来自 `mod_proxy` 模块。该模块默认未被编译。

## 编译代理模块

如果你使用 Apache 接口来编译和安装 Apache，那么在 Apache 源码发布目录下执行以下步骤来构建带有代理模块的新 Apache 可执行文件就非常简单：

- 如果你是第一次运行 `configure` 脚本，请输入以下命令：

```
./configure --prefix=/dir/where/you/want/to/install/apache \
--enable-mode=proxy
```

- 另一方面，如果你在编译 Apache 之前已经运行过 `configure` 脚本，请运行：

```
./config.status -enable-module=proxy
```

这样，你之前的配置选项将应用于创建一个新的配置文件。现在运行 `make` 命令，如果没有返回任何错误信息，则运行 `make install` 命令将新编译的 Apache 可执行文件安装到相应的目录中。

## 代理模块指令

Apache 的代理模块带有一组用于使用该模块的指令。所有这些指令在主服务器配置或任何虚拟服务器配置上下文中均可用。

### ProxyRequests on | off

此指令允许你启用或禁用缓存代理服务。然而，它不会影响 `ProxyPass` 指令的功能。默认值为 "off"。

### ProxyRemote match remote-proxy-server-URL

此指令允许你将代理服务器与另一个代理服务器建立接口。`match` 的值可以是 URL 方案的名称（http、ftp 等），也可以是部分 URL。

`remove-proxy-server-URL` 可以是 `http://remove-proxy-hostname:port`。注意，目前仅支持 HTTP 协议。换句话说，你只能指定处理 HTTP 协议的代理服务器；但你可以按照如下方式从你的代理服务器将 FTP 请求转发到同时支持 HTTP 和 FTP 协议的代理服务器：

`ProxyRemote ftp http://ftp.proxy.nitec.com:8000`

这将所有发送到本地代理服务器的 FTP 请求发送到 `ftp://ftp.proxy.nitec.com`。请求将通过 HTTP 发送，因此实际的 FTP 事务将在远程代理服务器上发生。

如果你只想将特定网站的所有代理请求直接转发到你的代理服务器，可以使用此指令实现。例如：

`ProxyRemote http://www.isp.com/ http://web-proxy.isp.com:8000`

这将所有匹配 `*.isp.com` 的请求发送到 `web-proxy.bigisp.com`。然而，如果你想将所有代理请求转发到另一个代理，可以使用星号作为匹配短语，例如：

`ProxyRemote * http://proxy.domain.com`

这将所有本地代理请求发送到 `proxy.domain.com` 代理服务器。

### ProxyPass relative-URL destination-URL

此指令允许你将 Web 服务器的文档树映射到你代理服务器的文档空间。例如：

`ProxyPass /internet/microsoft www.microsoft.com/`

在名为 `proxy nitec.com` 的代理服务器的 `httpd.conf` 文件中找到此指令，将允许代理用户访问 Microsoft 站点：

`ProxyPass /internet/microsoft`

这将允许 `www.microsoft.com` 站点用户通过 `/internet/microsoft` 访问 `nitec.com` 代理服务器。

### ProxyReverse relative-URL destination-URL

此指令在你使用 Apache 创建反向代理时非常有用。在反向代理设置中，此指令修复了 Location 头。例如：

```
<VirtualHost 192.168.0.50>
ServerName www.nitec.com
ProxyRequests on
ProxyPass / http://www.nitec.com/
ProxyReverse /
</VirtualHost>
```
