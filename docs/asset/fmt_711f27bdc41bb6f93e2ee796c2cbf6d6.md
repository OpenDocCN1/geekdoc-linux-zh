
```
<IfDefine HAVE_SSL>
LoadModule ssl_module modules/libssl.so
</IfDefine>
```

Apache 服务器的 SSL 版本在`httpd.conf`中作为虚拟主机设置。SSL 指令通过使用`HAVE_SSL`标志的`IfDefine`块启用。系统实现了几个默认指令，例如 SSL 指令的位置以及服务器 SSL 版本将监听的端口（`443`）。其他指令则被注释掉了。你可以通过删除前的`#`符号并设置你自己的选项来启用它们。这里显示了几个指令：

```
<IfDefine HAVE_SSL>
## SSL 虚拟主机上下文

# 服务器证书:
SSLCertificateFile /etc/http/conf/ssl.crt/server.crt

# 私钥:
SSLCertificateKeyFile /etc/http/conf/ssl.key/server.key

# 证书颁发机构 (CA):
#SSLCACertificatePath /etc/http/conf/ssl.crt
#SSLCACertificateFile /etc/http/conf/ssl.crt/ca-bundle.crt
```

在`/etc/httpd/conf`目录下，`mod_ssl`将建立包含 SSL 认证和加密密钥数据的`SSL`目录。`sslcrt`将存储服务器证书。`ssl.key`存储认证所需的公钥和私钥。撤销证书的吊销列表保存在`ssl.crt`中。`csr`目录存放用于向证书颁发机构请求正式证书的证书签名请求。`ssl.param`处理`DSA`密钥加密方法使用的参数。检查每个目录下的`readme`文件以获取其包含的 SSL 文件的详情。

`mod_ssl`安装将为你提供一个名为`snakeoil`的演示证书，你可以用它来测试 SSL 配置。当你拥有正式证书时，可以在`ssl.crt`目录下使用`make certificate`命令进行安装。这将覆盖`server.crt`证书文件。

# 第 24 章：代理服务器

代理服务器作为本地网络与大型网络（如互联网）可用服务之间的中间节点。本地客户端对 Web 服务的请求可以由代理服务器处理，从而加速交易并控制访问。代理服务器维护常用 Web 页面的当前副本，通过消除访问原始站点的需求提供 Web 访问加速。它们还执行安全功能，保护服务器免受未经的访问。`Squid`是一个用于 Web 客户端的免费开源代理缓存服务器，旨在加速互联网访问并为 Web 服务器提供安全控制。它为 Web 客户端实现了代理缓存服务，在用户发出请求时缓存 Web 页面。用户访问的页面副本保存在`Squid`缓存中，当请求产生时，`Squid`会检查其是否有最新副本。如果`Squid`有最新副本，它将从缓存返回，而不是查询原始站点。如果没有最新副本，它将从原始站点检索。替换算法通常会替换缓存中的旧对象。通过这种方式，浏览器可以使用`Squid`缓存作为代理`HTTP`服务器。`Squid`目前处理支持`HTTP`、`FTP`和`SSL`协议的 Web 页面（`Squid`支持`FTP`，每个都有相应的下载，见表 24-1）。它还支持`ICP`（互联网缓存协议）、用于 Web 缓存的`HTTP`（缓存协议）以及用于状态信息的`SNMP`（简单网络管理协议）。

你可以在`squid-cache.org`了解更多关于`Squid`的信息。有关详细信息，请查看其网站上的`Squid` `FAQ`和用户手册。`FAQ`也安装在`usr/share/doc/squid`目录下。

作为代理，`Squid`的功能不仅仅是缓存对象。它作为 Web 浏览器（客户端）与它们访问的服务器之间的中间节点。客户端不再直接连接 Web 服务器，而是连接代理服务器。代理将请求转发到 Web 服务器。这对于 Web 服务器位于防火墙服务器之后的情况非常有用，可以保护其免受外部访问。代理位于 Web 服务器上，随后可以在客户端和 Web 服务器之间传输请求和响应。这种设计适用于 Web 服务器在受保护的本地网络上运行，同时仍可被访问。你可以使用`Squid`代理为本地主机提供互联网访问。与其使用提供完整互联网访问的网关，本地主机可以使用代理允许它们部分访问（见第 5 章）。你可以将两者结合，允许网关访问，但使用代理服务器为 Web 访问提供更多控制。此外，`Squid`的缓存功能可以为本地主机提供更快的 Web 访问。

