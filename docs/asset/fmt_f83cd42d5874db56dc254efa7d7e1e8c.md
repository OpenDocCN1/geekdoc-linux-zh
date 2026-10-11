
| 窗口管理器 | 描述 | URL |
|---|---|---|
| AfterStep | 外观和感觉类似 NEXTSTEP | http://www.afterstep.org |
| amwm | Amiga 窗口管理器 | http://www.lysator.liu.se/~marcus/amwm.html |
| blackbox | 极简主义窗口管理器 | http://blackbox.alug.org |
| CDE | 通用桌面环境（商业软件） | http://opengroup.org |
| ctwm | 基于带有扩展功能的 twm | http://brudg.ctlr.c-l.iiu.se/~dl/ctwm |
| Enlightenment | 复杂且功能强大；支持 GNOME | http://www.enlightenment.org |
| fwm | 基于带有诸多改进的 twm；也可用版本 2 | http://www.fwm.org |
| fwm95 | 基于 fwm2 | http://www.foxproject.org/xclass/fwm95.html |
| IceWM | 高度可配置 | http://icewm.sourceforge.net |
| KDE | K 桌面环境；非常流行 | http://www.kde.org |
| lwm | 轻量级窗口管理器；无功能 | http://users.ch.genedata.com/~enh/lwm/ |
| mlwvm | 使您的桌面看起来像 Mac | http://www2u.biglobe.ne.jp/~y-miyata/mlwvm.html |
| mwm | Motif 窗口管理器（也包含在免费的 LessTif 发行版中） | http://www.openmck.org 和 http://www.lesstif.org |
| olvwm | OpenLook 窗口管理器；基于 Sun Microsystems 的代码 | ftp://ftp.x.org/R5contrib/ |
| sawmill | 功能包括基于 Lisp 的配置脚本语言 | http://sawmill.sourceforge.net |
| scwm | Scheme 约束窗口管理器；功能包括脚本 | http://scwm.mit.edu/ |
| twm | 随 XFree86 提供；极简主义窗口管理 | http://www.x.org |
| vtwm | 基于 twm，但包含虚拟桌面 | http://www.visi.com/~hawked/vtwm.html |
| WindowMaker | 模拟 NeXt 界面 | http://www.windowmaker.org |
| wm2 | 极小且紧凑 | http://www.all-day-breakfast.com/wm2/ |
| wmx | wm2 的变体，同样极小且紧凑 | http://www.all-day-breakfast.com/wmx/ |
| XFCE | XFce 桌面环境；具有类似 CDE 的面板 | http://www.xfce.org |

注意，表 9.3 并未列出 GNOME。这是因为 GNOME 不是一个窗口管理器，而是一套与兼容 GNOME 的窗口管理器（如 Enlightenment）一起使用的库和客户端集合。在笔记本电脑上使用 GNOME 或 KDE 需要数百兆的额外存储空间，但为您的 X11 会话提供了现代化的图形界面。

### 最大化您的屏幕空间

您可以在 X11 会话中利用的一个窗口管理器功能是使用额外的显示屏，即 *virtual desktop*（虚拟桌面）。并非所有窗口管理器（尤其是那些为极简主义者设计的管理器）都提供此功能。传统的 X11 窗口管理器，如 *fvwm* 和 *olvwm*，其名称中包含了关于此功能的暗示（即 *v*）。当使用支持虚拟桌面的窗口管理器时，您通常会发现一个被称为 *pager*（分页器）的小窗口、对话框或按钮组，用于在各界面之间进行导航。

使用虚拟桌面是整理工作区域（也许按功能分类）的好方法。例如，您可以在一个桌面上进行文字处理，在另一个窗口中进行电子邮件处理，在第三个窗口中浏览网页，等等。图 9.3 显示了一个支持四个虚拟桌面的典型分页器，其中两个桌面正在运行应用程序。

