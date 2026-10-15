
如果这是你第一次使用 `ssh` 登录该系统，它会要求你确认是否真的想要连接。当出现此提问时，输入 `yes` 并按回车：

Host key not found from the list of known hosts.
Are you sure you want to continue connecting (yes/no)?

它应该以正常方式提示你输入用户名和密码。随后连接将像普通的 `telnet` 连接一样工作。唯一的区别是信息在网络上传输时经过了加密。你现在应该能够使用 `ssh` 命令运行远程命令，并使用 `scp` 命令复制文件。

## 如何获取更多信息

### 关于安全

这一章将成为你对抗安全问题战斗中的有用盟友。遗憾的是，没有任何章节或一本书能替你赢得战争；计算机安全是一场在不断变化的战场上进行的无休止的冲突。每一个新的操作系统升级都会带来新的安全漏洞的可能。每个新应用程序都可能有自己的隐藏危险。即使你对网络没有做任何更改，黑客也可能发现某些以前一直隐藏的新漏洞。幸运的是，互联网上的资源可以提醒你关注最新发现的安全漏洞，并告诉该如何应对它们。

## CERT

CERT 协调中心（CERT Coordination Center）是卡内基隆大学（Carnegie Mellon University）软件工程学院生存性系统计划（Survivable Systems Initiative）的一部分，这是一个联邦资助的研究开发中心。CERT 代表计算机应急响应小组（Computer Emergency Response Team）。它由 DARPA（国防高级研究计划署）于 1988 年应对臭名昭著的互联网蠕虫事件而创立。CERT 旨在成为报告所有计算机安全事件的中心。自 1988 年以来，CERT 扩大了其目的，包括：

- 协助创建新的事件响应小组。
- 在响应大型事件时协调团队的努力。
- 为事件响应专业人员提供培训。
- 研究安全漏洞的原因、漏洞预防、系统安全改进以及大型网络的生存性。

作为这些努力的一部分，CERT 发布告告，警示新发现的安全问题并解释如何防御这些问题。这些告告可以在 CERT 网站 `http://www.cert.org` 获取。你也可以通过订阅 CERT 告告邮件列表让 CERT 告告邮件发送到你的邮箱。

要订阅，请向 `cert-advisory-request@cert.org` 发送电子邮件。在主题行中输入你的 `your-e-address`。例如：

```
Subject: SUBSCRIBE login@mydomain.com
```

如果你想从 CERT 邮件列表中删除你的名字，请向 `cert-advisory-request@cert.org` 发送电子邮件。在主题行中输入 `UNSU your-email-address`。例如：

```
Subject: UNSUBSCRIBE login@mydomain.com
```

订阅列表后，你最终将开始接收消息。平均而言，你可以预期收到关于各种主题的消息。一个典型的 CERT 告告分为以下部分：

| 主题 | 描述 |
| :--- | :--- |
| 主题 | 对漏洞的简要描述。 |
| 受影响的系统 | 谁容易受到。例如，“此漏洞影响 Linux 5.0 及更高版本。” |
| 概述 | 对漏洞的非常短的描述。 |
| 描述 | 对漏洞更深入的描述。 |
| 影响 | 会发生什么样的损害。例如，“通过此漏洞，任何访问 FTP 的用户都可以获得 root 权限。” |
| 解决方案 | 你可以修复问题的方法，例如下载 |

CERT 还维护了一个安全工具库。我强烈建议访问 CERT 网站 `http://www.cert.org`。

## CIAC

另一个安全信息的良好来源是 CIAC 网站 `http://www.ciac.org`。CIAC 代表计算机事件能力（Computer Incident Capability）。像 CERT 一样，它发布告告或其他安全信息。它也有邮件列表。根据 CIAC 网站，你可以向 `majordomo@rumpole.ln1.org` 发送电子邮件订阅订阅列表。在邮件的正文（而不是主题）中输入：

```
subscribe ciac-bulletin
```

你应该在 30 分钟内收到列表服务器的回复。该列表在添加你之前需要确认订阅，以解决他们将他人加入列表的问题。只需按照确认邮件中的指令操作，你就会收到来自列表显示你已订阅的信息。

如果你在使用这些命令订阅或取消订阅时遇到任何问题，请向 `owner-majordomo@rumpole.ln1.org` 或 `ciac@ciac.org` 发送电子邮件寻求协助。在 `majordomo@rumpole.ln1.org` 的邮件正文中可以使用其他命令：

```
help 将发送指令的帮助文件。

unsubscribe ciac-bulletin 将从列表中取消订阅，但你必须从最初订阅的电子邮件地址提交此请求。
```
