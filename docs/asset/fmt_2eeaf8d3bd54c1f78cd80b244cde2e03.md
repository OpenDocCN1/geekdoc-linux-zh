
当你连接到互联网时，看到的第一个页面是主页。你可以选择将主页设置为你想看的网页，而不是别人想让你看到的页面。你可能还出于某种原因想调整历史记录设置（但绝对不是因为偏执）。这些步骤解释了你需要做什么：

- 1. 点击 GNOME 面板上的蓝色地球图标启动 Mozilla。
Mozilla 出现了“欢迎来到 Red Hat Linux”屏幕。你可以使用此页面查找更多关于 Red Hat 及其产品的信息。
专心于配置 Mozilla 并跳过所有的 Red Hat 信息；不过，那里有很多有用信息，你可以根据自己的意愿探索它的世界。

- 2. 选择 编辑(Edit)：首选项(Preferences)。
首选项窗口的左侧是一个类别列表，你可以将其看作是首选项窗口中位置的地图。

- 3. 点击导航器(Navigator)类别旁边的箭头加号将其展开。
在这里，你决定了启动 Mozilla 时显示哪个网页，以及点击导航工具栏上的主页按钮时加载哪个网页。

![](img/453364505e32ffec24f7d88ac7824962_165_0.png)

# 第 11 章：网络冲浪与音乐享受

- 4. 在首选项窗口的“主页(Home Page)”区域，在“位置(Location)”字段中填写你想作为主页的网页 URL。
你也可以浏览到你选择的网站，点击“首选项”，然后点击“使用当前页面(Use Current page)”。
例如，输入 `www.linuxworld.com`，每当你启动浏览器或点击 Mozilla 窗口左角的主页按钮时，都能看到关于 Linux 的有趣信息。
Mozilla 会记住你去过哪里并让你选择（并前往）之前的位置。Mozilla 记住多久（列表变得有多大）取决于你选择多少天的历史。历史配置选项决定了你访问的位置保存的天数。如果你磁盘空间不足，请选择一个较低的历史数字，例如一天或两天。否则，保持默认设置即可。
如果你的 Linux 电脑连接到带有代理防火墙的网络，你必须配置 Mozilla 以使其工作。要这样做，从首选项窗口选择 高级(Advanced)>代理(Proxies)。点击“手动代理配置”单选按钮并输入你的防火墙名称。在 HTTP 代理文本框中输入 `proxy.mynetwork.com`（如果那是防火墙名称），并在端口(Port)文本框中输入 `80`。如果你使用的是 Red Hat 默认防火墙或我们在书中描述的包过滤防火墙，则无需执行此配置。

![](img/453364505e32ffec24f7d88ac7824962_166_0.png)
![](img/453364505e32ffec24f7d88ac7824962_166_1.png)

## 安装插件

Mozilla 执行你对浏览器期望的任务，例如显示带有文本的图形。在帮助的情况下，Mozilla 不会额外显示动画和 JavaScript 等内容。当涉及到特殊功能时，Mozilla 是一块空白。
然而，在像你这样的朋友的一点帮助下，Mozilla 可以更进一步。这种帮助是以插件的形式提供的。`插件（plug-in）` 是 Mozilla 在需要执行额外功能时使用的软件。要使用插件，你只需要——抱歉——把它插进去即可。
插件的流程非常简单：
- 获取插件并将其放在 Mozilla 插件目录中。
- 可选，配置 Mozilla 首选项以使用这些插件。

# 第三部分：Linux，哈！它有什么用？无处不在！

我们介绍了如何下载和安装几个流行且必要的插件。让我们从流行的 Macromedia Shockwave Flash 插件开始。Mozilla 可以显示动画和其他酷炫的内容。按照以下步骤操作：

- 1. 启动 Mozilla 和你的互联网连接（如有必要），然后点击 帮助(Help)>关于插件(About Plug-ins) 菜单检查哪些插件已经拥有访问权限。
Mozilla 显示只安装了默认插件 `libnullplugin.so`。你需要下载并安装一些插件。
点击已安装插件(Installed-ins)页面顶部的 Netscape 链接将带到 Netscape 页面。

- 2. 在文本框中输入地址 `www.macromedia.com/downloads` 并按回车。
打开 Macromedia 下载页面。

