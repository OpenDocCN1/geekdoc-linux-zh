
## 基于名称的虚拟主机

使用基于 IP 的虚拟主机时，你受限于系统支持的 IP 地址数量。使用基于名称的虚拟主机时，你可以在不使用额外 IP 地址的情况下支持任意数量的虚拟主机。即使你的机器只有一个 IP 地址，你仍然支持无限数量的虚拟主机。这种功能是通过 `HTTP/1.1` 协议实现的，它允许服务器识别其被访问时的名称。这种方法要求客户端（远程用户）使用支持 `HTTP/1.1` 协议的浏览器（目前的浏览器都支持，但其他可能不支持）。使用此类协议的浏览器可以发送一个 `host` 头部，指定在机器上使用的特定主机。

要实现基于名称的虚拟主机，请为每个主机使用 `VirtualHost` 指令，为虚拟主机使用 `NameVirtualHost` 指令。如果你的系统只有一个 IP 地址，你需要使用该地址。在 `VirtualHost` 指令中，使用 `ServerName` 指令来指定你想为该主机使用的名称。使用 `ServerName` 指定域名对于避免 DNS 查询非常重要。DNS 查询失败将禁用该虚拟主机。每个 `VirtualHost` 指令都将 `NameVirtualHost` 指令中指定的 IP 地址作为其参数。在 `VirtualHost` 块中使用 Apache 指令来单独配置每个主机。基于名称的虚拟主机使用 `host` 头部指定的域名来确定要使用的虚拟主机。如果不存在此类信息，则使用第一个主机作为默认主机。下面的示例实现了两个名称虚拟主机。`www.mypics` 和 `www.myproj` 被实现为基于名称的虚拟主机，而不是基于 IP 的主机：

```
<VirtualHost 192.168.1.5>

ServerName www.mypics.com

ServerAdmin webmaster@mail.mypics.com

DocumentRoot /var/www/mypics/html

ErrorLog /var/www/mypics/logs/error_log

...

<VirtualHost 192.168.1.5>

ServerName www.myproj.org

ServerAdmin webmaster@mail.myproj.org

DocumentRoot /var/www/myproj/html

ErrorLog /var/www/myproj/logs/error_log

</VirtualHost>
```

如果你的系统只有一个 IP 地址，实现虚拟主机将防止通过该地址访问你的主服务器。你将无法直接将主服务器作为 Web 服务器；你可以间接使用它来管理你的虚拟主机。你可以配置一个虚拟主机来管理主服务器的 Web 页面。然后，你将使用主服务器来支持一组作为网站运行的虚拟主机，而不是主服务器直接运行。如果你的系统有两个或多个 IP 地址，你可以使用其中一个用于主服务器，另一个用于你的虚拟主机。你甚至可以在服务器上同时使用基于 IP 的虚拟主机和基于名称的虚拟主机。你还可以使用 IP 地址来支持不同的虚拟主机组。你可以进一步让域名地址访问 `ServerAlias` 指令。

```
ServerAlias www.mypics.com www.greatpics.com
```

指向你虚拟主机的 IP 地址必须匹配配置的虚拟域名之一。对于不匹配这些虚拟主机的请求，可以使用 `_default*` 设置一个默认主机。

```
<VirtualHost _default*>
```

## 动态虚拟主机

如果你实现了许多虚拟主机，可以使用名为“动态虚拟主机”的技术来动态生成这些虚拟主机。实现虚拟主机的代码会变得更小，结果是服务器访问它们的速度更快。添加更多虚拟主机只需创建相应的目录并在 DNS 服务器中添加条目。

要实现动态虚拟主机，服务器使用 `mod_alias` 命令（Apache 1.3 及更高版本支持）来重写服务器名称和文档根（1.3 之前的版本使用 `mod_rewrite` 模块）。动态虚拟主机可以是基于名称的也可以是基于 IP 的。在任何情况下，你都必须设置 `CanonicalName` 指令，以便服务器使用虚拟的主机名。对于基于名称的主机，只需关闭 `CanonicalName`。这允许服务器从请求头中获取主机名。对于基于 IP 的主机，你将 `CanonicalName` 指令设置为 `DNS`。这允许服务器在 DNS 中查找。

