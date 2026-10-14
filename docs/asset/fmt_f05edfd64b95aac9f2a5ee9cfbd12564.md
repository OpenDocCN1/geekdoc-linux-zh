
See the following figure for a description of the most important buttons and areas.

Different buttons in the Messenger window include:

- `Get Msg`—Click to download new messages.
- `New Msg`—Click to compose a new message.
- `Reply`—Click to reply to sender of the current message.
- `Forward`—Click to send a copy of the current message to another person.
- `Delete`—Click to delete the message from your mailbox.

You can also organize your messages into different boxes. To select a different message box, click the `Inbox` menu.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_100_1.png)

The Netscape Messenger window.

## Composing an Email Message

Sending email is just as easy as reading email. To send a message, click the `New Msg` button (see the previous figure). This will present you with a window where you can compose and address an email message like the one shown in the following figure. When done composing a message, click `Send Now` to forward your email message to your mail server for delivery.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_101_0.png)

Messenger 的撰写窗口——在这里输入新的电子邮件信息。

Kmail 在界面上与 Netscape 的 Messenger 组件非常相似。然而，目前 Messenger 是一款更精致的产品，工具和功能更好。

## 新闻

如果你有时间在 Usenet 上闲逛，无疑会找到很多有用和无用的东西。如果你想冲浪，你需要一个像样的新闻阅读器。同样，你的选择有几种：在 KDE 下你有 `knews`，在任何 X-Windows 下，包括 KDE，你有 Netscape 的 `Collabra`。

> Techno Talk：什么是 Usenet？
>
> Usenet 是一个全球分布式讨论系统。它由按主题分类的主题层级组成（新闻组）。信息在新闻服务器之间广播和传播。一些组是经过审核的，这意味着用户发布的信息需要在发布前得到批准。其他组则未经过审核。
>
> 有关 Usenet 是什么以及不是什么的详细描述，请参阅 http://www.cis.ohio-state.edu/hypertext/faq/usenet/usenet/what-is/part1/faq.html

`Collabra` 对电子邮件和新闻的区别不大。虽然访问它们的配置不同，但结果相似。你使用 `Collabra` 订阅你感兴趣的新闻组，然后使用 Messenger 阅读和发布信息。但是，在阅读新闻之前，你需要先下载一份可用的信息列表。当你点击其中一个时，该信息将被下载，你就可以查看它。如果你想发布信息，你基本上像撰写电子邮件一样撰写，但它会被发布到新闻服务器。从那里，信息会在全球范围内传播。

将你的系统配置为使用新闻很简单：你连接到一个新闻服务器（`nntp` 服务器；该机器的名称由你的 ISP 提供），并从该服务器下载一份非常长且很大的可用新闻组列表。（有成千上万个不同的组。）然后你选择所有感兴趣的组并开始阅读（见接下来的三个图）。作为 sanity check，你可能想为每天做这件事分配一定的时间。很容易沉迷于阅读新闻而没有意识到几个小时已经过去了。作为选择，我倾向于除非在搜索特定信息时，否则不查看新闻组。几年前，我曾经花费比任何人份额都多的时间阅读新闻。今天我尽量远离；很容易被噪音淹没。

如果你的 ISP 在特殊端口下提供新闻服务，请在 `Port` 空间中输入；否则保留默认的 `119`。组织也使用新闻来分发信息。其中一些新闻组只能通过需要身份验证的安全服务器访问：如果你的新闻服务器需要此功能，请在 `Port` 空间旁边的 `Secure` 复选框中进行勾选。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_102_0.png)

新闻配置面板。要配置你的新闻，请在 Communicator 的任何窗口中使用 `Edit` 菜单下的 `Preferences` 命令。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_102_1.png)

在你定义新闻服务器后，你将看到此窗口。在这里，你可以从你的新闻服务器提供的组中选择要加入的组。

如果你知道感兴趣的新闻组名称，请在 `Discussion Group` 旁输入并点击 `Join`。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_102_2.png)

Messenger 显示的新闻组列表。

使用 `Reply` 按钮回复帖子。如果你按住它，会出现一个菜单，允许你选择回复方式：回复到组、回复给发帖人，或两者兼顾。加粗列出的帖子表示尚未阅读。

## Telnet

`Telnet` 是与 Internet 上另一台计算机交互的另一种方式。它是一个仅限命令行程序，允许你通过命令行界面访问远程类 UNIX 计算机。`Telnet` 在第 17 章“Command Toolbox: Useful Shell Commands and Shortcuts”中讨论。

要访问内容，请点击章节和节标题。

## Complete Idiot's Guide to Linux

（出版商：Macmillan Computer Publishing）

作者：Manuel Ricart

ISBN：078971826x

出版日期：12/22/98

搜索本书：

## 第 10 章

自定义 KDE

## 本章内容

- 将应用程序添加到面板或应用程序启动器
- 其他 KDE 选项
- KDE 控制中心

KDE 具有相当高的可定制性；以下是你可以自定义桌面的快速指南。KDE 大部分是通过使用 `kdelnk` 文件进行自定义的（文件扩展名为 `kdelnk`）。这些文件提供 KDE 用于将文件与应用程序关联、将图标与应用程序和文档关联、将磁盘驱动器等设备与图标关联（见第 7 章“Working with Disks”）等配置信息。

KDE 面板可以通过多种方式进行自定义。以下各节介绍了其中一些最有用的方法。

## 将应用程序添加到面板或应用程序启动器

将应用程序添加到面板是一个简单的两步过程。首先，你需要创建一个提供有关要添加应用程序信息的 `kdelnk` 文件。该文件将可执行程序与图标及其文件关联。然后你通过将其拖入面板或将其放在应用程序启动器会找到的特殊目录中来安装 `kdelnk` 文件。

### 创建代表应用程序的 Kdelnk 文件

为应用程序创建 `.kdelnk` 文件很容易。该过程与我们在第 7 章“Working with Disks”中为软盘和 CD-ROM 驱动器创建 `.kdelnk` 文件的过程非常相似。右键单击桌面上的空白区域。当弹出菜单出现时，选择 `New` 然后 `Program`。会出现一个窗口，要求你为此 `kdelnk` 文件提供名称。将名称从默认的“`Program.kdelnk`”更改为代表你的程序的名称，例如“`Netscape.kdelnk`”。一个看起来像齿轮的图标出现在你的桌面上。

创建图标后，右键单击它并选择 `Properties` 命令。这将为你呈现一个面板，如下图所示。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_104_0.png)

此窗口控制 `kdelnk` 文件的属性。

点击 `Execute` 选项卡以更改将图标与实际程序关联的设置。`Execute` 面板看起来像下一个图中的那样。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_104_1.png)

执行选项卡允许你将程序与 `kdelnk` 文件关联。

如果你知道程序文件的位置，只需将其输入 `Execute` 字段即可。例如，Netscape 程序的路径是 `/opt/netscape/communicator/netscape`。如果你不知道确切路径，你也可以使用 `Browse` 按钮手动查找文件。
