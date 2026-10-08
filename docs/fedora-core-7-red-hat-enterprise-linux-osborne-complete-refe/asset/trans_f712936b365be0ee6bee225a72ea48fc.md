

**注意** Apache Web 服务器还可以提供关于服务器活动和配置的详细报告，让你能够向远程服务器显示这些信息。`Location` 指令 `server-info` 将显示你的 Web 服务器配置详情，而 `server-status` 指令将显示 Web 进程。页面 `server-info` 和 `server-status` 将显示这些报告，例如在 `http://localhost/server-info`。使用 `ExtendedStatus` 指令来启用详细报告。

# Apache 上的虚拟主机

虚拟主机允许 Apache Web 服务器将多个 Web 站点作为其自身的一部分进行托管。实际上，服务器可以充当多个服务器，每个托管的 Web 站点对外部用户来说看起来都是独立的。Apache 支持基于 IP 地址和基于名称的虚拟主机。基于 IP 地址的虚拟主机使用有效的已注册 IP 地址，而基于名称的虚拟主机使用完全限定域名地址。这些域名地址由请求浏览器的 host 头提供。服务器随后可以仅根据域名确定要使用的正确虚拟主机。请注意，SSL 服务器需要 IP 虚拟主机。有关更多信息，请参见 `httpd.apache.org`。

# 基于 IP 的虚拟主机

在基于 IP 地址的虚拟主机方法中，你的服务器必须为每个虚拟主机拥有不同的 IP 地址。你使用的 IP 地址已经被配置为引用你的系统。网络系统管理操作可以配置你的机器以支持多个 IP 地址。你的机器可以为每个地址提供独立的物理网络连接，或者一个特定的连接可以配置为同时监听多个 IP 地址。实际上，任何这些 IP 地址都可以访问你的系统。

你可以配置 Apache 为每个虚拟主机运行独立的守护进程，分别监听每个 IP 地址，或者你可以运行一个单一的守护进程来监听所有虚拟主机的请求。要配置一个管理所有虚拟主机的单一守护进程，请使用 `VirtualHost` 指令。要为每个主机配置独立的守护进程，也请使用 `Listen` 指令。

# 基于名称的虚拟主机

使用基于 IP 的虚拟主机时，你受限于系统支持的 IP 地址数量。使用基于名称的虚拟主机时，你可以使用额外的 IP 地址来支持任意数量的虚拟主机。即使你的机器只有一个 IP 地址，你仍然可以支持无限数量的虚拟主机。这种能力由 HTTP/1.1 协议使其成为可能，该协议让服务器能够识别其被访问的名称。此方法要求客户端（即远程用户）使用支持 HTTP/1.1 协议的浏览器，就像当前的浏览器那样（尽管旧版浏览器可能不支持）。使用此类协议的浏览器可以发送 host 头，指定要在机器上使用的特定主机。

如果你的系统只有一个 IP 地址，实施虚拟主机会阻止通过该地址直接访问你的主服务器。你将无法再直接使用主服务器作为 Web 服务器；你只能间接使用它来管理你的虚拟主机。你可以配置一个虚拟主机来管理主服务器的 Web 页面。然后，你将使用主服务器来支持一组作为 Web 站点运行的虚拟主机，而不是让主服务器直接作为一个站点运行。如果你的机器有两个或更多 IP 地址，你可以将一个用于主服务器，将另一个用于你的虚拟主机。你甚至可以在你的服务器上混合使用基于 IP 的虚拟主机和基于名称的虚拟主机。你还可以使用单独的 IP 地址来支持不同的虚拟主机集合。你甚至可以拥有多个域名地址访问同一个虚拟主机。为此，请在选定的 **VirtualHost** 块内放置一个 **ServerAlias** 指令，列出域名名称。

```
ServerAlias www.mypics.com www.greatpics.com
```

发送给你的虚拟主机所用 IP 地址的请求必须匹配其中一个配置的虚拟域名。为了捕获不匹配这些虚拟主机之一的请求，你可以使用 `_default_:*` 设置一个默认虚拟主机。未匹配的请求随后将由该虚拟主机处理。

```
<VirtualHost _default_:*>
```

# 动态虚拟主机

