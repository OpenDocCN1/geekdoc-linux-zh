

不幸的是，许多 MUA 对 POP3 或 IMAP 一无所知。为了解决这个问题，你可以使用一个名为 Fetchmail 的程序来使用 POP3 或 IMAP 联系邮件服务器，从服务器上下载邮件，然后将这些邮件注入到本地 MTA，就好像它们来自标准的 SMTP 服务器一样。以下各节将说明如何安装、配置和使用 Fetchmail 程序。

## 安装 Fetchmail

与其它软件包类似，Fetchmail 可以使用 synaptic 或 apt-get 进行安装。

你可以在 http://www.catb.org/~esr/fetchmail 获取 Fetchmail 的最新版本。

## 配置 Fetchmail

安装 Fetchmail 后，你必须在主目录中创建文件 .fetchmailrc，它提供了 Fetchmail 程序的配置。

你可以使用任何文本编辑器创建并随后编辑 .fetchmailrc 文件。配置文件非常直接且很容易创建；以下各节说明了创建和编辑文件的手动方法。以下各节中提供的信息并未讨论 .fetchmailrc 文件中所有可用的选项，但涵盖了让基本的 Fetchmail 安装运行起来所需的最常见选项。你必须使用文本编辑器创建文件以包含如示例所示的条目——当然要根据你的个人信息进行修改。对于高级配置，请参阅 Fetchmail 的 man 手册。man 手册写得很好，详细记录了所有配置选项。

> CAUTION
> .fetchmailrc 文件分为三个不同的部分：全局选项、邮件服务器选项和用户选项。重要的是这些部分必须按列出的顺序出现。不要将选项添加到错误的分区。将选项放在错误的位置是新用户在使用 Fetchmail 配置文件时最常见的问题之一。

## 配置全局选项

.fetchmailrc 的第一部分包含全局选项。这些选项会影响你在配置文件中后面列出的所有邮件服务器和用户帐户。其中一些全局选项可以用你稍后在本节中了解到的本地配置选项来覆盖。以下是可能出现在 .fetchmailrc 文件全局部分的一些选项的示例：

```
set daemon 600
set postmaster foobar
set logfile ~/.fetchmail.log
```

此示例中的第一行告诉 Fetchmail 它应以守护进程模式启动，并在每 600 秒，即 10 分钟，检查邮件服务器是否有新邮件。守护进程模式

意味着 Fetchmail 启动后，它会将自身移至后台并继续运行。如果没有这一行，Fetchmail 启动时只会检查一次邮件，然后终止并且不再检查。

第二个选项告诉 Fetchmail 使用本地帐户 foobar 作为最后的收件地址。换句话说，Fetchmail 接收到任何无法投递到指定帐户的电子邮件都应发送给 foobar。

第三行告诉 Fetchmail 将其活动记录到文件 ./fetchmail.log。或者，你也可以使用行 set syslog——在这种情况下，Fetchmail 将通过 syslog 设施进行日志记录。

## 配置邮件服务器选项

.fetchmailrc 文件的第二部分包含应检查新邮件的每个邮件服务器的信息。以下是邮件部分可能的样子示例：

```
poll mail.samplenet.org
proto pop3
no dns
```

第一行告诉 Fetchmail 在全局选项部分设置的每个轮询间隔检查邮件服务器 mail.samplenet.org（在我们的示例中为 600 秒）。或者，第一行可以以 skip 开头。如果邮件服务器行以 skip 开头，则不会按轮询间隔进行轮询，而只会在 Fetchmail 命令行中明确指定时才进行轮询。

第二行指定在联系邮件服务器时应使用的协议。在本例中，我们使用的是 POP3 协议。其它合法选项有 IMAP、APOP 和 KPOP。你也可以在此处使用 AUTO——在这种情况下，Fetchmail 将尝试自动确定与邮件服务器一起使用的正确协议。

第三行告诉 Fetchmail 不应尝试执行动态名称服务器（DNS）查找。如果你通过拨号连接运行，可能需要包含此选项。

## 配置用户帐户

.fetchmailrc 的第三部分也是最后一部分包含有关上一节中指定的服务器上的用户帐户的信息。以下是示例：

```
user foobar
pass secretword
fetchall
flush
```

第一行当然只是指定用于登录电子邮件服务器的用户名，第二行指定该用户的密码。许多注重安全的人对在配置文件中放置明文密码感到不寒而栗，并且

