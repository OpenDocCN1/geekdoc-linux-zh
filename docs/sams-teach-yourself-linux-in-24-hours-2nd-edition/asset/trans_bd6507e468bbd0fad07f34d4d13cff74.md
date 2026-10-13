
你可以使用 -help 选项获取 Netscape 初始命令行选项的列表。一些常用选项列在表 13.1 中。

## 表 13.1 常见的 Netscape Communicator 命令行选项

| 描述 | 选项 |
|---|---|
| 显示版本 | -version |
| 不记住会话设置 | -no-session-management |
| 不记住窗口设置 | -dont-save-geometry-prefs |
| 不显示许可页面 | -no-about-splash |
| 忽略已保存的窗口设置 | -ignore-geometry-prefs |
| 启动到 Composer | -composer or -edit |
| 启动到 Discussions（新闻阅读器） | -discussions or -news |
| 启动到 Messenger | -messenger or -mail |
| 限制颜色 | -install |
| 设置 X11 资源（来自 /opt/netscape/communicator 目录下的 Netscape.ad 文件） | -xrm resource |
| 显示 GUI 帮助 | -nethelp |
| 显示帮助 | -help |
| 启动后图标化 | -iconic |
| 以浮动工具栏启动 | -component-bar |
| 使用黑白 | -mono |
| 使用服务器 svr | -display svr |
| 使用位于 X,Y 的 WxH 大小窗口 | -geometry=WxH+X+Y |
| 使用 X 种颜色 | -ncols X |

其中一些选项在从终端窗口的命令行启动 Netscape 时很有用。例如，正如我在本小时前面指出的那样，geometry 设置可以帮助减小浏览器的初始窗口大小。对于屏幕空间有限的笔记本电脑用户来说，一个更好的选项是 -component-bar 选项，例如：

```
# netscape -component-bar &
```

该命令运行 Netscape，但应用程序及其附加组件，包括 Mailbox、Discussions 和 Composer，会出现在一个短小的垂直浮动窗口中（见图 13.2），你可以将其放在屏幕的一侧。然后，你可以通过点击小窗口中的一个图标来运行所需的组件。

### 图 13.2

Netscape Communicator 为小型桌面提供了一个方便紧凑的组件栏，可用于启动 Navigator 和其他组件。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_323_0.png)

如果你需要使用 Netscape 的帮助，请使用 Netscape 的帮助菜单信息系统。要获取帮助，请打开帮助菜单，然后点击“帮助内容”菜单项。帮助对话框会出现，如图 13.3 所示。与某些浏览器不同，Netscape 附带了你入门所需的所有帮助文件。你可以找到有关每个组件的信息以及如何设置和使用它们，同时还有关于 HTML 页面组成的完整讨论。

### 图 13.3

Netscape Communicator 附带完整的帮助和学习系统。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_323_1.png)

你可以通过点击 Looking Glass 桌面上的图标或点击 KDE 桌面面板上的图标从命令行启动 Netscape。Netscape 启动后，Navigator 主窗口会出现。如果你点击 Netscape 的位置字段或 Netscape 按钮栏中的主页按钮，Netscape 会使用地址 file:/usr/doc/html/Caldera_Info 在你的系统上加载一个介绍性帮助页面，如图 13.4 所示。

### 图 13.4

Netscape Communicator 会自动显示安装在计算机上的 OpenLinux 和 Linux 文档的本地链接。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_324_0.png)

这是一种方便快捷地阅读 OpenLinux 附带的大量文档的方式，如果你想了解更多关于系统的信息，这也是一个很好的开始阅读或搜索的地方。

要浏览到 Internet 地址，请确保你拥有活动的 Internet 连接，然后点击位置字段并输入 URL。Netscape 接受几种类型的 URL：

- about:mozilla 是 Mozilla 复活节彩蛋
- file:// 用于读取本地文件或显示本地图形
- ftp:// 用于登录并显示远程 FTP 服务器
- http:// 用于加载并显示远程网页
- news://your.favorite.newsgroup 用于阅读 Usenet 文章

