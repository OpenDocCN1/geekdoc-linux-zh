

# 教程：Plasma 5

## 在 VirtualBox 中使用 Plasma 5

硬件加速桌面是 Plasma 5 的一个杀手级功能，但其缺点是在 VirtualBox 中作为来宾系统时表现不佳。解决方法可能听起来很残酷，但在机器设置中关闭 3D 加速即可奏效。您可能还会遇到字体和图标缩放不正确的问题——此时，您需要在 KDE 字体设置中手动设置字体的 DPI 大小。

## 善用 Windows 键

许多新的 Linux 用户来自 Windows 世界，那里有很多人们已经熟悉的键盘快捷键和其他功能。在 Linux 电脑上使用 GNOME 或在 Mac 上运行 OS X 的人都知道，桌面隐喻完全不同，用户需要改变习惯才能在新桌面上高效工作。而在 KDE 中情况则恰恰相反：您可以重现某些按键绑定，使其在 Windows 中同样适用。在本例中，我们将使用 Windows 键来启动开始菜单。

默认的 KDE Plasma 桌面不允许您在单个按键上分配操作，但有一种名为 KSuperkey 的变通方法。安装后，只需使用 `ksuperkey` 命令启动它（并将其添加到 KDE 的自动启动部分），然后只需按下 Windows 键——在 KDE 中它被识别为 Meta。KSuperkey 与默认的 Plasma 5 应用程序启动器配合良好。

对于第一个技巧，我们需要 `wmctrl` 包，几乎在任何 Linux 发行版中都能找到。一旦您拥有了它，请创建一个包含以下内容的脚本：

```sh
#!/bin/sh
target=on
if xprop -root _NET_SHOWING_DESKTOP | fgrep "= 1"; then
    target=off
fi
wmctrl -k $target
```

将其保存为 'showdesktop.sh' 文件，然后使其可执行（`chmod +x showdesktop.sh`），最后将其分配给系统设置中快捷键部分的 Win+D 绑定。

锁定屏幕是一个更简单的过程：不需要将任何内容包装成脚本；相反，使用普通命令就足够了：

```sh
qdbus org/freedesktop/ScreenSaver /ScreenSaver org.freedesktop.ScreenSaver.SetActive True
```

## 自定义按键绑定

作为上一步的延续，我们将尝试重现 Win+D 和 Win+L 组合键的行为，分别用于最小化所有窗口和锁定桌面。

![](img/0fc17bd4c29dc437e3ac28a53f7559db_43_0.png)

## 内置网络浏览器

Linux 有大量的浏览器，但您是否想过直接在桌面上拥有一个浏览器？我们在 Ubuntu 的 Unity 中见过类似的东西，但在 KDE 中，迷你浏览器是以 plasmoid（等离子元件）的形式实现的，这意味着它不会与应用窗口一起挡路，而是静静地待在桌面上。要添加它：只需右键单击桌面并选择 'Add Widgets...'（添加部件...）项，然后搜索 'Web browser'（网络浏览器）。双击将其添加到桌面，并查看默认 www.kde.org 页面在一个小窗口中打开。该 plasmoid 除了快捷键绑定外没有太多设置，因此要更改网站，请在 plasmoid 的文本输入字段中输入其地址，并带有强制的 'www.' 前缀。该 plasmoid 将加载您的页面并自动调整其布局以匹配 plasmoid 本身的大小——您可以调整大小以使 plasmoid 内的页面可读。

网络浏览器 plasmoid 当前使用 QtWebKit 引擎，与 Firefox 浏览器相同，但 KDE 团队计划切换到较新的 QtWebEngine，后者基于 Chromium 代码，渲染页面更好。尽管如此，当前的 plasmoid 能力很强，在 html5test.com 上获得了不错的 390 分成绩。

![](img/0fc17bd4c29dc437e3ac28a53f7559db_44_0.png)

![](img/0fc17bd4c29dc437e3ac28a53f7559db_44_1.png)

## 启动单个设置模块

所有 KDE Plasma 5 设置都方便地分组在系统设置应用程序中，也可以通过调用 **systemsettings5** 命令来启动该应用程序。不可否认，这个应用程序非常好用，但找到完美的设置可能需要一些时间，您可能希望以更优雅的方式访问所有内容。这可以通过使用 **kcmshell5** 命令来完成。首先，让我们看看我们有哪些模块：

```sh
$ /usr/bin/kcmshell5 --list
```

将任何模块作为 **kcmshell5** 的参数，它将启动相应的单个模块，而不访问控制面板。例如：