```
UseCanonicalName Off
CanonicalName DNS
```

然后你必须启用服务器定位不同的文档根并为虚拟主机使用 `VirtualDocumentRoot` 指令。例如，如果你将不同的主机目录放在 `/var/www/hosts`，你可以设置 `VirtualDocumentRoot` 指令来指定子目录。

```
VirtualDocumentRoot /var/www/hosts/%0/html
```

当安装虚拟主机时，`%0` 将替换为虚拟主机名。使用该主机名创建动态虚拟主机目录是重要的。例如，对于名为 `myproj.org` 的虚拟主机，你会创建一个名为 `/var/www/hosts/myproj.org` 的目录。然后在 `/var/www/hosts/myproj.org/html` 中为文档根和 CGI 程序创建子目录。使用 `VirtualScriptAlias` 指令来指定 CGI。

```
VirtualScriptAlias /var/www/hosts/%0/cgi-bin
```

基于名称的动态主机的简单示例：

```
UseCanonicalName Off
VirtualDocumentRoot /var/www/hosts/%0/html
VirtualScriptAlias /var/www/hosts/%0/cgi-bin
```

如果对 `myproj.org/html/mypage` 发起请求，它将求值为 `/var/www/hosts/myproj.org/html/mypage`。这里显示了一个动态虚拟主机的简单示例：

```
<VirtualHost 192.168.1.5>
ServerName my.myproj.org
ServerAdmin webmaster@mail.myproj.org
VirtualDocumentRoot /var/www/hosts/%0/html
VirtualScriptAlias /var/www/hosts/%0/cgi-bin
...
</VirtualHost>
```

要实现基于 IP 的动态主机，将 `CanonicalName` 设置为 `DNS` 而不是 `Off`。

```
UseCanonicalName DNS
VirtualDocumentRoot /var/www/hosts/%0/html
VirtualScriptAlias /var/www/hosts/%0/cgi-bin
```

## 插值字符串

`mod_alias` 支持各种插值字符串，每个以 `%` 开头后跟一个数字。如你所见，`%0` 引用整个地址，`%1` 只引用第一段，`%2` 引用第二个，`-1` 引用最后，`-2` 从倒第二部分引用。例如，如果你想使用 Web 地址的第二部分作为目录名称，将使用以下指令：

```
VirtualDocumentRoot /var/www/hosts/$2/html
VirtualScriptAlias /var/www/hosts/$2/cgi-bin
```

在这种情况下，对 `www.golf.com/mypage` 的请求将仅使用 Web 地址的第二部分。这将是 `www.golf.com` 中的 "golf"，并求值为 `/var/www/hosts/golf/html/mypage`。

如果你使用 `%2`，例如在 `/var/www/hosts/%2/html` 中，对 `www.golf.com/mypage` 的请求将求值为 `/var/www/hosts/golf.com/html/mypage`。相同的方法适用于 IP 地址，其中 `%1` 引用第一个 IP 地址段，`%2` 引用第二个段，依此类推。

## 虚拟主机的日志

动态虚拟主机的一个缺点是你可以为所有主机设置一个日志。但是，你可以创建自己的 shell 脚本来提取该日志中不同主机的条目。

```
LogFormat "%h %l %u %t %r\" %s %b"
CustomLog logs/access_log common
```

## IP 地址

实现动态虚拟主机很慢，因为服务器将执行 DNS 查询以通过其 IP 地址发现服务器名称。你可以通过直接使用虚拟主机的 IP 地址来跳过此步骤。因此，对于 IP 主机 `192.198.1.6`，你会创建一个目录 `/var/www/hosts/192.198.1.6`，并为主机的文档根创建一个子目录。你将使用 `VirtualDocumentRoot` 和 `VirtualScriptAlias` 指令使用 IP 地址作为目录名。现在，IP 地址可以直接映射到文档根目录，不再需要 DNS 查询。还要确保在日志中包含 IP 地址，`%A`。
