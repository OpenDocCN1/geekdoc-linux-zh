
该示例展示了构建 `sendmail.cf` 文件时使用的 `m4` 命令格式。路径 `../m4/cf.m4` 是构建 `sendmail.cf` 文件所需的 `m4` 源码树路径。如果该路径没有通过 `include` 命令包含在宏配置中，则必须在 `m4` 命令行中指定。注意，该路径名是以 `./` 开头的相对路径。旧版本的 `m4` 实际上需要相对路径。切换到 `cf/cf` 目录并不是为了方便，而是为了在正确的源码树路径运行 `m4` 的必要步骤。这在 Linux 系统上已不再需要。用于 Linux 的 GNU `m4` 程序可以接受该参数的绝对路径，这意味着宏配置文件可以存储在系统中的任何位置。Red Hat 在通过 RPM 安装 Sendmail 时利用了这一事实。RPM 获取了 `/etc/mail` 中 Red Hat 配置文件的副本，并在宏配置文件内部包含了指向 `cf.m4` 的绝对路径。

第二个命令行参数是新宏配置文件的名称，`test.m4`。它读取源文件 `../m4/cf.m4` 和 `test.m4`，并输出文件 `.cf`。由 `m4` 命令输出的文件是 `sendmail.cf` 的正确格式。

## 测试配置文件的兼容性

`test.cf` 的格式是成为 `sendmail.cf` 文件的格式，但在将其移动到 `/etc/mail/sendmail.cf` 之前，您应该确保它可以正常工作。如列表 4.9 所示，通过快速测试即可获知结果。

### 列表 4.9 测试兼容性

```
[root]# sendmail -v -t -C /etc/sendmail.cf
Warning: .cf is out of date: sendmail 8.11.0 supports
version 9, .cf file is version 8

^D
No recipient addresses found in header
[root]# sendmail -v -t -C ../test.cf
^D
No recipient addresses found in header
```

如列表 4.9 所示，`test.cf` 配置文件解决了我们在通过编译新源码升级 Sendmail 时出现的兼容性问题。该测试没有证明其他的任何问题，我不会假装这个简单的配置就是最佳配置，但它满足了我们让的 Sendmail 运行起来的目标。

## 安装新配置

一旦您决定使用新的配置文件，请将其移动到 Sendmail 期望查找配置的位置。Sendmail 8.11 配置文件的默认名称为 `/etc/mail/sendmail.cf`。在大多数 Linux 系统上，配置文件是 `/etc/sendmail.cf`。将新文件放在适用于您系统的相应位置。在本示例中，我们使用默认设置从源码编译了 Sendmail 8.11，因此我们需要将 `test.cf` 移动到 `/etc/mail/sendmail.cf`，这如列表 4.10 所示。

### 列表 4.10 将新配置文件就位

```
[root]# mv /etc/mail/sendmail.cf /etc/mail/sendmail.cf
mv: /etc/mail/sendmail.cf: No such file or directory
[root]# cp test.cf /etc/mail/sendmail.cf
[root]# sendmail -v -t
```

To: craig.wren.foobirds.org
From: craig
Subject: Test
Please ignore this test.
^D
craig.wren.foobirds.org -- Connecting to wren.wren.foobirds.org. via esmtp...
220 wren.foobirds.org SMTP Sendmail 8.11.0/8.11.0;
, 29 Aug 2000 20:42:44 -0

400
>>> EHLO ibis.foobirds.org
250-wren.foobirds.org Hello root@almond.nuts.com [172.16.2.1],leased to meet you
>>> MAIL From:<craig@ibis.foobirds.org> SIZE=78
250 2.1.0 <craig@ibis.foobirds.org>... Sender ok
>>> RCPT To:<craig@wren.foobirds.org>
250 2.1.5 <craig@wren.foobirds.org>... Recipient ok
>>> DATA

354 Enter mail, end with "." on a line by itself
>>>
250 2.0.0 e7U0Frg00818 Message accepted for delivery
craig@wren.foobirds.org... Sent (e7U0Frg00818 Message
accepted for delivery)
Closing connection to wren.foobirds.org.
>>> QUIT

221 2.0.0 wren.foobirds.org closing connection

第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

![](img/9639113aa446fb8976cb3d377f7aafdd_124_0.png)

## m4 宏语言

## 创建基础配置

接下来，我们将 `test.cf` 复制到 `/etc/mail`。第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

第一步是将当前的 `sendmail.cf` 文件移动到备份文件，在列表 4.10 中命名为 `sendmail.cf.hold`。在这种情况下，移动未成功，因为我们刚刚从源码文件安装了 Sendmail，并没有 `/etc/mail/sendmail.cf` 文件。尽管如此，始终先运行 `mv` 以确保我不会覆盖我想要恢复的文件。

所有以下命令都用于本章。Sendmail 8.11 配置文件的默认名称为 `/etc/mail/sendmail.cf`，使用默认设置。在大多数 Linux 系统上，配置文件是 `/etc/sendmail.cf`。将新文件放在适用于您系统的相应位置。在本示例中，我们使用默认设置从源码编译了 Sendmail 8.11。

### 表 4.3 m4 命令

| 命令 | 目的 |
| :--- | :--- |
| EXPOSED_USER | 定义一个域名。 |
| HACK | 处理一个包含修复的文件。 |
| include | 包含 `cf.m4` 文件。 |
| LOCAL_CONFIG | 标记部分的开始。 |
| LOCAL_RULE_n | 标记规则集的开始。 |
| LOCAL_RULESETS | 标记规则集的开始。 |
| MASQUADE_AS | 定义一个域名。 |

### 表 4.3 m4 命令（继续）

| 命令 | 目的 |
| :--- | :--- |
| MODIFY_MAILER_FLAGS | 定义邮件器标志。 |
| SITE | 识别 UUCP 站点名称。 |
| SITECONFIG | 指向包含 SITE 命令的文件。 |
| UUCPSMTP | 将 UUCP 主机映射到 Internet 主机。 |

表 4.3 中的命令最重要的一点是，其中有些命令是你永远不会使用的。仅仅因为某个命令出现在示例文件中，并不意味着它对你是正确的，或者它是推荐的命令。Sendmail 附带的一些示例文件非常旧。这些文件中使用的某些命令已经过时，可以忽略。表 4.3 中的最后三个命令是很好的例子。SITE、SITECONFIG 和 UUCPSMTP 是配置系统处理 UUCP 邮件的过时技术。这些功能已被第 6 章中基于数据的方法所取代。