- 3. 点击页面中间的“获取免费播放器(Get Free Players)”按钮。

- 4. 点击“立即下载(Download Now)”按钮，打开 `install_player_6_linux.tar.gz` 窗口。

- 5. 点击“保存(Save)”按钮，软件将保存到你的主目录。

- 6. 打开 Gnome 终端(Gnome Terminal)。

- 7. 你需要变成 root（超级用户），因此在终端中输入此命令：
```
su
```

- 8. 输入此命令解压 Flash 媒体：
```
tar xzf install_player_6_linux.tar.gz
```
创建 `install_player_6_linux` 目录，其中放置了 Flash 插件。

- 9. 将文件复制到 Mozilla 插件目录：
```
cp install_player_6_linux/libflashplayer.so /usr/lib/mozilla-*/plugins
```

![](img/453364505e32ffec24f7d88ac7824962_167_0.png)

# 第 11 章：网络冲浪与音乐享受

我们在此命令中使用指定星号 (`*`)是因为你使用的 Mozilla 版本可能与我们不同。星号替换了 Mozilla 版本号。

- 10. 选择 帮助(Help)->关于插件(About Plug-ins)，窗口打开，如图 11-1 所示。
步骤 1 中描述的 Mozilla 窗口打开并显示了你刚刚安装的 Flash 插件。

![](img/453364505e32ffec24f7d88ac7824962_168_0.png)

图 11-1：插件窗口显示了 Flash 插件。

你的 Mozilla 浏览器现在可以显示任何使用 Flash 内容的网页。

安装 Macromedia Flash Player 插件对非常有帮助。此列表显示了一些适用于 Linux 的常用插件，你应该考虑安装：

- Acrobat (Adobe)：读取 Adobe 便携式文档格式 (PDF) 文件。许多网站通过 PDF 文件而不是 HTML或其他格式提供信息。你可以从 `ftp://ftp.adobe.com/pub/adobe/accrobatreader/unix/4.x` 下载 Acrobat 插件。（注意你可以使用开源的 xpdf 程序查看 PDF 文件）。

- Shockwave (Macromedia)：提供多媒体、图形和游戏支持。你可以从 `www.macromedia.com/downloads` 下载 Shockwave 插件。

# 第三部分：Linux，嘿！它有什么用？无所不能！

- RealPlayer (RealAudio): 允许你播放 RealNetworks 的音频和视频流。许多网络电台台仍使用 RealNetworks 协议来传输其内容。你可以下载 RealPlayer 插件 
```
http://proforma.real.com/real/player/unix/unix.html?src=downloader,000814rpchoice_cl
```
安装 RPM 包，然后将插件拷贝到 Mozilla 插件目录，就像 Macromedia Flash 一样：
```
cp /usr/lib/RealPlayer8/rnpno.so /usr/lib/mozilla-*/plugins/
```
你也可以使用 RealPlayer8 应用程序直接收听 RealAudio 流。

- Java (Sun Microsystems): 一种许多网站使用它提供动态内容的编程语言。虽然动态内容有多种形式，但它基本上是任何随时间推移而改变的内容。Java 擅长提供那些有趣的且往往让人烦恼的、旋转并耍其他愚蠢技巧的 Webset。从 `java.sun.com/j2se/1.4.1/download.html` 下载 Linux 版 Java 2 Platform 标准版 (J2SE) RPM 包。

说到曲子，下一节将展示如何从你的 CD-ROM 播放音乐。

## 使用 CD 播放器随音乐起舞

想象你正独自坐在电脑前工作。或者，你可能正在读一本让你感到无聊的书。当然，现在是周六晚上。真闷。想找点消遣吗？也许是音乐；但我们可以向你展示如何使用电脑来听一些音乐。
在接下来的章节中，我们将向你展示 Red Linux提供的将你的工作站变成音频系统的工具，包括播放 CD 所需的所有应用程序，以及将 PC 连接到声卡和扬声器的工具。首先确保你的电脑可以播放音乐。

## 设置音响系统

在第 3 章描述的安装过程中，Red Linux 应该已经自动配置了你的电脑音频系统。然而，你可能会遇到问题——特别是在旧电脑上——因此 Red Hat 提供了一个声卡检测实用程序。

# 第 11 章：网络冲浪与随音乐起舞
