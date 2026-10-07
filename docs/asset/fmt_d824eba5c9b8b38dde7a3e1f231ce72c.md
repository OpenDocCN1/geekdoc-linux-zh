
> 注意
要挂载文件系统，必须使用 UUID 设备文件指定要挂载的文件系统。

如果你需要相同的挂载单元 `data.automount`，系统仅在用户首次访问 `/data` 目录时才会挂载文件系统。还可以使用 `systemd-mount` 命令和 `systemd-umount` 命令使用 systemd 手动挂载和卸载文件系统。例如，`systemd-mount -A /dev/sda5 /data` 命令将指示系统在用户首次访问 `/data` 目录时（`-A`）将 `/dev/sda5` 挂载到 `/data` 目录。

# X Windows 系统

本章目前专注于使用命令行界面执行任务。虽然大多数 Linux 管理员完全在 shell 界面执行任务，但其他 Linux 用户使用 GUI 运行图形程序。因此，你需要了解组成 Linux GUI 的组件。此外，你还需要如何启动、停止和配置它们。

# Linux GUI 组件

Linux GUI 设计无论系统安装了什么种显卡和显示器都能完全运行。它由许多组件组成，每个组件都与视频硬件独立工作。

Linux 安装包含了图 8-8 列出的所有 GUI 组件。这些 GUI 组件共同在典型的 Linux 安装中需要 4 GB 以上的空间。

# CompTIA Linux+ 与 LPIC-1：Linux 认证

图 8-8 Linux GUI 的组件

![](img/0065b92b6d2dfbf8ba2a41373880797d_359_0.png)

# X Windows

回想第 1 章，Linux GUI 的核心组件是 X Windows，它提供了在终端屏幕上显示的窗口中绘制图形图像的能力。告诉 X 如何绘制图形和显示的程序称为 X 客户端。X 客户端不需要与服务器运行在同一系统中。

X Windows 是由数字设备公司（DEC）和麻省理工学院（MIT）于 1984 年联合开发的。

## CompTIA Linux+ 和 LPIC-1：Linux 认证指南

## 注意 38

要了解更多关于 KDE 的信息，请访问 `kde.org`。

K 中的 Qt 工具包是由名为 Trolltech 的团队在 20 世纪 90 年代在挪威创建的。然而，在当时建立一个追者框架需要一段时间。此外，大多数开源开发者倾向于使用 C 语言进行开发，而不是 C++。此外，Qt 直到 1998 年才开源，这也是缺点，因为大多数开发者更倾向于可以自由修改的源代码。

由于对 Qt 工具包的普遍不满，GNOME 于 1997 年被创建，并从那以后成为大多数 Linux 发行版的默认桌面环境。GNOME 42 是本书时 GNOME 的最新版本；它使用了 Mutter 窗口管理器和 GTK+ C 语言。GTK+ 最初是为 GNU 图像处理程序（GIMP）开发的；与 GIMP 一样，它是开源的。GNOME 42 的图形界面共同设计用于提供不同的功能，包括面向移动端的 GNOME Shell。GNOME Shell 的替代方案包括 Unity。还有许多基于 GNOME 的现代桌面环境，包括源自 GNOME 3 的 Cinnamon 桌面环境和源自 GNOME 2 的 MATE 桌面环境。

## 注意 39

要了解更多关于 KDE 和 GNOME 信息，请访问 `gnome.org`。

KDE、GNOME 和基于 GNOME 的桌面环境使用系统资源（如内存和 CPU 时间）来提供图形界面。因此，Linux 管理员不在 Linux 服务器上安装桌面环境。对于需要桌面环境的 Linux 服务器，Linux 管理员应该选择安装占用系统资源少的轻量级桌面环境。XFCE 是目前常用的轻量级环境。

## 注意 40

要了解更多关于 XFCE 的信息，请访问 `xfce.org`。

## 注意 41

桌面环境通常用于运行许多不同的程序。因此，它们必须提供一种机制，允许程序轻松相互通信，以实现复制和粘贴等功能。这种功能可以由 Wayland 控制器提供，但基于 Wayland-XOrg 的系统使用桌面总线（D-Bus）软件组件来提供图形程序之间的通信。

## 启动和停止 X Windows

