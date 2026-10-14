
```
Biff
DEB: biff
RPM: biff
WWW: ftp://ftp.uk.linux.org/pub/linux/Networking/mail/
```

`biff` 工具会在新邮件到达时通过打印邮件消息的头部和前几行来通知你。

要打开 `biff`，请使用 `y` 作为选项。要关闭 `biff`，以便停止在新邮件到达时收到通知，请使用 `n` 作为选项。与大多数工具不同，`biff` 选项不需要加连字符。

⇒ 要打开 `biff`，输入：

```
$ biff y [RET]
```

有些人会将上一行放入他们的 `.bashrc` 文件中，这样 `biff` 在所有 shell 中都会始终处于开启状态（请参阅 Recipe 3.5.6 [更改 Shell 提示符]，第 80 页）。

单独输入 `biff` 且不带任何选项会告诉你 `biff` 是设置为 `y` 还是 `n`。

⇒ 要查看 `biff` 的设置，输入：

```
$ biff [RET]
```

配套工具 `xbiff` 仅在 X Window System 中工作（你也可以在 X 中使用常规的 `biff`）。

启动 `xbiff` 时，它会绘制一个包含邮箱的窗口，看起来像图 32-1。当邮件到达时，`xbiff` 会响起系统铃声，窗口图标颜色反转，邮箱标志会升起，如图 32-2⁵ 所示

⁵ Noah Friedman 提供了一套可用的替代“Spam”图像，可从 http://www.splode.com/~friedman/software/packages/index.html 获取。

NOTES: `biff` 的原始版本是以一只狗的名字命名的。在 20 世纪 80 年代初，在 UC Berkeley 的一个计算机实验室里，一个女孩在去使用电脑时会带上她的狗 Biff。Biff 以在邮递员送来当天的邮件时对邮递员狂吠而闻名。Biff 在伯克利的 BSD UNIX 黑客中也很受欢迎，当其中一位黑客编写了邮件通知工具时，他想到了 Biff 和邮递员——因此得名。（Biff 这只狗于 1993 年 8 月去世。）

![](img/be7f02611e5cefde1a18c788fede22f7_658_0.png)

图 32-1. 一个 `xbiff` 窗口。

![](img/be7f02611e5cefde1a18c788fede22f7_658_1.png)

图 32-2. 当邮件等待时 `xbiff` 窗口。

## 32.4.3 统计你有多少封邮件

```
Elm
DEB: mailutils
RPM: elm
WWW: http://www.instinct.org/elm/
```

使用随 `Elm`⁶ 分发的 `messages` 工具来统计文件夹或文件中的邮件数量。将邮件文件夹的名称作为参数给出；不带参数时，它会统计你收件箱中等待的邮件数量。

⁶ 在 Debian 系统上，`messages` 随 GNU Mailutils 包一起提供。

⇒ 以下是两种使用方法。

- 要查看你等待的电子邮件数量，输入：`$ messages [RET]`

- 要统计邮件文件夹 `~/email/saved` 中的电子邮件数量，输入：`$ messages ~/email/saved [RET]`

## 32.4.4 查看邮件发件人

查看邮件发件人有两种方法，它们使用两个名称相似的不同工具。

### METHOD #1

```
Elm
DEB: mailutils
RPM: elm
WWW: http://www.instinct.org/elm/
```

使用随 `Elm`⁷ 分发的 `frm` 来输出邮件的发件人姓名和主题列表。将邮件文件夹的名称作为选项给出；不带选项时，`frm` 会读取你的收件箱。

⇒ 以下是两种使用方法。

- 要输出显示传入邮件发件人姓名和主题的列表，输入：`$ frm [RET]`

- 要输出显示文件 `~/email/saved` 中邮件的发件人姓名和主题的列表，输入：`$ frm ~/email/saved [RET]`

如果没有邮件，`frm` 会告诉你。

### METHOD #2

`from` 工具的工作方式与 `frm` 类似，但它不输出主题行；相反，它输出发件人的姓名和邮件接收时间。

⇒ 要输出传入邮件消息的列表，显示发件人姓名以及接收时间和日期，输入：

```
$ from [RET]
```

如果没有邮件，`from` 不会输出任何内容。

## 32.4.5 验证电子邮件地址

```
vrfy
DEB: vrfy
RPM: vrfy
```

