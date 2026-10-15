
你可以在 `http://www.catb.org/~esr/fetchmail` 获取 Fetchmail 的最新版本。

#### 配置 Fetchmail

安装 Fetchmail 后，你必须在主目录中创建文件 `.fetchmailrc`，它提供了 Fetchmail 程序的配置。

你可以使用任何文本编辑器创建并随后编辑 `.fetchmailrc` 文件。配置文件非常直接且很容易创建；以下各节说明了创建和编辑文件的手动方法。以下各节中提供的信息并未讨论 `.fetchmailrc` 文件中所有可用的选项，但涵盖了让基本的 Fetchmail 安装运行起来所需的最常见选项。你必须使用文本编辑器创建文件以包含如示例所示的条目——当然要根据你的个人信息进行修改。对于高级配置，请参阅 Fetchmail 的 `man` 手册。`man` 手册写得很好，详细记录了所有配置选项。

> CAUTION
> `.fetchmailrc` 文件分为三个不同的部分：全局选项、邮件服务器选项和用户选项。重要的是这些部分必须按列出的顺序出现。不要将选项添加到错误的分区。将选项放在错误的位置是新用户在使用 Fetchmail 配置文件时最常见的问题之一。

#### 配置全局选项

`.fetchmailrc` 的第一部分包含全局选项。这些选项会影响你在配置文件中后面列出的所有邮件服务器和用户帐户。其中一些全局选项可以用你稍后在本节中了解到的本地配置选项来覆盖。以下是可能出现在 `.fetchmailrc` 文件全局部分的一些选项的示例：

```
set daemon 600
set postmaster foobar
set logfile ~/.fetchmail.log
```

此示例中的第一行告诉 Fetchmail 它应以守护进程模式启动，并在每 600 秒，即 10 分钟，检查邮件服务器是否有新邮件。守护进程模式意味着 Fetchmail 启动后，它会将自身移至后台并继续运行。如果没有这一行，Fetchmail 启动时只会检查一次邮件，然后终止并且不再检查。

第二个选项告诉 Fetchmail 使用本地帐户 foobar 作为最后的收件地址。换句话说，Fetchmail 接收到任何无法投递到指定帐户的电子邮件都应发送给 foobar。

第三行告诉 Fetchmail 将其活动记录到文件 `./fetchmail.log`。或者，你也可以使用行 `set syslog`——在这种情况下，Fetchmail 将通过 syslog 设施进行日志记录。

#### 配置邮件服务器选项

`.fetchmailrc` 文件的第二部分包含应检查新邮件的每个邮件服务器的信息。以下是邮件部分可能的样子示例：

```
poll mail.samplenet.org
proto pop3
no dns
```

第一行告诉 Fetchmail 在全局选项部分设置的每个轮询间隔检查邮件服务器 `mail.samplenet.org`（在我们的示例中为 600 秒）。或者，第一行可以以 `skip` 开头。如果邮件服务器行以 `skip` 开头，则不会按轮询间隔进行轮询，而只会在 Fetchmail 命令行中明确指定时才进行轮询。

第二行指定在联系邮件服务器时应使用的协议。在本例中，我们使用的是 POP3 协议。其它合法选项有 IMAP、APOP 和 KPOP。你也可以在此处使用 `AUTO`——在这种情况下，Fetchmail 将尝试自动确定与邮件服务器一起使用的正确协议。

第三行告诉 Fetchmail 不应尝试执行动态名称服务器（DNS）查找。如果你通过拨号连接运行，可能需要包含此选项。

#### 配置用户帐户

`.fetchmailrc` 的第三部分也是最后一部分包含有关上一节中指定的服务器上的用户帐户的信息。以下是示例：

```
user foobar
pass secretword
fetchall
flush
```

第一行当然只是指定用于登录电子邮件服务器的用户名，第二行指定该用户的密码。许多注重安全的人对在配置文件中放置明文密码感到不寒而栗，并且它们应该是组或世界可读的。保护此信息的唯一方法是确保文件只能由所有者读取；也就是说，文件权限为 600。

