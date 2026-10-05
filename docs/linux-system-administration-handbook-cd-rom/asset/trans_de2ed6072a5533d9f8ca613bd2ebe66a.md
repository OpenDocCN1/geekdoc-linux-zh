

## 7.4 .forward 文件

互联网上的账户可能希望所有电子邮件都发送到同一个位置。.forward 的示例展示了 .forward 文件的另一个功能——你可以使用命令而不是电子邮件地址。vacation 程序（休假程序）在 RedHat 中是不可用的（但在 CD-ROM 上有），它允许你在 .forward 文件中放置一个程序。每当有邮件进入时，该程序就会运行。vacation 程序会存储该邮件，然后向邮件发送者返回一条自定义消息，通知他们你休假（或出差、不在办公室、脑子不在状态等）。这样发送者就知道邮件已经送达了。

## Procmail

如果 procmail 作为邮件投递代理（MDA）安装在你的系统中（检查 `sendmail.cf` 中的 `Mlocal` 条目以确认），你就可以立即使用 procmail 过滤你所有的收件邮件。如果没有，你可以在 procmail 中放置对 `procforward` 的引用，以便在每次有新邮件到达时运行。procmail 用于在邮件进入时进行处理。这包括将来自“Plan9 MUSH 顾问委员会”的所有邮件放入一个邮箱，并与其他所有邮件分开，或者通过将其发送到 `/dev/null` 来过滤掉来自 billg@microsoft.com 的那些烦人邮件。

procmail 设置为默认的本地邮件处理器，设置 procmail 使用非常简单。创建一个 `.procmail` 文件并开始添加供 procmail 过滤的规则。如果 procmail 不是你的本地邮件处理器，你有三个选择：

- 1. 修改本地邮件处理器（man 页面给了你可以对 `/etc/sendmail.cf` 文件所作的修改建议）。如果你使用 m4 配置文件，请在文件中添加 `FEATURE(local_procmail)`。
- 2. 定期运行 procmail 或使用 `cron` 过滤已存在的邮箱。这允许你使用 `.forward`（在休假等情况下），但邮件并不总是被排序的，而且你必须等待。
- 3. 在 .forward 中放置对 procmail 的引用。注意，这不会让你轻松地转发所有内容。在 .forward 文件中，放入如下的一行：

```
|IFS=' &&exec /usr/local/bin/procmail -f-|exit 75 #YOUR_USERNAME
```

任何发送到 `/dev/null` 的内容都会被立即丢弃。这被称为“垃圾桶”。得亏 Linux 是一个 32 位操作系统，它的垃圾桶是最快的系统之一。

## 第 7 章 • 电子邮件

正如你所料的，问题 1 是最好的，因为它对每个人来说所需的精力最少。⁵ 这里有一个示例 `.procmailrc` 副本：

```
PATH=/bin:/usr/bin:/bin
MAILDIR=$HOME/Mail  #你最好确保它存在
DEFAULT=$MAILDIR/mbox  #完全可选
LOGFILE=$MAILDIR/from  #推荐
```

:0

+   * ^From.*mark

from_me

:0

+   * ^Subject::.*Flame

/dev/null

匹配行并对其执行某些操作有三个部分，也称为“配方”（recipes）。一个配方以一个以 `:0` 开头的行开始。在 `:0` 之后，你可以包含一些标志（例如 `H` 只扫描标头）。模式匹配针对以 `*` 开头的行进行。行的其余部分将原封不动地发送给 `egrep`⁶。如果所有行都匹配（这些行之间是“与”关系），则执行相应的操作。否则，它将移动到下一个配方。

只能有一个操作行，即不以 `*` 或 `:` 开头的那行。以 `!` 开头的操作将把程序转发给指定的用户。其他任何内容都将被认为是要追加的文件名（如果它尚的话）。

这两个示例显示，所有邮件都有一个 `From` 行，并且以 `mark` 结尾的邮件（这将是我发送给你的电子邮件）将被放入 `~/Mail/from` 邮箱。第二个示例显示，所有以单词“Subject”开头并以“Flame”结尾的电子邮件将将发送到 `/dev/null`（垃圾桶）。

