
我们查看 `xorg.conf` 的可能内容，以便你了解 X 正在寻找什么。`xorg.conf` 文件的组件（或部分）指定了 X 会话或服务器布局，以及服务器使用的文件路径、任何与直接相关的选项、连接到系统的鼠标和键盘的任何可选支持模块、安装的显卡、使用的显示器以及 Ubuntu 使用的分辨率颜色。这些是核心组件：

- `ServerLayout`: 定义显示、一个或多个屏幕布局并命名输入设备。
- `Files`: 定义颜色、字体或字体服务器端口号的位置。

### 基础与 X Server

- `Module`（模块）——告诉 X 服务器需要加载哪些图形显示支持模块。
- `InputDevice`（输入设备）——定义输入设备，如键盘和鼠标；可以使用多个设备。
- `Monitor`（显示器）——定义任何连接显示器的能力；可以使用多个显示器。
- `Device`（设备）——定义一个或多个显卡，并指定启用或禁用哪些可选功能（如果有）。
- `Screen`（屏幕）——定义一个或多个分辨率、颜色深度、可能存在的默认深度以及其他设置。

接下来的章节提供了这些元素的简要描述；`xorg.conf` 页面包含了所有你可以用于自定义桌面设置的选项和关键字的完整文档。

## ServerLayout 节

如前所述，`xorg.conf` 文件中的 `ServerLayout` 节定义了显示和屏幕布局，并命名了输入设备。一个来自自动配置的 `xorg.conf` 文件的典型 `ServerLayout` 节可能如下所示：

```
Section "ServerLayout"
Identifier          single head configuration
Screen               "Screen0" 0 0
InputDevice          "Mouse0" "CorePointer"
InputDevice          "Keyboard0" "CoreKeyboard"
InputDevice          "DevInputMice" "AlwaysCore"
EndSection
```

在此示例中，使用了单个显示器（数字指定屏幕），并使用了两个输入设备 `Mouse0` 和 `Keyboard0` 用于会话。

## Files 节

`xorg.conf` 文件的 `Files` 节可能如下所示：

```
Section "Files"
RgbPath             "/usr/lib/X11/rgb"
FontPath             "unix:/7100"
EndSection
```

该节在文本文件 `rgb.txt` 中按名称列出了各种部分，以及指向 X 字体服务器的端口号。字体服务器在启动时启动，不需要活跃的 X 会话。如果不使用字体服务器，`FontPath` 条目可以列出根目录下的每个字体目录，使用 `"/usr/lib/X11/fonts/"` 目录，如示例所示：

```
FontPath             "/usr/lib/X11/fonts/100dpi"
FontPath             "/usr/lib/X11/fonts/misc"
FontPath             "/usr/lib/X11/fonts/75dpi"
```

`FontPath "/usr/lib/X11/fonts/type1"`

`FontPath "/usr/lib/X11/fonts/Speedo"`

...

这些目录包含了在 X 会话期间可用的默认压缩字体。字体服务器使用 `/etc/X11/fs` 目录下的名为 `config` 的文件进行配置。该文件包含了字体服务器的字体列表（或目录）。通过在该文件中添加 `alternate-server`（备用服务器）条目并重启字体服务器，你可以为 X 会话指定远程字体服务器。这有助于集中字体支持并减少本地存储需求（尽管对于 Ubuntu 和 X 安装的近 5,000 个字体需要 25MB 空间）。

## Module 节

`xorg.conf` 文件的 `Module` 节指定了为 X 会话要加载的可加载模块或驱动程序。该节可能如下所示：

```
Section "Module"
Load "dbe"
Load "extmod"
Load "fbdevhw"
Load "glx"
Load "record"
Load "freetype"
Load "type1"
Load "dri"
Section
```

这些模块范围从特殊的显卡支持模块到字体光栅化器。模块位于 `/usr/lib/modules` 目录下的子目录中。

## InputDevice 节

`InputDevice` 节如示例所示配置了特定设备，例如键盘或鼠标：

