
# 第 4 章 安装后配置

```
Hit http://gb.archive.ubuntu.com dapper/main Sources
Get 18 http://gb.archive.ubuntu.com dapper/restricted Sources [1478b]
Hit http://gb.archive.ubuntu.com dapper/universe Sources
Hit http://gb.archive.ubuntu.com dapper/multiverse Sources
Get 19 http://gb.archive.ubuntu.com dapper-updates/main Packages [37.7kb]
Get 20 http://gb.archive.ubuntu.com dapper-updates/restricted Packages [14B]
Get 21 http://gb.archive.ubuntu.com dapper-updates/main Packages [37.kb]
Get 22 http://security.ubuntu.com dapper-universe Sources
Get 23 http://security.ubuntu.com dapper-restricted Packages
Get 24 http://security.ubuntu.com dapper-multiverse Sources
Get 25 http://security.ubuntu.com dapper-main Sources
Get 26 http://security.ubuntu.com dapper-restricted Sources
Get 27 http://security.ubuntu.com dapper-universe Sources
Get 28 http://gb.archive.ubuntu.com dapper-backports Sources
Get 29 http://gb.archive.ubuntu.com dapper/main Sources
Get 30 http://gb.archive.ubuntu.com dapper/restricted Sources
Get 31 http://gb.archive.ubuntu.com dapper/universe Sources
Get 32 http://gb.archive.ubuntu.com dapper/multiverse Sources
Get 33 http://gb.archive.ubuntu.com dapper/universe Sources
Fetched 299KB in 2s (140kB/s)
Reading package lists... Done
```

现在你需要执行以下命令来升级软件：

```
$ apt upgrade
```

## 配置软件源

Ubuntu 使用软件源来获取可安装软件的信息。默认情况下，它允许访问一部分软件（尽管这是官方支持的）。然而，Ubuntu 基于一个老得多的 Linux 发行版，名为 Debian。Debian 拥有超过 17,000 个不同的软件包，这意味着 Ubuntu 也可以访问它们。

要启用这些功能，你需要使用 Ubuntu 的另一个 GUI 封装器，名为 synaptic。你可以在“系统”->“管理”->“软件包管理器”中找到它。在提示输入密码并在 synaptic 出现后，你可以通过“设置”->“软件”菜单访问源信息。这里显示了几个选项，通常默认设置即可。然而，书中描述许多软件需要启用额外的源才能访问。

只需点击第一个选项 Ubuntu 6.06 LTS (Binary)，点击右侧的“编辑”按钮即可看到图 4.2 所示界面。在这里你可以勾选 Multiverse 源，以便下载来自更广泛的 Debian universe 以及某些非自由驱动程序和解码器。

每个二进制条目都有对应的源项，Ubuntu 有时使用它们来检索源代码信息。确保更新相应的源项，但注意这与二进制源的操作略有不同。不要担心，你只需要输入 `universe` 和 `multiverse` 这两个单词，中间用空格隔开，如图 4.3 所示。

对 Updates（更新）、Back Ports（回拨）和 Security Updates（安全更新）重复此过程，以便让你访问所有相关软件。完成这些后，点击“关闭”按钮返回 synaptic。此时，Ubuntu 检测到你更改了源信息，并建议你刷新更新。点击工具栏上的“刷新”按钮刷新可用更新。关闭 synaptic 完成操作并返回桌面。

图 4.3 在更新二进制仓库时，请务必确保配对的源仓库包含相同的信息。

## 安装显卡驱动

Ubuntu 在检测和配置显卡方面表现非常出色。然而，它在 3D 支持方面确实稍显吃力，主要是因为你必须安装专有驱动才能启用完全的 3D 支持。幸运的是，这项非常简单，我们将在命令行中完成。

按照之前的描述打开终端窗口，并使用以下命令：

```
$ sudo apt-get install drivername configtool
```

根据你的显卡更改 `drivername` 和 `configtool`。对于 Nvidia 显卡，你需要分别将它们更改为 `nvidia-glx` 和 `nvidia-settings`；对于 ATI 显卡，请使用 `xorg-driver-fglrx` 和 `fglrx-control`。APT 会智能地检测任何其他所需的包并根据需要进行安装。

APT 完成后，你必须对 `xorg.conf` 文件进行一些微调，该文件是 X 用来配置自身的文件。使用以下命令用文本编辑器（Text Editor，一个易于使用的 GUI 编辑器）打开该文件，并寻找 Devices（设备）部分：

```
$ sudo gedit /etc/X11/xorg.conf
```

具体来说，你正在寻找 `driver` 那一行，因为你需要对它进行细微修改，ATI 和 Nvidia 显卡的操作不同。对于 ATI 显卡，你需要确保它看起来像这样：

```
Driver "fglrx"
```

对于 Nvidia，它应该像这样：

```
Driver "nvidia"
```

这些条目告诉 X 使用你安装的 ATI 或 Nvidia 驱动。剩下的就是重启电脑以让 Ubuntu 加载新驱动。重新登录 Ubuntu 并打开终端窗口。对于 Nvidia 显卡，输入 `glxgears` 或对于 ATI 显卡输入 `fglglxgears`（图 4.4），弹出一个包含旋转彩色齿轮的小窗口。看到这个就说明你的驱动已安装正确，且 3D 加速已启用。

![](img/757e95bd85c59465935194247625328c_103_0.png)

图 4.4 谁能想到像旋转齿轮这么简单的事情能带来如此巨大的快乐？看到这个说明你的显卡已准备好进行 3D 操作了。

现在你已经配置好了 3D 加速，请前往第 13 章“游戏”，查看 Linux 如何处理像 Doom 3 和 Quake 4 这样的游戏，这两者都需要 3D 加速。

## 更改 Ubuntu 的外观和感受

GNOME 是 Ubuntu 的默认窗口管理器，有许多选项可以更改它的外观和感受。默认主题是 Ubuntooks；它结合了 GNOME Clearlooks 主题，混合了来自 Tango 项目的图标，并添加了直接来自 Ubuntu 的点缀。然而，它并不符合所有人的口味，因此在本节中，我们将如何更改 Ubuntu 的视觉风格。

### 更改桌面背景

你可以做的最简单且最显著的改变可能是更改默认桌面背景。这只需在桌面上点击右键并选择“更改桌面背景”选项，即可看到图 4.5 所示的对话框。Ubuntu 自带了少量壁纸供初始选择，但我们建议去网上寻找丰富的选择。我们最喜欢的网站是 http://www.gnome-look.org，你可以在那里找到大量精美的桌面壁纸。

![](img/757e95bd85c59465935194247625328c_104_0.png)

图 4.5 选择一种默认壁纸，或使用“添加壁纸”选项使用你自己的图像文件。

当你点击一张壁纸时，Ubuntu 会自动应用，以便你快速查看是否喜欢。当你对选择满意时，只需点击“完成”关闭对话框。

### 更改颜色

接下来是 Ubuntu 的默认颜色。当 Ubuntu 在 2004 年 10 月最初发布时，它采用以棕色为主的主题，导致一些用户对 Ubuntu 开发团队风格选择产生质疑。从 Ubuntu 6.06 开始，棕色被温暖的焦糖色取代（老实说，这只比棕色好一点）。

幸运的是，GNOME 提供了一系列工具来修改默认设置。只需前往“系统（System）、偏好（Preferences）、主题（Theme）”选项即可快速更改整个主题（见图 4.6）。如前所述，Ubuntu 默认使用 Ubuntooks，但你可以从其他选项中选择。就像桌面背景小组件一样，选中的主题会自动应用，而且快速找到适合自己的选项并不困难。
