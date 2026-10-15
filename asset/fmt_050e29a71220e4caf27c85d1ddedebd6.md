
# 第 19 章：设置邮件服务器

## 配置虚拟用户

发往你 `sendmail` 服务器的入站邮件将指向你的机器，并请求将邮件投递到特定域名下的某个特定个人。对于 `sendmail` 服务器支持的每个域名，你可以指定如何处理发往该域名接收者的邮件。

在 `sendmail` 中，你可以在 `/etc/mail/virtuosable` 文件中设置虚拟定义。本质上，你是在告诉 `sendmail` 根据你设置的定义将邮件地址重定向到特定的用户名或域名。

如果你的服务器处理多个域的邮件，配置 `virtuosable` 文件就尤为重要。这是因为默认情况下，相同用户名（无论域名是什么）的邮件将存储在同一个邮箱箱中。例如，如果你的服务器处理 `example.com` 和 `linuxxtoys.net` 域的邮件，那么 `chris@example.com` 和 `chris@linuxxtoys.net` 的邮件都将被重定向到 `/var/spool/mail/chris` 邮箱。通过 `virtuosable` 文件，你可以许多方式更改这种行为。`virtuosable` 文件默认是空的。以下是几个示例，说明了如何根据 `virtuosable` 定义以不同的方式引导入站邮件。

```
chris@linuxxtoys.net      chris
cnegus@linuxxtoys.net
francois@linuxxtoys.net  francois@spidermaker.com
info@linuxxtoys.net       info-list
bogus@linuxxtoys.net      error:No such user here
@example.net             example-catchall
@example.com            %@linuxxtoys.net
```

在前两行中，发往 `linuxxtoys.net` 的 `chris` 或 `cnegus` 的入站邮件被重定向到名为 `chris` 的本地邮件服务器的邮箱。在下一行中，发往同一域名下 `francois` 的任何邮件都会去往 `francois@spidermaker.com`。之后，发送给 `info` 用户名的邮件将保存到 `info-list` 邮件账户中。以 `bogus@linuxxtoys.net` 开头的行说明了一个错误情况。在这里，发往用户名 `bogus` 的邮件将被拒绝，并将错误信息“No such user”（没有此类用户）返回给发送者。

> 注意：通常情况下，告诉用户该用户不存在并不是一个好主意。

## 本地主机名称

如果你为一个域名设置了 `sendmail` 服务器，那么在某一天，你可能想在同一台计算机上提供多个域名的服务。要在同一台计算机上创建虚拟服务器，你必须将每个正在服务的域名的名称添加到 `/etc/mail/local-host-names` 文件。例如，如果你的 `sendmail` 服务器正在处理 `linuxxtoys.net`、`example.com` 和 `example.net` 域名的邮件账户，那么 `local-host-names` 文件内容如下：

```
# local-host-names -在此处包含你机器的所有别名。
linuxxtoys.net
example.com
example.net
```

即使你的邮件服务器只服务于一个域名，在该文件中标识该域名也是一个好主意。当发往此处列出的域名的邮件到达服务器时，`sendmail` 知道如何在本地投递这些邮件。对于未在此列出的域名的邮件，`sendmail` 将其解释为需要中继。

> 注意：如果你想卸载当前定向到你的 `sendmail` 的特定域名的邮件处理工作，可以使用 `/etc/mail/mailertable` 文件。在设置了 DNS 记录指向该域名的你的 `sendmail` 后，并在 `mailertable` 文件中列出该名称，你可以指定另一台计算机，`sendmail` 将该域的所有流量转发到那里。例如：

```
example.com smtp:mx1.linuxxtoys.net
```

此示例显示，你的 `sendmail` 接收到的所有发往 `example.com` 的邮件都会转发到名为 `mx1.linuxxtoys.net` 的服务器。`smtp` 表示支持简单邮件传输协议。

## 用户重定向

用户重定向自己邮件的一种方法是使用 `.forward` 文件，用户可以将该文件放置在自己的家目录下（例如，`/home/jkjat/.forward`）。纯文本 `.forward` 文件的格式是逗号分隔的邮件收件者列表。`.forward` 文件的用途包括：

- 将邮件通过管道交给程序以过滤邮箱内容：

  `/usr/bin/procmail`

- 将寄发给一个用户（例如 `jkjat`）的邮件发送到另一个用户（例如 `cht09`, `cht09@other.mbox.com`）

如前所述，你也可以使用 `make all` 来重新构建所有数据库。
