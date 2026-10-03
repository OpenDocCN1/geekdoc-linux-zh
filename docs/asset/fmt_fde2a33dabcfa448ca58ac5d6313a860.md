
## Window Maker

然后运行 `startx`。一旦进入环境，你就可以移动窗口、调整它们的大小并切换工作空间。Window Maker 最酷的功能之一是 `clip`。`clip` 可以配置为像 dock 一样吸引图标，但它的主要功能提供了一个在工作空间之间进行切换以及允许创建额外工作空间的简单界面。

Window Maker 最酷的功能之一是为窗口管理器存在的 dock 应用。这些是图标大小的应用程序，例如 DC 播放器、性能监控器、时钟、微仪表板等。虽然我使用多种 dock 环境（每当有机会就会展示它们），但 Window Maker 是我一直会回去使用的那个。

### KDE

现在让我们来看看目前最受欢迎的两个桌面环境之一。除了 GNOME 之外，没有哪个桌面环境能获得如此媒体的报道和关注。实际上，说“KDE 桌面环境”有点冗余，因为 KDE 代表 K Desktop Environment（酷炫桌面环境）。这个 K 代表什么？它代表“Kool”（酷炫）！

真的如此。

可以说，KDE 值得得它所获得的所有赞誉。这是一个美观、精炼且易于使用的桌面，配备了各种应用程序和工具。当那些行政事务让你感到压力很大时，你会发现有很多游戏可以消遣。说认真的，当我为父母配置他们的第一台电脑时，我安装了 Linux 和 KDE。我的父母是电脑领域的新的新手，而他们现在运行着 Linux。

曾几何时，KDE 的主页曾会询问 UNIX（以及 Linux）是否准备好进入桌面。而现在，他们谈论的是企业级。

与人们熟悉的 Windows 桌面一样，KDE 在左下角有一个大按钮，可以打开配置工具、程序、游戏等。桌面切换器位于看起来熟悉的任务栏中间，该任务栏支持停靠应用程序。（参见 9.6 节）。

除了常规工具集外，KDE 还拥有 KOffice，这是一套完整的生产力套件，包括文字处理器、电子表格、演示文稿包等。更棒的是，KDE 还带了 Konqueror，这是一个多功能文件查看器和管理器，它正迅速成为互联网上最好的浏览器之一。

KDE 的唯一缺点是它已经变成了一个“资源大户”，它需要一定程度的性能支持，包括处理器和内存。一台配备 16MB RAM 的 A486 可以制作 Linux 防火墙和 Web 服务器，但对于 KDE 来说还不够。

就像 Window Maker 一样，你的 Linux 发行版 CD 可能包含 KDE，但在 K Desktop Environment 网站（`http://www.kde.org/`）上始终提供最新版本。

提到强大的桌面，允许我介绍窗口管理器世界的另一颗星：GNOME。

### GNOME

GNOME 代表 GNU Network Object Model Environment（GNU 网络对象模型环境）。它是 GNOME 项目的全功能桌面环境。在 GNOME 面板（一个大脚）下，你会发现了一系列丰富的应用程序、系统工具、网络应用程序、游戏等等。

GNOME 的方法与 KDE 项目略有不同，因为它更多像是一个桌面工具包，而不是一个集成环境。在某些方面，这正是它的优势之一。让我们举个例子：在我写这本书的期间，GNOME 的默认窗口管理器是 Sawfish。而一年前，它是 Enlightenment。

由于这种“随处可插”的方法，许多窗口管理器（如 Window Maker）都集成了 GNOME 支持（有时被称为“感知 GNOME”）。例如，如果你想从 Window Maker 运行 GNOME 环境，可以点击应用程序菜单中的“运行”（Run）并启动一个 `xterm` 窗口。输入以下内容：

```
panel
```

如果你看图 9.7 的屏幕截图，你会看到 GNOME 桌面运行在下方的 Sawfish 窗口管理器之上。

> **预告**：如果我已经让你们兴奋地想要尝试更现代、更快、更慢的窗口管理器（甚至是下一个类 Windows 风格的候选者），而不是你们发行版 CD 中附带的版本，请不要担心。让它去互联网上走一趟，这就是第 10 章涵盖的内容。第 11 章将告诉你所有关于寻找和编译软件、你想知道但不敢于问的问题。请保持关注。

### QVWM

**图 9.7** GNOME 提供了一个平滑、精炼的桌面环境

GNOME 目前的优势之一来自它与 HELIX 的关联。这种优势是一个易于使用的网络更新和安装设施。在安装方面，如果你有互联网连接，GNOME 的安装非常简单且——

