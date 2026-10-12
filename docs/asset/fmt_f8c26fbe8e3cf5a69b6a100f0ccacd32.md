
这字面意思是我们根据 `aliases` 文本文件创建了一个名为 `aliases.db` 的数据库。如果你这样做，就不需要运行 `newaliases` 或重启 `postfix`。同样的技巧也适用于我很快将要介绍的其他一些 `hash` 数据库。

# 迁移到 Linux 业务桌面

## 设置 POP3 或 IMAP 服务器

绝大多数邮件客户端都使用 POP3 或 IMAP 来读取邮件。POP3 和 IMAP 服务器监听来自用户的取邮件请求。这两个协议通常都是 `imap` 包的一部分。要检查你是否安装了 `imap`，请使用以下版本的 `rpm` 命令：

```
rpm -q imap
```

如果系统响应 `imap-2002d` 或类似的内容，则该包已加载。如果没有，请挂载你的发行版 CD-ROM 并安装 `imap`。你可能还需要激活 `/etc/xinetd.d` 目录下的那些服务。你会在那里找到关于 IMAP 和 POP3 的段落。关键是确保服务没有被禁用。以下是我的 `pop-3` 文件内容：

```
service pop-3

{
    socket_type    = stream
    protocol      = tcp
    wait           = no
    user           = root
    server         = /usr/sbin/ipop3d
    disable       = no
}
```

只要 `disable` 设置为 `no`，服务就是激活状态。你现在需要刷新 `xinetd` 进程以使更改生效。找到 `xinetd` 的进程 ID，并向它发送一个 `SIGHUP`。小心那个 `-1`！记住，在这种情况下漏掉连字符可能会导致整个系统崩溃，因为 `init` 的 PID 就是它。

```
kill -1 cat /var/run/xinetd.pid
```

## 不那么笨的 Postfix 小技巧

一旦你的组织变得相对复杂，你会发现自己想要对邮件进行一些看起来并不并不重要的操作。第一点也是最重要的一点当然是邮件能够流通，你可以发送和接收邮件。我敢打赌，人们首先想到的第一个增强功能是垃圾邮件控制，或者未经请求的商业邮件。

# 第15章 电子邮件

UCE。但正如他们所说，那只是一个开始。关于这一点，我打算把最好的留到最后——或者是最糟糕的？让我们进入正题吧，好吗？

### 多重域名与相似地址的困境

想象一下，你决定注册几个域名，所有这些域名都驻留在同一台机器上。毕竟，你的 Linux 系统完全有能力处理这些负载，而且你不想为那些可能是低流量的域名从头开始。。但是，你要做的是一种标准方法，即向你的虚拟公司获取仅包含信息的邮件。你甚至可能希望这些邮件被发送到不同的地方。简而言之，你需要的是：

```
info@mycompany.com
info@mysecondomain.com
info@myinfosite.com
```

现在，你的系统中只能有一个 `info` 登录账号。如果 `info` 不是系统上的一个用户，你可以添加一个 `info` 别名，将 `info` 邮件重定向到真实用户，而不是创建一个伪用户。例如，如果 `mary` 要接收 `info` 的邮件，你会有如下这样的 `aliases` 条目：

```
info: mary@somedomain.com
```

问题出现在你想让所有这些不同的 `info` 地址发送给不同的人时。你不能为 `info` 设置两个别名条目。解决这个问题的方法是使用 `virtertable` 功能。在你的 `main.cf` 文件中查找此行：

```
virtual_maps = hash:/etc/postfix/virtertable
```

这将为你提供虚拟用户表的路径，以及设置这些具有等效用户域名的方法。文件的格式非常简单：

```
username@somedomain.com      real_user
```

```
info@somedomain.com        mary@somedomain.com
info@mysecondomain.com     tom@otherdomain.com
info@myinfosite.com         natika@bigschool.edu
```

### 迁移到 Linux 业务桌面

最后，当你更改文本文件时，你需要更新数据库。运行命令：

