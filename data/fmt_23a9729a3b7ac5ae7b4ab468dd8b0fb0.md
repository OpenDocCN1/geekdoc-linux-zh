
```
evoknow.com
ad-engine.com
classifiedworks.com
```

这里，每一行指定 sendmail 服务器服务的域名。

## 使用 `/etc/mail/virtualtable` 创建虚拟邮件服务器

如果你想为多个域名提供邮件支持，可以使用 sendmail 设置虚拟邮件服务。例如，假设你想为名为 `yourclient.com` 的域名提供虚拟邮件服务。方法如下：

- 1. 在 `/etc/mail/sendmail.cw` 文件中添加该域名（`yourclient.com`），以便 sendmail 接受此主机的邮件。
- 2. 在 `/etc/mail/relay-domains` 文件中添加该域名（`yourclient.com`），以便 sendmail 为该域名中继消息。

要将虚拟域用户映射到一个或多个本地账户，请按如下方式使用 `/etc/mail/virtusertable` 文件：

```
virtual_e-mail address  real_e-mail_address
```

以下是一些示例：

```
webmaster@yourclient.com  mike
mike@yourclient.com      mike
info@yourclient.com     jason
jason@yourclient.com    jason
```

在前面的示例中，发往 `webmaster@yourclient.com` 和 `mike@yourclient.com` 等虚拟电子邮件地址的邮件都将发送给本地用户 `mike`，类似地，发往 `info@yourclient.com` 和 `jason@yourclient`。

邮件会被发送到另一位本地用户 `jason`。这为 `yourclient.com` 提供了他们原本没有的邮件服务器。对外界来说，看起来 `yourclient.com` 拥有一个邮件服务器。如果你还为该域名提供 `yourclient.com` 域名的 DNS 服务，可以通过以下操作让整个过程看起来非常专业：

- 在 `yourclient.com` 域名的 DNS 中添加一条 A 记录，指向你的 sendmail 服务器。例如，如果你的 sendmail 服务器主机的 IP 地址是 `192.168.1.10`，你可以在 `yourclient.com` 域名的 DNS 配置文件中添加以下行。
- 在 `yourclient.com` 域名的 SOA 记录中添加一条 MX 记录，指向 `mail.yourclient.com`。例如：

```
mail.yourclient.com. IN A 192.168.1.10
```

```
yourclient.com. IN MX 5 mail.yourclient.com.
```

这使得其他（毫不知情的）世界认为 `yourclient.com` 拥有一个真正的邮件服务器，只要你已按照前面讨论的虚拟配置设置好 sendmail。

ISP 的网站客户经常请求虚拟邮件服务。换句话说，付费让 ISP 进行网站托管（`www.client-domain.com`）的人或公司也经常请求虚拟邮件服务。在这种情况下，创建一个单一的 `/etc/mail/virtusertable` 通常难以管理。例如，如果你托管数百个域名，每当你或你的助理管理员修改该文件时，`/etc/mail/virtusertable` 就会成为人为错误的来源。在这种情况下，你可以创建一个更易管理的解决方案。例如，假设你需要为两个名为 `client-a.com` 和 `client-b.com` 的客户提供两个虚拟邮件服务。以下是操作步骤：

- 为每个域名创建单独的虚拟电子邮件映射文件。使用 `domain.ftr` 之类的命名约定（`.ftr` 是 fake-to-real 的缩写）。
- 创建一个 `/etc/mail/client-a.ftr` 文件，其中包含通常会放入该域名 `/etc/mail/virtusertable` 中的内容。例如，该文件可能如下所示：

```
user1@client-a.com client1
webmaster@client-a.com unix@home-town-isp.com
@client-a.com client1
```

