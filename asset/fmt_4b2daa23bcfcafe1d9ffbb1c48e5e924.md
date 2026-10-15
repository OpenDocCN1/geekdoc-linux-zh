
# 添加数据库支持

一旦在选择的文件中插入该行，请重新编译 `Sendmail` 以生效。（编译 `Sendmail` 的说明请参见第 3 章。）

然而，在费这些精力之前，请检查你的 `Sendmail` 程序已在使用哪些选项。默认数据库选项设置取决于 `Sendmail` 源码分发版构建程序所检测到的数据库库。在 Linux 系统上，默认通常是 `-DNEWDB`。但构建程序能够很好地检测你系统的能力，因此你的 `Sendmail` 程序可能包含额外的选项。列表 6.1 显示了在随 `sendmail-8.11.0.i386.rpm` 文件分发的 `Sendmail` 程序中编译入的选项。

## 列表 6.1 检查 `sendmail` 编译选项

```
[root]# sendmail -bt -d0.4

Version 8.11.0

Compiled with: MAP_REGEX LOG MATCHHEGECOS MIME7TO7 MIME8TO7 NAMED_BIND

NETINET NETWOB NEWDB NIS QUEUE SASL SCANF SFIOT

STARTTLS USERDB

canonical name: wren.foobirds.org

a.k.a.: wren

UUCP nodename: wren.foobirds.org

a.k.a.: wren

a.k.a.: [172.16.12.3]

========== SYSTEM IDENTITY (readcf) ==========

(short domain name) Sw = wren

(canonical domain name) Sj = wren.foobirds.org

(subdomain name) Sm = foobirds.org

(node name) $ = wren.foobirds.org

==================================
```

```
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)

Enter <ruleset> <address>

^ >
```

列表 6.1 显示了 `Sendmail` 在 `-bt` 测试模式下运行。同时 `Sendmail` 还接收了调试值 `-d0.4`。该调试值会导致 `Sendmail` 在接受输入之前显示几行信息。我们并没有真正要给 `Sendmail` 处理的输入；我们只是想查看显示内容，然后使用 `Ctrl+D` 退出。`Sendmail` 程序显示的第一行告诉我们这是 `Sendmail` 8.11.0。第二行是我们感兴趣的行。它列出了 `Sendmail` 编译时包含的所有选项。其中四个 `MAP_REGEX`、`NEWDB`、`NIS` 和 `USERDB` 与数据库相关，且 (img/b8082498451dba2bf0cf2907c85c4c83_0.png) 是我们想要的四个选项。

供 `Sendmail` 使用的数据库比你可能用过的还要多。其中一些对 Linux 站点来说几乎毫无价值——bitdomain 数据库为一个不运行任何 Linux 站点的网络转换地址，而 uucdomain 数据库则转换 UUCP “bang”地址（即旧的 hostuser 电子邮件地址），这种地址现在几乎没有人使用了。其他数据库具有重叠的功能，你可能在你的站点不需要同时使用它们。RPM 提供的默认配置包含的定义和功能不足上述列表的一半，而且该配置所具备的数据库功能可能已经超过了你实际需要的。为了帮助你评估确实需要的数据库，我们将详细检查所有这些数据库。

## Cr、Cw 和 Ct 文件

我们所涵盖的前三个数据库在严格意义上并不是数据库。它们是用于加载 `sendmail.cf` 类的磁盘文件。“cr”和“cw”在配置 `Sendmail` 时起着重要作用，但由于网络安全环境的变化，“ct”文件已不再有任何用处了。

加载 `ct` 变量的文件通常被称为“ct”文件，因为该文件的传统名称是 `/etc/sendmail.ct`。在 `Sendmail` 8.11 中，该文件的默认名称变为 `/etc/mail/trusted-users`，但其功能保持不变。它用于将用户名添加到受信任以其他用户身份发送邮件的用户列表中。默认情况下，`ct` 包含 `daemon`、`root` 和 `ucp` 用户名。

你永远不会使用 `/etc/mail/trusted-users` 文件，而且你这样做有几个充分的理由。首先，让人们以他人的身份发送邮件是一个坏主意。通常情况下，如果你不想扩展信任用户列表，或者如果你决定绝对必须向信任用户列表添加用户名，那么你添加的数量不足以支撑将它们单独放在一个文件的必要性。例如，你可以将用户名“mail”添加到信任用户列表中。你可以编辑宏配置文件添加 `FEATURE(use_ct_file)` 命令，重新构建 `sendmail.cf` 文件，并创建一个仅包含 `mail` 一个单词的 `trusted-users` 文件。但为什么要这样做呢？你可以轻松地编辑宏配置文件添加 `define(`TRUSTED_USERS`, `mail`)` 命令，重新构建 `sendmail.cf` 文件即可大功告成。这种方法不仅稍微简单，而且安全，因为创建的文件更少，因此需要设置权限的文件也更少。

> **警告** 尽管有此示例，但不建议使用 `TRUSTED_USERS` 或 `use_ct_file`，因为你不应该向信任用户列表添加任何用户。在垃圾邮件发送者和安全破解横行的时代，信任用户是一个坏主意。

与从不使用的“ct”文件不同，“cr”文件始终被使用。“cr”文件的真实名称是 `relay-domains`（中继域）文件。`Sendmail` 总是使用在 `relay-domains` 文件中找到的数据。该文件的目的和结构是下一个主题。

## `relay-domains` 文件

当邮件到达 `Sendmail` 服务器时，它会被接受、拒绝或中继。如果邮件地址是服务器本身，那么只要是服务器接受为自己的名称，邮件将被接受进行本地投递，这意味着邮件被存放在本地用户的邮箱中，或者根据一个电子邮件数据库的指示进行路由。如果邮件地址不是服务器本身，则邮件会被拒绝或中继。中继是通过重新发送到投递地址来实现。在 `Sendmail` 8.9 之前，所有由 `Sendmail` 服务器接收的指向另一个主机的邮件都会被中继。现在，除非你告诉 `Sendmail` 进行中继，否则没有邮件会被中继。这一变化对于许多使用 `Sendmail` 服务器作为 PC 发送邮件的系统管理员来说是一个头疼的问题。但垃圾邮件发送者利用 `Sendmail` 的中继功能来隐藏垃圾邮件的真实来源。现在所有管理员都必须为垃圾邮件付出，那就是创建显式中继配置所需的额外工作。

显式启用中继的一种方法是在 `/etc/mail/relay-domains` 文件列出允许中继的主机名。`Sendmail` 将写入该文件的任何内容复制到 R 类。R 类中的任何主机都被允许中继邮件。列表 6.2 显示了 `relay-domains` 文件的内容。

## 6.2 使用 `relay-domains` 文件

```
[root]# cat /etc/mail/relay-domains

foobirds.org

[root]# ps -ax | grep sendmail

542 ? S 0:00 sendmail: accepting connections

[root]# kill -HUP 542

[root]# sendmail -bt

TEST MODE (ruleset 3 automatically invoked)

Enter <ruleset> <address>

> $R
```
