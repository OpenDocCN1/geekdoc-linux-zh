
## 01 选择一个发行版

市面上有大量易于使用的 Linux 发行版，可以帮助你立即开始使用可用的 LxQt 桌面环境——选择权在于你。

Lubuntu 是 Ubuntu 的专用 LxQt 版本，包含一个“daily”PPA，其中包含最新的代码（ppa:ubuntu-dev/lubuntu-daily）。该 PPA 兼容大多数 Ubuntu 14.04 和 14.10 衍生版，包括 Kubuntu、LXLE、Mint 以及许多其他版本。要获取 LxQt，你需要安装 `lqt-metapackage`、`lqt-session` 和 `lxsession` 软件包。

安装 LxQt 的另一种方式可能是 Arch/Manjaro（LxQt 在 AUR 中）或 OpenManjaro 的开发版本，后者默认附带 LxQt（Plasma 5 将在稍后推出）。

## 02 我们目前拥有什么

桌面占用 95 MB 的内存。它具备控制中心、电源管理小工具、可定制的底部面板、外观和感觉设置管理器、窗口管理器 Chameleon、QTManager 控制台以及 PCManFM 文件管理器。键盘布局指示器和 NetworkManager 小工具目前缺失，但你可以分别使用 XFCE 的小工具和精美的 CMST（ConnMan 的前端）。

## 03 PCManFM 中的缩略图

我们可以调整并添加 PCManFM 文件管理器的额外功能。首先，让我们为除图像外的文件类型添加缩略图支持。例如，对于 PDF，在 /usr/share/thumbnailers 创建一个带有缩略图扩展名的新文件，内容如下：

```ini
[Thumbnailer Entry]
TryExec=convert
Exec=convert %i[0] -thumbnail %s %o
MimeTypes=application/pdf;application/x-pdf;image/pdf;
```

使用此模板，你可以添加更多 “convert” 支持的类型（它是 ImageMagick 的一部分）。

默认情况下，窗口装饰由 OpenBox 管理，但你可以将其更改为 Kwin 或 Emeralla。PCManFM 比较简洁，但请记住，它是目前唯一的 Qt5 文件管理器。

## 04 获取 Otter 浏览器

Otter 网页浏览器每周更新，因此如果你对它的进展感兴趣，可以在项目网站上跟踪其开发。对于兼容 Ubuntu 的 Linux 系统，有一个非常方便的 PPA。那么，废话不多说，我们直接进入主题：

```bash
sudo add-apt-repository ppa:otter-browser/daily
sudo apt-get update
sudo apt-get install otter-browser-git
```

Otter 浏览器具有各种出色的功能，例如标签分组、鼠标手势和高度可定制的 UI。如果需要，你可以选择在系统设置中的 Web 浏览器菜单中选择 `otter-browser` 将其设置为默认网络应用程序。

# 技巧 | 窍门 | 技巧 | 应用

## 轻盈生活

Qt5 已经存在多年，越来越多的 Qt 应用程序正在转向使用它。目前，我们可以围绕 LxQt 构建一个相当好用且易用的桌面环境。网络连接可以通过 ConnMan 及其 CMST 前端进行管理，Dropbox 客户端使用 Qt5 很方便，LxQt 系统设置的工作效果与同名的 KDE 模块一样好。还可以访问网页浏览器、电子邮件客户端和多功能媒体播放器。

它与 KDE 桌面相比如何？没有简单的答案。首先，手工制作的 LxQt 桌面功能比 KDE 2 或新的 Plasma 5 桌面都少，但它轻量得多。纯 LxQt 所需的内存少于 100 兆字节，每个额外的 Qt5 应用程序增加的资源非常少。其次，目前的 Plasma 5 选择（如 Kubuntu 或 Netrunner）被迫混合 Qt4 和 Qt5 部分，因此生成的桌面环境不均匀且消耗更多资源。

最后，你必须记住 Plasma 5 尚未完全成熟。尽管其当前状态肯定比 2008-2009 年早期的 KDE 4 版本好得多，但一些核心应用程序仍保留在 Qt4 世界中。不幸的是，从 KDE 4 到 Plasma 5 桌面的过渡期是不可避免的。但是，如果你坚持下去，你的耐心将得到回报！

## 05 获取 Drawpile

最新的 Drawpile 版本（0.9.8）可以通过 Getdeb 服务在此安装：www.getdeb.net/app/DrawPile。

该程序有多种用途。首先，它是一个易于理解的绘图软件，与 MS Paint、Kolourpaint 和 Pinta 相当——简单、美观，适合儿童。其次，其用户界面针对 Web 项目进行了优化（具有画笔、调色板、透明度处理）。最后，它可以在矩形区域容纳聊天窗口。Drawpile 允许多人同时在一个画布上绘画。

## 06 使用 PhotoQt 查看图像

PhotoQt 通过 PPA 提供，输入类似以下内容：