在此示例文件中，`user1@client-a.com` 地址已被映射到本地账户 `client1`，`webmaster@client-a.com` 已被映射到远程 ISP 账户，而该域名的所有其他可能的电子邮件地址均被映射到本地账户。最后一条条目非常有用且经常被请求。它允许 `client-a.com` 域名在其网站或其他商业出版物和广告中使用他们想要的任何电子邮件地址，同时仍能将邮件正确投递。例如，如果 `www.client-a.com` 发布了一个名为 `info@client-a.com` 的电子邮件地址，任何发送到该账户的邮件都会愉快地由 `client1` 用户处理。
- 现在为第二个客户创建 `/etc/mail/client-b.ftr` 文件。该文件可能与前一个示例类似，但假设 `client-b.com` 的所有者希望所有电子邮件地址自动映射到她在本地 ISP 邮件服务器中已有的账户。在这种情况下，该映射文件将如下所示：

```
@client-b.com $1@home-town-isp.com
```

- 现在你有了两个虚拟用户映射文件，可以使用以下命令创建最终的 `/etc/mail/virtusertable` 文件：

```
touch /etc/mail/virtusertable
```

```
cat *.ftr > /etc/mail/virtusertable
```

这里，第一条命令如果文件尚不存在则创建 `/etc/mail/virtusertable` 文件。第二条命令将所有 `.ftr` 文件连接至 `/etc/mail/virtusertable`。这有效地创建了最终的 `/etc/mail/virtusertable`。
- 现在你可以运行 `makemap` 程序按如下方式创建文件的数据库版本：

```
makemap hash /etc/mail/virtusertable < /etc/mail/virtusertable
```

正如前面的示例所示，创建多个虚拟用户映射文件可以帮助你非常轻松地跟踪各个域名。任何时候你想要更改特定域名的映射，只需修改该域名的 `ftr` 文件，然后使用此处讨论的技术创建最终的 `/etc/mail/virtusertable` 文件即可。

由于大多数邮件客户端程序允许用户将发件人 `From:` 行设置为他们想要的任何内容，你可能不需要对虚拟站点的外发流量进行任何映射。但是，如果你希望确保虚拟邮件站点用户的外发邮件被转换为其虚拟域名，可以使用 `/etc/mail/genericstable` 文件。

例如，假设有一个名为 `classifiedworks.com` 的虚拟邮件站点，你有一个类似 `/etc/mail/classifiedworks.ftr` 的 `.ftr` 文件，其中包含以下行：

```
sales@classifiedworks.com  sheila
```

这里，`sales@classifiedworks.com` 地址被映射到名为 `sheila` 的本地用户。现在当 `sheila` 使用 sendmail 服务器发送邮件时，你希望她的邮件显示为 `sheila@classifiedworks.com` 而不是 `sheila@yourdomain.com`。在这种情况下，创建一个包含以下行的 `/etc/mail/genericstable` 文件：

```
sheila  sales@classifiedworks.com
```

正如你在此处所见，我们正在反转 `virtusertable` 文件的内容。为了保持域名特定信息的分离，你可能希望为每个域名创建一个单独的反向映射文件。假设该文件的扩展名为 `.rtf`。在为你提供虚拟邮件服务的每个域名创建此类文件后，你可以按如下方式创建合并的 `/etc/mail/genericstable` 文件：

```
touch /etc/mail/genericstable
cat *.rtf > /etc/mail/genericstable
```

现在运行 `makemap` 程序以创建此文件的数据库版本：

```
makemap hash /etc/mail/genericstable < /etc/mail/genericstable
```

总之，对于每个虚拟邮件域名，创建一个将假电子邮件地址映射到真实地址的 `.ftr` 文件，并再创建一个将真实地址映射到假电子邮件地址的文件。创建这些文件后，将它们合并以创建 `/etc/mail/virtusertable`（用于 `*.ftr`）和 `/etc/mail/genericstable` 文件（用于 `*.rtf`）。然后按上面所示运行 `makemap` 以创建这些文件的数据库版本。只要你已将每个虚拟域名列在 `/etc/mail/sendmail.cw` 和 `/etc/mail/relay-domains` 文件中，过程就完成了。

## 测试你的 sendmail 配置
