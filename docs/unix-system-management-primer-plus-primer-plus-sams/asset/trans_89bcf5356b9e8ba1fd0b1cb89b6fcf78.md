

## 第15章 • 与用户交互

包含每个被封装服务的横幅（banners）的目录。当用户访问服务时，TCP Wrappers 会在横幅目录查找与该服务同名的文件；TCP Wrappers 向访问服务的用户显示该文件的内容。

例如，你可以将以下横幅放在 `/etc/banners/in.telnet` 中：
`这是一个私有服务器。如果需要访问，请发送电子邮件至 root@example.com。`

然后你可以在 `/etc/hosts.allow` 或 `/etc/hosts.deny` TCP Wrappers 配置中添加以下行：
`in.telnetd ALL : /etc/banners/banner : severity auth.info : ALLOW`

现在当用户使用 Telnet 连接到 server1 时，他们会看到以下横幅消息：
```bash
server1
Trying 192.168.1.80...
Connected to server1.
Escape character is '^'.

这是一个私有服务器。如果需要访问，请发送电子邮件至 root@example.com。
UNIX(r) System V Release 4.0 (server1.example.com)

login:
```

使用 TCP Wrappers 显示的横幅还可以包含为每个传入连接动态填充的变量。表 15.1 列出了这些变量。

### 限制横幅中的信息量

之前显示的横幅包含了一些信息（Unix(r) System V Release 4.0），这些信息指示了服务器的具体操作系统。这些信息对于黑客来说非常有价值，他们可以使用它来判断何种攻击对服务器是有效的，因此你应该限制像 `/etc/issue` 或 TCP Wrappers 等横幅中特定服务器的信息量。

![](img/894492738e879267320b8d6f9a044180_458_0.png)

表 15.1 TCP Wrappers 横幅变量

| 变量 | 显示内容 |
| --- | --- |
| %a | 客户端 IP 地址 |
| %A | 服务器 IP 地址 |
| %c | 客户端信息：user@hostname |
| %d | 服务器进程名 |
| %h | 客户端主机名或 IP 地址 |
| %H | 服务器主机名或 IP 地址 |
| %n | 客户端主机名 |
| %N | 服务器主机名 |
| %p | 服务器进程 ID |
| %s | 服务器信息：daemon@hostname |
| %u | 客户端用户名（来自 identd） |
| %% | 字面量百分 '%' 字符 |

如果你没有 TCP Wrappers 的访问权限，可以使用 `/etc/issue` 在 Unix 中显示横幅。大多数操作系统会在提示符行上方显示 `/etc/issue` 文件的内容。此功能由 `getty` 进程负责（在 Red Hat Linux 上称为 minicom），因此请检查 `getty` 的 man页以查看它是否支持 Red Hat Linux 的 `/etc/issue` 和 `/etc/issue.net`。

### 在今日公告中发布消息

系统管理员可以使用 Unix 的今日公告（Message of the Day）功能发布关于新软件、即将进行的维护计划的非正式公告，或仅仅打印一条友好的消息。Unix 将今日公告存储在 `/etc/motd` 中，并在用户登录后在每个用户的终端上显示该消息，如下：

```bash
bash$ telnet orange
Trying 192.168.1.21...
Connected to character is orange.
Escape character is ']'.
```

Unix 5.8

```
login: joesuser
Password:
Last login: Thu Jun 6 16:45:56 from apple
```

欢迎来到 Example.COM UNIX 服务器。关于此服务器的所有问题、意见和建议都应发送至 helpdesk@example.com。

重要提示！！！此服务器将于明天早上进行维护而关闭。它最晚于早晨 6 点恢复可用。谢谢。

```bash
bash$
```

在默认配置下，用户可以通过在主目录中创建一个名为 `.hashlogin` 的文件来抑制 motd 功能，因此不要期望 100% 的用户都能看到这些消息。你始终可以通过通过编辑 `/etc/profile` (Bourne shell) 和 `/etc/.login` (csh) 中的登录脚本来强制显示 motd。

> **保持今日公告简短**
确保你的今日公告简短且扼要。用户倾向于跳过阅读时间超过 5 或 10 秒的公告——他们希望在登录后尽快开始工作。

### 在新闻组中发布消息

Usenet 新闻组是线程化论坛，用户可以在具有共同兴趣的小组中发布消息。尽管大多数新闻组是公开访问的，互联网上的任何人都可以发布消息，但单个新闻服务器可以拥有对特定组织的私有新闻组。用户可以检查这些私有新闻组以获取有关你服务的公告，甚至发布问题和评论。当你的系统不可用时，新闻组对于与通信非常方便，因为用户不需要登录他们的系统即可查看它们。

如果你使用新闻组，请确保保持发布频率。就像公告板一样，用户必须主动选择查看或订阅特定的新闻组；如果用户知道消息发布频繁，他们更有可能去检查新消息。

### 在网页上发布消息

许多组织创建了自己的内部网，用于发布停机状态等内部信息。

> **保持发布内容的时效性**
许多组织创建了自己的内部网，用于发布停机状态等内部信息。大多数用户经常访问网页，因此你必须保持页面更新。

### 通过电子邮件发送消息

许多组织创建了自己的内部网，用于发布停机状态等内部信息。尽可能，不要将你的通信限制在单一论坛（如网站）。如果你在多个论坛上分发消息，你将在更短的时间覆盖更广泛的受众，因为每个人都倾向于使用不同的论坛。

> **提前发送紧急电子邮件**
许多组织创建了自己的内部网，用于发布停机状态等内部信息。某些用户在某些时间无法访问某些论坛（例如，出差的人可能只能通过传真机访问电子邮件）。例如，你可以在网站本身上宣布网站停机，并通过新闻组和电子邮件发送给你的客户。

## UNIX 系统管理入门教程

使用电子邮件与用户通信的问题是，向数千名用户发送单条消息会消耗巨大的资源。如果你的用户群超过一百人，投资创建这些邮件的邮件列表软件是明智的。

一些强大的商业软件可以从你自己的服务器发送批量邮件，一些公司也在网页上提供此功能。一些著名的邮件列表软件和网站包括：

- Yahoo Groups http://groups.yahoo.com
- Mailman http://www.list.org
- Majordomo http://www.greatcircle.com/majordomo
- LISTSERV http://www.lsoft.com/products/default.asp?item=listserv

