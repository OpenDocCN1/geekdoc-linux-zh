
Otter Browser 具有各种令人喜爱的功能，如标签分组、鼠标手势和高度可定制的 UI。你可以通过在系统设置的网络浏览器菜单中选择 `otter-browser` 来将该浏览器设置为默认网络应用程序。

# 教程 Qt5 桌面环境

## 轻量级常驻

Qt5 已经存在多年，越来越多的 Qt 应用程序正转向使用它。目前，我们可以围绕 `LxQt` 构建一个合理且高度可用的桌面环境。网络连接可以通过 `ConnMan` 及其 `CMST` 前端进行管理。`Dropbox` 客户端已经使用 Qt5，而 `LxQt` 系统设置功能的表现与同名 KDE 模块一样出色。此外，还可以使用一个网络浏览器、电子邮件客户端和多功能媒体播放器。

它与 KDE 桌面环境相比如何？没有简单的答案。首先，手工打造的 `LxQt` 桌面环境功能比 KDE4 或新的 Plasma 5 桌面环境都少，但它的资源占用要轻得多。纯 `LxQt` 需要不到 100 MB 的内存，每个额外的 Qt5 应用程序增加的占用极少。其次，当前的 Plasma 5 选择（如 Kubuntu 或 Netrunner）被迫混合 Qix 和 Qt5 部分，导致生成的桌面环境不均匀且消耗更多资源。最后，Plasma 5 尚未成熟。尽管其当前状态比 2008–2009 年初期的 KDE4 发布版本更好，但一些核心应用程序仍然停留在 Qt4 世界中，因此从 KDE4 到 Plasma 5 桌面环境会有一个过渡期。

![](img/c9d26cf718256f071c3af699b9670538_55_0.png)

### Trojitá 拥有传统布局并支持邮件分类功能

## 05 获取 Drawpile

最新版本的 Drawpile (0.9.8) 可以通过 Getdeb 服务在此安装：`www.getdeb.net/app/DrawPile`。

该程序有几个用途。首先，它是一款易于理解的绘图软件，可与 MS Paint、KolourPaint 和 Pinta 相媲美——简单、美观，适合儿童。其次，其界面专为 Web 项目使用进行了优化（包括画笔、调色板、透明度处理）。最后，那个黑色矩形包含一个聊天窗口。Drawpile 允许多个人同时在一个画布上绘图。

## 06 使用 PhotoQt 查看图像

PhotoQT 通过 PPA 提供，输入类似以下内容：

```
sudo add-apt-repository ppa:sandrog31/ppa
sudo apt-get update
sudo apt-get install photoqt
```

然后可以在 `PCManFM` 的“打开方式...”菜单中选择该程序。PhotoQT 默认以全屏模式打开图像，并在左上角显示图像文件名及其编号。通过图像任意部分的右键菜单可以获得额外操作。你可以使用相应的键盘箭头浏览图像。

## 07 使用 Albert 启动应用和搜索

同样，有一个 PPA 便于安装：

```
sudo add-apt-repository ppa:milarimingard/albert
sudo apt-get update
sudo apt-get install albert
```

第一次启动 Albert 时，你会看到其配置窗口，你可以在其中更改某些设置，更重要的是，为调用 Albert 分配一个快捷键。关闭窗口后，Albert 不会退出，而是隐藏在后台。按下你的快捷键，你就会看到搜索框。根据你的输入，Albert 将提供应用程序、Chromium 书签或你可以应用字符串的搜索引擎。

## 08 管理你的邮箱

Trojitá 的二进制文件由 OBS 系统提供（`bit.ly/L9KV3LU`），但仅有 Qt4 版本。虽然其他 Linux 发行版存在 Qt5 版本，但在 Ubuntu 的情况下，我们需要从源代码编译 Qt5 版的 Trojitá。幸运的是，官方网站提供了非常直接的构建说明（`http://trojita.fasko.net/download.html`）。

启动程序并提供你的 IMAP 邮箱详情。公共服务（如 Gmail）运行正常。Trojitá 拥有传统布局，并支持邮件分类、HTML 支持以及高效的网络使用。

![](img/c9d26cf718256f071c3af699b9670538_56_0.png)

## 09 使用 SPlayer 享受音乐和视频