使用 `vrfy` 来确定给定的电子邮件地址是否有效。当你不确定是否拥有某人的正确电子邮件地址时，这很有用。如果地址有效，`vrfy` 会输出一条消息表明收件人存在；如果地址无效，`vrfy` 会输出一条消息说用户未知。

⇒ 要验证电子邮件地址 `user@example.edu` 是否有效，输入：

```
$ vrfy user@example.edu [RET]
```

使用 `-f` 选项指定包含电子邮件地址的文本文件；`vrfy` 会尝试验证文件中包含的所有电子邮件地址。

⇒ 要验证文件 `net-legends-faq` 中包含的所有电子邮件地址，输入：

```
$ vrfy -f net-legends-faq [RET]
```

NOTES: `vrfy` 依赖于远程系统来获取此信息；在当今高度企业化的互联网时代，越来越多的站点不再向公众提供此类信息。然而，它仍然足够有用，值得提及。

## 32.4.6 搜索邮件归档

你可以像搜索任何文本文件一样搜索邮件归档的内容：使用 `grep` 输出匹配模式的行，或在文本查看器或编辑器中浏览归档并在上下文中显示搜索文本。

### METHOD #1

要搜索邮件归档的文本，请以通常的方式使用 `grep`（请参阅第 14 章 [搜索文本]，第 333 页）。

⇒ 要输出 "~/Mail/emily" 中包含文本 "password" 的所有行，不区分大小写，输入：

```
$ grep -i password ~/Mail/emily [RET]
```

### METHOD #2

使用文本查看器或编辑器浏览邮件归档并搜索文本，如第 9 章 [Viewing Text] 第 211 页和第 10 章 [Editing Text] 第 231 页所述。

通过主题搜索邮件归档是一种不错的方法；`less` 工具特别有用，因为搜索词会被高亮显示。

⇒ 要在 `less` 中高亮当前正在浏览的文件中的所有主题行，并将光标移动到下一条，输入：

```
/Subject:.* [RET]
```

## 32.5 使用邮件附件

MIME（"Multipurpose Internet Mail Extensions"）是用于编码和将文件附加到邮件消息的 Internet 标准。它在通过电子邮件发送图像、音频或其他非纯文本数据时使用。

通常，你使用 MUA 读取和发送 MIME 邮件。以下配方展示了在命令行上发送和接收 MIME 邮件的方法，当你只是使用 `mail` 工具偶尔读取和发送带附件的邮件时很有用，但任何合理的 MUA 中内置的处理 MIME 邮件的方法无疑会比这里描述的技术更容易、更方便（参见配方 32.7 [Using Other Mail User Agents] 第 631 页）。

### 32.5.1 读取邮件附件

除了使用你的 MUA 外，读取附件有两种方法。

### METHOD #1

```
Metamail

DEB: metamail

RPM: metamail

WWW: http://bmrc.berkeley.edu/~trey/emacs/metamail.html
```

要读取邮件附件，将消息写入文件然后运行 `metamail`。

## Balsa

在安装了 GNOME 的 X 中工作的图形邮件客户端；其界面在某种程度上受到了专有的 Eudora 的启发。

![](img/be7f02611e5cefde1a18c788fede22f7_665_0.png)

```
DEB: balsa
RPM: balsa
WWW: http://www.balsa.net/
```

## Elm

菜单驱动的 MUA，在 1990 年代初期在经验丰富的用户中很受欢迎——它有一些有趣的功能，包括以批处理模式向多个地址同时发送邮件的方式，并附带一个将备忘录作为电子邮件消息发送的工具。多年来人们对 `Elm` 的兴趣大大减弱，大多数新手被建议改用 `Mutt`。

![](img/be7f02611e5cefde1a18c788fede22f7_665_1.png)

```
RPM: elm
WWW: http://www.instinct.org/elm/
```

## Gnus

`Emacs` 新闻阅读器（随 `XEmacs` 预装）也可用于读取和发送邮件。它功能众多，应该会吸引 `Emacs` 爱好者——但警告：有些人会觉得它令人望而生畏！

![](img/be7f02611e5cefde1a18c788fede22f7_666_0.png)

*Figure 32-5. Gnus.*

```
DEB: gnus
RPM: gnus
WWW: http://gnus.org/
```

## MEW