```sh
$ /usr/bin/kcmshell5 kwincompositing
```

...将启动桌面合成器设置。此技术允许您从列表中启动任何模块，然后，也许创建带有此类命令的快捷方式，或将其与键盘快捷键绑定。还可以使用单个命令启动多个模块。例如：

```sh
$ /usr/bin/kcmshell5 mouse kcm_xserver
```

...将显示一个漂亮的窗口，其中所有这些模块作为单个窗口内的不同部分显示。

关于更多 Plasma 5 的技巧和窍门，访问 KDE wiki 总是值得的 – 社区成员一直在上传指南至 [userbase.kde.org/Tutorials](http://userbase.kde.org/Tutorials)。

> **Plasma 5 桌面是模块化的，因此我们可以终止 shell 而不干扰其他任何东西，无论是后台进程还是图形应用程序**

## 统一外观

据我们所知，消除基于 Qt 和基于 GTK 的应用程序之间视觉差异的第一次尝试是在 Red Hat Linux 8.0 中引入 Bluecurve 主题时进行的。如今，问题仍然存在：现代 GTK2 和 GTK3 应用程序不太适合 KDE 桌面。这个问题有各种变通方法，包括 QtCurve 主题，它对 GTK2 效果很好，但对 GTK3 支持不佳。另一个选择是使用 Orion GTK 主题，其外观类似于 Plasma 5 Breeze（默认主题），但与之仍有很大的视觉不一致性。幸运的是，我们有 Breeze 主题到 GTK 的可用移植版本，位于 [github.com/dirkv1/gnome-breeze](https://github.com/dirkv1/gnome-breeze)，涵盖浅色和深色变体。只需将主题复制到 `~/.themes` 或 `/usr/share/themes`，然后在 *System Settings*（*Widget style* -> *GNOME Application style* (*GTK*)）中选择它。现在，无论使用哪种图形工具包，您都能获得一致的视觉体验。

![](img/0fc17bd4c29dc437e3ac28a53f7559db_45_0.png)

# 使用 MonoDevelop 窗体创建用户界面

创建基于 GTK 的 UI 过去是一项令人沮丧的工作，但 MonoDevelop 改变了这一切...

+   **Tim Hanna** 自 Amiga PC 时代起就从事 IT 行业。作为记者、导师、演讲者以及科学书籍的作者，他多次见证移动市场的各个方面

使用 GTK 很痛苦：其基于句柄函数的编码范式在 Palm OS 时代可能看起来很酷，但现在看起来非常过时。

V-CL 试图通过为大多数 GUI 类提供面向对象封装来改善这种情况。这导致了更紧凑的代码，但它离真正的 RAD（快速应用程序开发）还差得远：看到您正在工作的用户界面是生产力的真正助推器。Visual Basic 在这方面一直是领导者。该产品的第一个版本在 DOS 下运行，但它并未吝啬于提供 WYSIWYG-GUI 编辑器。

尽管 Mono 包含对 Microsoft 的 Windows.Forms 命名空间的运行时仿真，但 MonoDevelop 的 WYSIWYG 编辑器是基于 GTK 的。由于该框架与 Mono 一样具有跨平台性，对于大多数基于桌面的应用程序来说，使用 GTK 不应是问题。此外，这里讨论的许多概念也可以应用于各种其他 GUI 工具。

MonoDevelop 将为您生成默认的 GTK 2.0 项目骨架。除了已知的 C# 文件外，我们的项目现在还有一个包含窗体布局和几个图标的资源文件的文件夹。实际的程序执行仍然通过 `Program.cs` 处理，默认情况下包含以下代码：

```csharp
class MainClass
{
    public static void Main (string[] args)
    {
        Application.Init ();
        MainWindow win = new MainWindow ();
        win.Show ();
        Application.Run ();
    }
}
```

`Application.Init()` 是 GTK 框架主类中的静态方法。在创建并显示 `MainWindow` 类的新实例后，我们调用 `Run()` 以启动事件循环。

## 资源

-   **MonoDevelop**
    -   [monodevelop.com](http://monodevelop.com)

首先启动 MonoDevelop。我们在这个 C# 和 MonoDevelop 系列的第一部分中涵盖了安装和部署说明（第 157 期）。然后基于模板 C# > Gtk 2.0 Project 创建新项目。

![](img/0fc17bd4c29dc437e3ac28a53f7559db_45_1.png)

右：这次我们将制作一个简单的电阻色码计算器