## 第 9 章 X 与图形化桌面

如果你想调整 X 显示设置，可以尝试这种方法：在命令行启动 `xvidtune` 后，立即点击 Show（显示）并记录下那些设置。我的设置看起来像这样：

```
Vendor: Unknown, Model: Unknown

Num hsync: 1, Num vsync: 3

hsyncync range 0: 30.00 - 70.00

vsync range 0: 50.00 - 180.00

*1024x768* 85.00 1024 1032 1152 1360 768 784 787 823
```

最后一行是启动 `xvidtune` 后点击 Show 的结果。之前的行是在 `xvidtune` 启动时打印的。现在，来看一眼 `XF86Config` 文件。任何 ModelLine 参数看起来眼熟吗？其中一个应该和你的设置完全匹配。在稍微调了一下水平数字后，点击 Test（测试）然后点击 Show，我看到了这些设置的修改版本：

```
*1024x768* 85.00 1024 1032 1152 1360 768 784 787 823
```

顺便说一下，这样做（因为在我折腾之前我的屏幕看起来还好）让它变窄了。我剪掉了第一行，并将其添加到 `/etc/X11/XF86Config` 文件的原始行下方，并注释掉了原始行（永远留有备份！）。我的系统运行正常，我不想丢失设置。此点的意义在于，并不是每一个窗口配置看起来都是完美的，并不是每个屏幕都能让你通过那些小按钮来修改设置。此外，即使在物理屏幕上，通过按钮调整屏幕可能意味着你的 X 显示看起来很棒，但你的文本却是错乱的。

## “乱套”的 X 会话

偶尔，你的 X 显示会发生一些奇怪的事情。事情看起来就是不对劲。如果你像我一样倾向于实验，情况尤为如此。在我撰写这个主题的过程中，我经常尝试不同的 X 和桌面。我还会下载并测试大量的 Beta 软件，以及比应得份额更多的 Alpha 软件。因此，显示偶尔会出问题。

你可以关闭 X 并重启会话，但那不是我们 Linux 世界喜欢的方式。相反，尝试使用 `xrefresh` 命令。

```
xrefresh
```

如果你不输入其他内容，`xrefresh` 会清空屏幕（这非常快）并在空白背景上重绘。为了获得有趣的效果，可以指定一个重绘的颜色。这是通过 `-solid` 标志实现的，如“solid color”所示。在这个例子中，我的 X 会话将从一个平坦的红色背景重绘：

```
xrefresh -solid red
```

## 屏幕截图

在结束本章之前，我为你们准备了一个特别节目。我将回答一个似乎每个人都在问的问题，你可能可能也在问自己。你是否好奇过如何获得精美的屏幕截图？我的意思是，我是如何获得本章中展示的 KDE、GNOME 和 Window Maker 桌面的那些漂亮截图的？实现这一现象是否涉及某种复杂的魔法？

事实是，获取屏幕截图有多种方法。桌面软件包有它们自己的小工具。例如，在 KDE 中，你可以点击大 K，选择 Graphics（图形）菜单，然后点击 Screen capture（屏幕截图）。看看图 9.10 了解它是如何工作的。

个人而言，我喜欢的方法是使用系统自带且安装妥当的小工具。它被称为 `import`，这里是它的工作原理示例：

```
import -border -frame -colorspace GRAY image_name.jpg
```

![](img/c0ecd438ac7835cfc0d30912433fa8b5_180_0.png)

**图 9.10** KDE 的屏幕截图工具

一旦按下回车键，光标会变成十字。点击你想捕捉窗口上的光标，它将保存到你决定的任何文件名。让这个工具非常灵活且非常易用的原因是，你可以通过指定适当的扩展名来定义图像类型。如果你喜欢 PNG 文件，将 `.jpg` 扩展名改为 `.png`。

如果你想捕捉整个桌面，尝试这个版本的命令：

```bash
import --window root my_screenpic_name.jpg
```

想要更有趣的吗？你可以捕捉另一个 X 显示器上的远程屏幕，只要已经授予了适当的 `xhost` 权限（如之前讨论）。

```
import --root -display remotehost:0 screen_cap.tif
```

那将捕捉名为“remotehost”机器的整个桌面，并将整体保存为名为 `screen_cap.tif` 的 TIF 文件。啊，太有趣了。

### 资源

- GNOME 窗口管理器：`http://www.gnome.org/`
- ICE 窗口管理器：`http://icewm.sourceforge.net`
- KDE 环境 (KDE) 首页：`http://www.kde.org/`
- Qvwm 首页：`http://www.qvwm.org/`
- Window Maker：`http://www.windowmaker.org/`
- X 窗口管理器：`http://www.plig.org/xwinman/`
- XFree86 项目官方网站：`http://www.xfree86.org/`