正如本章之前解释的，当 `init` 守护进程启动到 5 或 `graphical.target` 时，一个名为 GNOME 显示管理器（GDM）的程序会显示图形登录屏幕。如果你点击 GDM 内的用户账户和设置（齿轮）图标，你将能够从已安装的桌面环境或窗口列表中进行选择，如图 8-9 所示。

## 第 8 章 系统初始化、X Windows 和本地化

**图 8-9** 在 Fedora 系统上在 GNOME 显示管理器中选择图形会话

![](img/0065b92b6d2dfbf8ba2a41373880797d_362_0.png)

> 注意 42
GNOME 显示管理器是 X 显示管理器 (`XDM`) 的变体，它为用户显示基础图形登录。Linux 发行版上其他常用的显示管理器包括 KDE 管理器 (`KDM`)、简单桌面显示管理器 (`SDDM`) 和 LightDM 管理器。

Fedora Linux 上由 GNOME 显示管理器启动的默认环境使用的是 Wayland。当你选择特定用户时，从会话菜单中选择 Plasma，否则 GNOME 显示管理器将继续使用 KDE Plasma 作为你所选用户账户的默认环境。

GNOME 显示管理器是登录并访问系统上可用桌面环境的最简单方法。然而，如果你在此情况下运行级别 1 (`rescue.user-target`) 或运行运行级别 2，你可以从 shell 运行 `startx` 来启动 X Windows 以及默认窗口管理器或环境（例如 Wayland 上的 GNOME）。

## 配置 X Windows

X Windows 是与计算机硬件接口的 GUI 配置。为了让 X Windows 执行其功能，它需要关于鼠标、显示器和视频适配器的信息。这些信息通常从启动时加载的内核模块中检测，也可以在配置文件中指定。键盘类型（例如英语布局）通常在安装过程中手动指定，如图 2-8 所示，但之后可以通过调整桌面环境中的设置，或者通过在后文第 X 章中讨论的修改相应选项来更改。

## CompTIA Linux+ 和 LPIC-1：Linux 认证指南

如果你使用 Xorg，Windows 将其配置存储在 `/etc/X11/xorg.conf` 文件中，以及存储在 `/etc/X11/xorg.conf.d` 目录下的文件中。尽管 Fedora 默认没有 `/etc/X11/xorg.conf` 文件，但如果安装了，它就会存在。键盘和任何用户配置的设置都存储在那里，可以使用桌面环境中的设置工具修改显示分辨率。在 GNOME 中，你可以导航到活动（Activities）、显示应用程序（Show Applications）、设置（Settings）打开设置工具，然后选择显示器（Displays）查看可用设置，如图 8-10 所示。

## 图 8-10 选择显示设置

![](img/0065b92b6d2dfbf8ba2a41373880797d_363_0.png)

> 注意 43
Wayland 没有等效的 `xorg.conf`；Wayland 的所有手动配置必须由 Wayland 合合器执行。

> 注意 44
如果你选择了不兼容的设置，任何错误都将生成到 `~/.xsession` 文件。

## 可访问性

许多桌面环境可以配置以适应用户需求。用于增加可访问性的工具被称为辅助技术。在 GNOME 中，你可以导航到活动（Activities）、显示应用程序（Show Applications）、设置（Settings）打开设置工具，然后选择辅助功能（Accessibility）来配置辅助技术，如图 8-11 所示。

如果你开启图 8-11 所示的始终辅助功能（Always Accessibility）选项，你可以使用桌面右上角的辅助功能图标启用和禁用每个辅助技术。以下是你可以配置的辅助技术列表：

- 高对比度（High Contrast）：修改配色方案以适应视力低的人群。
- 大字体（Large Text）：增大文本字体以适应视力低的人群。
- 启用动画（Enable Animations）：在窗口上显示视觉效果以便识别。

## 图 8-11 配置辅助技术

![](img/0065b92b6d2dfbf8ba2a41373880797d_364_0.png)

