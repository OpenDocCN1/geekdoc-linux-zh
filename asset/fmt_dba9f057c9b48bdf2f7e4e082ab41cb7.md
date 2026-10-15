
通过这些信息，我们知道可以在示例 Red Hat 系统上使用用户数据库。如果你的系统不满足这两个条件，在更新配置之前你将无法使用该数据库。

Sendmail 在别名数据库之后、`.forward` 文件之前将用户数据库应用于入邮件。与别名和 `.forward` 文件不同，用户数据库也可以应用于出邮件，以转换发送者地址，并实际上创建一个反向别名。列表 6.6 显示了一个基于列表 6.5 中别名数据库最后四行的真实用户数据库文件。

+ 列表 6.6 示例用户数据库文件

```
[root]# cd /etc/mail

[root]# cat userdb

andy.wright:maildrop andy

andy:mailname andy.wright@foofirds.org

sara.henson:maildrop sara

sara:mailname sara.henson@foofirds.org

kathy.McCafferty:maildrop kathy

kathleen.McCafferty:maildrop kathy

kathy:mailname katheleen.mccafferty@foofirds.org

[root]# makemap btree userdb.db < userdb
```

在列表 6.6 中，我们切换到 `/etc/mail` 目录并显示我们创建的用户数据库文件的内容。我们随意将此文件命名为 `userdb`。与别名文件一样，用户数据库文件在被 Sendmail 使用之前必须转换为数据库。我们使用 `makemap` 命令来构建数据库。`makemap` 程序读取标准输入并写入所选类型的数据库。`makemap` 命令在本章稍后的部分有详细描述。在列表 6.6 中，该命令有两个参数：数据库类型和要写入的数据库名。用户数据库必须是 `btree` 类型，且数据库名必须是 Sendmail 配置中定义的。

除了 `maildrop` 关键字外，用户数据库条目与别名数据库条目非常相似。`mailname` 条目重写发送地址。冒号（:）之前的值是本地用户名。`mailname` 关键字后面的值是应该在邮件上使用的发送者地址。因此，该行

```
andy:mailname andy.wright@foofirds.org
```

将来自用户 andy 的所有邮件发送者地址转换为

```
andy.wright@foobirds.org。
```

转换出邮件地址是一个重要功能，因为它平衡了地址的处理方式。远程用户发送 andy.wright@foobirds.org。foobirds.org 的 MX 记录将邮件导向一个服务器——说是 .foobirds.org。如果没有 `mailname` 条目和用户数据库，当他回复邮件时将以 `andy@foobirds.org` 发出。这并不优雅！有了上面的 `mailname` 条目，他的目标正是远程用户所期的。很棒！

```
andy.wright@foobirds.org, 这正是远程用户所期的。
```

我们可以在用户数据库中重写如下 `maildrop` 条目：

```
andy.wright:maildrop andy
```

这显示了与别名条目一样，`maildrop` 条目也可以接受多个交付地址。这些条目除了增加了 `maildrop` 关键字外，唯一的区别是 `maildrop` 条目必须指向真实地址。

![](img/9639113aa446fb8976cb3d377f7aafdd_178_0.png)

注意：事实上，如果此系统具有 6.5 所示的别名文件，不需要 6.6 所示的 `maildrop` 行。该别名文件已经完成了地址映射。6.6 所示的 `maildrop` 行只是示例。如果你决定使用 `maildrop` 条目，请不要重复别名数据库中已有的条目。

`mailname` 条目提供了别名数据库中不具备的功能。`mailname` 条目重写出邮件地址。冒号（:）之前的值是本地用户名。`mailname` 关键字后面的值是应该在邮件上使用的发送者地址。正如我们看到的

```
andy:maildrop andy
```

然而，用户数据库并不是重写出邮件地址的唯一方法，我们稍后会看到。使用用户数据库的决定主要取决于你最喜欢并认为最易于理解的数据库。虽然使用用户数据库在程度上是一个选择问题，但使用访问数据库往往是必须的，特别是在充满垃圾邮件发送者的世界里。

# 访问数据库

访问数据库是邮件 Relay 服务器的一个强大配置工具。它对中继过程提供了比 `relay-domains` 文件更精细的控制。与 `relay-domains` 文件不同，访问数据库不是 Sendmail 的默认部分。

# access 数据库 157

配置。如果你想使用 access 数据库，必须在配置中添加 `access_db` 功能。`generic-linux.mc` 配置未包含对 access 数据库的支持，但 `redhat.mc` 配置通过以下命令包含了支持：

```
FEATURE(`access_db`)
```

此命令使用默认的数据库类型哈希和默认路径 `/etc/mail/access.db`。你可以通过向命令提供可选的参数字段来更改这些值，例如例所示：

```
FEATURE(`access_db`,'btree /var/mail/access')
```

然而，我不建议使用这些默认值。哈希类型在所有 Linux 系统上都支持，并且所有的管理员都能 `/etc/mail` 中找到 access 数据库。更改这些值不会带来任何收益，反而可能导致混乱。请在配置中添加 `access_db` 功能，但请使用默认参数。

使用 access 数据库根据邮件的源或目的来接受或拒绝邮件。`address`（地址）字段是数据库的键，而 `action`（动作）字段是从数据库返回的值，指定了 Sendmail 针对邮件或来自指定地址应采取的动作。

# Address 字段

`address` 字段可以定义用户、单个电子邮件地址、源 IP 网络地址或域名。`address` 字段可以以可选的标签（tag）开头，告诉 Sendmail 将该字段的检查限制在某些条件条件下。提供了三个可选的标签关键字：

- `To:` 仅当邮件被发送到指定地址时，执行该动作。
- `From:` 仅当从指定地址接收邮件时，执行该动作。
- `Connect:` 仅当指定地址是 SMTP 连接结束时的系统地址时，执行该动作。

tag 字段不是必须的。它对邮件访问提供了更细粒度的控制，但并非总是需要细粒控制。在很多情况下，你希望对中继（relaying）有更广泛的控制而不是更细的控制，因为你既不想接受来自不良源的邮件，也不想向他们发送邮件。如果不包含 tag 字段，默认将地址视为邮件的源。因此，默认情况下，只有当邮件来自指定地址时才会执行动作。在 Sendmail 配置中添加以下 `blacklist_recipient` 功能：

```
FEATURE(`blacklist_recipients`)
```
