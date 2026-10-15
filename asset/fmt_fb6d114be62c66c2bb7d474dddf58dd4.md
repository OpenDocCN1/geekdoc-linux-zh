
接下来，你应该让该邮件服务器的用户在主目录下设置他们自己的用户偏好。在每个用户的 `$HOME/.spamassassin/user_prefs.cf` 文件中设置的偏好有助于告诉 SpamAssassin 如何处理该封邮件。以下是用户可能想要在该文件中包含的行示例：

| required_score | 3 |
| whitelist_from | jsmith@example.com bjones@example.net |
| blacklist_from | *.example.org |

`required_score` 行（默认设置为 5，但此处设置为 3）设置了将消息被视为垃圾邮件所需的评分。分数基于 SpamAssassin 执行的标准的匹配或不匹配标准。请参阅 http://spamassassin.org/tests.html。

`whitelist_from` 和 `blacklist_from` 行允许你设置个人、个人或域名地址，这些地址不应被视为垃圾邮件（白名单）或应该始终被视为垃圾邮件（黑名单）。要修改 SpamAssassin 行为的其他方法，请输入以下命令：

```
man Mail:SpamAssassin::Conf
```

此时，SpamAssassin 应该已经在运行，并根据你以及使用邮件服务器的用户输入识别垃圾邮件。接下来，每个用户需要在下一节中决定如何处理被标记为垃圾邮件的消息。

> 提示：你可以与垃圾邮件一起使用的技术包括 SpamCop。SpamCop (www.spamcop.net) 提供了一项服务，允许你将收到的垃圾邮件输入到数据库中，帮助他人拦截相同的邮件。

# 设置邮件客户端过滤垃圾邮件

每个用户都可以在其邮件阅读器中运行过滤，以决定如何处理由 SpamAssassin 标记为垃圾邮件的邮件。常见的做法是将标记为垃圾邮件的邮件重定向到单独的文件夹。由于某些真实邮件会被误标记为垃圾邮件，你可以每一两周检查一次垃圾邮件文件夹，以确保没有错过任何内容。

以下是从 Evolution Mail 添加过滤器的示例：

- 1. 在你的收件箱下创建一个标记为 SPAM 的文件夹。
- 2. 点击 Edit（编辑）-> Message Filters（邮件过滤器）。
- 3. 从 Filters 窗口，点击 Add（添加）。出现 Add Rule 窗口。
- 4. 识别一个规则名称（例如 Spam），该规则添加了一个查找特定头部（`X-Spam-Flag`）并包含文本（YES）的条件。然后在 Add Action（添加操作）下，选择一个操作（移动到文件夹）并识别包含垃圾邮件的文件夹（SPAM）。

当你想要从邮件服务器接收邮件时，所有带有 `X-Spam-Flag` 的消息都会分类到你的 SPAM 文件夹中。作为替代方案，你可以检查主题行中是否出现 [SPAM] 作为分类垃圾邮件的标准。

# 第四部分：Fedora RHEL 网络和服务器设置

其他邮件阅读器（Sea Monkey、pine、Netscape mail 等）也包含了根据你输入的标准对邮件进行过滤和排序的功能。

Evolution 的一个新功能在 Evolution 框架内包含了 SpamAssassin 功能。Evolution 使用 `spamad` 守护进程运行守护化版本的 SpamAssassin。垃圾邮件进程会自动过滤你的邮件为垃圾邮件。当它发现垃圾邮件时，会自动将其放入 Evolution 窗口中的 Junk 文件夹中。你可以忽略这些消息，或者快速扫描并删除它们。

# 从服务器获取邮件 (POP3 或 IMAPv4)

在设置好邮件服务器后，你将希望让用户从服务器访问电子邮件。这意味着每个用户都要登录邮件服务器读取他们的邮件，或者更可能的是配置 POP3 或 IMAPv4 让用户从其工作站访问邮件。以下是 POP3 和 IMAPv4 的描述：

- POP3 — 使用 POP3，用户在本地工作站上下载和管理邮件。POP3 更简单，需要的服务器资源更少。
- IMAPv4 — 使用 IMAPv4，用户在服务器上管理邮件消息。IMAPv4 需要更多的服务器资源，但允许用户从多个设备访问邮件。
