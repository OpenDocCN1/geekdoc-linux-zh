
虽然花费了一些时间，但远程桌面（以及屏幕投送/共享/录制）功能也已添加到 Wayland 中。遗憾的是，TeamViewer 和 Simple Screen Recorder 等流行工具尚未更新以支持 Wayland。`Green Recorder`（`http://bit.ly/kfx25green`）运行良好，Gnome 的 `Boxes` 应用程序及其内置的屏幕录制工具（Ctrl+Alt+Shift+R）也是如此。

![](img/7a0a282248f9658f0c87e55744c797b6_25_1.png)

我们喜爱 `Guake` 下拉式终端，但为了让它在 Wayland 下工作，你需要在 Gnome 中设置其快捷键。

将会显示大量信息，指交叉祈祷其中包括一行：

`Type=wayland`

如果没有，请检查第 45 页的故障排除框。任何核心 GTK 应用程序都支持 Wayland，因此 Gnome 的所有核心工具都没问题。其他事物仍绑定于 X，因此 Wayland 自带其自己的 XWayland 层来处理这些。由于 XWayland 必须是一个完整的 X Server，且大多数人至少运行一个不支持 XWayland 的应用程序，运行 XWayland 有时被视为浪费资源。然而 XWayland 很精简，只运行应用程序所需的部分，因此这种论点是站不住脚的。例如，Fedora 30 捆绑的 Firefox 版本仍需要通过 XWayland 运行。

### 走向另一面的 Wayland

KDE Plasma 现在与 Wayland 配合良好，而 Plasma 5.16（在你阅读此文章时应该已经发布）应该会运行得更好。它甚至应该支持 Nvidia 驱动，尽管根据 Gnome 的支持情况来看，使用 XWayland 的应用程序可能会行为异常或完全失常。Unity 的情况更令人担忧，因为其部分应用程序仍依赖 GTK2，其窗口管理器需要重写以支持 Wayland，或者被完全替换。

Weston，即 Wayland 的参考合成器，并不一定是你日常使用的桌面替代方案。但它非常适合测试，即使仅仅因为你可以在现有的桌面和显示服务器内运行 Weston——虽然在 Arch 的 Wayland Gnome 会话内运行时，它似乎当前运行非常缓慢。在 Fedora 上，即使你只从光盘运行实时会话，你也可以安装并运行 Weston：

`$ sudo dnf install weston` `weston`

你应该会看到一个带有灰色、整齐镶嵌背景的小窗口。这可能不是世界上最令人兴奋的东西，但总比什么都没有好（事实上，你也可能看到什么都没有，或者错误信息）。点击左上角终端图标可以打开一个终端，你可以从中进一步探索 Weston。

你可能会同意所有主要桌面都缺少的一项功能是旋转窗口。在 Weston 中并非如此：尝试将指针悬停在终端标题栏上，同时按住 Super（Windows 键）并移动鼠标。不可思议，不是吗？还有其他令人兴奋的快捷键，例如使用 Super+Alt 和滚轮改变窗口不透明度。

你可以通过注销当前桌面并在密码提示处选择 Weston 会话来在当前桌面之外启动 Weston 会话。如果你在 Fedora 的实时环境中跟随操作，退出 Gnome 前需要为实时用户设置密码。最简单的方法是按下 Super 进入 Activities 视图，然后输入 `users` 的前几个字母。然后点击建议的 Users 小部件。现在当你注销并尝试重新登录时，你会被要求输入密码，此时你可以选择新的 Weston 会话。完成时按 Ctrl+Alt+Backspace 退出 Weston。

正如我们所提到的，Wayland 还有另一种更模块化的方法。这将吸引桌面

![](img/7a0a282248f9658f0c87e55744c797b6_26_0.png)

> Ubuntu 的 `Weston` 包在 `/usr/lib/weston` 目录中包含一些演示。

