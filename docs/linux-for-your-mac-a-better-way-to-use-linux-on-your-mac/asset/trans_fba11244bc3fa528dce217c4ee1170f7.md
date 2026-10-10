

或者选择新闻组。传统上，新闻组的选择保存在主目录中名为 `.newsrc` 的文件中。该文件可能如下所示：

```
comp.linux.setup:
comp.os.linux.portable:
comp.os.linux.powerpc:
...
```

有许多不同的 Linux 新闻组。请参阅附录以获取更完整的列表。你应该知道，并非每个 ISP（互联网服务提供商）都订阅了所有新闻组。你可能无法通过你的 ISP 的新闻服务器找到 `alt.barny.die.die.die`。为了在 Discussions 中读取 Usenet 新闻，你必须首先下载，然后勾选你想阅读的那些组。

为了开始操作，再次使用“首选项”菜单项，选择“邮件与新闻组”，然后单击“新闻组”菜单项。单击“添加”按钮，你将看到如图 9.21 所示的对话框。

输入你的 ISP 新闻服务器的名称，然后单击“确定”按钮退出首选项对话框。完成后，右键单击 Messenger 窗口左侧显示的你的 ISP 新闻服务器名称，然后在出现的弹出菜单中选择“订阅新闻组”菜单项。将显示一个订阅对话框，如图 9.22 所示。

将出现一个弹出对话框，要求输入你访问新闻服务器的用户名和密码。输入你的信息后，Communicator 将从你的 ISP 下载一个组列表。单击以选择（订阅）你的新闻组，完成后单击“确定”按钮。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_234_0.png)

图 9.21 *输入你的 ISP 新闻服务器的名称。*

![](img/1ea833f5a3e3c1547e3dd2891f52804a_235_0.png)

图 9.22 *下载你的 ISP 组列表后，通过单击每个期望的组来订阅新闻组。*

> 省时省力！不要通过滚动数千个新闻组来寻找，而是输入你想订阅的新闻组的前几个词。在“新闻组：”字段中单击，然后输入 comp.os.linux..，列表将自动滚动到这些组的开头！然后单击以勾选每个期望的组（你可能需要单击新闻组列表开头的小加号以展开选项）。

完成后，单击“确定”按钮。要从某个组获取消息，在 Messenger 窗口左侧单击你新定义的新闻服务器，然后单击一个新闻组名称。Messenger 将获取消息，然后你可以阅读和回复消息（如图 9.23 所示），这与使用 Messenger 的方式相同。

# 使用新闻阅读客户端

阅读 Usenet 新闻可以是一种有益的消遣，也是了解世界各地人员在许多不同主题上的技巧、窍门和技术的绝佳方式。当你订阅了一个新闻组但没有跟进回复或在新的主题上发帖时，你是在*潜水*。如果你为了看到回复而发布了一个愚蠢的评论，你就发了一个*诱饵*。如果有人大声痛斥你的评论，你就被*开火*了。交换书面嘲讽和侮辱是一场*骂战*。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_236_0.png)

图 9.23 *下载你的新闻组消息后，你可以单击每条期望的消息来阅读它们。*

而由数百人就某个主题进行的大规模论证和辩论则是一场*圣战*。

Linux 附带了足够多的 Usenet 软件工具，足以让你在 Usenet 上惹上麻烦！不过，总的来说，在较小的新闻组（如 `comp.os.linux.portable`）中，大多数 Linux 用户都非常文明和乐于助人；似乎是倡导团体表现得更加激烈。如果你文明、具体、切中要点并得体地回应，即使你是个*新手*（新用户），你也永远不会被被称为*losers*（失败者用户）。如果你在连接你的 ISP 新闻服务器时遇到问题，尝试创建一个名为 `NTTPSERVER` 的 shell 环境变量。你可以在命令行上快速轻松地做到这一点（如果你使用 *bash*，就像这样：

```
$ export NTTPSERVER=news.mysp.com
```

这将创建一个被许多新闻阅读客户端使用的变量，应该能解决任何连接问题，特别是当你试图访问由你的 ISP 维护的新闻阅读器，而不是其他 ISP 维护的新闻阅读器时。

# 经典新闻阅读器

Linux 提供了几个从 BSD UNIX 和其他较旧版本的 UNIX 继承下来的传统新闻阅读程序。这些包括 `tin` 和 `trn` 命令。几乎所有经典新闻阅读器都使用一个名为 `.newsrc` 的资源文件，其中包含你订阅的新闻组列表。这些新闻阅读器旨在控制台上使用，可以快速检索和显示关于你新闻组的信息。例如，你可以像这样启动 tin 阅读器：

