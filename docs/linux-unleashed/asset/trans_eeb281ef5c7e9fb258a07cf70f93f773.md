

下面展示了一个 `.xinitrc` 文件的示例。这是从普通的 XFree86 安装中获取的默认启动文件。该文件被切分为更小的部分，以便对每个子部分进行更详细的检查。第一个子部分涉及设置路径：

```
userresources=$HOME/.Xresources
usermodmap=$HOME/.Xmodmap
sysresources=/usr/X11R6/lib/X11/xinit/.Xresources
sysmodmap=/usr/X11R6/lib/X11/xinit/.Xmodmap
```

这些路径通常是在 XFree86 软件中设置好的，但你应该检查它们以确保其有效。如果存在指向其他目录的链接，请记得跟随链接。这些变量就是 XFree86 所需的全部内容。

下一个子部分检查某些系统资源是否存在，并根据检查结果执行操作。除非你对 X 会话有非常特殊的需求，否则这些检查中的大多数（如果不是全部）都不需要修改。

```
# 合并默认设置和键盘映射

if [ -f $sysresources ]; then
    xrdb -merge $sysresources
fi

if [ -f $sysmodmap ]; then
    xmodmap $sysmodmap
fi

if [ -f $userresources ]; then
    xrdb -merge $userresources
fi

if [ -f $usermodmap ]; then
    xmodmap $usermodmap
fi
```

`.xinitrc` 文件中的最后一个子部分如果存在 xsetroot 程序，则运行它以设置背景颜色（在这种情况下，设置为钢蓝色）。最后，执行 fvwm 窗口管理器并启动你的会话：

```
# 启动一些不错的程序
xsetroot -solid SteelBlue
fvwm
```

如果你想使用另一种窗口管理器，例如 Motif 的 mwm 管理器，请更改此子部分中的最后一行。确保窗口管理器文件在搜索路径中，以便启动例程能够找到它。

如果你想从 `.xinitrc` 文件中创建一个 xterm 会话（你需要一个 xterm 或其他实用程序来在 XFree86 中启动其他任务），请添加以下行：

```bash
xterm -e /bin/bash
```

在这种情况下，`bash`  shell 在 xterm 中调用。当然，你可以使用任何你想要的 shell。

如果你为自己创建 `.xinitrc` 文件，请将其放在你的主目录中。例如，你可以使用像这样的 `.xinitrc` 文件：

```bash
#!/bin/sh

xterm -fn 7x13bold -geometry 80x32+10+10 &
xterm -fn 7x13bold -geometry 80x32+30+50 &
oclock -geometry 70x70-7+7 &
xsetroot -solid SteelBlue &
exec fvwm
```

这会启动两个 xterm 和一个时钟，并将它们放置在桌面上，然后设置背景颜色为钢蓝色，最后启动桌面管理器。两个重要的注意事项：脚本中的最后一个命令前面带有 `exec` 命令，且最后一个命令不被发送到后台。如果你将最后一个命令发送到后台或忘记 `exec` 命令，X 启动后立即关闭！

## 总结

上述所有步骤将帮助你正确设置 XFree86，按照这些步骤操作后，你的 XFree86 会话应该能毫无问题地启动。有关使用 X 的具体细节超出了本书的范围。如果你不确定如何使用 X，请查看随发行版提供的文档文件，或咨询面向用户的书籍。

然而，如果你按照前面概述的步骤操作，你的 X 系统现在应该是可用的，你可以开始使用 X 系统作为你与 Linux 的主要接口。在 X 中工作之后，很难再回到基于字符的终端！

从这里开始，你可以前往与该主题相关的多个章节：

- Wabi，一种在 Linux 下运行 Windows 应用程序的方式，在第 23 章“Wabi”中讨论。
- Ghostscript，允许你在屏幕上查看 PostScript 文件并将其发送到打印机，在第 24 章“Ghostscript 和 Ghostview”中讨论。
- Linux 下的编程在第 V 部分讨论，从第 25 章“gawk”开始。
- 系统管理在第 VI 部分讨论，从第 32 章“系统管理基础”开始。

![](img/e8e6b47ac20475e23d48b4c476f5d891_452_0.png)

## Wabi