爱好者——那些喜欢最小化 GUI 的、留着胡须的、喜欢键盘快捷键胜过友好菜单的、更偏向 Openbox 和 i3 而非 Gnome 和 KDE 的人。哦，还有不使用 Nvidia 驱动的人。无论如何，这种方法由 Wayland 的 Sway 合成器（[https://swaywm.org](https://swaywm.org)）为代表。Sway 是 i3 的直接替代品，i3 是一个极简的平铺窗口管理器。你可以以常规方式在 Fedora 中安装它（这将给你一个相当旧的版本），或者你可以先添加 `copr` 仓库以获得更新版本：

```bash
$ sudo dnf copr enable tofik/sway
$ sudo dnf install sway
```

你会被要求接受一个 GPG 密钥，这取决于你。如果接受，一些依赖项和 `xvt-unicode` 终端程序将被安装，因为每个人都需要一个好的终端。

Sway 是 Drew DeVault（aka sircomm）的创意产物。1.0 版本的发布令人兴奋，因为它们引入了一个新库 wroot，可被任何 Wayland 桌面开发者复用。这为这些人节省了重现标准任务功能的负担，以及实施 XWayland 层这一不可忽视的任务。这是好事，除了节省精力外，它可能标准化了 Wayland 的基础接口，避免了人们常常抱怨困扰 Linux 生态系统的碎片化。正如 GitHub 所言，“约 50,000 行你本来就要写的代码”。

无论如何，注销当前桌面并在输入密码时选择 Sway 来启动它。你可能会对极简主义感到震惊，或者如果你习惯 i3，你会觉得宾至如归。没有菜单，没有 Activities 视图，无论你在哪里或多么猛烈地点击，什么都不会发生。然而，如果你按 Super+Return，一个支持 256 色和 Unicode 的终端将勤勉地占据整个屏幕。再按一次，另一个终端将打开，之前的终端礼貌地腾出空间。

这就是平铺窗口管理器的工作方式。你可以通过将指针悬停在窗口上来切换焦点，并且你可以使用 Super 和数字键在十（）个虚拟桌面之间切换。窗口可以使用 Super+Shift+Q 关闭。Sway 的配置文件位于 `~/.config/sway/config` 下，每个用户独立配置。该目录在你创建它之前不存在，所以请创建它；然后复制全局配置文件 `/etc/sway/config` 并进行自定义。我们的空间快要用完了，因此我们将你引导至 [https://github.com/swaywm/sway/wiki](https://github.com/swaywm/sway/wiki) 以了解更多关于配置和使用 Sway 的信息。哦，如果你想要正常退出，请使用 Super+Shift+E。

我们之前提到，Fedora 30 捆绑的 `Firefox` 版本需要 XWayland 层。这不是原始计划。Fedora 一直在努力开发一个原生 Wayland 版本的 `Firefox` 一段时间，但被认为尚未准备好用于此次发布。但很容易尝试，只需：

```bash
$ sudo dnf install firefox-wayland
```

该包仅提供一个新的启动器，因此仅 19K 大小。使用 `firefox-wayland` 看看它是否对你有效。如果你使用 Arch，你可以在 AUR 中找到此二进制包，名字起得很俏皮，叫 `fedora-firefox-wayland-bin`。

![](img/7a0a282248f9658f0c87e55744c797b6_26_1.png)

![](img/7a0a282248f9658f0c87e55744c797b6_26_2.png)

> Wayland 现在在 KDE Plasma 上可以工作，而且只会变得更好。

## 综述

Hailku ❯❯ KolibriOS ❯❯ OpenIndiana ❯❯ ReactOS ❯❯ VisopSys

![](img/7a0a282248f9658f0c87e55744c797b6_27_0.png)

Shashank Sharma

白天，Shashank 是一名新德里的事务律师，但到了晚上，他就化身开源义警！

### 开源操作系统

对于沙桑克·夏尔马（Shashank Sharma）来说，戴着眼罩单手使用 Arch 系统已不再具有挑战性，他现在正在寻找更具挑战性的任务。

### 我们如何测试……

本综述中的许多操作系统都建议用户首先在虚拟机这一安全环境中进行试用。我们听从建议，在将它们迁移到物理硬件之前，先按照各自官网说明的配置要求在虚拟机中运行了所有这些系统。

我们的目的是寻找一种替代操作系统，以便我们能有效地使用电脑。当然，我们并不指望能通过 Steam 串流玩游戏或通过 Netflix 看电影，但如果这些系统能够播放多媒体、浏览网页、处理文档等，且不会抛出意外错误，它们就会获得我们的青睐。我们将测试安装、软件支持等各种参数，唯一的目的是帮助我们锁定一个能让我们走出熟悉舒适区、同时尽可能减少舒适度牺牲的替代操作系统。

![](img/7a0a282248f9658f0c87e55744c797b6_27_1.png)