```
$ tin -nqr
```

此命令行告诉 tin 阅读器不要向新闻服务器查询新的新闻组，并使用保存在你的新闻资源文件中的组。在获取新闻组列表后，tin 可能显示如下页面：

```
Group Selection (news.bellatlantic.net 20)                    h=help
1 1003 alt.binaries.e-book
2 4767 comp.sys.laptops              Laptop (portable) computers.
3 567 alt.os.linux.cald
4 832 comp.os.linux.portable
  5 15690 comp.os.linux.advocancy      Benefits of Linux compared to
  6 17 comp.os.linux.answers           FAQs, How-To's, READMES, etc.
  7 133 comp.os.linux.announce         Announcements important to th
  8 1572 comp.os.linux.development.apps Writing Linux applications, p
  9 1879 comp.os.linux.development.system Linux kernels, device drivers
 10 3663 comp.os.linux.hardware         Hardware compatibility with t
 11 5720 comp.os.linux.misc             Linux-specific topics not cov
 12 7079 comp.os.linux.networking       Networking and communications
 13 4803 comp.os.linux.setup            Linux installation and system
 14 1765 comp.os.linux.x               Linux X Window System servers
 15 47 comp.unix.aux                  The version of UNIX for Apple
 16 34 comp.unix.machten              The MachTen operating system

<n>=set current to n; TAB=next unread; g,/=search pattern; o/attach;
\=line down; k/line up; h/elp; m/o/e; q/uit; r=toggle all/unread;
s/ubscribe; S/ub pattern; u/ns/ubscribe; U/ns/ub pattern; y/ank in/out
```

你可以通过使用向上或向下箭头键高亮显示一个组，然后按 Enter 来读取特定组中的消息。将显示一个初始消息列表，如下所示：

```
alt.os.linux.cald (1067/8) 490A OK OK 0 h-help
1 + 12 24 "tss.cr3"                   john burt
2 + 10 26 Caldera OpenLinux Workstation 3.1 Beta Harold Col
3 + 2 60 Netscape Problem              Remo Matte
4 + 20 Newsbie Alert ==>
5 + 6 6 KDE 2.1.1 help Dimitris Andavoglou
6 + 2 15 KDE 2.1.1 anti-aliasing Bob Raymond
7 + 4 28 Caldera Workstation or: Open Beta Fox7777
8 + 7 24 CDR on eDesktop 2.4 1198
9 + 2 11 Upgrade Caldera OpenLinux 2.3 to 2.4 Eduard de Vries
10 + 4 35 XFce 4.0.3 problems Robert Gelb
11 + 11 Anti-aliasing in KDE 2.1.1 Robert Gelb
12 + 2 11 KDat + KDE Ulrich Mensefeld
13 + 14 16 Linux commands John Aifab Alam
14 + 5 6 Kernel Update Ed
15 + 3 15 Kernel2.4.3 problem Dimitris Andavoglou
16 + 2 11 MySQL Startup Script under eServer 2.3 Mathis Moder

<*>=set current to n; TAB-next unread; /-search pattern; ^X kill/select;
a}uthor search; clatchup; j=line down; k=line up; K=mark read; l=list thread;
|=pipe; m|all; o=print; q/uit; r=toggle all/unread; s|ave; t|ag; w=post
```

正如你所见，tin 使用单字母命令。这几乎是所有基于控制台的新闻阅读器的工作方式。一旦你选择一个新闻阅读器，在几个会话之后，你就会变得非常擅长阅读和导航。

## 使用 slrn

slrn 新闻阅读客户端是一个基于控制台的阅读器，具有彩色和易于使用的分屏界面。如图 9.24 所示的分屏窗口允许你在阅读消息时浏览主题。此客户端可以从桌面面板或 X Window 终端的命令行启动，如下所示：

```
$ slrn -n -c
```

此命令行告诉 slrn 不要检查你的 ISP 新闻服务器上出现的任何新新闻组。-c 选项指定使用颜色来阅读消息。按 Enter 后，你将看到 slrn 的主窗口。

与许多电子邮件客户端和新闻阅读程序一样，slrn 响应单字母命令。你可以随时输入问号以获得帮助。请注意，slrn 将使用默认系统编辑器来编辑后续回复或撰写帖子。因此，如果你不想最终使用 vi 编辑器，你可以定义不同的系统编辑器，例如 pico，就像这样：

```
$ export EDITOR=/usr/bin/pico
```

