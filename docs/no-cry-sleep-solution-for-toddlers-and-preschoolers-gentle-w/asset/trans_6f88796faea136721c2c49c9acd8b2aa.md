

如果你的系统只有一个 IP 地址，实现虚拟主机将阻止使用该地址访问你的主服务器。你将无法再直接将主服务器用作 Web 服务器；你只能间接地使用它来管理你的虚拟主机。你可以配置一个虚拟主机来管理主服务器的网页。然后你将使用主服务器来支持一组作为网站运行的虚拟主机，而不是主服务器直接作为一个站点运行。如果你的机器有两个或更多 IP 地址，你可以使用其中一个作为主服务器，另一个用于你的虚拟主机。你甚至可以在服务器上混合使用基于 IP 的虚拟主机和基于名称的虚拟主机。你也可以使用单独的 IP 地址来支持不同的虚拟主机集合。你还可以让多个域名访问同一个虚拟主机。要这样做，请在选定的 VirtualHost 块内放置一个 ServerAlias 指令列出域名。

```
ServerAlias www.mypics.com www.greatpics.com
```

发送到用于你的虚拟主机的 IP 地址的请求必须与其中一个配置的虚拟域名匹配。为了捕获不匹配这些虚拟主机之一的请求，你可以使用 _default_:* 设置一个默认虚拟主机。未匹配的请求随后将由此虚拟主机处理。

```
<VirtualHost _default_:*>
```

## 动态虚拟主机

如果你在服务器上实现了许多具有相同配置的虚拟主机，你可以使用一种称为动态虚拟主机技术来动态生成这些虚拟主机。实现虚拟主机的代码变得更小，因此你的服务器访问它们的速度更快。添加更多虚拟主机变得很简单，只需创建适当的目录并在 DNS 服务器中为它们添加条目即可。

要使动态虚拟主机工作，服务器使用 mod_vhost_alias 模块中的命令（支持 Apache 1.3.6 及更高版本）来重写服务器名称和文档根目录，使其成为适当虚拟服务器的名称和文档根目录（对于 1.3.6 之前的旧版 Apache，你使用 mod_rewrite 模块）。动态虚拟主机可以是基于名称的，也可以是基于 IP 的。在任何一种情况下，你都必须以允许服务器使用虚拟主机名而不是服务器自己的名称的方式设置 UseCanonicalName 指令。对于基于名称的主机，你只需关闭 UseCanonicalName。这允许你的服务器从用户请求的 host header 中获取主机名。对于基于 IP 的主机，你将 UseCanonicalName 指令设置为 DNS。这允许服务器在 DNS 服务器中查找主机。

```
UseCanonicalName Off
UseCanonicalName DNS
```

然后你必须启用服务器以定位你各种虚拟主机的不同文档根目录和 CGI bin 目录。你使用 VirtualDocumentRoot 指令来指定虚拟主机目录的模板。例如，如果你将不同的主机目录放在 /var/www/hosts 目录中，那么你可以相应地设置 VirtualDocumentRoot 指令：

```
VirtualDocumentRoot /var/www/hosts/%0/html
```

%0 将在访问该虚拟主机时被替换为虚拟主机的名称。重要的是，你必须使用该主机的名称创建动态虚拟主机的目录。例如，对于名为 www.mygolf.org 的动态虚拟主机，你将创建一个名为 /var/www/hosts/www.mygolf.org 的目录。然后像 /var/www/hosts/www.mygolf.org/html 这样创建文档根和 CGI 程序的子目录。对于 CGI 目录，使用 VirtualScriptAlias 指令指定你使用的 CGI 子目录。

```
VirtualScriptAlias /var/www/hosts/%0/cgi-bin
```

以下是基于名称的动态虚拟主机指令的简单示例：

```
UseCanonicalName Off
VirtualDocumentRoot /var/www/hosts/%0/html
VirtualScriptAlias /var/www/hosts/%0/cgi-bin
```

如果对 www.mygolf.com/html/mypage 发出请求，那将求值为 /var/www/hosts/www.mygolf.com/html/mypage

以下是动态虚拟主机的简单示例：

```
UseCanonicalName Off
NameVirtualHost 192.168.1.5
<VirtualHost 192.168.1.5>
ServerName www.mygolf.com
ServerAdmin webmaster@mail.mygolf.com
VirtualDocumentRoot /var/www/hosts/%0/html
VirtualScriptAlias /var/www/hosts/%0/cgi-bin
...
</VirtualHost>
```

要实现基于 IP 的动态虚拟主机，请将 UseCanonicalName 设置为 DNS 而不是 Off。

```
UseCanonicalName DNS
VirtualDocumentRoot /var/www/hosts/%0/html
VirtualScriptAlias /var/www/hosts/%0/cgi-bin
```

## 插值字符串

mod_vhosts_alias 模块支持各种插值字符串，每个字符串都以 $ 符号开头，后跟一个数字。如你所见，$0 引用整个 Web 地址。$1 仅引用第一段，$2 引用第二段，$-1 引用最后一部分，$2- 引用从第二部分开始的部分。例如，如果你只想使用 Web 地址的第二部分作为目录名，你将使用以下指令：

```
VirtualDocumentRoot /var/www/hosts/%2/html
VirtualScriptAlias /var/www/hosts/%2/cgi-bin
```

