
| 字段说明符 | 说明 |
| --- | --- |
| `%a` | 远程 IP 地址 |
| `%A` | 本地 IP 地址 |
| `%b` | 发送的字节数，排除 HTTP 头部 |
| `%(variable)e:` | 环境变量的内容 |
| `%f` | 文件名 |
| `%h` | 远程主机 |
| `%l` | 远程主机名（如果提供则来自 ident） |
| `%m` | 请求方法 |
| `%P` | 服务请求的子进程的 ID |
| `%r` | 请求的第一行 |
| `%s` | 状态 |
| `%t` | 时间，采用 Common Log Format 时间格式（标准英语格式） |
| `%u` | 远程用户（来自 auth；如果返回状态 `%s` 为 401 则可能是伪造） |
| `%U` | 请求的 URL 路径 |
| `%v` | 提供请求的服务器的规范 ServerName |

**表 19-4.** Apache 日志字段说明符

Apache 提供了两个用于处理和管理日志文件的实用。`logresolve` 将日志文件中的 IP 地址解析为主机名。`rotatogs` 在不杀死服务器的情况下轮转日志文件。你可以指定轮转时间。

# Apache 虚拟托管

虚拟托管允许 Apache Web 服务器作为其自身托管多个 Web 站点。实际上，服务器可以充当几台服务器，每个托管的 Web 站点在外部用户看来都是单独的。Apache 支持基于 IP 地址和基于名称的虚拟托管。IP 地址虚拟主机使用有效的已注册 IP 地址，而基于名称的虚拟主机使用完全限定的域名地址。这些域名地址由请求浏览器的 host 头部提供。服务器随后仅根据域名即可确定要使用的正确虚拟主机。注意，SSL 服务器需要 IP 虚拟托管。更多信息请访问 http://apache.org。

## IP 地址虚拟主机

在 IP 地址虚拟托管方法中，你的服务器必须为每个虚拟主机拥有不同的 IP 地址。你使用的 IP 地址已设置好引用你的系统。网络系统管理操作可以让你的机器支持多个 IP 地址。你的机器可以为每个 IP 设置单独的物理连接，或者配置特定的连接以同时监听多个 IP 地址。事实上，任何 IP 地址都可以访问你的系统。

你可以配置 Apache 为每个虚拟主机运行单独的守护进程，分别监听每个 IP，或者运行一个单一守护进程来监听所有虚拟主机的请求。要设置单个守护进程管理所有虚拟主机，请使用 `VirtualHost` 指令。要为每个主机设置单独的守护进程，也使用 `Listen` 指令。

必须为每个虚拟主机设置一个 `VirtualHost` 指令块。在每个 VirtualHost 块中，你放置访问主机的相应指令。

## 基于名称的虚拟主机

通过基于 IP 的虚拟托管，你限于系统支持的 IP 地址数量。通过基于名称的虚拟托管，你可以在不需要额外 IP 地址的情况下支持任何数量的虚拟主机。即使机器只有一个 IP 地址，你仍然可以支持无限数量的虚拟主机。这种功能由 HTTP/1.1 协议实现，它允许服务器识别访问它的名称。这种方法要求客户端（远程用户）使用支持 HTTP/1.1 协议的浏览器（目前的浏览器支持，但旧的可能不支持）。使用此类协议的浏览器可以发送指定机器上特定主机的 host 头部。实现基于名称的虚拟托管，为每个主机使用 `VirtualHost` 指令。如果你的系统只有一个 IP 地址，你需要使用该地址。在 `VirtualHost` 指令中，你使用 `ServerName` 指令来指定你想为该主机使用的域名。DNS 查找会禁用虚拟主机。`VirtualHost` 指令各取 `VirtualHost` 指令中指定的相同 IP 地址作为参数。你使用 VirtualHost 块中的 Apache 指令单独配置每个主机。基于名称的虚拟托管在不存在此类信息时使用指定的域名，则使用第一个主机作为默认。以下示例实现了两个基于名称的虚拟主机。这里，`www.mypics.com` 和 `www.myproj.org` 使用 IP 主机实现了基于名称的虚拟主机：

```
ServerName turtle.mytrek.com

NameVirtualHost 192.168.1.5

<VirtualHost 192.168.1.5>
ServerName www.mypics.com
ServerAdmin webmaster@mail.mypics.com
DocumentRoot /var/www/mypics/html
```

