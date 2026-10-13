
`sendmail` 在 Berkeley 数据库格式的二进制文件 `/etc/userdb.db` 中查找数据库。按照以下步骤创建用户数据库文件：

1. 编辑文件 `/etc/mail/userdb`，并为每个需要识别邮件投递点的用户添加行。这些行看起来所示：

```
bob:name robert.smith@someplace.net
robert.smith:maitrop bob
```

在这种情况下，用户名 `bob` 发出的邮件将将地址标记为 `robert.smith@someplace.net`，而发往该地址的入站邮件将发送给用户 `bob`。

2. 使用以下命令将文本文件 `/etc/mail/userdb` 转换为 Berkeley 数据库文件，然后可以使用 `makemap` 运行 `sendmail`：

```bash
makemap btree /etc/mail/userdb < /etc/mail/userdb
```

这会从文本文件 `/etc/mail/userdb` 创建数据库文件 `/etc/mail/userdb.db`。

> 你必须记住在每次更改 `/etc/mail/userdb` 后运行 `makemap`；否则 `sendmail` 在发送邮件时将不会使用你最新的数据库。

## 准备邮件投递表

邮件投递数据库指定如何路由发往特定域的邮件。你在文本文件 `/etc/mail/mailertable` 中指定这些路由规则。例如，假设所有针对 `mydomain.net` 的邮件都不应发送到主机 `host.mydomain.net`。你可以通过 `/etc/mail/mailertable` 中的以下条目来实现：

```
.mydomain.net smtp:mailhost.mydomain.net
```

每行的左侧是域名。右侧形式为 `mailer:host` 形式，其中 `mailer` 是邮件传输代理，`host` 是指向 `mailer` 的主机名。

编辑文件 `/etc/mail/mailertable` 后，你必须运行以下命令 `makemap` 将其转换为二进制数据库：

```bash
makemap /etc/mail/mailertable < /etc/mail/mailertable
```

这里有一种更简单的方法来确保在进行任何更改后重新构建所有内容——只需以 root 登录并输入以下命令：

```bash
cd /etc/mail
make
```

## 第三部分：网络化 Linux

## 准备访问数据库

邮件投递数据库指定如何路由发往特定域的邮件。你在文本文件 `/etc/mail/mailertable` 中指定这些路由规则。例如，假设所有针对 `mydomain.net` 的邮件都不应发送到主机 `host.mydomain.net`。你可以通过 `/etc/mail/mailertable` 中的以下条目来实现：

```
.mydomain.net smtp:mailhost.mydomain.net
```

每行的左侧是域名。右侧形式为 `mailer:host` 形式，其中 `mailer` 是邮件传输代理，`host` 是指向 `mailer` 的主机名。邮件投递数据库指定如何路由发往特定域的邮件。你在文本文件 `/etc/mail/mailertable` 中指定这些路由规则。例如，假设所有针对 `mydomain.net` 的邮件都不应发送到主机 `host.mydomain.net`。邮件投递数据库的右侧指定了 `sendmail` 应该的操作。以下是一个示例：

```
spammer@somewhere.net      DISCARD
mail.com                   RELAY
buddy.com                   REJECT
192.168.1.150:2002:c5        REJECT
some,unresolvable.domain  OK
junk.com                   ERROR
```
