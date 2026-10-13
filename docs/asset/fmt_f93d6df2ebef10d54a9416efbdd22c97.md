
![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_323_1.png)

你可以通过点击 Looking Glass 桌面上的图标或点击 KDE 桌面面板上的图标从命令行启动 Netscape。Netscape 启动后，Navigator 主窗口会出现。如果你点击 Netscape 的位置字段或 Netscape 按钮栏中的主页按钮，Netscape 会使用地址 `file:/usr/doc/html/Caldera_Info` 在你的系统上加载一个介绍性帮助页面，如图 13.4 所示。

### 图 13.4

Netscape Communicator 会自动显示安装在计算机上的 OpenLinux 和 Linux 文档的本地链接。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_324_0.png)

这是一种方便快捷地阅读 OpenLinux 附带的大量文档的方式，如果你想了解更多关于系统的信息，这也是一个很好的开始阅读或搜索的地方。

要浏览到 Internet 地址，请确保你拥有活动的 Internet 连接，然后点击位置字段并输入 URL。Netscape 接受几种类型的 URL：

- `about:mozilla` 是 Mozilla 复活节彩蛋
- `file://` 用于读取本地文件或显示本地图形
- `ftp://` 用于登录并显示远程 FTP 服务器
- `http://` 用于加载并显示远程网页
- `news://your.favorite.newsgroup` 用于阅读 Usenet 文章

新术语 Linux 版的 Netscape Communicator 还支持许多不同的插件，即为浏览器添加功能的附加程序。其中一些插件使你能够收听现场广播或观看录制或现场视频。有关使用 Netscape 的插件的更多信息，请浏览以下网址：`http://home.netscape.com/plugins/index.html`

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

`irc`（Internet relay chat）命令位于 `/usr/bin` 目录下，是一个可用于在 Internet 上与其他人交谈的程序。运行 `irc` 时，你可以使用内置的 `irc` 命令连接到聊天服务器、查看谁正在聊天并设置许多其他选项。

`irc` 命令内置了超过 110 个不同命令和主题的帮助，其中许多主题还有进一步的子主题帮助。要使用此程序，你需要一个活动的 Internet 连接。默认情况下，`irc` 程序会尝试连接到默认聊天服务器（另一台支持 IRC 的计算机）。

连接后，屏幕分为两部分。正在进行的讨论和回复占据屏幕上部的大部分。你可以使用屏幕下部向 `irc` 程序输入命令或将键盘输入的句子作为消息发送给不同的活跃讨论。

使用 `irc` 与阅读和回复 USENET 新闻组（见第 11 小时“配置 Internet 电子邮件”和第 12 小时“配置 Internet 新闻”）大不相同。讨论和评论在你输入时被读取和发送。你应首先浏览 `irc` 命令的帮助设施，并阅读有关以下主题的所有可用介绍性信息：`basics`、`commands`、`etiquette`、`expressions`、`intro`、`ircII`、`menus`、`news`、`newuser` 和 `rules`。

要启动 `irc`，请在控制台或 X11 终端窗口的命令行中输入命令，如下所示：

```
# irc
*** Connecting to port 6667 of server irc-2.mit.edu
*** Welcome to the Internet Relay Network bball
*** If you have not already done so, please read the new user
information with
/HELP NEWUSER
...
```

按下 Enter 后，屏幕上会滚动显示大量信息。接下来，使用 `irc` `/HELP` 命令获取帮助主题列表，例如：

```
> /HELP newuser
> /HELP etiquette
```

下一步是查看哪些聊天组处于活动状态。使用 `/LIST` 命令。你会看到具有不同名称的组列表。要加入聊天组，请使用 `/JOIN` 命令，后跟聊天组的名称（前面带有井号），如下所示：

```
> /JOIN #linux
```

按下 Enter 后，你将加入该组，并可能会看到如下消息：

```
*** bball (-bball@207-132-114-136.s196.tnt2.brd.erols.com) has joined
channel #linux
*** Users on #linux: bball whizzo KerNEIDuDe cathy Scrotty
```

消息和聊天句子在你的屏幕上滚动。如果输入句子并按下 Enter，你的消息将被发送给聊天区域中的所有用户。要退出聊天会话，请使用 `/LEAVE` 命令，如下所示：

```
> /LEAVE
```

按下 Enter 后，你可以 `/LIST` 其他组或使用 `/QUIT` 命令退出 IRC。

要了解更多关于参与 `irc` 聊天会话的信息，请阅读内置帮助文件、`ircII` 手册页以及 `/usr/doc/irc` 目录下的 `irc` 文档。

了解更多关于在 Internet 上聊天的另一个地方是 `http://www.irchelp.org`。

## 安装和配置 AOL 即时通讯器

AOL 的即时通讯器，或 IM，是一个有趣且易于使用的 X11 客户端，用于通过互联网与朋友聊天。

该服务免费，您无需为软件付费。

该客户端会不断检查，并在朋友登录服务时立即通知您。然后您可以发送即时消息！

您首先需要在 AOL 的网站上注册，然后下载并安装 IM。

访问 `http://www.aol.com/aim/home.html` 并通过选择屏幕名称和密码并输入您的电子邮件地址来注册服务（您会通过电子邮件从 AOL 收到确认消息）。

接下来，前往下载部分，并选择 Java 版本。

下载名为 `aim_linux.sh`（一个自解压 shell 脚本）的五兆字节文件大约需要 20 分钟。

下载后，像这样开始安装：

```
# sh aim_linux.sh
```
