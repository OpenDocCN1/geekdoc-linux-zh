
```
FEATURE(`no_default_msa`, `dnl`)dnl
FEATURE(`smash`, `/usr/sbin/smsh`)dnl
FEATURE(`mailertable`, `hash -etc/mail/mailertable.db`)dnl
FEATURE(`virtuosert`, `hash -etc/mail/virtuosert.db`)dnl
FEATURE(`redirect`)dnl
FEATURE(`always_add domain`)dnl
FEATURE(`use_cw_file`)dnl
FEATURE(`use_ct_file`)dnl
FEATURE(`local_procmail`, `procmail -T -Y -a $d -u $d`)dnl
FEATURE(`access_db`, `hash -TCMFP` -o /etc/mail/access.db`)dnl
FEATURE(`blacklist_recipients`)dnl
```

`FEATURE` 宏用于设置某些特殊的长期功能。`no_default_msa` 特性告诉 sendmail 不要生成默认的 MSA 守护进程（通常是 `/usr/sbin/smsh`，作为接收邮件的简单 shell）。`mailertable` 和 `virtuosable` 选项设置了邮件传输表数据库和虚拟主机表数据库的位置。`redirect` 选项允许你拒绝已移动用户的邮件并提供新地址。`always_add domain` 选项导致所有投递邮件上将本地域名添加到主机名中。`use_cw_file` 和 `use_ct_file` 选项分别告知自身使用 `/etc/mail/local-host` 作为此服务器的备用主机名，使用 `/etc/mail/trusted-users` 作为受信用户。`local_procmail` 特性设置了...`confPRIVACY_FLAGS` 标志会导致 sendmail 在控制邮件上注入身份验证。例如，`authwarnings` `Authentication-Warning` 头部用于通知登录，而 `noexcept` 设置防止这些服务被请求。`restrict` 选项为 sendmail 提供了 `-q` 选项。

（注：原文此处似乎存在大量重复和乱码的文本片段，已根据指令逻辑进行了清理和翻译处理）

# 第 19 章：设置邮件服务器

来自 `chris@linuxxtoys.net` 的邮件。在在上一个例子中，转发到特定个人 `former-user@linuxxtoys.net` 的邮件被拒绝，并向发送者返回了自定义的错误信息（以防该用户不再在此工作）。

> 注意：在根据用户电子邮件地址创建中继规则时请务必小心。因为这些地址是由用户自己报告的，容易被伪造。

一旦你调整了此文件以适应你的需求，必须重新构建访问数据库 `access.db` 文件使更改生效。关于此主题的信息，请参阅“启动 sendmail 并生成数据库文件”。

## 配置虚拟服务器

如果你为一个域名设置了 sendmail 服务器，那么在某一天，你可能想在同一台计算机上提供多个域名的服务。要在同一台计算机上创建虚拟服务器，你必须将每个正在服务的域名的名称添加到 `/etc/mail/local-host-names` 文件。

例如，如果你的 sendmail 服务器正在处理 `linuxxtoys.net`、`example.com` 和 `example.net` 域名的邮件账户，那么 `local-host-names` 文件内容如下：

```
# local-host-names -在此处包含你机器的所有别名。
linuxxtoys.net
example.com
example.net
```

即使你的邮件服务器只服务于一个域名，在该文件中标识该域名也是一个好主意。当发往此处列出的域名的邮件到达服务器时，sendmail 知道如何如何在本地投递这些邮件。对于未在此列出的域名的邮件，sendmail 将其解释为需要中继。

> 注意：如果你想卸载当前定向到你的 sendmail 的特定域名的邮件处理工作，可以使用 `/etc/mail/mailertable` 文件。在设置了 DNS 记录指向该域名的你的 sendmail 后，并在 `mailertable` 文件中列出该名称，你可以指定另一台计算机，sendmail 将该域的所有流量转发到那里。例如：

```
example.com smtp:mx1.linuxxtoys.net
```

此示例显示，你的 sendmail 接收到的所有发往 `example.com` 的邮件都会转发到名为 `mx1.linuxxtoys.net` 的服务器。`smtp` 表示支持简单邮件传输协议。

## 配置虚拟用户

发往你 sendmail 服务器的入站邮件将指向你的机器，并请求将邮件投递到特定域名下的某个特定个人。对于 sendmail 服务器支持的每个域名，你可以指定如何处理发往该域名接收者的邮件。

在 sendmail 中，你可以在 `/etc/mail/virtuosable` 文件中设置虚拟定义。本质上，你是在告诉 sendmail 根据你设置的定义将邮件地址重定向到特定的用户名或域名。

如果你的服务器处理多个域的邮件，配置 `virtuosable` 文件就尤为重要。这是因为默认情况下，相同用户名（无论域名是什么）的邮件将存储在同一个邮箱箱中。例如，如果你的服务器处理 `example.com` 和 `linuxxtoys.net` 域的邮件，那么 `chris@example.com` 和 `chris@linuxxtoys.net` 的邮件都将被重定向到 `/var/spool/mail/chris` 邮箱。通过 `virtuosable` 文件，你可以许多方式更改这种行为。

`virtuosable` 文件默认是空的。以下是几个示例，说明了如何根据 `virtuosable` 定义以不同的方式引导入站邮件。

```
chris@linuxxtoys.net      chris
cnegus@linuxxtoys.net
francois@linuxxtoys.net  francois@spidermaker.com
info@linuxxtoys.net       info-list
bogus@linuxxtoys.net      error:No such user here
@example.net             example-catchall
@example.com            %@linuxxtoys.net
```

在前两行中，发往 `linuxxtoys.net` 的 `chris` 或 `cnegus` 的入站邮件被重定向到名为 `chris` 的本地邮件服务器的邮箱。在下一行中，发往同一域名下 `francois` 的任何邮件都会去往 `francois@spidermaker.com`。之后，发送给 `info` 用户名的邮件将保存到 `info-list` 邮件账户中。

以 `bogus@linuxxtoys.net` 开头的行说明了一个错误情况。在这里，发往用户名 `bogus` 的邮件将被拒绝，并将错误信息“No such user”（没有此类用户）返回给发送者。

> 注意：通常情况下，告诉用户该用户不存在并不是一个好主意。
