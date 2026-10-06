

# SuperProbe

SuperProbe 工具可以帮助你确定视频设备的类型和工作特性。该工具包含在 XFree86 包中。要运行 SuperProbe，请执行命令

SuperProbe

输出应类似于：

- - SuperProbe Version 2.18 (1998年12月22日)
- (c) Copyright 1993,1994 by David Wexelblatt
- <dwex@xfree86.org>
- (c) Copyright 1994-1998 by The XFree86 Project, Inc

此工作衍生自 Finn Thoegersen 生成的 'vgadoc2.zip' 和 'vgadoc3.zip' 文档包，并在获得所有适当许可后发布。额外信息来自 Richard Ferraro 编写的《Programmer's Guide to the EGA and VGA, 2nd ed》以及制造商手册。

欢迎提交 Bug，请发送至 XFree86@XFree86.org。特别是对于该程序未能正确检测的芯片组报告，我们将不胜感激。

在提交报告之前，请确保你拥有最新版本的 SuperProbe（参见 http://www.xfree86.org/FAQ）。

> 警告 - 此软件可能会导致你的机器挂起。在运行此程序之前请阅读 SuperProbe.1 手。

```
INTERRUPT WITHIN FIVE SECONDS TO ABORT!
First video: Super-VGA
Chipset: Matrox Millennium (PCI Probed)
RAMDAC: TI ViewPoint3026 24-bit TrueColor DAC/cursor, pixel-mux,clock (with 6-bit lookup tables (or 6-bit mode))
```

注意，该工具警告可能会导致某些系统挂起。你可以在探测之前输入 Ctrl+C 来中断程序。
现在通过完成练习 26.4 来练习使用 SuperProbe。

# 练习 26.4

# 使用 SuperProbe

SuperProbe 是一个有用但并非万能工具。为了获得经验，请在你的系统上运行它。输出是否正确陈述了系统视频设备的类型特性？

# xdtune

xvidtune 工具可以帮助你精调 X 配置。它允许你交互地调整视频模式和扫描率以获得最佳性能。该工具是 XFree86 包的一部分。

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_661_0.png)

如果你扫描率设置不当，xvidtune 工具可能会损坏显示器。请小心只提供正确的值。

# 重要的 X 目录和文件

/usr/X11R6/bin 目录包含 X 二进制文件。为了让 X 程序正常运行，/usr/X11R6/bin 目录应该出现在程序路径中，存储在 PATH 环境变量中。
另一个重要的 X 目录是 /etc/X11。它的子目录包含 X 配置。符号链接 /etc/X11/R 指向当前选的 X 服务器，它位于 /usr/X11R6/bin/etc/X11 目录还包含 XF86Config 文件，这是主配置文件，通常通过使用 Xconfigurator 或 FX86Setup 构建。关于 /etc/X11/FX86Config 文件的更多信息，请参见 FX86Config 页面。

# 总结 653

现在完成练习 26.5，该练习要求你学习主 X 配置。

# 练习 26.5
检查 /etc/X11/XF86Config

由于视频特性的差异，X 配置在不同系统之间可能会显著不同。将配置恰当的 X 安装的 XF86Config 文件与本节所示配置进行比较。你发现了哪些相似之处和不同之处？

# 总结

在本章中，你学习了 X 的安装和配置。涵盖的最重要主题是：

**X 窗口系统 (X)** 提供了 Red Hat Linux 使用的图形界面。X 的实现适用于多种 Unix 和非 Unix 平台。随 Red Hat Linux 分发的 X 版本由 XFree86 项目发布。

**服务器和客户端 (Servers and Clients)** 管理用户界面的 X 程序称为 X 服务器。使用界面的应用程序或其他程序称为 X 客户端。

**安装 X** 安装 X 涉及安装多个包。最重要的包之一是包含 X 服务器的包，必须选择适用于系统中安装的视频适配器类型。

**配置 X** 你可以使用多种工具来配置 X，如下：

- - Xconfigurator
- XF86Setup
- xf86config
- SuperProbe
- xvidtune

X 目录和文件 /usr/X11R6/bin 目录包含 X 二进制文件。/etc/X11 目录及其子目录包含 X 配置。符号链接 /etc/X11/P 指向当前选择 X 服务器。/etc/X11 目录还包含 XF86Config 文件，即主 X 配置。

# 关键术语

在继续下一章之前，确保你熟悉以下术语：

- - 桌面管理器 (desktop manager)
- 水平同步率 (horizontal sync rate)
- 垂直刷新率 (vertical refresh rate)
- 窗口管理器 (window manager)
- X 客户端 (X client)
- X 服务器 (X server)

# 更多信息来源

如果你对本章介绍的主题有更多信息，应当咨询以下来源：

- - XFree86 FAQ，www.xfree86.org
[/content]
```

等等，我发现漏掉了最后一段的翻译：

如果你对本章介绍的主题有更多信息，应当咨询以下来源：

- - XFree86 FAQ，www.xfree86.org
[/content]

让我重新检查并提供完整的翻译（由于你提供的原始文本在 `[content]` 处截断了，我将翻译你提供的所有内容）。

**纠正：你提供的文本最后一段是关于第27章的内容，完整翻译如下：**

[content]

# 第 27 章
理解和使用窗口管理器与桌面

RHCE 准备知识，本章涵盖主题：

- 熟悉 Red Hat Linux 下的窗口管理器和桌面环境，并知道如何选择它们。

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_668_0.png)

一组程序协作提供 X 环境。这些包括：

- **窗口管理器 (window manager)**，绘制边框、标题栏、菜单栏和窗口操作按钮
- **桌面管理器 (desktop manager)**，提供桌面环境，包括文件管理器、帮助系统和虚拟桌面
- X 客户端，你运行的应用程序

此外，如果你通过 X 登录，**显示管理器 (display manager)** 将通过 PAM 设施验证你的身份。本章向你介绍窗口管理器、桌面管理器和显示管理器，并解释如何选择和配置它们。

# 桌面环境

Red Hat Linux 允许你在两种主要环境之间选择：

- GNOME
- KDE

默认，GNOME 环境包含 GNOME 桌面管理器和 Enlightenment 窗口管理器。KDE 环境包含 KDE 桌面管理器和 KWM 窗口管理器。本节描述了这些桌面环境，解释如何在它们之间进行选择，并解释如何配置它们以与替代窗口管理器工作。

