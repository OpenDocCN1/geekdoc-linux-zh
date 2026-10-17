
你的邮件文件夹索引以列表形式显示，你可以通过光标键上下滚动来选择邮件（见图 11.6）。从邮件主列表中，你可以删除、恢复、保存、阅读并将邮件导出到你的目录。要阅读邮件，只需按 Enter 键即可。

图 11.6

你可以通过 pine 邮件文件夹的邮件列表来选择邮件。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_281_0.png)

`pine` 程序具有许多命令行选项和其他功能，例如内置帮助，你可以通过 `pine` 主菜单中的问号 (?) 来访问。

## 配置和使用 Netscape Messenger 进行电子邮件

Netscape Messenger 是 Netscape Communicator 套件中的一个组件，是 X Window System 的图形化电子邮件客户端。你可以通过在 Netscape Navigator 窗口中点击 Netscape 组件栏上的 Messenger 按钮，从 Communicator 菜单启动此程序。你也可以使用如下的 `-mail` 选项通过 `netscape` 命令启动它：

```
# netscape -mail &
```

当客户端启动时（如图 11.7 所示），选择 Edit 菜单，然后点击 Preferences 菜单项。当 Preferences 对话框出现时，点击 Mail & Groups 项，然后点击 Identity 列表项。输入你的姓名和电子邮件地址，如图 11.8 所示。

图 11.7

Netscape Messenger 是 X11 中易于使用的电子邮件界面。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_282_0.png)

图 11.8

在 Messenger 对话框中输入你的姓名和电子邮件地址，以及其他所需信息（如你的组织）。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_282_1.png)

默认情况下，Netscape Messenger 以 HTML 格式发送你的电子邮件正文。如果发送给其他 Netscape 用户是可以的，但对于使用 `mail`、`elm` 或 `pine` 的其他用户来说，这是一种混乱的通信方式。关闭 HTML 消息格式：点击 Mail & Groups 下的 Messages 列表项，然后在 Messages 对话框的 Message Properties 部分取消选择 HTML messages 按钮。

接下来，点击 Mail Server 列表项。此对话框（见图 11.9）用于设置多个关键项目，例如服务器名称和你的 ISP 的邮件检索协议。输入你的用户名（通常是你用于登录 ISP 的名称），然后在 Incoming mail server 字段中输入你的 ISP 邮件服务器的名称（将 outgoing server 条目保持为 localhost）。接下来，点击选择你的 ISP 使用的邮件服务器协议类型。

图 11.9

你可以使用 Messenger Mail Server 首选项对话框设置检索和发送邮件所需的关键信息。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_283_0.png)

点击 More Options 按钮更改其他设置，例如默认邮件文件夹或 Messenger 检查待处理邮件的频率。

完成后，点击 OK 保存更改。在主 Messenger 窗口中，点击 Get Msg 按钮（见图 11.7）。Messenger 会要求输入密码。点击 OK 按钮检索邮件。新的邮件会以列表形式出现在 Messenger 窗口中。要阅读邮件，点击邮件列表中的所需邮件，其文本会出现在 Messenger 窗口的下半部分。

此时，你可以使用各种 Messenger 按钮来回复、转发、保存、打印或删除邮件。要撰写新邮件，点击 Messenger 菜单栏中的 New Msg 按钮。Messenger Compose 窗口出现，如图 11.10 所示。

图 11.10

通过 Messenger 的 Compose 窗口撰写新邮件、收件人地址并附加网页或文件。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_284_0.png)

在 To: 字段中点击以输入收件人。要输入多个收件人，在输入电子邮件地址后按 Enter。接下来，点击 Subject: 字段并输入主题。如果你想随邮件发送附件，点击撰写窗口菜单栏中的 Attach 按钮，或选择 File 菜单和 Attach 菜单项。在 Compose 窗口的空白区域（格式栏下方）点击鼠标并输入邮件。完成后，你可以保存邮件为草稿、拼写检查邮件，或点击 Send Now 按钮发送邮件。