如果你想直接删除邮件，需要知道的是，你必须绝对确定你的逻辑是正确的。因为，如果你删除了所有包含“Flame”一字的邮件，那么你可能会丢失主题诸如“上午 10 点前免费提供焰烤汉堡”的消息。

> ⁵ 除了系统管理员除外，他们必须安装软件并确保 `sendmail` 没有故障。等一下。那是你。删掉那句。

> ⁶ `egrep` -扩展 grep，其语法与普通 grep 不完全相同

## 7.5 邮件列表

好吧，这是一个很糟糕的例子。你可能想将想要删除的邮件保存一段时间，并检查它们，以确保你没有丢失任何重要内容。

邮件列表允许较大的群体通过电子邮件进行通信。在许多情况下，它比使用 USENET 好，因为

- 邮件列表的创建不需要批准。任何连接到互联网的机器都可以创建任何主题的邮件列表。让成员订阅它是完全另一回事了。
- 邮件列表可以控制谁订阅。邮件列表管理员可以设置为任何人都可以订阅，也可以可以设置为只有管理员可以向邮件列表添加新成员。如果出现问题，管理员还可以移除违规成员。
- 邮件列表可以控制内容。这听起来没有想象中那么糟，因为它是 USENET 那种无政府状态的替代方案。管理员可以将列表设为开放的，并提供一个健康的讨论区域（例如为开发某款软件的开发者提供），或者可以将列表设为管理员必须批准进入列表的每封电子邮件（类似于经过审核的 USENET 组）。审核列表适用于新闻发布稿、幽默列表或任何讨论量应该较低的列表。

## Majordomo

目前使用的最好的邮件列表程序非 majordomo 属。Majordomo 上述所有功能，以及其他一些功能，例如发送定期摘要或为了以后使用进行存档。我们稍后会回到这个问题。

首先需要设置的是 majordomo 本身，如果它还没有安装。它的源码位于 CD-ROM 上。为了使用它，你需要在系统中安装 perl 5（以及 gcc）。首先，创建一个 majordomo 用户。考虑到 Linux 的八字符限制，用户名必须缩短为 `major-dom`。你还应该为 majordomo 用户创建一个主目录。你可以根据喜欢使用 `/home/major`，或者根据喜好使用 `/usr/local/domomo`，或者任何你有空间的地方。

所以 majordomo，将 `majordomo.tar.gz` 文件复制到目录并解压缩。对 `majordomo.cf` 文件进行任何修改；然后只需使用 `make` 命令创建它。安装完成后（应该在 majordomo 目录下），你只需要对 `/etc/sendmail.cf` 文件进行一处更改。你应该已经列出了 OA（或 AliasFile）条目。在下方，放入

```
OA/home/majordomo.aliases
```

这设置了一个额外的文件来处理别名。这使得 majordomo 管理员更容易添加新列表，而该人员不需要 root 权限即可修改列表。现在创建列表本身。让我们创建一个名为 `gastro` 的虚拟列表。我们将使用开放列表来共享配方，因此任何人都可以加入，也可以向小组发布留言。

在 `majordomo.aliases` 文件中（以后我称之为别名文件，以防你选择 `/etc/aliases`）添加以下内容：

```
gastro: * /home/majordomo/wrapper resend -l gastro-list*
gastro-list: :include:/home/majordomo/lists/gastro
owner-gastro: mark
gastro-owner: mark
gastro-request: * /home/majordomo/wrapper majordomo -l gastro
gastro-approval: mark
```

这设置了基础。列表本身将是“gastro@host”，者是 mark，任何加入请求也将发送到 majordomo。通常用户发送 E-mail@host 来订阅，但不同的邮件列表软件工作方式不同。

> 你为 majordomo 用户设置密码了对吧？？

> 注意这有一点安全风险，因为 root 实际上是唯一可以创建新别名的人。如果你愿意，删掉这个声明并使用 `/etc/aliases` 代替 `majordomo.aliases` 文件。

