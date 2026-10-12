
# Enlightenment

Enlightenment 依赖屏幕上略微倾斜的面板，其中包含系统信息和打开窗口列表。菜单可以从任何地方访问，但在桌面空白处的任何点击右键也会弹出选项。由于面板没有正确占据整个屏幕，实际上让你觉得错失了屏幕空间。它运行非常快、轻量，且在使用时高度依赖鼠标。由于面板隐藏的方式，它并不非常适合触摸屏，而且并没有多少实用的键盘快捷键。这是一个非常被忽视的桌面，它使用 GTK 或 Qt 驱动，这使其在运行混合不同代码的应用程序时表现得好得多。

> 最适合高度定制化、轻量化的设置。相关发行版：Bodhi Linux, Elive: https://www.enlightenment.org

- **优点**：轻量且在可用性和选项效果方面关注独特

- **缺点**：独特的界面可能让某些用户感到困惑

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_23_1.png)

上方：你可以从任何地方访问应用程序菜单，以防你无法到达面板。

LinuxUser | 重量级 | 新人入场 | 轻量级 *

## MATE, Enlightenment, LXQt & Openbox

测试过的 10 种 Linux 桌面环境

# 特性

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_24_0.png)

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_24_1.png)

## LXQt

这个轻量级桌面的 Qt 端口在视觉上有一些差异。

## Openbox

窗口管理器可以很容易地作为极简主义桌面使用。

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_24_2.png)

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_24_3.png)

上方：LXQt 的审美比任何其他东西都接近 KDE，尽管如此，它仍然是 LXDE。

上方：Openbox 真的只是一个窗口管理器，它控制窗口在桌面环境中的美学和位置，当作为桌面使用时，它的极简设计就会显现出来。

将优秀的 LXDE 移植到 LXQt 的好处是，它是我们去年使用的 Razor-Qt 桌面的最佳继承者。它经常被评为最喜爱之一。LXQt 取了 KDE 的一些功能并将其应用于 LXDE 框架——如果你是那种使用大量应用程序并偏好轻量级环境的人，那么 LXQt 是你的正确选择。

Openbox 通常被认为是一个窗口管理器——控制窗口在桌面环境中的美学和位置的东西。然而，Openbox 也可以与其他工具完全独立使用来实现极简桌面，使用最少的资源。

- **优点**：轻量级环境

- **优点**：独特的界面

- **缺点**：独特的界面可能让某些用户感到困惑

- **缺点**：资源占用高

上方：默认情况下，你可以让 MATE 看起来和旧的 GNOME 2 一模一样，尽管 Linux Mint 使用了略不同的……

# 特性

## 在终端模拟器中运行多个发行版……

GNURoot 应用让运行多个发行版变得简单

- 01 在你 Android 设备的 Play 商店中搜索 `GNURoot`。安装主 `GNURoot` 应用，然后选择你想要运行的辅助性发行版（helper distro）。

- 02 打开 `GNURoot` 应用，从顶部的下拉菜单中选择你正在使用的辅助性发行版。然后点击“Create New Root”（创建新根）框进行解压——这可能需要几分钟。

- 03 完成后，从第二个下拉菜单中选择发行版，并点击“Fake Root”（伪根）框（这样你就可以使用 `apt-get` 和其他命令），然后点击 Launch Roots（启动根）。

- 04 首次启动可能需要一段时间，导致几秒钟黑屏。现在你已经准备好运行下载的发行版了。

- 05 首先，为了确保所有内容都是最新的，请使用命令 `apt-get update` 和 `apt-get upgrade`。如果使用 Fedora，请改用 `yum update`。

> 要运行程序你需要 GUI。`GNURoot` 提供了一种实现 GUI 的方法

## ARM 设备

**在 x86 基础上运行 Linux**

**Android 设备**

对于本文，我们关注的是在 ARM 架构的设备上安装 Linux。然而，像三星 Galaxy Tab 3 是基于 x86 架构的。由于几乎所有的 Linux 发行版都基于 x86，这具有些挑战性。