要导航到不同的桌面，点击其中一个方块。您的整个显示屏将改变以反映新的桌面。几乎大多数窗口管理器都允许您配置 X11 会话中使用的虚拟桌面数量。传统的桌面，如 *fvwm*，使用一个名为 *resource file*（资源文件）的文本来包含仅在 X 会话之间才能更改的设置。较新的 X11 窗口管理器和桌面环境，如 KDE，提供了图形界面配置工具。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_253_0.png)

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_254_0.png)

> 图 9.4 KDE 的面板配置工具可用于更改多项面板设置，包括面板分页器上可用的虚拟桌面按钮数量。

以便在您的 X 会话中允许更改。例如，KDE 的 kpanel 配置工具（如图 9.4 所示）允许您将虚拟桌面的数量从两个更改为八个。

与运行多个 X 会话一样，在不同的虚拟控制台运行大量应用程序可能会消耗系统资源，但您将能够快速在应用程序之间切换，并在不同的显示面上整理您的工作。

### 使用外部监视器

如果您确实需要额外的屏幕空间，或者希望使用更大的显示器，您可以将笔记本连接到外部监视器（只要您的笔记本或扩展坞提供外部视频输出端口）。您可能需要在重启时修改笔记本的 BIOS 以启用外部显示器的使用。您可能还需要通过笔记本电脑键盘上的特殊 Fn 键组合来切换笔记本 LCD 显示屏的开启或关闭。

如果您可以在外部监视器上显示仅文本的 Linux 控制台，但无法显示 X11 会话，请检查是否需要编辑 `XF86Config` 以包含特殊启用外部显示器使用的选项。例如，NeoMagic 芯片组用户可能需要使用以下内容：

```
option “extern_disp”
option “intern_disp”
```

这些包含在 `XF86Config` 的*设备*段中的选项，将启用同时使用 LCD 和外部显示器。通常你可以预期使用外部显示器时能够使用更大的屏幕分辨率，但情况并非总是如此。你需要通过实验外部显示器来找到最佳设置。

### 多线程？Xinerama？

笔记本用户可能无法将 LCD 和外部显示器作为单个显示器使用，即使 XFree86 发布了新版本 4.0。虽然 X11 支持此功能，但多线程显示通常依赖于硬件，并且需要符合标准的图形卡。Xinerama 功能虽然由 XFree86 支持，但需要一个符合标准或支持 Xinerama 的窗口管理器——这是一个 Linux 尚未支持的特性。

#### 资源信息

- `http://www.gnu.org/software/bash/bash.html`

    - 学习并下载 GNU bash shell 最新版本的起点。

- `/usr/doc/bash-doc*`

    - 关于 bash 的在线技术信息宝库。

- `http://sunsite.auc.dk/zsh/`

    - zsh shell 的主页。

- `http://www.oase-shareware.org/shell/articles/ignorantsguide.html`

    - Heiner Steven 的 shell 编程文章集合。这是初学者 shell 编程的一个很好的提示和技巧集合。

### 键盘和控制台 HOWTO

Andries Brouwer 关于在 Linux 下使用键盘和控制台的指南。可在 `/usr/doc/HOWTO` 目录下找到。你可以在 http://www.linuxdoc.org 找到最新版本。

### XF86-SVGA 手册页

包含有关选项和设置的指南，例如 XF86-SVGA X11 服务器的虚拟屏幕。请参阅你笔记本的 X11 服务器的其他手册页，以了解可用的虚拟屏幕尺寸。

### http://www.xfree86.org

XFree86 X11 发行版的主页。这是了解 Linux 最新 X11 发行版的最佳地点。你还可以了解如何为这项伟大的事业做出贡献！

### Videomodes.doc

Eric S. Raymond 的 XFree86 视频定时 HOWTO，一篇关于为你的笔记本图形芯片组制作“调整过”的模型线论述。可在 `/usr/X11R6/lib/X11/doc` 目录下找到。

### http://www.plig.org/xwinman/

关于不同窗口管理器信息的汇编，也是开始学习一些真正酷炫的替代桌面的绝佳起点。

# 第 10 章：输入问题

- Linux 输入软件
- 在控制台中使用鼠标
- 配置触控板
- 使用摇杆
- 键盘和国际化
- 使用麦克风
- 视频捕获
- 资源信息