```
<VirtualHost www.myproj.org>
ServerAdmin webmaster@mail.myproj.org
DocumentRoot /var/www/myproj/html
```

# 462 Red Hat Linux 8: 完整参考

```
ErrorLog /var/www/mypics/logs/error_log
...
</VirtualHost>

<VirtualHost 192.168.1.5>
ServerName www.myproj.org
ServerAdmin webmaster@mail.myproj.org
DocumentRoot /var/www/myproj/html
ErrorLog /var/www/myproj/logs/error_log
...
</VirtualHost>
```

如果你的系统只有一个 IP 地址，实施虚拟主机可以防止用户通过该地址访问你的主服务器。你将无法再直接将主服务器作为 Web 服务器使用；你只能间接地使用它来管理你的虚拟主机。你可以配置一个虚拟主机来管理主服务器的 Web 页面。然后，你将使用主服务器来支持一组作为网站运行的虚拟主机，而不是让主服务器直接运行一个站点。如果你的机器有两个或多个 IP 地址，你可以将其中一个用于主服务器，另一个用于你的虚拟主机。你还可以在服务器上混合使用基于 IP 的虚拟主机和基于名称的虚拟主机。你也可以使用不同的 IP 地址来支持不同的虚拟主机组。你甚至可以设置多个地址访问同一个虚拟主机。要这样做，请在选定的 VirtualHost 块中放置一个列出域名的 `ServerAlias` 指令。

- `ServerAlias www.myproj.com www.greatpics.com`

发送到用于你虚拟主机的 IP 地址的请求必须匹配已配置的虚拟域名之一。为了捕获不匹配任何虚拟主机的请求，你可以使用 `*_default_*` 设置一个默认虚拟主机。未匹配的请求将由该虚拟主机处理。

```
<VirtualHost _default_:*>
```

## 动态虚拟主机托管

如果你在服务器上实现了许多虚拟主机，且它们的配置基本相同，那么可以使用一种名为“动态虚拟主机”（dynamic virtual hosting）的技术来动态生成这些虚拟主机。实现你虚拟主机的代码将变得小得多，因此，你的服务器访问它们的速度会更快。添加更多虚拟主机将变成创建相应目录并在 DNS 服务器中为它们添加条目的简单事项。

要实现动态虚拟主机，服务器使用 `mod_vhost_alias` 模块中的命令（支持 Apache 1.3.6 及以上版本）将服务器和文档根同时重写为相应虚拟服务器的路径（对于 1.3.6 之前的旧 Apache 版本，使用 `mod_rewrite` 模块）。动态虚拟主机可以是基于名称的也可以是基于 IP 的。在任何情况下，你都必须这样使用 `UseCanonicalName` 指令，允许服务器使用虚拟主机名而不是服务器自身的名称。对于名称托管，你只需关闭 `UseCanonicalName`。这允许你的服务器从用户请求的 Host 标头中获取主机名。对于基于 IP 的托管，你将 `UseCanonicalName` 指令设置为 `DNS`。这允许服务器在 DNS 服务器中查找主机。

```
UseCanonicalName Off
UseCanonicalName DNS
```

然后，你必须让服务器定位你各种虚拟主机的不同文档根目录和 CGI 二进制文件。你使用 `VirtualDocumentRoot` 指令指定虚拟主机目录的模板。例如，如果你将不同的主机目录放在 `/var/www/hosts/` 目录下，你可以相应地设置 `VirtualDocumentRoot` 指令。

```
VirtualDocumentRoot /var/www/hosts/%0/html
```

当访问虚拟主机时，`%0` 将替换为虚拟主机的名称。重要的是，要使用该主机名创建动态虚拟主机的目录。例如，对于一个名为 `my.golf.org` 的动态虚拟主机，你需要创建一个名为 `/var/www/hosts/my.golf.org` 的目录。然后为文档根和 CGI 程序创建子目录，如 `/var/www/hosts/my.golf.org/html`。对于 CGI 指令，使用 `VirtualScriptAlias` 指令来指定你使用的 CGI 子目录。

```
VirtualScriptAlias /var/www/hosts/%0/cgi-bin
```

以下是基于名称的动态虚拟主机指令的简单示例：
