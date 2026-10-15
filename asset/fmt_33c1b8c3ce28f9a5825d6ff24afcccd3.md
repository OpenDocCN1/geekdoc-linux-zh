
# httpd.conf file

```
ServerName main.server.com
Port 80
ServerAdmin mainguy@server.com
DocumentRoot "/www/main/htdocs"

ScriptAlias /cgi-bin/ "/www/main/cgi-bin/"
Alias /images/ "/www/main/htdocs/images/"

<VirtualHost 192.168.1.100>
ServerName vhost1.server.com
ServerAdmin vhost1_guy@vhost1.server.com
DocumentRoot "/www/vhost1/htdocs"
ScriptAlias /cgi-bin/ "/www/vhost1/cgi-bin/"
</VirtualHost>

<VirtualHost 192.168.1.110>
ServerName vhost2.server.com
ServerAdmin vhost2_guy@vhost2.server.com
DocumentRoot "/www/vhost2/htdocs"
ScriptAlias /cgi-bin/ "/www/vhost2/cgi-bin/"
Alias /images/ "/www/vhost2/htdocs/images/"
</VirtualHost>
```

在前面的文件中，两个虚拟网站 `vhost1.server.com` 和 `vhost2.server.com` 在各自的 `<VirtualHost>` 容器中定义。每个 `<VirtualHost>` 容器中包含的指令仅适用于其服务的虚拟主机。因此，当 Web 浏览器请求 `http://vhost1.server.com/index.html` 时，Apache Web 服务器会在 `/www/vhost1/htdocs` 目录中查找 `index.html` 页面。同样，当 Web 浏览器请求 `http://vhost2.server.com/cgi-bin/hello.pl` 时，脚本将从 `/www/vhost2/cgi-bin` 目录运行。

然而，主服务器配置中的许多指令（即 `<VirtualHost>` 容器之外的任何指令）仍适用于未覆盖它们的虚拟主机。例如，注意上面的示例中 `vhost1.server.com` 没有为 `/images/` 目录别名设置 `Alias` 指令。因此，当 Web 浏览器请求 `http://vhost1.server.com/images/pretty_pic.gif` 文件时，图片将从 `/www/main/htdocs/images` 目录提供。因为 `vhost2.server.com` 用自己的设置覆盖了 `/images/` 别名，类似的请求将改为从 `/www/vhost2/htdocs/images` 目录提供。

正如你所见，你可以允许虚拟主机从主服务器继承配置，这使得在大型安装中虚拟主机配置易于管理，在这些安装中某些内容可以共享。例如，如果你决定只使用一个中央 CGI 仓库并允许虚拟主机使用其中存储的脚本，就无需在每个虚拟主机容器中创建 `ScriptAlias` 指令。只需在主服务器配置中使用一个 `ScriptAlias` 指令即可。每个虚拟主机都可以像其自身配置的一部分一样使用该别名。

## 如何使用基于名称的虚拟主机

这种创建虚拟主机的方法是最推荐的，因为它只需一个 IP 地址即可托管数百个甚至更多的虚拟网站。基于名称的虚拟主机唯一的微小问题是它不适用于不支持 HTTP/1.1 协议的 Web 浏览器。然而，只有非常早期的 Web 浏览器，如 Microsoft IE 1.x 或 Netscape Navigator 1.x，不支持 HTTP/1.1，因此这现在已不是大问题。大多数人使用的是 3.x 或更高版本的主要 Web 浏览器，它们都兼容基于名称的虚拟主机技术。

现在，让我们看一个例子。假设你有一个 IP 地址 `192.168.1.100`，想在同一台服务器上托管 `vhost1.domain.com` 和 `vhost2.domain.com`。你可以这样做：

- 1. 在你的 DNS 服务器上创建适当的 DNS 记录，将 `vhost1.domain.com` 和 `vhost2.domain.com` 指向 `192.168.1.100`。
- 2. 在 `httpd.conf` 文件中创建以下配置段：

```
NameVirtualHost 192.168.1.100

<VirtualHost 192.168.1.100>
    ServerName vhost1.domain.com
    ServerAdmin someone@vhost1.domain.com
    DocumentRoot "/www/vhost1/htdocs"

    #
    # Any other directives you need
    # can go here
    #

</VirtualHost>

<VirtualHost 192.168.1.100>
    ServerName vhost2.domain.com
    ServerAdmin someone@vhost2.domain.com
    DocumentRoot "/www/vhost2/htdocs"

    #
    # Any other directives you
    # need can go here
    #

</VirtualHost>
```

不要忘记在需要时创建文档根目录。此外，如果需要在每个虚拟主机配置中添加更多指令，也可以这样做。
- 3. 使用 `/usr/local/apache/apachectl restart` 命令重启 Apache，并使用 `http://vhost1.domain.com` 和 `http://vhost2.domain.com` 访问每个虚拟主机。

从上面的示例配置可以看出，两个虚拟主机容器都使用相同的 IP 地址（`192.168.1.100`）。那么当请求通过 `192.168.1.100` IP 地址到达时，Apache 如何知道正在请求哪个虚拟站点？事实证明，HTTP/1.1 要求 Web 浏览器向 Web 服务器发出的每个请求中都必须包含一个名为 `Host` 的新头部。例如，以下是 Web 浏览器向运行在 `rhat.domain.com` 上的服务器发出的 HTTP 请求的头部转储：

```
GET / HTTP/1.1
Host: rhat.domain.com
Accept: text/html, text/plain
Accept: postscript-file, default, text/sgml, */*;q=0.01
Accept-Encoding: gzip, compress
Accept-Language: en
User-Agent: Lynx/3.0.0dev.9 libwww-FM/2.14
```

当 Apache 看到 `Host: rhat.domain.com` 头部时，它就可以立即使用具有匹配 `ServerName` 的适当虚拟主机来处理请求。

## 如何使用基于 IP 的虚拟主机

基于 IP 的虚拟主机是 Apache 支持的两种虚拟主机类型之一。在这种设置中，每个虚拟主机都被分配一个唯一的 IP 地址。例如：

```
<VirtualHost 192.168.1.1>
    ServerName vhost1.server.com
    # Other directives go here
</VirtualHost>

<VirtualHost 192.168.1.2>
    ServerName vhost2.server.com
    # Other directives go here
</VirtualHost>
```

```
<VirtualHost 192.168.1.3>
    ServerName vhost3.server.com
    # Other directives go here
</VirtualHost>
```

这些 IP 地址中的每一个都必须绑定到服务器上的相应以太网接口。例如，上述配置要求托管上述站点的系统在其 DNS 服务器配置文件中具有以下 DNS 记录：

```
; Address Records
vhost1.server.com.  IN  A 192.168.1.1
vhost2.server.com.  IN  A 192.168.1.2
vhost3.server.com.  IN  A 192.168.1.3

; Reverse DNS records
1                   IN  PTR vhost1.server.com.
2                   IN  PTR vhost2.server.com.
3                   IN  PTR vhost3.server.com.
```

这些地址中的每一个都必须绑定到服务器上的一个或多个以太网接口。通常，在 Linux 系统上，可以使用 IP 别名技术绑定多个 IP 地址。例如：
