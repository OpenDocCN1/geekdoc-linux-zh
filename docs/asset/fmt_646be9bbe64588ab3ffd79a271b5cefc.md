
| :--- | :--- |

| OK | 接受此站点邮件，覆盖任何拒绝该站点邮件的规则 |

| RELAY | 允许此域通过服务器进行中继 |

| REJECT | 拒绝来自此站点的邮件并发送标准错误消息 |

| DISCARD | 直接丢弃从该站点收到的任何消息 |

| ERROR: "n message" | 其中 n 是符合 RFC821 标准的错误代码，message 可以任何你想返回给源服务器的消息 |

## 引入 Postfix

以下是三个用于控制 Sendmail 账户访问的规则示例。

第一个规则拒绝来自 `spam.com` 的消息。第二个规则拒绝来自 `lamer.com` 的消息并向该站点显示错误消息。第三个规则允许来自特定主机 `user5.lamer.com` 的邮件，尽管有一条规则拒绝来自 `lamer.com` 站点的邮件。

关于为什么要费力做此事的一个更个人化的例子：你会发现我收到了来自 Hotmail 域的大量垃圾邮件，所以我直接拒绝所有它们。然而，我的妻子使用 Hotmail 账户处理邮件。如果我不允许她的邮件通过，那对我来说将是个麻烦。

| spam.com | REJECT |

| :--- | :--- |

| lamer.com | ERROR: "550 Mail from spammers is not accepted at this site." |

| user5.lamer.com | OK |

打开 `/etc/access` 文件，输入规则，然后重启 Sendmail：

```bash
# /sbin/sendmail restart
```

# 使用 Fetchmail 获取邮件 681

遗憾的是，许多 MUA（邮件用户界面）对 POP3 或 IMAP 一无不知。为了解决这个问题，你可以使用一个名为 Fetchmail 的程序通过 POP3 或 IMAP 连接邮件服务器，从服务器下载邮件，并将这些消息注入到本地 MTA（邮件传输代理），就像它们来自标准的 SMTP 服务器一样。接下来的章节将解释如何安装、配置和使用 Fetchmail 程序。

## 安装 Fetchmail

与其他 `.rpm` 文件一样，Fetchmail 可以用 `rpm -i` 命令进行安装。该命令将所有文件安装到它们的默认位置。如果由于某种原因，你需要进行自定义安装，请参阅第 7 章“管理软件”，获取有关更改 `rpm` 默认选项的更多信息。

你可以在 `http://uxedo.org/~es/fetchmail` 获取 Fetchmail 的最新版本。它提供源码格式和 RPM 二进制格式。随书附带的 CD 和 DVD 上的 Fedora 版本提供了较新的 Fetchmail 版本，并在 `/usr/share/doc/fetchmail` 目录下安装了实用的 Fetchmail 文档。该目录直接包含 FAQ（常见问题解答）、功能列表和安装文档。

## 配置 Fetchmail

安装 Fetchmail 后，你必须在主目录下创建 `.fetchmailrc` 文件，该文件为 Fetchmail 程序提供配置。

你可以使用任何文本编辑器创建并随后编辑 `.fetchmailrc` 文件。该配置文件非常直观且易于创建；接下来的章节将解释创建和编辑文件的手动方法。接下来的章节介绍的信息没有讨论 `.fetchmailrc` 文件中所有可用选项，但包含了让基础 Fetchmail 安装并运行所需的最常用选项。你必须使用文本编辑器创建该文件，以包含如示例所示的条目——当然，需要根据你的个人信息进行修改。对于高级配置，请参阅 Fetchmail 的 `man` page（手动帮助页）。该帮助页编写得非常好，并详细记录了所有配置选项。

> 注意
> `.fetchmailrc` 文件分为三个部分：全局选项、邮件服务器选项和用户选项。这些部分必须按照列出的顺序出现，这一点非常重要。不要将选项添加到错误的部分。将选项放在错误的位置是新用户在配置 Fetchmail 文件时最常见的问题之一。

### 配置全局选项

`.fetchmailrc` 的第一部分包含全局选项。这些选项会影响你稍后在配置文件中列出的所有邮件服务器和用户帐户。正如你在本节稍后将学到的，某些全局选项可以使用本地配置选项覆盖。以下是可能出现在 `.fetchmailrc` 文件全局部分的选项示例：

### 第 25 章 处理电子邮件

```
set daemon 600

set postmaster foobar

set logfile ./fetchmail.log
```

示例中的第一行告诉 Fetchmail 它应该以守护模式启动，并每隔 600 秒（即 10 分钟）检查一次邮件服务器是否有新邮件。守护模式意味着 Fetchmail 启动后会将自己移动到后台并继续运行。如果没有此行，Fetchmail 只会在启动时检查一次邮件，然后终止且不再检查。

第二个选项告诉 Fetchmail 使用本地账户 `foobar` 作为最后的备用地址。换句话说，它收到的任何无法投送到指定账户的电子邮件都应该发送到 `foobar`。

第三行告诉 Fetchmail 将其活动记录到文件 `./fetchmail.log`。或者，你可以使用 `set syslog` 行——在这种情况下，Fetchmail 通过 syslog 设施记录日志。

### 配置邮件服务器选项

`.fetchmailrc` 文件的第二部分包含每个应检查新邮件的邮件服务器的信息。以下是邮件部分的示例：

```
poll mail.samplenet.org

proto pop3

no dns
```

第一行告诉 Fetchmail 它应该在全局选项部分设置的每个轮询间隔（在我们的示例中为 600 秒）检查邮件服务器 `mail.samplenet.org`。或者，第一行可以用 `skip` 开头。如果邮件服务器以 `skip` 开头，则不会按轮询间隔进行轮询，而只在 Fetchmail 命令行中明确指定时进行轮询。

第二行指定了连接邮件服务器时应使用的协议。在这种情况下，我们正在使用 POP3 协议。其他有效的选项还有 IMAP、APOP 和 KPOP。你也可以在这里使用 `AUTO`——在这种情况下， Fetchmail 会尝试自动确定与邮件服务器通信正确的协议。你可以自行确定与邮件服务器通信的正确协议。

第三行告诉 Fetchmail 它不应尝试进行 DNS 查找。如果你通过拨号连接运行程序，你可能想要包含此选项。

### 配置用户帐户

`.fetchmailrc` 的第三部分也是最后部分，包含上一节指定的服务器上用户帐户的信息。以下是一个示例：

```
user foobar

pass secretword

fetchall

flush
```
