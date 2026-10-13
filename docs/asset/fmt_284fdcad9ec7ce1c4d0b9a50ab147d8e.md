
有一点 `sendmail` 不做最终投递，`sendmail` 的作者明智将此任务交给了其他程序。`sendmail` 是一个以超级用户权限运行的大型复杂程序，这几乎是安全问题的根源，而在 `sendmail` 的过去，这种情况极少发生。最终投递增加的额外复杂性是 `sendmail` 不需要的东西。

## sendmail 的辅助文件

`sendmail` 依赖于许多辅助文件来完成工作。最重要的是 `aliases` 别名文件和配置文件 `sendmail.cf`。统计文件 `sendmail.st` 可以创建也可以不创建，取决于你是否需要统计数据。如果你打算将 `sendmail` 作为 SMTP 服务器运行（大多数站点都是如此），应该安装帮助文件 `sendmail.hf`。关于 `sendmail.st` 和 `sendmail.hf` 只需要说明这些了。（其他辅助文件在《sendmail 安装与操作指南》（简称 SIOG）中有介绍）。另一方面，`aliases` 和 `sendmail.cf` 文件足够重要，值得在专门的章节中进行介绍。

## Aliases 文件

`sendmail` 会检查收件者地址是否有别名，即收件者的备用名称。例如，每个互联网站点都要求有一个有效的邮件管理员（postmaster），以便向其报告问题。大多数站点并没有一个名为 postmaster 的实际账户可以将邮件管理员的邮件重定向到负责邮件管理的人员或人员。例如，在虚构的站点 go.com 中，用户 `joe` 和 `betty` 共同负责邮件管理，`aliases` 文件有如下条目：

```
postmaster: joe, betty
```

这一行告诉 `sendmail` 发送给 postmaster 的邮件应被投递给登录名 `joe` 和 `betty`。事实上，这些也可以是别名：

```
postmaster: firstshifts, secondshifts, thirdshifts
firstshifts: joe, betty
secondshifts: lou, emma
thirdshifts: ben, mark
```

在所有这些示例中，别名名称位于冒号左侧，而这些名称对应的别名位于右侧。`sendmail` 会反复评估别名，直到它们解析为真实用户或远程地址。在前面的示例中，为了解析别名 `postmaster`，`sendmail` 首先将其展开为收件者列表 `firstshifts, secondshifts, thirdshifts`，然后将这些别名中的每一个都进一步展开为最终列表——`joe, betty, lou, emma, ben, mark,` 和 `clara`。

虽然别名的右侧可以引用远程主机，但左侧不能。别名 `joe@whizzer.com` 是本地的，但 `joe@go.com: joe@whizzer.com` 则不是。

## 从文件读取别名——:include: 指令

别名可以用于创建邮件列表。（在前节的示例中，别名 `postmaster` 实际上是本地邮件管理员的邮件列表）。对于大型或频繁更改的列表，你可以使用 `:include:` 别名形式引导 `sendmail` 从文件中读取列表成员。如果 `aliases` 文件包含以下行：

```
homeboys: :include:/home/alphonse/homeboys.aliases
```

并且文件 `/home/alphonso/homeboys.aliases` 包含：

- alfonso
- joe
- betty
- george

其效果等同于别名 `homeboys: alphonse, joe, betty`。该指令对于频繁更改或由邮件管理员以外的用户管理的邮件列表非常方便。如果你发现某个用户要求频繁更改别名，可能想将其交由他或她控制。

## 发送给程序的邮件

别名还可以用于将电子邮件的内容发送给程序。例如，使用邮件列表是为了你可以通过向特殊地址 `list-request` 发送信件来获取有关列表的信息或进行订阅。信件的正文通常只包含一个单词，例如 `help` 或 `subscribe`，这会导致程序向发送者发送邮件。假设 `gonzo` 邮件列表有这样一个名为 `gonzo-request` 的别名：

```
gonzo-request: ~/usr/local/lib/auto-reply
```

在这种别名形式中，管道符号 `|` 告诉 `sendmail` 使用程序邮件器（mailer），该程序通常被定义为 `/bin/sh`。（参见本章稍后的“操作员——邮件器”部分）。`sendmail` 将消息馈给 `/usr/local/lib/auto-reply` 的标准输入，如果它正常退出，`sendmail` 认为信件已投递。

## 发送到文件

你也可以创建一个别名，导致 `sendmail` 将其消息附加到命名文件中。一个例子是别名 `nobody`，这在系统中很常见：

```
nobody: /dev/null
```