## 第 10 章 使用 PPP 接入互联网

PPP 可以作为包进行安装。在 Red Hat、Caldera 或任何使用 Red Hat 包管理器 (RPM) 的 Linux 发行版中，你可以使用：

```
rpm -ivh ppp.i86.rpm
```

如果你运行 Debian、Corel Linux 或 Storm Linux，命令类似：

```bash
dpkg -i ppp.deb
```

实际上，对于 Debian 用户，有一种更好的方法（称为 `apt-get`），但我将在下一章讨论。此外，这需要已经连接到网络，而这正是你正在做的。

## 从 ISP 获取的信息

下一步是从你的 ISP 获取一些信息：你的用户名（很可能是你的电子邮件地址）和密码，以及 DNS 或域名服务器地址。显然，你需要 ISP 的电话号码来拨入他们的网络。如果你有之前提到的那些漫游账户，确保获取你可能经常去的地区的本地接入列表。将该列表保存在你的 Palm Pilot、Handspring 或 PDA 上。

你还应该拥有电子邮件包的服务器信息。你需要获取的信息是 POP 和 SMTP 服务器地址。某些 ISP 使用代理进行浏览。询问这一点，如果你的 ISP 是这种情况，请随手记录。这与连接没有关系，但当你运行 Netscape Navigator 时会需要它。

## 信息所在的位置

如果你的 ISP 给了你 DNS 地址，请使用你喜欢的编辑器编辑 `/etc/resolv.conf` 文件并添加如下信息（`XXX` 被你的 ISP 提供的数字替换）：

```
nameserver XXX.XXX.XXX.XXX
```

### 基础知识

定义：POP 是邮局协议（Post Office Protocol）。像许多互联网协议一样，这个协议已经有所改进。你的 ISP（互联网服务供应商）可能正在使用（或提供）POP3，即第 3 版本。POP 是电子邮件客户端获取邮件的手段。

SMTP 是邮件问题的另一端。它的全称是简单邮件传输协议（Simple Mail Transfer Protocol），它是负责将消息从一个位置传输到另一个位置的程序。

NNTP 是新闻新闻协议（Network News Transfer Protocol）。这种通信标准允许在客户端和服务器之间传输 Usenet 消息。网景导航者浏览器（Netscape Navigator）拥有一个支持 NNTP 的阅读器。在你的 Linux 发行版中，你还会找到 `tin` 和 `trn`。在图形化世界，可以寻找 KDE 中的经典 X 程序 `xrn`，以及 GNOME 中的 `pan`。

最简单形式的 PPP 设置涉及一个聊天脚本（chat script）和一个配置适当的选项文件。这些文件可能位于 `/etc/ppp` 目录下。有更优雅的方法来设置 PPP，但操作原始文件将让你非常直观地理解它的工作原理：

第一个要编辑的是选项文件。我的看起来像这样：

```
/dev/modem

57600

modem

crtscts

lock

defaultroute

noidpdefault

connect "/usr/sbin/chat -vf /etc/ppp/chat-script"
```

我的调制调器位于 `/dev/ttyS0`，但为了方便，我也有一个指向 `/dev/modem` 的符号链接（如果不存在，使用命令 `ln -s /dev/tty0 /dev/modem` 来链接）。

其他项目意味着什么？`57600` 是我的波特率，`crtscts` 表示我的调制调器应该使用硬件流控。`lock` 意味着 `pppd` 创建一个锁文件，以确保在我尝试连接 ISP 时，其他用户不会尝试使用我的调制调器（记住，Linux 是多用户系统）。下一个参数 `defaultroute` 意味着连接建立后应建立指向 PPP 接口的默认路由。这意味着所有非本地流量都通过我的点对点接口。`connect` 之前的最后一个参数是 `nodefault`，意味着我没有为连接指定本地地址。`pppd` 进程将尝试通过从系统获取本地地址来自行解决这个问题。

`connect` 语句描述了你如何建立 PPP 连接。这就是你的聊天脚本。`chat` 是一个命令，其目的是与你的 ISP 建立连接。这个小程序与你的调制调器对话，并监控类似于 `CONNECT` 字符串或登录提示的内容。示例聊天脚本如下：

```
ABORT 'NO CARRIER'

ABORT 'NO DIALTONE'

ABORT 'ERROR'

ABORT 'NO ANSWER'

ABORT 'BUSY'

** ATZ

OK ATDT550000

CONNECT **

login: myISPLogin

password: myISPpassword
```