## 订阅邮件列表

当你确信邮件系统正常工作时，你可能想订阅一个邮件列表。邮件列表由自动邮件服务器处理，通过将消息转发给邮件列表的所有成员来工作。订阅邮件列表的一个明智方法是注册摘要版，其中当天的邮件流量被浓缩成每天一次或两次的邮件。

你可以通过浏览以下网址了解更多关于邮件列表的信息：

`http://www.lsoft.com/lists/listref.html`

很可能你能找到一个感兴趣的邮件列表（前述网站可让你搜索当时可用的 135,000 个列表中的超过 21,000 个）。祝你玩得开心！

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_285_0.png)

要通过电子邮件参与关于 OpenLinux 的讨论并与其他 OpenLinux 用户交换信息，请发送邮件至 `majordomo@rin.caldera.com`，并在邮件正文中包含以下行：

```
subscribe caldera-users youremailaddress@yourisp.com
```

一封电子邮件会要求你确认订阅。请根据邮件指示回复。如需了解此服务的更多信息，请发送邮件至 `majordomo@rin.caldera.com`，并在邮件正文中包含单词 `help`。你会收到一封包含大量关于使用 Caldera 邮件列表细节的回复。对于 Caldera OpenLinux 列表的摘要版，请发送邮件至 `majordomo@rin.caldera.com`，并在邮件正文中包含以下行：

```
subscribe caldera-users-digest youremailaddress@yourisp.com
```

## 配置 procmail 并编写对抗垃圾邮件的配方

### 新术语

我们都习惯于收到垃圾邮件或电话营销电话。日复一日，我们收到信用卡、房屋净值贷款、新长途服务或当地食品市场里烤牛肉特价的优惠。你可以对不需要的邮寄邮件、传真和电话营销电话做些什么，但目前尚无关于垃圾邮件（也称为 SPAM，不应与著名的罐装肉制品混淆）的全国性法规。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_285_1.png)

### 新术语

然而，你可以使用位于 `/usr/bin` 目录下的 `procmail` 来过滤你的来信。你需要创建一个目录、创建几个文件、编写一个小脚本，并通过编写简短的过滤器或 `procmail` 配方来自定义来信的处理方式。设置系统以整理来信并处理垃圾邮件只需一分钟左右。

第一步是在你的主目录中创建一个名为 `.procmailrc` 的文本文件。然后，输入以下内容，指定你的邮件目录名称（如果你使用 `pine`，目录为 `mail`）、`.procmail` 目录的位置（你很快会创建它）以及你的 `procmail` 过滤器文件名称：

```
MAILDIR=$HOME/mail
PMDIR=$HOME/.procmail
INCLUDERC=$HOME/.procmail/rc.mailfilter
```

保存此文件。接下来，在你的主目录中创建一个名为 `.forward` 的文本文件。此文件需要包含以下行：

```
"|IFS=' ' && exec /usr/bin/procmail -f - || exit 75 #username"
```

此命令行控制 `procmail`，你应使用自己的用户名代替 `"username"`。现在，使用 `chmod` 命令使你的 `.forward` 文件对所有人可读，并使你的主目录对所有人可搜索。见以下示例（确保你在主目录中）：

```
# chmod 644 .forward
# chmod a+x .
```

你几乎完成了。现在，使用 `mkdir` 命令创建一个名为 `.procmail` 的目录，进入该目录并创建一个名为 `rc.mailfilter` 的文本文件。

此文件用于存放你的 `procmail` 过滤器或配方。虽然这些配方可以非常复杂（事实上复杂到可以编写自己的邮件投递服务），但本节介绍一些简单的配方供你入门。

首先，检查示例邮件的邮件头（包含 From:、To: 或 Subject: 行）。英国 MG 运动车摘要在每封邮件中都有以下主题行：

```
Subject: mgs@autox.team.net digest #905 Mon Nov 17 10:09:07 MST 1997
```
