

颜色深度。您的 XF86Config 文件的 Screen（屏幕）部分应为每种颜色深度都包含 Display（显示）子节条目。例如：

```
Section "Screen"
Driver "svga"
Device "My Video Card"
Monitor "LCD Panel 1024x768"
Subsection "Display"
Depth 8
Modes "1024x768" "800x600" "640x480"
EndSubsection
Subsection "Display"
Depth 16
Modes "1024x768" "800x600" "640x480"
EndSubsection
Subsection "Display"
Depth 24
Modes "1024x768" "800x600" "640x480"
EndSubsection
EndSection
```

这些条目展示了 8 位平面（256 种颜色）、16 位（数千种颜色）和 24 位（数百万种颜色）颜色深度的配置，每种颜色深度对应不同的分辨率。使用带有 bpp（位平面）选项的 startx 可以启动具有数百万种颜色的 X11 会话：

```
# startx -- -bpp 24
```

按下回车键后，X 将启动。X 服务器会确定笔记本电脑是否支持数百万种颜色的 1024×768 分辨率。如果不行，则会尝试下一个分辨率，依此类推，直到找到一种可用的设置。理想情况下，您应该了解笔记本电脑显示屏在各种颜色深度下的局限性，然后定制系统的 XF86Config 文件以支持每种分辨率和颜色深度。一些笔记本电脑，如 Sony 的 505TX 和 TR 系列，还可以使用 XF86Config 的 Device（设备）部分中的特殊选项条目来支持这些模式。例如：

```
Option "lcd_center"
Option "no_stretch"
```

这些条目在 `/usr/X11R6/lib/X11/doc` 目录下的 README.neo 文件中（505s 使用 NeoMagic 图形芯片组）中有详细说明，它们禁用了低分辨率模式的拉伸，并将低分辨率屏幕居中显示在笔记本电脑的 LCD 上。这使得在使用分辨率和高颜色深度的各种组合时，能够提供更佳的字体显示效果。这也是阅读笔记本电脑图形芯片组文档的另一个良好理由。使用不同的选项可能导致显示效果是扭曲还是清晰可读的巨大差异！

# 选择窗口管理器

X11 为您的 X 会话提供了各种服务器和客户端。可移动窗口、滚动条、拖放、按钮、对话框、图标以及现代图形化 Linux 接口的其他许多神奇之处，都归功于一种名为 *window manager*（窗口管理器）的特殊 X11 客户端。得益于世界各地数千名程序员的努力，X11 拥有成百上千的窗口管理器。能够根据需求选择窗口管理器是选择 Linux、X11 和开源软件的另一个好理由，同时也可以避免使用那些将您锁定在可能并不适合您的界面上的专有系统。

为您的笔记本电脑选择窗口管理器时，需要考虑诸多因素：

-   **RAM 使用量。** 窗口管理器需要和使用多少内存？
-   **CPU 资源。** 运行窗口管理器需要多少 CPU 处理能力？
-   **硬盘空间。** 窗口管理器及其相关软件占用多大的空间？
-   **关联客户端。** 窗口管理器包含多少个客户端，有多少客户端能与其良好协作或利用其特殊功能？
-   **功能。** 支持哪些特殊功能，如拖放、图标坞、菜单或面板？
-   **易用性。** 使用、配置和维护窗口管理器及其相关软件有多容易？
-   **安全性。** 窗口管理器是否存在安全漏洞？
-   **支持。** 有多少人正在开发这个窗口管理器？它是否包含在大多数主要 Linux 发行版中？是否有新的客户端正在为其开发？
-   **“酷炫”因素。** 当其他移动 Linux X11 爱好者看到您的笔记本电脑显示屏时，是否会羡慕得流口水？

XFree86 附带一个窗口管理器——Tab 窗口管理器（*twm*），但大多数 Linux 发行版现在都包含支持 GNOME 的 Enlightenment 窗口管理器和 K 桌面环境。表 9.3 列出了 X11 和 Linux 可用的众多流行窗口管理器。

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

# 最大化您的屏幕空间

您可以在 X11 会话中利用的一个窗口管理器功能是使用额外的显示屏，即 *virtual desktop*（虚拟桌面）。并非所有窗口管理器（尤其是那些为极简主义者设计的管理器）都提供此功能。传统的 X11 窗口管理器，如 *fvwm* 和 *olvwm*，其名称中包含了关于此功能的暗示（即 *v*）。当使用支持虚拟桌面的窗口管理器时，您通常会发现一个被称为 *pager*（分页器）的小窗口、对话框或按钮组，用于在各界面之间进行导航。

使用虚拟桌面是整理工作区域（也许按功能分类）的好方法。例如，您可以在一个桌面上进行文字处理，在另一个窗口中进行电子邮件处理，在第三个窗口中浏览网页，等等。图 9.3 显示了一个支持四个虚拟桌面的典型分页器，其中两个桌面正在运行应用程序。

要导航到不同的桌面，点击其中一个方块。您的整个显示屏将改变以反映新的桌面。几乎大多数窗口管理器都允许您配置 X11 会话中使用的虚拟桌面数量。传统的桌面，如 *fvwm*，使用一个名为 *resource file*（资源文件）的文本来包含仅在 X 会话之间才能更改的设置。较新的 X11 窗口管理器和桌面环境，如 KDE，提供了图形界面配置工具。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_253_0.png)

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_254_0.png)

> 图 9.4 KDE 的面板配置工具可用于更改多项面板设置，包括面板分页器上可用的虚拟桌面按钮数量。

以便在您的 X 会话中允许更改。例如，KDE 的 kpanel 配置工具（如图 9.4 所示）允许您将虚拟桌面的数量从两个更改为八个。

与运行多个 X 会话一样，在不同的虚拟控制台运行大量应用程序可能会消耗系统资源，但您将能够快速在应用程序之间切换，并在不同的显示面上整理您的工作。

# 使用外部监视器

如果您确实需要额外的屏幕空间，或者希望使用更大的显示器，您可以将笔记本连接到外部监视器（只要您的笔记本或扩展坞提供外部视频输出端口）。您可能需要在重启时修改笔记本的 BIOS 以启用外部显示器的使用。您可能还需要通过笔记本电脑键盘上的特殊 Fn 键组合来切换笔记本 LCD 显示屏的开启或关闭。

如果您可以在外部监视器上显示仅文本的 Linux 控制台，但无法显示 X11 会话，请检查是否需要编辑 XF86Config 以包含特殊