```
Section "InputDevice"
Identifier "Keyboard0"
Driver "kbd"
Option "XkbModel" "pc105"
Option "XkbLayout" "us"
Section
Section "InputDevice"
Identifier "Mouse0"
Driver "mouse"
Option "Protocol" "PS2"
Option "Device" "/dev/input/mice"
Option "ZAxis" "4"
Option "EmulateButtons" "yes"
Section
```

你可以配置多个设备，可能存在多个 `InputDevice` 节。指定 USB 设备的 `InputDevice` 节可能如下：

```
Section "InputDevice"
Identifier "Mouse0"
Driver "mouse"
Option "Protocol" "PS2"
Option "Device" "/dev/input/mice"
Option "ZAxis" "5"
Option "EmulateButtons" "off"
Section
```

## Monitor 节

`Monitor` 节配置 `ServerLayout` 节中指定的显示设备，示例所示：

```
Section "Monitor"
  Identifier "Monitor0"
  VendorName "Monitor Vendor"
  ModelName "Monitor Model"
  DisplaySize 300
  HorizSync 31-48
  VertRefresh 50-70
  Option "dpms"
Section
```

注意，X 服务器根据此节中的水平和垂直同步值自动确定最佳时序。如果需要，可能在使用 XFree8 4.0 之前的旧式 modeline。如果在配置 X 时自动检测显示器，其定义将插入你的 `xorg.conf` 文件。该数据库包含 600 多个显示器，位于 `/usr/share/hwdata` 目录。

## Device 节

`Device` 节提供了计算机使用的图形芯片的详细信息，示例所示：

```
Section "Device"
  Identifier "Intel Corporation Mobile 945GM/GMS,943G Express Integrated Graphics Controller"
  Driver "intel"
  BusID "PCI:0:2:0"
Section
```

此示例识别安装的显卡为集成 Intel 945 芯片组。`Driver` 进入 Xorg 服务器加载 `intel` 内核模块。不同的芯片组有不同的选项。例如，这里是 NeoMagic 视频芯片：

```
Section "Device"
Identifier "NeoMagic (laptop/notebook)"
Driver "neomagic"
VendorName "NeoMagic (laptop/notebook)"
BoardName "NeoMagic (laptop/notebook)"
Option "externDisp"
Option "internDisp"
Section
```

在此示例中，`Device` 节指定了显卡的驱动程序 (`neomagic_drv.`) 并启用了两个芯片组选项 (`externDisp` 和 `internDisp`)，以便笔记本屏幕和连接的显示器上显示。

Xorg 服务器支持数百种不同的视频芯片。如果你更改了安装的 X，你需要编辑 `Device` 节或使用本章讨论的 X 配置工具之一生成新的 `xorg.conf` 文件，以反映新卡的能力。

## Screen 节

`Screen` 节将之前节整合在一起。它还可以指定一个或多个分辨率。示例所示：

```
Section "Screen"
Identifier "Screen0"
Device "Video0"
Monitor "Monitor0"
DefaultDepth 24
Sub "Display"
Viewport 0 0
Depth 16
Modes "1024x768" "800x600" "640x480"
EndSection
```

# 参考文献

- `www.x.org`—X Window 系统维护者
- `www.x.org/Downloads_mirror.html`—下载 X 最新版本源码的镜像站点列表
- `www.xfree86.org`—XFree86 项目 Inc. 的主页，该项目在近 10 年中为 Linux 提供了图形化界面
- `https://wiki.ubuntu.com/X`—学习 X 和 Ubuntu 的入门之处
- `https://wiki.ubuntu.com/X/Config`—关于在 Ubuntu 上配置 X 的绝佳信息

# 第 4 章

## 本章内容

# Ubuntu 桌面选项

- 桌面环境
- 使用 GNOME：入门指南
- KDE 与 Ubuntu
- Xfce 与 Ubuntu
- LXDE 与 Ubuntu
- MATE 与 Ubuntu MATE
- Ubuntu Budgie
- Ubuntu Kylin
- 参考文献