第三行告诉 Fetchmail 它应该从服务器获取所有邮件，即使它们已经被阅读过。

第四行告诉 Fetchmail 在完成下载后应从邮件服务器删除邮件。这是默认值，因此我们实际上不必指定此选项。如果你想在下载后将邮件保留在服务器上，请使用选项 `no flush`。

你刚刚插入的配置选项将整个 `.fetchmailrc` 文件配置为如下所示：

```
set daemon 600
set postmaster foobar
set logfile ./fetchmail.log

poll mail.samplenet.org
proto pop3
no dns

user foobar
pass secretword
fetchall
flush
```

此文件告诉 Fetchmail 执行以下操作：

- 每 600 秒检查一次 POP3 服务器 `mail.samplenet.org` 是否有新邮件。
- 使用用户名 foobar 和密码 secretword 登录。
- 从服务器下载所有邮件。
- 在完成下载后从服务器删除邮件。
- 将无法投递给本地用户的任何邮件发送到账户 foobar。

如前所述，`.fetchmailrc` 文件中可以包含的选项远不止此处列出的这些。然而，这些选项足以让你使用基本配置开始运行。

为了获得额外的灵活性，你可以定义多个 `.fetchmailrc` 文件，以便使用同一个 Linux 用户账户从不同的远程邮件服务器检索邮件。例如，你可以为最常用的账户定义设置并将其保存在默认的 `.fetchmailrc` 文件中。然后可以像这样快速检索邮件：

```
$ fetchmail -a
1 message for andrew at mail.ourphotos.me.uk (1108 octets).
reading message 1 of 1 (1108 octets) . flushed
```

通过使用 Fetchmail 的 `-f` 选项，你可以指定一个替代资源文件，然后轻松地从另一台服务器检索邮件，如下所示：

```
$ fetchmail -f .myothermailrc
2 messages for andrew at andrew.hudson.com (5407 octets).
reading message 1 of 2 (3440 octets) ... flushed
reading message 2 of 2 (1967 octets) . flushed
You have new mail in /var/spool/mail/andrew
```

通过使用 `-d` 选项以及一个时间间隔（以秒为单位），你可以使用 Fetchmail 的守护进程或后台模式。命令将作为后台进程启动，并在指定的间隔从指定的远程服务器检索邮件。有关更高级的选项，请参阅 Fetchmail 手册页，其编写良好并详细记录了所有选项。

## CAUTION

> 因为 `.fetchmailrc` 文件包含你的邮件服务器密码，所以它应该只能由你读取。这意味着它应由你拥有，并且权限不应大于 600。如果 `.fetchmailrc` 文件的权限大于此，Fetchmail 将会抱怨并拒绝启动。

#### Choosing a Mail Delivery Agent

由于邮件处理的模块化特性，可以使用多个应用程序来处理邮件并实现不仅仅是投递邮件的功能。从存储区域获取邮件并将其显示给用户是 MDA 的目的。MDA 功能可以在某些邮件客户端（MUA）中找到，这可能会让那些仍不熟悉 UNIX 邮件概念的人感到困惑。例如，Procmail MDA 提供基于规则集的过滤；KMail 和 Evolution 都是 MUA，提供过滤功能，但 MUA pine、mutt 和 Balsa 则不提供。一些 MDA 执行简单的排序，而其他 MDA 则旨在消除不需要的电子邮件，例如垃圾邮件和病毒。

你会根据想要对邮件做什么来选择 MDA。我们将介绍五种 MDA，它们提供的功能可能在你的特定情况下有用。如果你需求简单（只是按规则组织邮件），提供过滤功能的 MUA之一可能更适合你的需求。Ubuntu 将 Evolution MUA 作为默认选择（并且如前所述它包含一些 MDA 功能），因此请先尝试它并 see whether it meets your needs. If not, investigate one of the following MDAs provided by Ubuntu.

Unless otherwise noted, all the MDA software is provided through `synaptic` and `apt-get`. Chapter 31, “Managing Software,” details the general installation of any software.

#### Procmail