```
postmap hash:/etc/postfix/virtertable
```

### 多重域名

解决方案是在 `access` 数据库中阻止来自特定域名的访问。在讨论 hash 映射时你会熟悉这一点。该文件的位置由此变量定义：

```
smtpd_sender_restrictions = hash:/etc/access
```

### 停止垃圾邮件！

另一个技巧是阻止来自特别烦人的域名的邮件。这里有一个例子：不久前，我处理了一起通过中继发送的批量邮件事件。垃圾邮件的格式是向同一个域名发送数百个邮件地址，大部分是该系统中不存在的用户。可能，垃圾邮件发送者希望能命中一些合法的邮件地址。

解决方案是在 `access` 数据库中阻止来自特定域名的访问。在讨论 hash 映射时你会熟悉这一点。该文件的位置由此变量定义：

```
smtpd_sender_restrictions = hash://etc/access
```

# 第15章 电子邮件

这两个设置中的第一个 `smtpd_hello_required` 规定任何入站服务器必须使用 `HELO` 命令识别自身。失败会导致邮件被丢弃。虽然这不应该是问题，但你应该考虑可能没有正确识别身份的朋友邮件会被丢弃。第二个变量 `disable_vrfy_command` 拒绝 `VRFY` 查询，潜在的破解者可能利用它来定位你系统上的用户名。

当然，垃圾邮件发送者使用大量烦人的技巧来绕过你的系统，向你服务器上的成千上万的人发送邮件，并希望某些邮件地址是有效的。因为他们已经在通过其他他们自己的站点进行中继了，所以他们不在乎某些邮件是否退回。这不会影响他们。问题是这会影响到你。许多垃圾邮件发送者也没有提供正确的主机名、返回地址，有时头信息落入这些类别完全是伪造的。为了减少某些流量，在 `main.cf` 中添加以下内容：

```
smtpd_recipient_restrictions =
  reject_invalid_hostname,
  reject_non_fqdn_sender,
  reject_non_fqdn_recipient,
  reject_unknown_sender_domain,
  reject_unknown_recipient_domain,
  reject_unauth_destination,
  reject_unauth_pipelining,
  permit_mynetworks,
  reject_non_fqdn_hostname
```

### 迁移到 Linux 业务桌面

从编辑你的访问文件 `access file` 开始，添加你想拒绝的域名名称，并用空格与 `REJECT` 隔开。

```
spammer.dom             REJECT
anotherspammer.dom    REJECT
```

要激活新的访问数据库，请使用 `postmap` 命令。

```
hash:/etc/mail/access
```

### 跟踪这些邮件

有时，可能需要跟踪在你的系统中传输的邮件消息。原因是什么呢？你可能注意到电子邮件滥用在增加，无论是内部还是外部，在这种情况下，将每条消息的副本发送给管理员是理想的。通过使用 `always_bcc` 参数，每条消息的密送抄送 `bcc` 将发送到你指定的管理员用户。由于该人员将收到大量消息，创建一个临时用户账户是合理的。以这种方式跟踪和记录消息可能是一项艰巨的任务。

以下是操作方法。编辑你的 `main.cf` 文件并添加以下行：

```
always_bcc=adminuser@yourdomain.com
```

管理员是你创建的接收所有这些邮件副本的用户。重新加载 postfix，该用户名将开始接收通过系统的每封邮件的副本。要激活该功能，请执行 postfix：

```
postfix reload
```

### 通过 Webmin 使用 Postfix

Webmin 为 Postfix 提供了丰富的配置选项，你确实应该熟悉它。Webmin 提供了多个模块来管理一切内容，包括当前邮件队列中的消息、客户端和服务器限制、日志以及更多内容。你可以在 Webmin 的 `服务器` 下找到 Postfix 配置，也可以通过在浏览器地址栏中输入如下 URL 直接跳转到它：

```
http://your_server:10000/postfix/index.cgi
```