当你安装 Ubuntu 时，默认情况下你使用的是 GNOME 图形用户界面（GUI）。这通常被称为桌面。GNOME 具有吸引许多用户的特定优势。然而，我们中的一些人有独特的需求，或者只是喜欢折腾。本章将讨论 GNOME 的替代方案，并简要提到它们的一些优缺点以及关于如何安装每种方案的信息。这并不是可用选项的完整列表，而是对最流行选项的简要调查。

# GNOME 并非唯一选项

当你安装标准桌面版 Ubuntu 时，你也安装了 GNOME。这不仅不是你的唯一选项，而且你并不限于一次只能安装一个桌面环境。我们在本章中讨论的每个选项都可以在标准版 Ubuntu 中与 GNOME 并行安装，并且你可以在每次登录时选择使用哪一个，以及选择哪一个作为默认选项。这使得测试新选项的风险降低，因为切换回你已经熟悉的界面非常简单。

# 桌面环境

传统上，计算机的 GUI 具有“桌面比喻”；具体来说，界面使用物理办公桌的概念作为比喻，使与计算机的交互变得容易理解。就像现实世界中的办公室一样，计算机桌面环境使用文件来存储完成办公任务所需的信息。计算机系统通过添加应用程序进一步延伸了这种比喻，这些程序允许用户根据需要创建、操作和删除这些文档，就像在现实世界中可能执行的那样，但效率更高、功能更强。

计算机桌面包含一个窗口系统，这是另一个比喻，用于处理信息，使得对数字领域后台发生的复杂性进行概念化变得更容易。图形显示中的文件、文件夹（或目录）和应用程序可以在用户的桌面上移动，就像纸质文档和文件为了方便和效率而可以被移动到物理桌面的不同位置一样。使用这个窗口系统包括为了在显示这些操作的同时，在屏幕上绘制窗口所需的图形组件（称为小部件/`widgets`），以及在后台执行操作所需的所有程序代码，同时在显示这些操作时通过物理桌面这种精美的比喻来呈现这些操作。例如，在桌面上将文档从一个文件夹移动到另一个文件夹不仅仅是鼠标点击加拖放那么简单。在后台，桌面环境正在监听窗口管理器的指令，将文件从一个目录移动到另一个目录，然后在任务完成后告诉窗口管理器在屏幕上绘制该事件。

软件存储库包含了 Linux 可用的所有流行桌面环境，安装和尝试它们轻而易举。富有冒险精神的人找到其他在 Ubuntu 上运行的桌面环境并下载它们。我们在这里不涵盖这一过程。

也可以在使用一个桌面环境的同时，使用不同的窗口管理器来替换它，而不是使用该桌面环境自带的那个。例如，标准的 GNOME 窗口管理器被称为 `Mutter`。它稳定且运行良好。其他界面可能使用不同的窗口管理器，例如 `Compiz`。为了增加趣味性，你可以将其中任何一个替换为其他窗口管理器，例如 `Enlightenment`，它以独特的方式运行，例如当你右键点击屏幕时，菜单会在屏幕上弹出，而不是锚定在特定位置。

本章侧重于完整的桌面环境，使用每个环境的默认窗口管理器。此外，由于这是一本专注于 Ubuntu 的书，本章集中于经过 Ubuntu 优化过的环境版本（如 KDE 和 Xfce），而不是它们的默认版本，尽管默认版本在 Ubuntu 存储库中也可用，以防你想自行寻找它们。

# 使用 GNOME：入门指南

Ubuntu 的默认桌面是 GNOME 3。它不仅被 Ubuntu 使用，还被其他几个 Linux 发行版使用，例如 Debian、Fedora、Red Hat Enterprise Linux 和 Oracle Linux。

GNOME 3 的官方 GUI 称为 GNOME Shell。在本章中，与 Ubuntu 18.04 安装相比，唯一更改的是背景；这里使用的背景是纯简单的，以确保屏幕截图清晰。

登录后，将显示桌面（见图 4.1）。

![](img/5cab8f9f4d9f23fd52004a70bd1c9014_81_0.png)

图 4.1 GNOME Shell 桌面。

通过桌面，你可以执行以下操作：

