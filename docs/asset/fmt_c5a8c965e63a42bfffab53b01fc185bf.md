
但是其他主题真的可以定制吗？确实，你会在两者中都找到带有主题、插件和效果的类似安排。所有的 Mint 桌面大多基于 GTK，因此基础元素可以通过 https://www.gnome-look.org/browse/?135 的 GTK 主题覆盖。如果你在使用 Mint MATE 或决定尝试 Cinnamon，标准桌面可以通过 `mint-cinnamon` 包可用，或者你可以通过 `cinnamon-converter` 获取手动安装。你也可以尝试 XFCE 或 MATE，如果你使用 `mint-meta-xfce` 和 `mint-meta-mate`（这很好地去掉了那个）包的话。再次，如果你只需要核心选项，也有极简包。这些都将帮助添加你的登录界面，所以你可以从桌面菜单中选择。谈到登录界面，你也可以处理那个。由于 Cinnamon 主题在启动过程更早阶段运行，GRUB 可以被主题化，你可以使用 Plymouth 屏幕（https://gnome-look.org/browse/?108）到桌面。（有时）看到应用程序被调用它们中是令人放心的，它们在减小时会消失。由于这样，你可能想要关闭它们，然后你可以通过“设置”中的取消勾选轻松地这样做。

此外，Mint 还提供了几个在 Ubuntu 桌面界面找到的其他选择。是由于 Snap 的缺失阻止了我们从 Canonical 的 Snap 商店安装 Snap。没有另一个支持的（在我们处于这个时期时），三个官方支持的 Mint 发行版是 Cinnamon、Xfce 和 MATE、跨发行版打包系统或禁用机器上的 X.org。Linux 社区的独立开发者似乎对此有共识。跨发行版打包系统或禁用机器上的 X.org……好的是我们现在发现了可以启用它们的方法。此外，Wayland 目前是不可能的，所以一旦有了支持它的决定，我们将在页面上查看。

当 Snap 发布时的直接后果是 Ubuntu 20.04 及以后版本没有方法获取 Chromium 浏览器，因为它将其封装为 snap。我们认为更多人应该使用 Firefox，或者我们在 linuxformat.com 上跟踪的用户似乎他们得到的是那样。但对于获取没有 Ubuntu DEB 包的 Chromium，这是一个潜在令人担忧的方法，如果你渴望在 DEB 包中获得一点 Google，那么从 Mint Store 或通过 Flatpak 获取它，这允许它在 Ubuntu（以及 Mint）之外安装。

我们认为认为 Flatpak 是在 Ubuntu（以及 Mint）之外安装软件的健康方式。Flatpak 在 Linux 上开箱可用，你可以在软件管理器中轻松找到一些 Flatpak 应用程序；如果你想要最新版本的 GIMP，Flatpak 选项是环境结果中的第二个选择。你还会找到 Spotify 和 Steam 的 Flatpak，这样你就可以像从前一样排队你的 Rush 并玩 Snap Invaders。

如果你确实想要 Snaps，也许是为了最新版本的 Blender 或 PyCharm IDE，很容易处理掉阻止它们的文件，然后用 `apt` 安装：

```bash
$ sudo apt rm /etc/apt/conf.d/nosnap.pref
$ sudo apt install snap
```

Snap 可以从命令行搜索并安装。现在你可以浏览 https://snap.io 上的内容，但为了一个完整的 GUI，你也会恰当地管理 Snap Store。它是以 Snap 的形式提供的，你可以拥有它：

## 安装 KDE Plasma

用 KDE Plasma 流畅、华丽的体验转变你的桌面，并配合 Wayland 完全迈向下一世代！

如今没有官方的 Linux Mint KDE 版本，但这并不意味着 Mint 用户会错失 KDE Plasma 奇妙的体验。它很现代，但仍然有一个传统的应用程序菜单。它非常精细，但不再像以前那样是个资源消耗大户。而且它的 Dolphin 文件管理器用起来非常愉快，尤其是如果你觉得 Nemo 稍微太简单了。尽管如此，安装新的桌面环境会有其自己的后果；在他们指怪我们运行了你的系统之前，最好先意识到这一点。

最后是磁盘空间占用的问题。KDE Plasma 元软件包（metapackage）提供了一个最小化的桌面；根据截图，它包含 246 个软件包，仅占用 850MB 空间。如果你选择完整版，所有应用程序将接近 3GB。接下来是核心功能的重复，例如文本编辑器、媒体播放器和截图工具。它们都开始让 Dolphin 文件管理器在电影中显得拥挤，看起来有点奇怪。