无论使用 U 盘（本文使用了 U 盘）还是 SD 卡，进行微调以使功能正常工作，对于三星 Galaxy Tab 3、Ubuntu 和 openSUSE（这种模式）似乎是最佳选择。

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_27_0.png)

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_27_1.png)

Store (github.com/distroot)；它通过 `Linux Proot` 提供的进程在非 x86 设备上运行。无需担心任何技术障碍，因为该应用并不会让你以 root 身份使用。相反，你只需要下载并安装适用于不同 ARM 设备的“应用”（如 `Ubuntu`、`Fedora` 或 `Arch`）。

按照通常，你可以通过点击顶部的“apt”创建额外的终端，然后在左上角的垂直菜单之间切换。右上角的（三个）图标允许你调整窗口大小和移动窗口，包括字体大小（你可能在小屏幕上需要更看清文本）以及用于各种缓冲区组合的特殊键。

### 获取图形界面

虽然运行 Linux 非常有用，但你的选择有限。`GNURoot` 的四个主要发行版的特点是，它们只能在没有 GUI 的情况下运行。如果你需要 GUI，`GNURoot` 提供了一种实现它的方法，使用“VNC server”（其目的是为了启动一个 VNC 服务器）。要查看 GUI，你需要安装 (github.com/distroot/vroot) 或 Gentoo (github.com/poRoot 是 VRoot 的旧版本)，然后使用许多可用的 VNC 客户端之一。`Wheezy` 发行版在终端中启动。更新并升级后，你可以安装你需要的图形环境——第一次运行时看起来应该像 'root1!'。然后你可以打开 `VNC Viewer` 应用并指向此地址，输入密码为 'password'。随后将启动虚拟桌面——注意，没有真正的桌面环境

28 www.linuxuser.com

## 在你的 Android 设备上运行 Linux

安装一个超便携的 Linux 版本

# 特性

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_28_0.png)

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_28_1.png)

这是 Debian 的 Whezy，用于 `GNURoot` 运行 `Xfce` 桌面环境

## 从 Android 启动 PC

使用 `DriveDroid` 在没有 live CD 或 USB 的情况下在 PC 上安装并启动

如果你希望在 PC 上使用 Linux，那么 live CD 或 U 盘允许你随地启动。更好的是，`DriveDroid` 使用你的 Android 手机，你可以随身携带。在应用中选择 ISO 或 IMG 文件后连接 USB 到 PC，然后重启（进入 BIOS）。然后启动你选择的发行版。

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_28_2.png)

默认情况下，这是一个 `xterm` 窗口用于 `Whezy`。通过清除屏幕，你可以移动鼠标指针并选择它。在顶部的工具栏上使用如 `Ctrl`、`Alt` 等按键帮助我们避免设备变砖——如果发生这种情况。另一个缺点是重置你的手机并删除所有应用和数据，所以要提前备份。从这个终端，鼠标指针可以拖动。虽然有点慢，你可能会遇到错误并可能同步。你也可以通过 `apt-get` 安装 `Xfce`。然后在 `VNC` 窗口安装后，你就准备好了。在启动引导程序后，你也可以在 Play 商店安装兼容的发行版。最简单的方法是使用 `Linux Deploy` (github.com/linux-deploy) 和 `Linux Farm`。两者都允许在 Android 设备内安装发行版。它们不是虚拟机，因为它们直接运行在 SD 卡上并从终端访问根或使用 GUI。使用 `Linux Deploy` 易用的界面，可以安装并启动 `Ubuntu` 以及 `Fedora` 以及 `Debian`、`Kali` 和 `openSUSE`——只需几次点击即可设置。尽管该应用本身目前处于 Alpha 测试阶段，你可能想在它准备好时尝试。然而，在这里我们关注更可靠的 `Linux Deploy`。启动应用会带你进入带有黑屏的

## 完整安装

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_28_3.png)

29 | linuxuser.com

## 在 Linux Deploy 上运行发行版

在 root 的 Android 设备上轻松安装选择的发行版

- 01  Linux Deploy 并点击顶部的箭头图标访问设置。点击“Distribution”选择你想更改的发行版、版本和架构。
