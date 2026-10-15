
它们本身可被用作分配给其他参数的值。在下一个示例中，myhostname 和 mydomain 被设置为邮件服务器运行的主机及其网络域：

```
myhostname=turtle.mytrek.com
mydomain=mytrek.com
```

myorigin 参数指定服务器发送的电子邮件的源地址。默认情况下，它被设置为 myhostname 参数的值，如下所示。请注意，$ 在 myhostname 变量之前以便对其进行求值。

```
myorigin=$myhostname
```

如果您使用的是直接连接到 Internet 的单台系统，您可能希望保留此配置，将邮件标记为由您的主机发送。但是，如果您的系统作为网络的网关运行，您的邮件服务器会从该网络上的不同主机发送邮件。您可能希望将源地址更改为域名，以便邮件被视为从该域发送。

```
myorigin=$mydomain
```

## 本地网络

mydestination 参数保存您的邮件服务器将接收邮件的域名列表。默认情况下，这些包括 localhost 和您系统的主机名。

```
mydestination = $myhostname localhost.$mydomain
```

如果您希望邮件服务器接收整个本地网络的邮件，则需要同时指定其域名。这样，服务器就可以接收仅针对该域而不是特定主机的邮件。

```
mydestination = $myhostname localhost.$mydomain $mydomain
```

此外，如果您的主机使用其他主机名，并且 DNS 记录通过这些名称标识您的主机，则您还需要指定这些名称。例如，您的主机也可能是邮件可以发送到的 Web 服务器。主机 turtle.mytrek.com 也可能被标识为网站 www.mytrek.com。两个名称都必须列在 mydestination 参数中。

```
mydestination = $myhostname localhost.$mydomain $mydomain www.$mydomain
```

如果您的系统是一个或多个本地网络的网关，您可以使用 mynetworks 参数指定它们。这允许您的邮件服务器中继发往这些网络的邮件。网络使用其 IP 地址指定。relay_domains 参数让您可以指定可以中继消息的网络的域名地址。默认情况下，它被设置为 mydestination：

```
mynetworks=192.168.0.0
relay_domains=$mydestination
```

连接到 Internet 的本地网络中的主机需要知道中继主机，即邮件服务器的身份。您使用 relayhost 参数设置此项。此外，myorigin 应仅设置为 mydomain。如果有 DNS 服务器将网关标识为邮件服务器，您只需将 relayhost 设置为 mydomain 的值。如果没有，则 relayhost 应设置为网关/邮件服务器的特定主机名。如果您的本地网络未运行 DNS 服务器，请确保将 disable_dns_lookups 设置为 yes。

```
relay_host=$mydomain
```

## 直接连接

如果您的系统直接连接到 Internet，并且您使用 ISP 接收邮件，您可以将 Postfix 配置为 null 客户端仅发送邮件。将 relay_host 参数设置为仅您的域名。此外，在 master.cf 文件中，注释掉 SMTP 服务器和本地投递代理条目。

```
relayhost = $mydomain
```

## 伪装

如果您的邮件服务器在本地网络的网关上运行，并且您希望隐藏该网络中的主机，您可以选择伪装本地主机，让它看起来所有邮件都来自域本身，而不是特定主机。要设置此选项，您使用 masquerade_domains 参数。在以下示例中，所有由本地主机如 rabbit.mytrek.com 发送的邮件都将被标记为仅来自 mytrek.com。因此，由用户 chris@rabbit.mytrek.com 发送的消息将被发送为来自 chris@mytrek.com。

```
masquerade_domains = $mydomain
```

默认情况下，收到的邮件不会被伪装。这允许 Postfix 仍然将收到的邮件投递到特定主机。如果您希望收到的邮件也被伪装，您必须将 envelope_recipients 参数添加到分配给 masquerade_class 参数的值列表中。在这种情况下，Postfix 将不再能够投递收到的邮件。

## 虚拟域

如果您的网络已实现虚拟域，您将需要设置一个虚拟域表，然后使用 virtual_maps 选项指定该表。设置表很简单，只需在文本文件如 /etc/postfix/virtual 中列出虚拟名称及其真实地址。然后使用 postmap 命令创建 Postfix 表：

```
postmap /etc/postfix/virtual
```