- 点击左上角的“活动”（Activities）搜索计算机中安装的程序。
- 从“Dash”（Dash，有时也称为收藏菜单）中选择程序，它是左侧的垂直栏，紧接“活动”链接下方（见图 4.2）。若要在 Dash 中添加或删除项目，可以在悬停在图标上时右键点击并从弹出菜单选择“添加”或“移除”。
- 点击左下角的“显示应用程序”图标（看起来像一个点阵）显示已安装的程序（见图 4.3）。
- 点击右上角的电源图标显示音量、账户设置等更多内容（见图 4.4）。
- 在桌面的顶部中央你可以看到日历。来自 Ubuntu 的通知也显示在这里。

![](img/5cab8f9f4d9f23fd52004a70bd1c9014_82_0.png)

图 4.2 GNOME Shell 桌面，顶部有“活动”链接。

![](img/5cab8f9f4d9f23fd52004a70bd1c9014_82_1.png)

图 4.3 点击“显示应用程序”图标显示已安装的程序。

![](img/5cab8f9f4d9f23fd52004a70bd1c9014_83_0.png)

图 4.4 从菜单调整音量、账户设置等内容。

# KDE 与 Ubuntu

KDE 项目始于 1996 年，目标是为 Linux 创建一个免费、运行良好且集成良好的桌面环境，这意味着程序和界面将保持一致，而不是杂杂部分的组合。

KDE 项目一直关注终端用户，而不是为系统管理员创建 GUI。从从开始这一点很重要，意图是让任何计算机用户感到舒适并能够做他们想做的，而不需要完全理解后台发生的情况。这种情况持续至今，并被其他桌面环境共享，特别是 GNOME，后者是 1997 年由参与 KDE 项目的人员在对软件许可产生争议后离开而创立的。

该争议的原因已不再存在，因为现在的许可证同样免费，但这两个项目在关注点上产生了分歧：GNOME 提供了一个具有禅意简约感的桌面以及优雅的默认设置和用法，而 KDE 则提供了更多的视觉效果和配置选项。它们都是非常优秀的桌面环境，集成良好且具有高度的专业性，是 Linux 世界中最重要的两个。如果你从未用过任何，请尝试两者。

Kubuntu 是 Ubuntu 社区早期启动的项目，目标是让用户能够在 Ubuntu 中安装和使用 KDE。为了让那些已经知道自己喜欢 KDE 而非 GNOME 的人更容易，你可以下载并安装 Kubuntu ，它是去掉 GNOME 并增加 Kubuntu 特定增强的 Ubuntu。你也可以通过从 Ubuntu 存储库安装 `kubuntu-desktop` 包，在标准版 Ubuntu 中并行安装 Kubuntu。

Kubuntu（见图 4.5）对大多数任务使用不同的默认设置：浏览器、电子邮件等。大部分都是专门为 KDE 桌面环境编写的，使得 KDE 成为可用集成度最高、一致性最好的 Linux 桌面之一。

![](img/5cab8f9f4d9f23fd52004a70bd1c9014_84_0.png)

图 4.5 Kubuntu 桌面。

## Xfce 与 Ubuntu

Xfce 是一个更轻量的桌面环境，比 GNOME 或 KDE 需要的内存和处理能力更少，因此通常被建议在旧旧设备上使用。它不应该被局限于这一角色，因为它在当前的硬件上运行得也非常良好，并且往往出于其他原因成为一个高质量的选择。Xfce 的开发遵循传统的 UNIX 软件哲学：只做一件事，并把它做好，然后与其他程序协作。

Xfce 桌面环境的部分是模块化的；你可以随心所欲地添加或删除组件，并替换执行相同程序的。Xfce 中创建或包含的所有内容预计将按照简单的标准运行，允许其他程序轻松地与之交互。

一方面，这有时意味着人们在看 Xfce 时会认为它不像两个主流桌面环境那样无缝集成和顺滑。另一方面，这意味着如果你更倾向于使用 GNOME 文件管理器（Nautilus）而不是 Xfce 自带的（Thunar），那么你可以安装 Nautilus 并与 Thunar 并行使用，或者完全删除 Thunar。这是 Xfce 保持轻量化的重要部分——它的依赖要求非常少且具有高度的灵活性。
