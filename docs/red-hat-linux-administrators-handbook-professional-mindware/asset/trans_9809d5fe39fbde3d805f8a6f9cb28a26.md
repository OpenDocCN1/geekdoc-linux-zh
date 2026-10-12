

的 `<VirtualHost>`。因此，在配置虚拟主机时，你需要决定每个虚拟主机配置需要进行哪些更改。

指令要么覆盖主服务器中给出的配置，要么对其进行补充，具体取决于该指令。例如，`<VirtualHost>` 容器中的 DocumentRoot 指令会覆盖主服务器的 DocumentRoot，而 AddType 指令则会补充主服务器的 MIME 类型。

现在，当请求到达时，Apache 使用到达时的 IP 地址和端口来查找匹配的虚拟主机配置。如果没有虚拟主机匹配该地址和端口，则由主服务器配置处理。如果匹配某个虚拟主机地址，Apache 将使用该虚拟服务器的配置来处理请求。

在上一示例中，使用的虚拟主机配置与主服务器相同，区别在于 DocumentRoot 被设置为 `/www/apachehandbook/public/htdocs`，且 ServerName 被设置为 `www.apachehandbook.com`。在 `<VirtualHost>` 容器中通常设置的指令包括 DocumentRoot、ServerName、ErrorLog 和 TransferLog。

你可以在 `<VirtualHost>` 容器中放置几乎任何配置指令，除了 ServerType、StartServers、MaxSpareServers、MinSpareServers、MaxRequestPerChild、BindAddress、Listen、PidFile、TypeConfig、ServerRoot 和 NameVirtualHost。如果使用 suEXEC 包装器，则可以在 `<VirtualHost>` 容器内部使用 User 和 Group。

你可以拥有任意数量的 `<VirtualHost>` 容器。你可以让一个或多个虚拟主机由主服务器处理，或者为每个可用的地址和端口创建一个 `<VirtualHost>`，使主服务器没有请求需要处理。

## Apache 基于 IP 的虚拟主机配置

在单个主 Apache 服务器配置中设置基于 IP 的虚拟主机非常简单。只需为每个虚拟 IP 地址创建一个 `<VirtualHost>` 容器。例如，若要创建一个名为 `vhost1.domain.com`（192.168.0.50）且 DocumentRoot 目录为 `/www/vhost1/` 的虚拟主机，请将以下行添加到 `httpd.conf` 文件中：

```
<VirtualHost 192.168.0.50>
DocumentRoot "/www/vhost1/"
ServerName vhost1.domain.com
</VirtualHost>
```

## Apache 基于名称的虚拟主机配置

设置基于名称的虚拟主机也非常简单。第一步是将 `NameVirtualHost` 指令设置为基于名称的虚拟主机的 IP 地址。此指令指定应作为基于名称的虚拟主机目标的 IP 地址。例如，假设你希望在一个监听 IP 地址 192.168.0.50 的 Apache 服务器上设置两个虚拟主机，例如 `www.client1.com` 和 `www.client2.com`。以下是此类配置的一个示例：

```
NameVirtualHost 192.168.0.50
```

```
<VirtualHost 192.168.0.50>
    ServerName www.client1.com
    DocumentRoot "/www/client1"
</VirtualHost>
```

```
<VirtualHost 192.168.0.50>
    ServerName www.client2.com
    DocumentRoot "/www/client2"
</VirtualHost>
```

对于使用特定 IP 地址的所有基于名称的虚拟主机，每个 IP 地址只需要一个 `NameVirtualHost` 指令。当来自符合 HTTP/1.1 标准的浏览器的请求到达这些虚拟主机之一时，Apache 将 `ServerName` 指令与请求中 `Host` 头提供的 主机名进行匹配。因此，Apache 能够确定请求的是哪个虚拟主机。

在为 Apache 创建虚拟主机配置后，启动（或重启）Apache 服务器以使配置生效。此外，在重启 Apache 服务器之前，不要忘记创建虚拟主机配置中可能使用的任何目录。

![](img/f9ec99365f159bfe663f8ac29732663c_356_0.png)

### 提示

从 Apache 1.3.x 开始，你可以使用 `-s` 选项运行 Apache 来验证虚拟主机配置。

## 将 Apache 用作代理服务器

Apache 中的代理支持来自 `mod_proxy` 模块。此模块默认未编译。

### 编译代理模块