如果你在服务器上实现了许多具有相同配置的虚拟主机，你可以使用一种称为*动态虚拟主机*的技术来动态生成这些虚拟主机。实现虚拟主机的代码将变小得多，因此你的服务器访问它们的速度会更快。添加更多虚拟主机只需创建相应的目录并在 DNS 服务器中添加它们的条目即可。

为了让动态虚拟主机工作，服务器使用 `mod_vhost_alias` 模块（支持 Apache 1.3.6 及以上版本）中的命令，将服务器名称和文档根重写为相应虚拟服务器的名称（对于 1.3.6 之前的旧版 Apache，你使用 `mod_rewrite` 模块）。动态虚拟主机可以是基于名称的或基于 IP 的。在这两种情况下，你都必须以允许服务器使用虚拟主机名而不是服务器自身名称的方式设置 **UseCanonicalName** 指令。对于基于名称的主机，你只需关闭 **UseCanonicalName**。这允许你的服务器从用户请求的 host 头中获取主机名。对于基于 IP 的主机，你将 **UseCanonicalName** 指令设置为 DNS。这允许服务器在 DNS 服务器中查找主机。

```
UseCanonicalName Off
UseCanonicalName DNS
```

然后，你必须启用服务器以定位你的各个虚拟主机的不同文档根目录和 CGI bin 目录。你使用 **VirtualDocumentRoot** 指令来指定虚拟主机目录的模板。例如，如果你将不同的主机目录放在 `/var/www/hosts` 目录中，那么你可以相应地设置 **VirtualDocumentRoot** 指令。

```
VirtualDocumentRoot /var/www/hosts/%0/html
```

当访问该虚拟主机时，`%0` 将被替换为虚拟主机的名称。重要的是，你必须使用该主机的名称创建动态虚拟主机的目录。例如，对于一个名为 **www.mygolf.org** 的动态虚拟主机，你需要创建一个名为 `/var/www/hosts/www.mygolf.org` 的目录。然后创建文档根和 CGI 程序的子目录，如 `/var/www/hosts/www.mygolf.org/html`。对于 CGI 目录，使用 **VirtualScriptAlias** 指令指定你使用的 CGI 子目录。

```
VirtualScriptAlias /var/www/hosts/%0/cgi-bin
```

以下是基于名称的动态虚拟主机指令的一个简单示例：

```
UseCanonicalName Off
VirtualDocumentRoot /var/www/hosts/%0/html
VirtualScriptAlias /var/www/hosts/%0/cgi-bin
```

如果请求了 **www.mygolf.com/html/mypage**，那么它将评估为

```
/var/www/hosts/www.mygolf.com/html/mypage
```

这里展示了一个动态虚拟主机的简单示例：

```
UseCanonicalName Off

NameVirtualHost 192.168.1.5

<VirtualHost 192.168.1.5>
    ServerName www.mygolf.com
    ServerAdmin webmaster@mail.mygolf.com
    VirtualDocumentRoot /var/www/hosts/%0/html
    VirtualScriptAlias /var/www/hosts/%0/cgi-bin
    . .
</VirtualHost>
```

如果要实现基于 IP 的动态虚拟主机，则将 **UseCanonicalName** 设置为 **DNS** 而不是 Off。

```
UseCanonicalName DNS
VirtualDocumentRoot /var/www/hosts/%0/html
VirtualScriptAlias /var/www/hosts/%0/cgi-bin
```

# 插值字符串

`mod_vhost_alias` 模块支持各种插值字符串，每个字符串以 `%` 符号开头，后跟一个数字。正如你所见，`%0` 引用整个 Web 地址。`%1` 仅引用第一段。`%2` 引用第二段，`%-1` 引用最后一部分，而 `%2+` 引用从第二部分开始的内容。例如，如果你只想使用 Web 地址的第二部分作为目录名，你应该使用以下指令：

```
VirtualDocumentRoot /var/www/hosts/%2/html
VirtualScriptAlias /var/www/hosts/%2/cgi-bin
```

在这种情况下，对 **www.mygolf.com/html/mypage** 发出的请求将仅使用 Web 地址的第二部分。对于 **www.mygolf.com**，这将是 "mygolf"，并评估为

```
/var/www/hosts/mygolf/html/mypage
```

如果你使用 `%2+` 代替，如在 `/var/www/hosts/%2+/html` 中，对 **www.mygolf.com/html/mypage** 的请求将评估为

```
/var/www/hosts/mygolf.com/html/mypage
```

