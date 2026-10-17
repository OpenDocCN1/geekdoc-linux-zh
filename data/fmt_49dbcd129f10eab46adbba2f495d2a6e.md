
```apache
<VirtualHost *:443>
    ServerName www.mytrek.com
    SSLCertificateFile /etc/httpd/ssl/mytrek.crt
    SSLCertificateKeyFile /etc/httpd/ssl/mytrek.key
</VirtualHost>
</IfDefine>
```

# 514 第 V 部分：网络服务器

| 协议 | 说明与端口 |
|---|---|
| HTTP | Web 页面，端口 3128 |
| FTP | 通过网站进行 FTP 传输，端口 3128 |
| ICP | 互联网缓存协议，端口 3130 |
| HTTPC | 超文本缓存协议，端口 4827 |
| CARP | 缓存数组路由协议 |
| SNMP | 简单网络管理协议，端口 3401 |
| SSL | 安全套层 |

表 24-1 Squid 支持的协议

从技术上讲，你可以使用代理服务器简单地管理 Web 服务器与与其通信的客户端之间的流量，而完全不进行缓存。`Squid` 作为代理缓存服务器兼具了这两种功能。

`Squid` 提供了安全功能，允许你对托管了你服务器的主机进行控制。你可以拒绝某些主机的访问并允许其他主机的访问。`Squid` 还支持使用 `SSL` 等加密协议（参见第 23 章）。加密通信将通过隧道（直接通过而不读取）从 `Squid` 服务器直接传输到 Web 服务器。

`Squid` 由加州大学圣地亚哥分校的应用网络研究实验室（NLNAR）根据 GNU 公共许可证支持并分发。该工作基于 Harvest 项目，旨在创建一个包含名为 `cached` 的高性能守护程序的 Web 索引系统。你可以从 `Squid` 官网 `www.squid-cache.org` 获取源码版本和在线文档。`Squid` 软件软件包由 `Squid` 服务器、几个针对 LDAP 和 HTTP 等缓存的支持脚本，以及一个名为 `cachemgr.cgi` 的缓存管理器组成。`cachemgr.cgi` 允许你查看 `Squid` 服务器运行期间的统计数据。

你可以使用 `squid` 脚本启动、停止和重启 `Squid` 服务器，如下所示：

```
# service squid restart
```

你还可以使用 `system-config-services` 工具（系统 | 管理 | 服务器设置 | 服务）或 `chkconfig` 设置 `Squid` 服务器为自动启动。

## 配置客户端浏览器

`Squid` 同时支持标准代理缓存和透明缓存。对于标准代理缓存，用户需要配置其浏览器以专门访问 `Squid` 服务器。而透明缓存则不需要用户配置浏览器。透明缓存通过 `Iptables` 使用网络过滤来拦截请求并将其重定向到代理缓存（参见第 20 章）。

对于标准代理缓存，用户需要在浏览器配置中指定其代理服务器。为此，他们需要运行 `Squid` 代理服务器的主机 IP 地址以及它所使用的端口。代理通常使用端口 3128。要配置运行在第 5 章描述的本地网络上的代理服务器，你需要在浏览器的代理配置设置中输入以下内容。代理服务器运行在 `turtle.mytrek.com` (`192.168.0.1`) 上，并使用端口 3128。

```
192.168.0.1:3128
```

在 Firefox、Mozilla 和 Netscape 上，在示例本地网络中，首先应选择“编辑”菜单下“偏好”中的代理面板。然后，在“手动代理配置”的“查看”面板中输入上述信息。用户将看到 FTP、Gopher、HTTP 以及安全代理的条目。对于标准的 Web 访问，在 FTP、Gopher 和 Web 框中输入 IP 地址。在它们的端口框中输入 3128。

对于 Gnome，在“偏好”菜单或窗口中选择“网络代理”，对于 KDE 桌面上的 Konquer，选择“偏好 | 网页浏览”菜单上的“代理”面板。在这里，你可以输入服务器地址和端口号。如果你的本地主机使用 Internet Explorer（如 Windows 系统），你可以在“Internet 选项”访问的局域网设置中设置代理。

在 Linux 或 Unix 系统上，本地主机可以使用 `http_proxy`、`gopher_proxy` 和 `ftp_proxy` 变量来配置 Linux 支持的 Web 浏览器访问。你可以将这些定义放在 `.bash_profile` 或 `/etc/profile` 文件中，以便在每次登录时自动定义它们。

```
http_proxy=192.168.0.1:3128
ftp_proxy=192.168.0.1:3128
gopher_proxy=192.168.0.1:3128
export http_proxy ftp_proxy gopher_proxy
```

或者，你可以使用代理的 URL。

```
http_proxy=http://turtle.mytrek.com:3128
```

对于 Elinks 浏览器，你可以在配置文件 `/etc/elinks.conf` 中指定代理。设置 FTP 和 Web 代理选项，如下所示：

在本地主机上的客户端使用代理服务器之前，必须在服务器的 `squid.conf` 文件中赋予其权限，该文件在后文“安全性”部分描述。可以很容易启用整个网络的访问。对于此处使用的示例网络，你需要在 `squid.conf` 文件中放置以下条目。这些将在后续章节中详细说明：

```
protocol.http.proxy.host turtle.mytrek.com:3128
protocol.ftp.proxy.host turtle.mytrek.com:3128
```

```
acl mylan 192.168.0.0/255.255.255
http_access allow mylan
```

提示 需要访问你的 `Squid` 服务器作为代理的 Web 客户端。

## 第24 章：代理服务器：Squid

516 第 V 部分：网络服务器

### squid.conf 文件

`Squid` 配置文件是 `squid.conf`，位于 `/etc/squid` 目录。在 `/etc/squid/squid.conf` 中，你可以设置系统选项。`squid.conf` 的默认版本包含了所有条目的详细说明。例如，`maximum_size` 设置了对象的限制。

```
maximum_size 4096 KB
```

作为代理，`Squid` 将使用某些端口，例如 3128。如果你需要其他端口，可以在 `squid.conf` 中设置它们。以下条目显示了如何使用 HTTP：

```
http_port 3128
```

> **注意** `Squid` 使用简单网络管理协议 (`SNMP`) 向管理网络的代理程序提供状态信息和统计数据。你可以通过 `squid.conf` 配置 `SNMP`。

### 安全性

`Squid` 可以利用其作为客户端与 Web 服务器之间中间人的角色来实现访问控制，确定谁可以访问以及如何访问。这通过检查对已设置控制的主机和域名的访问控制（ACL）来实现。当来自这些主机的 Web 客户端尝试连接服务器时，它将执行该控制。`Squid` 支持多种控制，可以拒绝或允许访问远程主机的（参见表 24-2）。`Squid` 为每个 Web 服务器设置防火墙。

配置 `Squid` 的第一步是创建 ACL。这些是你想要设置控制的主机和域名列表。你使用 `acl` 命令定义 ACL，在其中为要设置控制的系统创建规则。然后，你使用 `http_access` 等命令来定义这些控制。你可以通过使用多个 `acl` 选项（如 IP 地址、域名甚至是日期）来定义一个系统或一组系统。例如，`src` 选项用于定义名为 `mylan` 的本地网络上的系统或组。要为 `192.168.0.0/255.255.255` 的本地网络上的组定义 `acl` 条目，使用以下 ACL 定义：

```
acl mylan src 192.168.0.0/255.255.255
```
