

## Apache 虚拟主机

虚拟主机允许 Apache Web 服务器作为其自身的一部分托管多个网站。实际上，服务器可以充当多个服务器，每个托管网站对外部用户来说看起来都是独立的。Apache 支持基于 IP 地址的虚拟主机和基于名称的虚拟主机。基于 IP 地址的虚拟主机使用有效的注册 IP 地址，而基于名称的虚拟主机使用完全限定的域名。这些域名由请求浏览器的主机头提供。然后服务器可以根据域名 alone 确定要使用的正确虚拟主机。请注意，SSL 服务器需要 IP 虚拟主机。有关更多信息，请参阅 httpd.apache.org。

## 基于 IP 地址的虚拟主机

在基于 IP 地址的虚拟主机方法中，您的服务器必须为每个虚拟主机拥有不同的 IP 地址。您使用的 IP 地址已设置好以引用您的系统。网络系统管理操作可以设置您的机器以支持多个 IP 地址。您的机器可以为每个地址拥有单独的物理网络连接，或者特定连接可以配置为同时监听多个 IP 地址。实际上，任何 IP 地址都可以访问您的系统。

您可以配置 Apache 为每个虚拟主机运行一个单独的守护进程，分别监听每个 IP 地址，或者您可以让单个守护进程运行，监听所有虚拟主机的请求。要设置单个守护进程管理所有虚拟主机，请使用 VirtualHost 指令。要为每个主机设置单独的守护进程，也请使用 Listen 指令。

必须为每个虚拟主机设置一个 VirtualHost 指令块。在每个 VirtualHost 块内，您放置访问主机的适当指令。您应该具有 ServerAdmin、ServerName、DocumentRoot 和 TransferLog 指令，指定该主机的特定值。您可以在 VirtualHost 块中使用任何指令，除了 ServerType（1.3）、StartServers、MaxSpareServers、MinSpareServers、MaxRequestsPerChild、Listen、PidFile、TypesConfig、ServerRoot 和 NameVirtualHost。

尽管您可以在 VirtualHost 指令中的地址使用域名，但使用实际 IP 地址更为可取。这样，您就不依赖于域名服务来建立正确的域名关联。请确保为您的主服务器保留一个 IP 地址。如果您将机器上所有可用的 IP 地址都用于虚拟主机，您将无法再访问您的主服务器。当然，您也可以将主服务器重新配置为虚拟主机。以下示例显示了两个基于 IP 的虚拟主机块：一个使用 IP 地址，另一个使用与 IP 地址关联的域名：

```
<VirtualHost 192.168.1.23>
ServerAdmin webmaster@mail.mypics.com
DocumentRoot /groups/mypics/html
ServerName www.mypics.com
ErrorLog /groups/mypics/logs/error_log
....
</VirtualHost>
```

```
<VirtualHost www.myproj.org>
ServerAdmin webmaster@mail.myproj.org
DocumentRoot /groups/myproj/html
ServerName www.myproj.org
ErrorLog /groups/myproj/logs/error_log
...
</VirtualHost>
```

## 基于名称的虚拟主机

使用基于 IP 的虚拟主机，您受限于系统支持的 IP 地址数量。使用基于名称的虚拟主机，您可以使用不增加 IP 地址的方式支持任意数量的虚拟主机。即使您的机器只有一个 IP 地址，您仍然可以支持无限数量的虚拟主机。这种功能由 HTTP/1.1 协议提供，该协议允许服务器识别其被访问的名称。此方法要求客户端，即远程用户，使用支持 HTTP/1.1 协议的浏览器，如当前浏览器所做的那样（尽管较旧的浏览器可能不支持）。使用此类协议的浏览器可以发送主机头，指定机器上要使用的特定主机。

要实现基于名称的虚拟主机，请为每个主机使用 VirtualHost 指令，并使用 NameVirtualHost 指令指定要用于虚拟主机的 IP 地址。如果您的系统只有一个 IP 地址，您需要使用该地址。在 VirtualHost 指令内，您使用 ServerName 指令指定要为该主机使用的域名。使用 ServerName 指定域名非常重要，以避免 DNS 查找。DNS 查找失败会禁用虚拟主机。VirtualHost 指令各自以 NameVirtualHost 指令中指定的相同 IP 地址作为其参数。您在 VirtualHost 块内使用 Apache 指令分别配置每个主机。基于名称的虚拟主机使用主机头中指定的域名地址来确定要使用的虚拟主机。如果不存在此类信息，则第一个主机用作默认值。以下示例实现了两个基于名称的虚拟主机。

在这里，www.mypics.com 和 www.myproj.org 被实现为基于名称的虚拟主机，而不是基于 IP 的主机：

```
ServerName turtle.mytrek.com

NameVirtualHost 192.168.1.5

<VirtualHost 192.168.1.5>
  ServerName www.mypics.com
  ServerAdmin webmaster@mail.mypics.com
  DocumentRoot /var/www/mypics/html
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