- 屏幕阅读器（Screen Reader）：朗述屏幕上的活动窗口。
- 声音键（Sound Keys）：在按下 Num Lock 或 Lock 键时发出蜂嗡声。
- 光标大小（Cursor Size）：允许对跟随鼠标的屏幕部分启用放大镜。
- 缩放（Zoom）：允许在放大期间修改光标和十字线效果。
- 视觉警报（Visual Alerts）：显示一个可以使用鼠标的屏幕上视觉警报。
- 屏幕键盘（Screen Keyboard）：显示一个可以使用鼠标的屏幕上键盘。
- 重复键（Repeat Keys）：当单键被连续按下时模拟多次按下。
- 光标闪烁（Cursor Blinking）：为当前字段添加闪烁的光标。
- 打字辅助（Typing Assist）：触发三种功能：
  - 粘性键（Sticky Keys）：按顺序按下两个键时模拟同时按键。
  - 慢键（Slow keys）：在每次按键后添加延迟。
  - 反弹键（Bounce keys）：忽略快速重复按键。
  - 鼠标键（Mouse keys）：允许用户使用键盘上的方向键控制鼠标。
  - 定位光标（Locate Pointer）：当你快速移动鼠标时将增大鼠标光标尺寸（更容易在屏幕上找到）。
  - 点击辅助（Click Assist）：允许通过长按左键一段时间模拟右键点击，或通过将鼠标指针悬停在桌面区域上触发左键点击。
  - 双击延迟（Double-Click Delay）：用于设置桌面解释为双击的点击之间的延迟（例如打开应用程序）。

如果你的计算机具有相应的软件和硬件，你还可以提供其他技术。例如，如果你有盲文显示设备，可以安装显示软件使其与桌面环境协同工作。如果你的系统有音频麦克风，可以配置语音识别软件；如果你的系统有摄像头或触控板，可以配置手势识别。

## CompTIA Linux+ 与 LPIC-1：Linux 认证指南

## 本地化

本地化（Localization）指的是系统中针对全球某个特定区域的集合设置。加拿大多伦多的 Linux 系统设置与法国巴黎的 Linux 系统设置不同，包括时间、时区、语言、字符集和键盘类型。本地化设置通常在 Linux 发行版的安装过程中选择（如前面的图 2-7 和 2-8 所示），但之后也可以进行更改。

## 时间本地化

Linux 内核并不以第 2 章中 `date` 命令输出的格式来存储年、月、日、时、分、秒。相反，Linux 内核将时间存储为自 1970 年 1 月 1 日（UTC，Unix 的诞生）以来的秒数；这被称为纪元（epoch time），可以通过向 `date` 命令提供参数来显示，如下面的输出所示：

```
[server1] # date +%s

1538523499

```

```
[server1] ##
```

默认情况下，系统从系统的 BIOS 获取当前时间。你可以使用 `hwclock` 命令查看或修改时间。不带参数时，`hwclock` 仅打印来自 BIOS 的时间，你也可以指定选项来修改时间。例如，`hwclock --set --date="2023-08-20 08:16:00"` 会将 BIOS 时间设置为 8 月 20 日上午 8:16。

另一种，你可以使用 `date` 命令设置 Linux 时间。例如，命令 `date -s "2023-08-20 08:16:00"` 会将 Linux 时间设置为 2023 年 8 月 20 日上午 8:16。你可以使用 `hwclock --sync` 将 BIOS 时间设置为与当前 Linux 时间一致，以确保在启动时从 BIOS 加载当前时间。

> 注意
> 回想第 1 章所提到的，你还可以通过网络从服务器获取时间，例如使用网络时间协议（NTP）。NTP 的配置将在第 13 章中讨论。

时间信息取决于区域时区。例如，加拿大多伦多的早上 8:16 是法国巴黎的下午 2:16。时间信息存储在 `/etc/localtime` 文件中，该文件包含了根据你的时区相对于元时间计算时间的规则。此文件通常是 `/usr/share/zoneinfo` 目录下区域文件的副本或符号链接，后者存储了所有的时区信息，如下：

```
[server1] # -11 /etc/localtime

lrwxrwxrwx 1 root root 37 Jul 8 20:13 /etc/localtime ->

/../usr/share/zoneinfo/America/Toronto

```

```
[server1] ##
```

要更改时区，你可以从 `/usr/share/zoneinfo` 目录复制时间文件，以修改 `/etc/localtime` 符号链接指向 `/usr/share/zoneinfo` 下的正确信息文件。

除了 `/localtime` 之外，某些发行版还有一个 `/etc/timezone` 文件，它包含某些应用程序所需的 `/usr/share/zoneinfo` 目录下的引用时区文件，如下面的输出所示：

```
[server1] # cat /etc/timezone

America/Toronto

```

```
[server1] ##
```
