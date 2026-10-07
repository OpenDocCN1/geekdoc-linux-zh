

# Linux Web 服务器工具箱

根据大学测试，Linux 被认为拥有 UNIX 世界中最为稳定的内核和库。尽管如此，如果你的服务器运行在某些其他系统上，这仍然是一项重要的特性。

# 代理服务器

你可以按照以下方式启用 `ProxyRequests` 指令来使用 Apache 的代理服务器功能：

```
#ProxyRequests On
```

> 注意：默认配置中未使用 `ProxyRequests` 指令。

当 Apache 服务器充当网关并将浏览器请求发送另一台服务器时，它就是一个代理服务器。
结合代理服务器功能，你可以启用文档缓存，这样频繁被请求的文档就会存储在此服务器上，并直接返回给浏览器，无需访问原始存储位置。这如图 11-1 所示。

![](img/e01f1106dd2902613fa07890c8baa7e6_317_0.png)

图 11-1：启用缓存的代理服务器通过存储经常访问的文档来节省时间，从而无需每次都从互联网获取。

`httpd.conf` 中提供了几个与缓存相关的指令。默认的 OpenLinux 配置文件中没有使用其中任何一个，因为假设你的服务器不会充当互联网网关。如果你的服务器将充当网关，你可以

# 第 11 章：配置 Apache Web 服务器

可以设置特定参数，例如文档缓存的大小以及文档过期前必须从原始源重新获取的时间。
提供了以下缓存指令（在默认的 `httpd.conf` 文件中均已注释）：

- CacheRoot：给出存储缓存文档的目录。
- CacheSize：给出可用于存储缓存文档的兆字节（MB）数。当达到此限制时，访问次数最少的文档将从缓存中删除。
- NoCache：给出一个不应被缓存的文档列表。例如，如果你希望你的股票报价网站的所有文档每次都更新，而不是被缓存以避免连续五天获取相同的内容，那么可以在 `NoCache` 指令后列出 `stocks.com`。

## 虚拟主机

Apache 允许你使用单台物理计算机为多个域名提供 Web 服务。这被称为虚拟托管。例如，如果你为几家关联业务托管站点，每个业务都有独立的域名，只需使用一台运行 Apache 的计算机，即可为每个域名的 Web 页面提供服务。

启用虚拟主机的第一步是调整你的域名服务器 IP 路由，使得不同的域名（如果适用，还有不同的 IP 地址）全部指向同一计算机。
一旦网络流量到达你的单一 Web 服务器，你就可以轻松配置 Apache 来提供所有文档。只需使用本节之前描述的 `BindAddress` 指令以及下面描述的指令即可。

由于没有人假设你会使用虚拟托管，或知道你额外的主机名，使用虚拟主机所需的指令在 Linux 的默认 `httpd.conf` 文件中被注释掉了。
`Listen` 指令允许你指定另一个 IP 地址和端口（或仅另一个端口），让 Apache 服务器监听其服务的 Web 请求，如下：

```
Listen 205.23.56.1:80
```

然而，虚拟主机最重要的部分是 `VirtualHost` 容器。你的 `httpd.conf` 或 `srm.conf` 配置文件的这部分并不是一个指令。它像一个 HTML 标签。你将另一个域名或主机名作为值，并将其放在角括号中，如下：

```
<VirtualHost newweb.corp.com>
```

# Linux Web 服务器工具箱

然后你像结束 HTML 标签一样结束这个特殊的容器，如下：

```
</VirtualHost>
```

在这行之间，你可以使用我们已经描述的大多数指令。但它们仅适用于 `VirtualHost` 容器中定义的新主机名的 Web 流量。例如，包含一个 `DocumentRoot` 指令，它定义了存储所有新主机名文档的目录。你还可以拥有 `ErrorLog` 和 `TransferLog` 指令，将此主机的记录存储在不同主日志文件中。以下示例取自 `httpd.conf` 文件：

```
<VirtualHost host.foo.com>
ServerAdmin webmaster@host.foo.com
DocumentRoot /www/docs/host.foo.com
ServerName host.foo.com
ErrorLog logs/host.foo.com-error_log
TransferLog logs/host.foo.com-access_log
</VirtualHost>
```

每个提供服务的域名都应该有独立的服务器信息记录（如日志和文档）。为了方便，你应该为每个提供服务的虚拟主机至少包含上一个示例中的指令。

![](img/e01f1106dd2902613fa07890c8baa7e6_319_0.png)

你可以拥有任意数量的 `VirtualHost` 容器，因此可以使用单台 Apache 服务器为任意数量的站点提供 Web 服务。唯一的限制是用于页面的硬盘大小以及你能处理 Web 服务器的大小。

虽然大多数指令可以包含在 `VirtualHost` 容器中，但某些指令与 Web 服务器的整体运行，不应包含在 `VirtualHost` 容器中。这些包括 `MinSpareServer` 及相关指令、`UserId`、`PidFile`、![](img/e01f1106dd2902613fa07890c8baa7e6_319_0.png)