SPlayer 是一款顶尖的媒体怪物，它可以播放几乎所有媒体（本地和远程），甚至包括一些蓝光光盘。Ubuntu 系列有一个 PPA（`ppa:arvm/SPlayer`），但它提供的是 Qt4 版本的 SPlayer，而我们需要 Qt5 版本。因此执行以下命令：

```
sudo apt-get build-dep splayer
```

然后下载源代码压缩包（`bit.ly/1Bl8gPT`）并使用其中的 `Install.txt` 文件中的说明。Qt5 开关通过以下方式应用到 `make` 命令中：

```
make QMAKE=/usr/lib/x86_64-linux-gnu/qt5/bin/qmake
```

当然，你之前应该已经安装了 `qt5-qmake` 和其他 Qt5 开发软件包。

![](img/c9d26cf718256f071c3af699b9670538_56_1.png)

## 10 使用 FocusWriter 编写文本

FocusWriter 是一个简单的类似打字机的编辑器，它隐藏了几乎所有的控制，以免分散你写作的注意力。但它还有许多有用的功能，如自动保存、实时统计、拼写检查、多文档支持等。你可以使用官方 PPA 安装它：

```
sudo add-apt-repository ppa:gotcodcc/gcppa
sudo apt-get update
sudo apt-get install focuswriter
```

## 11 用 Cool Retro Term 增加趣味

LxQt 已经拥有一个支持标签、颜色配置文件等功能很棒的 OFterminal 应用程序，但我们可以更进一步，安装由 Qt5 和 OpenGL 驱动的旧式终端 Cool Retro Term。以下应用程序模仿了 Amiga、IBM 和 Apple 工作站的历史性阴极射线管：

```
sudo add-apt-repository ppa:bugs-launchpad-net-falkensweb/cool-retro-term
sudo apt-get update
sudo apt-get install cool-retro-term
```

一旦启动，你可以在配置文件之间切换或手动更改效果。甚至可以放大整个屏幕，使 Cool Retro Term 像普通控制台应用程序一样易用，这非常方便。

## 添加更多应用

如果你坚持使用自定义的 LxQt 桌面环境，迟早你会想要更多。本教程中的应用程序并不是市面上所有的 Qt5 应用程序，因此请用以下内容为你的系统充电：

- `Votair` 基于 Qt Quick 和 LiquidUI 库构建的 2D 平台游戏。在 Linux 上编译该游戏需要技能，但有一个完美的指南：`bit.ly/1HIHMB9P`。

- `Friends` 该应用具有下一代 OML 界面，安装简单（`sudo apt-get install friends-app`）。要使用它，你必须参考 Unity 的在线账户部分，因此你需要该桌面环境或其 `go-daemon`（存储在 `~/.config/goa-1.0/` 中）。

- `Rosa ImageWriter` 这是著名的 SUSE Studio ImagerWriter 的 Qt5 移植版。该应用为舒适的 USB 介质写入进行了改进。请参阅 `bit.ly/1ZgurWL` 了解依赖于 KDE 软件交付且在特定桌面环境外难以使用的应用程序。

- `Qt-apps.ORG` 如果你想跟踪 Qt5 应用程序，`qt-apps.org` 网站是一个重要的书签。大多数新的和更新的应用程序都会出现在那里。

# 教程 AWS 云

AWS 管理控制台中的 AWS 徽标展示了基础设施服务

如果你想在自己的云环境中运行自己的 Linux 机器，不用再找了，看 `EC2` 就够了

使用 `Route 53` 保留域名名称并将 DNS 路由到你的云 Linux 服务器

通过带有用户名的菜单访问你的成本管理服务和账单信息

![](img/c9d26cf718256f071c3af699b9670538_57_0.png)

## 在 AWS 云中运行 Linux

### 顾问

`Filipe Martins` 和 `Anna Kobylinski` 二十年前曾在一本看似无辜的 Linux 书上合作，最终进入了企业 IT 领域，设计云拓扑，优化 Linux AMI 并管理 AWS 部署。通过 `@RealProfReal`、`@Cloudinsidr` 和 `@4digitalmasters` 在 Twitter 上参与他们的对话

## 在 EC2 上启动你自己的虚拟 Linux 实例并免费运行一年
