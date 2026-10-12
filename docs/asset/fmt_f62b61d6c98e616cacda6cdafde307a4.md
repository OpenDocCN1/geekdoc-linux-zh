
- 一个获取 Linux 软件更新和安全漏洞公告的良好网站：`www.freshmeat.com`。

- 访问 `www.cert.org` 查看计算机应急响应小组 (CERT) 关于已知安全问题的公告。这些公告通常包含修复方案（如果有的话）。

跟踪所有与 `Linux`、`Unix` 和 `Unix` 应用程序相关的问题——这些都可能影响你的 `Linux` 服务器。图 14.1 显示我正在检查 `geek-girl.com` 上的公告。

图 14.1 在 `geek-girl.com` 搜索 `Bugtrap` 存档 

![](img/0a4925a63d7144788f84b23689a2d0da_479_0.png)

1999 年第一季度（1月-3月）的 `Bugtrap` 存档：关于：`Melissa` 宏病毒。（1999年4月）

- 前序消息：`Brian Szymanski: Imex imod bug/security vulnerability`

- 前序消息：`Brian Szymanski: Imex imod bug/security vulnerability`

1999 年第一季度（1月-3月）的 `Bugtrap` 存档：`Imex imod bug/security vulnerability`。

- `<<subject Imex imod bug/security vulnerability`

- 1999 年第一季度（1月-3月）的 `Bugtrap` 存档：`Imex imod bug/security vulnerability`

- `Imex imod bug/security vulnerability`

- `LINUX-DEVELOPERS-HOW-MY-SERVER`. 请注意！！！

- 邮件来自 `Linux` 开发列表，但我目前不认识其中的任何人。

- 分组丢失。话虽如此，`Linux` 交换检查正确的

1999 年第一季度（1月-3月）的 `Bugtrap` 存档：关于 `Melissa` 宏病毒的 `Caesar`。（1999年4月）

- 后续消息：`Brian Szymanski: Imex imod bug/security vulnerability`

- 后续消息：`Brian Szymanski: Imex imod bug/security vulnerability`

1999 年第一季度（1月-3月）的 `Bugtrap` 存档：`Kfrees6` 安全问题。（1999年4月）

- `dgt`：我知道它存在于每一个 `Linux` 发行版中（特别是）

- 我的 `Slack Linux` 不受此问题影响，而且从来没有，

- 我认为我们不是唯一提供 `Linux` 操作系统系统的发行商

- `Slack Linux` 项目

图 14.1 是在 `Bugtraq` 存档中搜索字符串“`Linux`”的结果。此页面上的某些错误报告描述了关于 `insmod` 命令的报告问题，可能会导致安全问题。点击链接将带你进入错误报告，以便你可以阅读并评估该漏洞是否对你的系统构成威胁。

除了访问报告漏洞和安全问题的网站，我建议你访问提供攻击脚本的网站。其中两个网站是 `www.rootshell.com` 和 `www.universe.org`。这些网站让你可以使用入侵者用来攻击你系统时相同的脚本。你还可以确保你的系统不会受到旧攻击的侵害，并在新脚本发布时对其进行评估，以理解它们利用的漏洞。除了提供网络脚本外，这些网站还提供了有关当前安全领域动态的信息。

图 14.2 `rootshell.com` 上的利用报告

![](img/0a4925a63d7144788f84b23689a2d0da_479_0.png)

# 图 14.4 一份红帽安全公告

![](img/0a4925a63d7144788f84b23689a2d0da_483_0.png)

> 提示：管理员经常抱怨软件作者不修复漏洞，但我发现一个更常见的问题是，系统管理员没有使用那些已经发布的漏洞修复。每月留出专门的时间来下载并安装软件供应商提供的修复程序。将其转变为你日常工作的一部分。

## 移除不需要的软件

减轻软件更新负担的办法是移除所有你并不真正需要的软件。早些时候，我指出过在过去的一年里，`sendmail` 和 `IMAP` 在多个不同时期都遭受过攻击。为什么 `sendmail` 是首要目标？在某种程度上，是因为它是一个大型且复杂的系统，容易受到不同类型的攻击，但另一个原因也是 `sendmail` 处处运行。每个主要网络上的许多系统都在运行 `sendmail`，而且 `sendmail` 监控的 `SMTP` 端口通常被允许通过防火墙。入侵者寻找的是易攻目标，由于在桌面级 `Unix` 和 `Linux` 客户端上运行着许多 `sendmail` 副本，他们注定会发现某一个是配置错误或过时的。