*作者：Tim Parker*

### 本章内容

- Wabi 能做什么？ 416
- 安装 Wabi 418
- 运行 Windows 3.x 应用程序 419

Wabi（Windows 应用程序二进制接口）是一款为允许 Microsoft Windows 3.X 应用程序在 X 和 Motif 下运行而开发的 Linux 和 UNIX 应用程序。Wabi 充当 Microsoft Windows 窗口命令与 X 下对应功能之间的翻译器。通过运行 Wabi，你的 Linux 系统可以获得对大多数 Windows 应用程序的访问权限，同时保留 Linux 的所有特性（包括其防崩溃能力、更好的性能和窗口切换）。

并非所有 Windows 应用程序都能在 Wabi 下正常运行。为了在 Wabi 下干净地执行，Windows 应用程序必须是“行为端正”的，这意味着应用程序必须符合 Microsoft 为应用程序制定的所有标准。大多数标准应用程序，如文字处理程序和电子表格，行为端正，在 Wabi 下工作良好。一些软件包，特别是游戏和一些图形工具，为了从图形卡中获得更好的性能而偏离 Microsoft Windows 标准，这些软件在 Wabi 下无法可靠运行（如果还能运行的话）。此外，在 Wabi 的 2.1 版本（当前发行版）中，你无法运行 Windows 95 应用程序。

# 提示

一份已经过测试并被认证为能在 Wabi 下正常运行的应用程序列表可以从包括大多数 Linux FTP 站点在内的多个站点获取。其中一个站点是：

http://wabiapps.psgroup.com

不要因为你最喜欢的软件不能全部在 Wabi 下运行而感到气馁。大多数 Windows 3.x 应用程序都可以运行，主要例外是游戏。想在 Linux 下运行 CorelDraw？没问题。想运行 Microsoft Office？同样，小菜一碟。本质上，如果它是办公生产力工具，它就能运行（因为这些工具很少需要偏离 Windows 编程标准）。

### Wabi 能做什么？

如前所述，Wabi 位于 Windows 应用程序和 X 管理器之间的一层。当运行在 Wabi 下的 Windows 应用程序发出窗口请求时，例如打开新窗口、更改标题或修改字体，Wabi 会拦截该请求并将其转换为 X 等效操作。当 X Windows 进程想要向 Windows 应用程序发送消息时，Wabi 将 X 消息转换为 Windows 消息。只要应用程序遵循标准的 Windows 机制，Wabi 就可以处理转换并允许该应用程序在 X 下运行。

Wabi 本身并不做太多事情。没有真正的可供交互的 Wabi 应用程序，除了某些配置工具。然而，Wabi 确实拥有大量特性，允许在 X 下执行你在 Windows 或基于 Windows 的环境中熟悉的操作，例如：

- Windows 应用程序之间的剪切和粘贴
- 对 CPU 的增强模式支持
- DOS 格式磁盘访问
- Windows 应用程序之间的 OLE（对象链接和嵌入）
- Windows 应用程序之间的 DDE（动态数据交换）
- 网络支持
- Windows sockets 编程

Wabi 将大多数这些特性扩展到 X 环境，因此你可以在 Windows 和 X 应用程序之间进行剪切和粘贴，与两者下的网络应用程序交互，并允许同一应用程序上的多个用户。

对大多数用户而言，Wabi 不能做什么可能更重要。这个列表很短，但对于某些 Windows 应用程序来说确实有一些重要的考量。Wabi 不支持：

- MIDI（乐器数字接口）
- AVI（音频视频接口）
- IPX/SPX 网络
- 共享 Wabi 目录
- 基于 VGA 的视频驱动程序
- DOS 磁盘格式化
- (VDx) 虚拟设备驱动程序

这些不支持的特性中的一些，如 IPX/SPX 和 MIDI，可以通过其他 Linux 子系统提供。Wabi 也在不断通过新功能进行改进，因此未来可能会添加对这些项目支持。

由于版权限制，Wabi 不包含 Microsoft Windows 3.x，因此你除了 Wabi 还需要购买支持的 Windows 副本（尽管大多数用户某处都有 Windows 副本）。

![](img/e8e6b47ac20475e23d48b4c476f5d891_454_0.png)