新术语 Linux 版的 Netscape Communicator 还支持许多不同的插件，即为浏览器添加功能的附加程序。其中一些插件使你能够收听现场广播或观看录制或现场视频。有关使用 Netscape 的插件的更多信息，请浏览以下网址：http://home.netscape.com/plugins/index.html

一个有趣的插件是 RealPlayer 应用程序。该插件可以播放来自世界各地现场互联网电台的立体声音乐，并可在 Netscape 网页或单独窗口中显示视频剪辑或现场电视。见图 13.5。

### 图 13.5

来自 RealNetworks 的 RealPlayer 插件通过你的 PPP 连接显示实时视频和音频。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_325_0.png)

Netscape Communicator 会自动显示安装在计算机上的 OpenLinux 和 Linux 文档的本地链接。

要查看当前直播电视和广播电台的列表，请浏览以下网址：

```
http://www.timecast.com/stations/realvideo.html
```

有关获取最新 RealPlayer 插件的更多信息，请浏览以下网址：

```
http://www.real.com/products/player/50player/downloadrealplayer.html
```

## 使用 Internet Relay Chat 聊天

irc（Internet relay chat）命令位于 /usr/bin 目录下，是一个可用于在 Internet 上与其他人交谈的程序。运行 irc 时，你可以使用内置的 irc 命令连接到聊天服务器、查看谁正在聊天并设置许多其他选项。

irc 命令内置了超过 110 个不同命令和主题的帮助，其中许多主题还有进一步的子主题帮助。要使用此程序，你需要一个活动的 Internet 连接。默认情况下，irc 程序会尝试连接到默认聊天服务器（另一台支持 IRC 的计算机）。

连接后，屏幕分为两部分。正在进行的讨论和回复占据屏幕上部的大部分。你可以使用屏幕下部向 irc 程序输入命令或将键盘输入的句子作为消息发送给不同的活跃讨论。

使用 irc 与阅读和回复 USENET 新闻组（见第 11 小时“配置 Internet 电子邮件”和第 12 小时“配置 Internet 新闻”）大不相同。讨论和评论在你输入时被读取和发送。你应首先浏览 irc 命令的帮助设施，并阅读有关以下主题的所有可用介绍性信息：basics、commands、etiquette、expressions、intro、ircII、menus、news、newuser 和 rules。

要启动 irc，请在控制台或 X11 终端窗口的命令行中输入命令，如下所示：

```
# irc
*** Connecting to port 6667 of server irc-2.mit.edu
*** Welcome to the Internet Relay Network bball
*** If you have not already done so, please read the new user
information with
/HELP NEWUSER
...
```

按下 Enter 后，屏幕上会滚动显示大量信息。接下来，使用 irc /HELP 命令获取帮助主题列表，例如：

```
> /HELP newuser
> /HELP etiquette
```

下一步是查看哪些聊天组处于活动状态。使用 /LIST 命令。你会看到具有不同名称的组列表。要加入聊天组，请使用 /JOIN 命令，后跟聊天组的名称（前面带有井号），如下所示：

```
> /JOIN #linux
```

按下 Enter 后，你将加入该组，并可能会看到如下消息：

```
*** bball (-bball@207-132-114-136.s196.tnt2.brd.erols.com) has joined
channel #linux
*** Users on #linux: bball whizzo KerNEIDuDe cathy Scrotty
```

消息和聊天句子在你的屏幕上滚动。如果输入句子并按下 Enter，你的消息将被发送给聊天区域中的所有用户。要退出聊天会话，请使用 /LEAVE 命令，如下所示：

```
> /LEAVE
```

按下 Enter 后，你可以 /LIST 其他组或使用 /QUIT 命令退出 IRC。

要了解更多关于参与 irc 聊天会话的信息，请阅读内置帮助文件、ircII 手册页以及 /usr/doc/irc 目录下的 irc 文档。

了解更多关于在 Internet 上聊天的另一个地方是 http://www.irchelp.org。