如果你使用 APACII 界面来编译和安装 Apache，那么构建包含代理模块的新 Apache 可执行文件就像在你的 Apache 源码发行版目录中执行以下步骤一样简单：

- 1. 如果你是第一次运行 `configure` 脚本，请输入以下命令：

```
./configure \
--prefix=/dir/where/you/want/to/install/apache \
--enable-module=proxy
```

相反，如果你已经运行了 `configure` 脚本来编译 Apache，请输入以下内容：

```
./config.status --enable-module=proxy
```

当你创建新的配置文件时，之前的配置选项将被应用。

- 2. 运行 `make` 命令。如果没有返回错误消息，请运行 `make install` 命令将新编译的 Apache 可执行文件安装到适当的目录中。

### 代理模块指令

Apache 的代理模块附带了你使用该模块所需的一组指令。所有这些指令都可以在主服务器配置以及任何虚拟服务器配置上下文中使用。

`ProxyRequests on | off`

此指令允许你启用或禁用缓存代理服务。然而，它不影响 `ProxyPass` 指令的功能。默认值为 off。

`ProxyRemote match remote-proxy-server-URL`

此指令允许你将你的代理服务器与另一个代理服务器进行接口连接。*match* 的值可以是 URL 方案（`http`、`ftp` 等）的名称或部分 URL。

*remote-proxy-server-URL* 可以是 `http://remote-proxy-hostname:port`。目前仅支持 HTTP 协议。换句话说，你只能指定处理 HTTP 协议的代理服务器；然而，你可以将 FTP 请求从你的代理服务器转发到同时支持 HTTP 和 FTP 协议的服务器，如下所示：

```
ProxyRemote ftp http://ftp.proxy.nitec.com:8000
```

这将所有到达本地代理服务器的 FTP 请求发送到 `ftp://ftp.proxy.nitec.com`。请求将通过 HTTP 发送，因此实际的 FTP 事务将在远程代理服务器上发生。

如果你想将针对特定网站的所有代理请求直接转发到其代理服务器，你可以使用 `ProxyRemote` 指令做到这一点。例如，

```
ProxyRemote http://www.isp.com  http://web-proxy.isp.com:8000
```

将匹配 `www.isp.com` 的所有请求发送到 `web-proxy.isp.com`。

然而，如果你想将所有代理请求转发到另一个代理，请使用星号作为匹配短语。例如，

```
ProxyRemote  * http://proxy.domain.com
```

将所有本地代理请求发送到 `proxy.domain.com` 上的代理服务器。

`ProxyPass relative-URL destination-URL`

此指令允许你将 Web 服务器的文档树映射到你的代理服务器的文档空间。例如，

```
ProxyPass  /internet/microsoft  www.formserv.com/
```

上述在名为 `proxy.nitec.com` 的代理服务器的 `httpd.conf` 文件中找到的 `ProxyPass` 指令，允许代理服务器用户使用以下 URL 访问 FormServ Web 站点：

```
http://proxy.nitec.com/internet/formserv
```

此指令（**ProxyPass**）使 **proxy.nitec.com** 表现得像 **www.formserv.com** Web 站点的镜像。任何使用 *relative-URL* 的请求都将在内部转换为针对 *destination-URL* 的代理请求。

`ProxyPassReverse relative-URL destination-URL`

当你希望使用 Apache 创建反向代理服务器时，此指令非常有用。在这种反向代理设置中，此指令修复了实际 Web 服务器可能返回的 *Location* 头。例如，在下面的示例中，**www.nitec.com** 是获取另一个名为 *realserver.nitec.com* 的服务器所有页面的代理服务器：

```
<VirtualHost 206.171.50.50>
  ServerName www.nitec.com
  ProxyRequests on
  ProxyPass / realserver.nitec.com/
  ProxyPassReverse / realserver.nitec.com/
</VirtualHost>
```

**ProxyPass** 指令启用了此功能。但是，如果 *realserver.nitec.com* 上的页面在响应中发送 *Location* 头，**ProxyPassReverse** 指令会修复它，以确保客户端不会绕过代理服务器 **www.nitec.com**。

`ProxyBlock partial or full host name . . .`

此指令允许你阻止访问命名主机或域名。
例如，

```
ProxyBlock gates
```

阻止访问名称中包含 **gates** 一词的任何主机。这样，对 *http://gates.ms* 或 *http://gates.friendsofbill.com* 的访问将被阻止。你还可以指定多个主机，如下所示：

