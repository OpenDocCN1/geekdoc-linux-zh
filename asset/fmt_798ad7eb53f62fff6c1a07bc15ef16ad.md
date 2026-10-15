
| 指令 (DIRECTIVE) | 说明 |
| --- | --- |
| `CacheDefaultExpire` | 设置文档缓存过期时间（单位：秒）。 |
| `CacheEnable` | 支持缓存指定的目录。 |
| `CacheGCInterval` | 配置清理缓存旧数据的间隔（单位：小时）。 |
| `CacheLastModified` | 设置缓存文件的过期时间。如果网页没有关联的日期和时间，Apache 将相对于最后已知更改的时间进行设置。 |
| `CacheMaxExpire` | 设置缓存的最大时间（单位：秒）。 |
| `CacheRoot` | 配置代理服务器的默认目录。 |
| `CacheSize` | 设置缓存的大小（单位：KB）。 |

## 虚拟主机 (Virtual Hosts)

Apache 2.0.x 的优点之一是在单个 IP 地址上设置多个网站。这通过“虚拟主机”的概念实现。许多网站托管公司使用虚拟主机从单一服务器提供虚拟网站。

旧版本的 Apache 仅支持基于 IP 的虚拟主机，这需要为通过 Apache 服务器的每个网站配置独立的 IP 地址。Apache 2.0.x 支持基于名的虚拟主机。

在这种方案下，DNS 服务器将域名（如 `www.mommears.com` 和 `www.sysex.com`）映射到同一个 IP 地址，例如 `10.11.23.45`。你可以设置 `http.conf` 来识别不同的域名并提供相应的网站。

> 注意：你不能总是使用基于名的方案；它可能在旧版客户端（如 Netscape 2.0 和 Internet Explorer 4.0 浏览器）上出现问题。这些浏览器无法处理与当前 HTTP 1.1 相关的大信息。

以下代码是配置两个虚拟机的示例，此处针对 `www.sysex.com` 和 `www.mommears.com`：

```
VirtualHost *:80

VirtualHost 10.11.23.45

<VirtualHost 10.11.23.45>

ServerAdmin webmaster@sysex.com

DocumentRoot /www/site1/sysex.com

ServerName sysex.com

ErrorLog logs/sysex.com-error_log

CustomLog logs/sysex.com-access_log common

</VirtualHost>
```

此 `VirtualHost` 指令监听本地计算机上所有 IP 地址的请求。它识别网页的 TCP/IP 端口（80）。如果你想将多个网站映射到同一个 IP 地址，你需要将该部分的 `*` 替换掉。确保使用你本地 Web 服务器的 IP 地址。

```
<VirtualHost 10.11.23.45>

ServerAdmin webmaster@mommears.com

DocumentRoot /www/site2/mommears.com

ServerName mommears.com

ErrorLog logs/mommears.com-error_log

CustomLog logs/mommears.com-access_log common

</VirtualHost>
```

`www.sysex.com` 虚拟主机 `10.11.23.45:80` 中的指令优于 `http.conf` 文件中早期定义的任何指令。你可以通过添加你选择的指令来自定义每个虚拟主机。

如你所示，`mommears.com` 网站的设置类似的；请记住，相对目录取决于 `ServerRoot` 指令。

## 自定义 Apache 模块 (Customizing Apache Modules)

在 `/etc/http/conf.d` 目录下有许多 Apache 模块特定的配置文件，它们是通过之前“软件包”部分描述的某些模块 RPM 安装的。得益于主 `httpd.conf` 文件中的 `Include conf.d/*.` 指令，它们被包含在基础 Apache 配置中。

列表中最重要的是 `ssl.conf` 文件，因为你可以在该文件中为网站设置安全区域。这些模块文件汇总在表 25.10 中。

### 表 25.10：/ETC/HTTP/CONF.D 中的 APACHE 模块配置文件

| 文件 (FILE) | 说明 |
| --- | --- |
| `authz_ldap.conf` | 支持通过 LDAP 访问身份验证；该文件的默认版本包含了模块和相关的 LDAP 身份验证命令。 |
| `perl.conf` | 包含 Perl 解释器；支持使用 Perl 命令和脚本。 |
| `php.conf` | 包含 PHP 脚本语言解释器。 |
| `python.conf` | 包含 Python 解释器；支持使用 Python 命令和脚本。 |
| `squirrelmail.conf` | 支持 Squirrel 邮件器。 |
| `ssl.conf` | 添加安全套层 (SSL) 支持。 |
| `webalizer.conf` | 允许访问流量。 |
| `welcome.conf` | 默认指向 Red Hat。 |

## 安全虚拟主机 (Secure Virtual Hosts)

由于人们需要访问公共网站，他们还需要可以保持安全的页面。这包含了 `/etc/conf.d` 中的指令。从本质上说，你在 `ssl.conf` 中配置虚拟主机，使用的基础命令与 `httpd.conf` 相同。一旦配置了安全虚拟主机，你就可以通过浏览器访问该网站。

第一个关键指令设置了安全服务的 TCP/IP 端口。这是我们在 `httpd.conf` 中描述过的 `Listen` 指令。

```
Listen 0.0.0.0:443
```

## 第 25 章 WEB 服务 (CHAPTER 25 WEB SERVICES)

### 图 25.6
分析网站数据

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_773_0.png)

为了给之前描述的 Sytex 网站设置安全加密区域，我们可以在 `ssl.conf` 中添加以下 `VirtualHost` 容器：

```
<VirtualHost 10.11.23.45:443>

ServerAdmin webmaster@sysex.com

DocumentRoot /www/securesite1/sysex.com

ServerName sytex.com:443

ErrorLog logs/sytex.com-ssl_error_log

TransferLog logs/sytex.com-ssl_access_log

...

</VirtualHost>
```