然而，没有必要运行这么多 `sendmail` 副本。`Linux` 客户端不需要运行 `sendmail` 守护进程。它可以被配置为：将邮件转发到运行 `sendmail` 的部门服务器以发送出站邮件，并从邮件服务器收发入站邮件。简单来说，减少你在网络上运行的软件包副本数量，就能减少被入侵者利用的配置错误发生的概率。

我并不是要针对 `sendmail`。我也可以对 `IMAP` 以及几十种其他软件包重复同样的论点。事实上，大多数守护进程都属于这一类——客户端并不需要它们。有两种简单的方法可以访问（禁用）不需要的守护进程：

-   在 `/etc/inetd.conf` 文件中注释掉不需要的守护进程。大多数网络服务由 `inetd` 启动，而 `inetd` 只会启动在 `inetd.conf` 文件中列出的服务。从文件中移除服务可以防止外部人员使用指定的网络服务，但它不会阻止桌面客户端在出站连接中使用该服务。因此，如果从 `inetd.conf` 中删除了 `ftp`，用户可以使用 `ftp` 访问远程站点，但无法从远程站点通过 `ftp` 登录用户的桌面。

-   从启动项中移除启动不需要守护进程的脚本。某些网络服务守护进程（如 `sendmail` 和 `named`）在启动时会运行。使用 `sysconfig` 或 `linuxconfig` 从启动项中移除不需要的守护进程。例如，如果 `Linux` 客户端不是 Web 服务器，则不需要运行 `httpd` 脚本。即使 `httpd` 脚本在启动时不运行，客户端仍然可以使用 Web 浏览器。网络守护进程不是唯一需要的软件，客户端也不是唯一的目标。服务器上不需要的软件也可能为入侵者打开漏洞。如果你有一个专门的 `DNS` 服务器，它需要运行 `named`，但它不需要 `sendmail` 守护进程。同样，如果你运行一个专门的邮件服务器，它不需要 C 编译器（你可以在桌面系统上进行编译并将产物移动到服务器）。

| 安全与故障排除 |
| :--- |

| 第 4 部分 | 提示：你服务器上的所有东西都是入侵者的潜在工具。深思一下服务器为了工作真正需要什么。 |

限制服务器上安装软件的方法有两种。首先，在进行 `Linux` 安装时，不要安装你不需要的内容。在安装期间，根据你的系统计划仔细选择需要安装的软件包和加载的守护进程。另一种限制服务器软件的方法是在安装后将其移除。例如，要从带有 `rpm` 的系统中移除 `imap`，你可以输入 `rpm -e imap`。除了安装最新软件和移除不必要的运行外，你应该将访问限制在真正需要的系统上。`Linux` 通过提供两种强大的访问控制机制（`Wrapper` 和 `ipchains`）变得简单。

## 使用 Wrapper 控制访问

`Wrapper` 守护进程 `named tcpd` 由 `inetd` 执行。在 `Linux` 系统上使用 `Wrapper` 比许多其他 `Unix` 系统要容易，因为 `inetd.conf` 文件中的项已经指向了 `tcpd` 程序。注意：不记得 `inetd.conf` 文件的格式了吗？第 5 章“登录服务”中有解释。

以下是来自红帽 6 系统 `inetd.conf` 文件的内容：

```
ftp stream tcp nowait root /usr/sbin/tcpd in.ftpd -1 -a
telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd
shell stream tcp nowait root /usr/sbin/tcpd in.rshd
login stream tcp nowait root /usr/sbin/tcpd in.logind
talk dgram udp wait /usr/sbin/tcpd in.talkd
ntalk dgram udp wait root /usr/sbin/tcpd in.ntalkd
imap stream tcp nowait root /usr/sbin/tcpd imapd
finger stream tcp nowait root /usr/sbin/tcpd in.fingerd
```

如示例所示，`tcpd` 的路径被用来替换每个守护进程的路径。当 `inetd` 接收服务请求时，它启动 `tcpd`。`tcpd` 记录服务请求并检查访问控制信息，如果允许，则启动真正的守护进程处理请求。`Wrapper` 执行两个基本功能：记录服务的请求并为这些服务提供访问控制。如果你正在寻找入侵者，记录网络请求非常有用。