```bash
sudo add-apt-repository ppa:samoij13/ppa
sudo apt-get update
sudo apt-get install photoqt
```

然后可以在 PCManFM 的“打开方式...”菜单中选择该程序。PhotoQt 默认以全屏模式打开图像，左上角显示图像文件名及其序号。通过图像任意部分的右键菜单可提供其他操作。你可以使用相应的键盘箭头浏览图像。

## 07 使用 Albert 启动应用并搜索

同样，有一个 PPA 方便安装：

```bash
sudo add-apt-repository ppa:nilarimogard/webupd8
sudo apt-get update
sudo apt-get install albert
```

第一次启动 Albert 时，你会看到其配置窗口，你可以在其中更改某些设置，更重要的是，为调用 Albert 分配一个快捷键。关闭窗口后，Albert 不会退出，只是隐藏在后台。按下你的快捷键，你就会看到搜索栏。根据你的输入，Albert 会提供应用程序、Chromium 书签或可以应用你字符串的搜索引擎。

## 08 管理你的邮箱

Trojitá 二进制文件由 OIBS 系统友好提供，但只有 Qt4 版本。虽然其他 Linux 发行版存在 Qt5 版本，但在 Ubuntu 的情况下，我们需要从源码编译 Qt5 Trojitá。幸运的是，官方网站提供了非常直接的构建说明（http://trojita.flaska.net/download.html）。

启动程序并提供你的 IMAP 邮箱详细信息。公共服务，如 Gmail 运行正常。Trojitá 具有传统布局，具备邮件排序、HTML 支持和高效网络使用功能。

## 09 使用 SMPlayer 享受音乐和视频

SMPlayer 是一款一流的媒体播放器，几乎可以播放任何本地和远程媒体，甚至包括一些蓝光光盘。Ubuntu 家族有一个 PPA（ppa:vmw/SMPlayer），但它提供的是带 Qt4 的 SMPlayer，而我们需要 Qt5 版本。因此执行以下命令：

```bash
sudo apt-get build-dep smplayer
```

然后下载源代码包（bit.ly/1B18gPT）并使用其中的 Install.txt 文件中的说明。Qt5 开关通过以下方式应用于 make 命令：

```bash
make QMAKE=/usr/lib/x86_64-linux-gnu/qt5/bin/qmake
```

当然，你应预先安装 `qt5-qmake` 和其他 Qt5 开发包。

## 10 使用 FocusWriter 编写文本

FocusWriter 是一个简单的类打字机编辑器，它隐藏了几乎所有的控件，以免分散你写作的注意力。然而，它有很多有用的功能，如自动保存、实时统计、拼写检查、多文档支持等等。你可以使用官方 PPA 安装它：

```bash
sudo add-apt-repository ppa:gatecode/gcppa
sudo apt-get update
sudo apt-get install focuswriter
```

## 11 使用 Cool Retro Term 增添趣味

LxQt 已经拥有一个伟大的 QTerminal 应用程序，支持标签、颜色配置文件等，但我们还可以更进一步，安装由 Qt5 和 OpenGL 驱动的旧式终端，称为 Cool Retro Term。以下应用程序模仿 Amiga、IBM 和 Apple 工作站的历史阴极射线管美学：

```bash
sudo add-apt-repository ppa:bugs-launchpad-net-falkensweb/cool-retro-term
sudo apt-get update
sudo apt-get install cool-retro-term
```

一旦启动，你可以在配置文件之间切换或手动更改效果。甚至可以放大整个屏幕，使 Cool Retro Term 像常规控制台应用程序一样可用，这很方便。

## 添加更多应用

如果你坚持使用自定义 LxQt 桌面、扫描仪或笔记本电脑，你不会无穷无尽地想要更多。本教程中介绍的应用程序并不是所有存在的 Qt5 应用程序，你可以使用以下内容增强系统：

- **Voxel** 一个基于 Qt Quick 和 LiquidFun 库构建的有趣 2D 平台游戏。在 Linux 上编译该游戏需要技巧，但有一个完美的指南：bit.ly/1HLMB0P
- **Friends** 此应用具有精美的 QML 界面，易于安装（`sudo apt-get install friends-app`），要使用它，你必须参考 Unity 的在线账户部分，因此你必须安装 K36 或至少其 gpa-daemon（存储在 `~/.config/gpa-1.0/`）
- **Rosa ImageWriter** 这是著名的 SUSE Studio 映像写入器的 Qt5 移植版。该应用已改进，便于舒适的 USB 介质写入。请参阅 bit.ly/ZgrrQL 了解依赖于 KDE 软件交付且在某些桌面环境之外难以使用的应用程序。
- **Qt-apps.org** qt-apps.org 网站是一个重要的书签！这是一个跟踪 Qt5 应用程序的点。大多数新标题和更新标题都会出现在那里。