最后，很难完全卸载一个桌面。手动删除后，很难修复损坏的桌面。所以，不要尝试在没有虚拟机的情况下删除东西，或者使用 Timeshift 将内容恢复到良好状态（正如我们之前演示的那样）。

拥有（至少）Plasma 桌面可以将 Mint 的显示管理器从 SDDM 更改为正确的 SDDM（简单显示管理器）。如果从命令行安装，默认是关闭的，你可以通过以下方式更改它：

```bash
$ sudo apt install kde-plasma
```

![](img/2f8aba538b6f14f57de8cb694470acb2_9_0.png)

关于为什么在使用 KDE 时，这个 SDDM 可能比自动检测更轻松的原因

两个显示器都支持所有 Linux 桌面环境（轻量级窗口管理器），选择哪一个取决于你对主题的偏好。默认 SDDM 主题可能不是大多数人眼中的漂亮，但一旦你登录，你就会看到它与 Atom Screen (SDDM) 的区别。讽的是，我们发现自己处于一个类 Windows 的主题中。当我们处于自己想要的主题时，也许我们可以对其进行润色，并因为知道所有喜爱的物品只需点击即可获得而感到如家。在某种程度上，这就是

![](img/2f8aba538b6f14f57de8cb694470acb2_9_1.png)

每个小部件（有很多小部件）都可能被批评为太突兀。我们可以获得一个自定义的编辑模式，但让人疑惑这一切的意义何。更的是，KDE 4 的连续迭代让你在不确定按键该放哪里时却掌握了所有的按键。这个版本的 KDE 也面临着资源消耗大户的问题，并且在图形方面有些火热的独立性。大多数设备可能都能很好地运行那个图形驱动，所以硬件加速并不是你可以排除的。

当你听到 KDE 5（或 KDE Plasma 5）时，桌面倾向于拥有更加精简的外观。在我们的测试中，我们使用的内存比 Cinnamon 多一点，比 X 和 MATE 多得多，朋友之间多出一百兆左右又算什么呢？这完全没有区别。

最轻量的 KDE 应用程序大约占 850MB，但它非常

## 定制 Mint 20

一旦启动，内存杀手 Chromium。Plasma 确实是可配置的，但其方式不会过头。默认的中等重量启动器（应该在左下角）。右键点击它并选择“显示替代”。你会发现它可以切换为现代启动器（类似于 Gnome）或更具层级感的菜单设计。KDE 自带了一个图形商店 Discovered（KDE 应用程序之一，不会为了任何机会运行不必要的层）。你可以轻松地在菜单中找到它，你也可以参考 Mint 的软件管理器。你想要了解的是对 Flatpak 的支持。如果你运行终端（唯一的应用程序）并运行：

```bash
sudo apt install flatpak-mint
```

现在，在发现 Discover 之后，你可以通过右下角的设置添加它们来运行 FlatHub（或任何其他 Flatpak）。只需点击“显示命令”，这比 Snap 详细得多。任何人都可以建立自己的 Flatpak 仓库，但 Canonical 之外的唯一仓库是 Snap。两者都具有一些沙箱功能，但我们必须确保下载的随机边界的安全性。在 Flathub 和常见的 snap 软件包上设置应用程序很容易，而后者一直处于“验证中”。

我们提到过 Wayland 并不是所有桌面都显式支持，但这种情况正在发生。在最新的 MATE 版本中，如果你将 Marco 窗口管理器切换为 Cinnamon，大部分内容现在都可以与 Wayland 工作。这样你就能体验未来。Wayland 将引入支持，但这可能还有很长的路要走。是桌面而不是发行版带来了 Wayland——因为你有 KDE Plasma 的支持。使用 K 窗口管理器：只需拉取几个包即可：

```bash
sudo apt install plasma-workspace-wayland
```

现在你注销，明天将可用一个名为 Plasma 的新会话。Cinnamon 上的 Plasma 今年取得了很大进展。我们将用 Nvidia 驱动进行测试。

泛认为 Plasma 让你感到突兀的一点是它是自动保存的。如果你希望在没有那些杂乱终端和其他任何你打开的内容的情况下启动它们，回到 Mint-the SDDM。

![](img/2f8aba538b6f14f57de8cb694470acb2_10_0)