# 468 第六部分：互联网与网络服务

| 协议 | 说明与端口 |
| --- | --- |
| `HTTP` | Web 页面，端口 `3128` |
| `FTP` | 通过网站进行 `FTP` 传输，端口 `3128` |
| `ICP` | 互联网缓存协议，端口 `3130` |
| `HTCP` | 超文本缓存协议，端口 `4827` |
| `CARP` | 缓存数组路由协议 |
| `SNMP` | 简单网络管理协议，端口 `3401` |
| `SSL` | 安全套接层 |

表 24-1 `Squid` 支持的协议

从技术上讲，你可以使用代理服务器来管理 Web 服务器与与其通信的客户端之间的流量，而完全不进行缓存。`Squid`将代理缓存服务器的功能结合在了一起。

`Squid`还提供了许多安全功能，让你能够控制访问你 Web 服务器的主机。你可以拒绝某些主机的访问，并允许其他主机访问。`Squid`还支持使用`SSL`等加密协议（见第 23 章）。加密通信将直接通过`Squid`服务器（在不读取的情况下）传递到 Web 服务器。

`Squid`由加州大学圣地亚哥分校国立应用实验室（`NLARP`）根据`GNU`公共许可证支持并分发。该工作基于`Harvest`项目，旨在创建一个包含名为`cached`的高性能缓存守护进程的 Web 索引系统。你可以在`Squid`的主页`squid-cache.org`上找到当前的源码版本和在线文档。`Squid`软件包包含`Squid`服务器、若干个用于`LDAP`和`HTTP`服务的支持脚本，以及一个名为`cachemgr.cgi`的缓存管理器脚本。`cachemgr.cgi`让你查看`Squid`服务器运行时的统计信息。你可以使用`chkhconfig`、`GNOME`的`services-admin`、`Debian`的`rcconf`或`sysv-rc-conf`让`Squid`自动启动。

## 配置客户端浏览器

`Squid`支持标准代理缓存和透明缓存。对于标准代理缓存，用户需要配置其浏览器以专门访问`Squid`服务器。另一方面，透明缓存不需要用户配置浏览器。缓存是透明的，允许像访问普通网站一样进行访问。透明缓存通过`IPTables`使用网络过滤来拦截请求并将其重定向到代理缓存（见第 20 章）。

对于标准代理缓存，用户需要在其 Web 浏览器配置中指定代理服务器以及它使用的端口。代理通常实际上使用运行在第 5 章描述的本地示例网络`turtlemynet.com`上的代理服务器，你输入以下内容（该代理服务器运行在`turtlemynet.com` (`192.168.0.1`) 并使用端口`3128`）：

```
192.168.0.1 3128
```

# 第 24 章：代理服务器 469

在`Firefox`、`Mozilla`和`Netscape`上，示例本地网络上的用户首先选择“编辑”（Edit）菜单下“首选项”（Preferences）中的“代理”（Proxy）面板。然后，在手动配置的“查看”（View）面板中，输入之前的信息。用户将看到`FTP`、`HTTP`和安全代理的条目。对于标准 Web 访问，为`FTP`和 Web 框输入 IP 地址。对于端口框，在“首选项”（Preferences）菜单中选择“代理”（Proxy），或者对于`GNOME`，在“首选项 | Web 浏览”（Preferences | Web Browsing）菜单窗口中选择“代理”（Proxy）。在这里，你输入代理服务器地址和端口号。如果你的本地主机使用的是`Internet Explorer`（如`Windows`系统所示），你通过“选项”（Options）窗口在“局域网”设置中设置代理项。

在`Linux`或`Unix`系统上，本地用户可以使用`http_proxy`和`ftp_proxy`壳变量来配置`Linux`支持的浏览器（如`Lynx`）的访问。你可以在`bash_profile`或`/etc/profile`文件中定义这些变量，以便在每次登录时自动定义它们。

```
http_proxy=192.168.0.1:3128
ftp_proxy=192.168.0.1:3128
export http_proxy ftp_proxy
```

或者，你可以使用代理的 URL。

`http_proxy=http://turtle.mytrek.com:3128`

对于`Elinks`浏览器，你可以在其配置文件`/etc/elinks.conf`中指定代理。同时设置`FTP`和 Web 代理选项：

```
protocol.http_proxy.host turtle.mytrek.com:3128
protocol.ftp_proxy.host turtle.mytrek.com:3128
```
