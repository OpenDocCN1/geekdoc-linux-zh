
### XFree86-W32 — (版本 3.3.3.1, 1,793K)

XFree86-W32 是适用于基于 ET4000/W32 芯片构建的显卡的 X 服务器，包括 Genoa 8900 Phantom 32i、Hercules Dynamite、LeadTek WinFast S200、Sigma Concorde、STB LightSpeed、TechWorks Thunderbolt 和 ViewTop PCI。如果你正在安装 X Window 系统，而你的 VGA 显卡基于 ET4000/W32 芯片组，则应安装 XFree86-W32。你还需要安装 XFree86 软件包、一个或多个 XFree86 字体软件包、X11R6-contrib 软件包、`Xconfigurator` 软件包和 XFree86-libs 软件包。最后，如果你要开发作为 X 客户端运行的应用程序，还需要安装 XFree86-devel。

### XFree86-XF86Setup — (版本 3.3.3.1, 596K)

`XF86Setup` 是一个用于设置和配置 XFree86 服务器的图形用户界面配置工具。`XF86Setup` 可以配置视频设置、键盘布局、鼠标类型等。`XF86Setup` 不能用于非 VGA 兼容的显卡、固定频率显示器或 OS/2。如果你以前使用过 `XF86Setup`，并且更愿意继续使用它来配置 X 服务器，请安装 `XF86Setup`。如果你对 `XF86Setup` 没有偏好，则应安装并使用 `Xconfigurator`，这是 Red Hat 为 X Window 系统提供的图形用户界面配置工具。

### XFree86-Xnest — (版本 3.3.3.1, 2,242K)

`Xnest` 是一个运行在 X 窗口中的 X Window 系统服务器。`Xnest` 是一个“嵌套”窗口服务器，实际上是真实 X 服务器的客户端；真实 X 服务器为 `Xnest` 管理窗口和图形请求，而 `Xnest` 为自己的客户端管理窗口和图形请求。如果你需要一个作为真实 X 服务器客户端运行的 X 服务器（也许用于测试目的），则需要安装 `Xnest`。

### XFree86-Xvfb — (版本 3.3.3.1, 2,707K)

`Xvfb`（X 虚拟帧缓冲区）是一个 X Window 系统服务器，能够运行在没有显示硬件和物理输入设备的机器上。`Xvfb` 使用虚拟内存模拟一个哑帧缓冲区。`Xvfb` 不打开任何设备，但在其他方面就像一个 X 显示器。`Xvfb` 通常用于测试服务器。使用 `Xvfb`，可以在不使用支持所需深度的真实硬件的情况下，测试任意深度的 `mfb` 或 `cfb` 代码。`Xvfb` 还用于测试 X 客户端在不常见深度和屏幕配置下的表现，以 `Xvfb` 作为后台渲染引擎进行批处理，进行负载测试，帮助将 X 服务器移植到新平台，并为那些实际上并不需要 X 服务器却坚持要有一个的程序提供一种不显眼的运行方式。如果你需要测试 X 服务器或 X 客户端，你可能希望为此安装 `Xvfb`。

### Xconfigurator — (版本 4.1.3, 433K)

[W][S]

`Xconfigurator` 是一个全屏、菜单驱动的程序，引导你完成 X 服务器的设置。`Xconfigurator` 基于 XFree86 的实用程序 `xf86config` 的源代码。如果你正在安装 X Window 系统，则应安装 `Xconfigurator`。

## X

本节包含与 X Window 系统图形用户界面相关的软件包。

### X11R6-contrib — (版本 3.3.2, 474K)

[W][S]

如果你想使用 X Window 系统，应安装 X11R6-contrib。此软件包包含来自 X Window 系统第 11 版第 6 次发布 contrib 磁带中的许多有用程序。这些由不同用户贡献的程序包括 `listres`、`xbitf`、`xedit`、`xeyes`、`xcalc`、`xload` 和 `xman` 等。你还需要安装 XFree86 软件包、与你的显卡对应的 XFree86 软件包、一个或多个 XFree86 字体软件包、`Xconfigurator` 软件包和 XFree86-libs 软件包。最后，如果你要开发

### XFree86-100dpi-fonts — (Version 3.3.3.1, 1,228K)

如果你要使用 X Window System，并且你有一台能够支持 100 dpi 的高分辨率显示器，你应该安装 XFree86-100dpi-fonts。该软件包包含大多数 Linux 系统上使用的 100 dpi 字体集。如果你要安装 X Window System，你还需要安装 XFree86 软件包、对应你显卡的 XFree86 软件包、X11R6-contrib 软件包、`Xconfigurator` 软件包以及 XFree86-libs 软件包。如果你需要显示某些字体，你可能还需要安装其他 XFree86 字体软件包。最后，如果你要开发作为 X 客户端运行的应用程序，你还需要安装 XFree86-devel 软件包。

### XFree86 — (Version 3.3.3.1, 14,458K)

[W][S]

如果你想在你的机器上安装 X Window System（TM），你需要安装 XFree86。X Window System 提供了开发图形用户界面的基础技术。简单来说，X 在用户屏幕上绘制 GUI 的元素并建立将用户交互发送回应用程序的方法。X 还支持远程应用程序部署 — 在另一台计算机上运行应用程序，同时在你的机器上查看输入/输出。X 是一个功能强大的环境，支持许多不同的应用程序，例如游戏、编程工具、图形程序、文本编辑器等。XFree86 是在 Linux 以及其他平台上运行的 X 版本。该软件包包含 X 工作站的基本字体、程序和文档。然而，该软件包不提供你用来驱动视频硬件的程序。要控制你的显卡，你需要安装对应你计算机显卡的特定 X 服务器软件包。除了安装此软件包之外，你还需要安装对应你显卡的 XFree86 软件包、X11R6-contrib 软件包、`Xconfigurator` 软件包以及 XFree86-libs 软件包。你可能还需要安装其中一个 XFree86 字体软件包。最后，如果你要开发作为 X 客户端运行的应用程序，你还需要安装 XFree86-devel。

### XFree86-75dpi-fonts — (Version 3.3.3.1, 1,060K)

[W][S]

XFree86-75dpi-fonts 包含大多数 X Window System 上使用的 75 dpi 字体。如果你要使用 X Window System，你应该安装此软件包，除非你有一台可以支持 100 dpi 分辨率的显示器。在这种情况下，你可能更喜欢 XFree86-100dpi-fonts 软件包中提供的 100dpi 字体。你可能还需要安装其他 XFree86 字体软件包。要安装 X Window System，你需要安装 XFree86 软件包、对应你显卡的 XFree86 软件包、X11R6-contrib 软件包、`Xconfigurator` 软件包以及 XFree86-libs 软件包。最后，如果你要开发作为 X 客户端运行的应用程序，你还需要安装 XFree86-devel 软件包。

### XFree86-ISO8859-2 — (Version 1.0, 77K)

如果你使用 X Window System 并且想要显示中欧字体，你应该安装 XFree86-ISO8859-2 软件包。该软件包包含一套符合 ISO 8859-2 标准的完整中欧字体。此软件包中包含的字体免费分发，可自由使用，但须遵守随附的版权声明：Copyright (c) 1996, 1997 BIZNET Poland, Inc. All Rights Reserved. BIZNET 是 BIZNET Poland, Inc. 的注册商标。你可能还需要安装一个或多个其他 XFree86 字体软件包。要安装 X Window System，你需要安装 XFree86 软件包、对应你显卡的 XFree86 软件包、X11R6-contrib 软件包、`Xconfigurator` 软件包以及 XFree86-libs 软件包。最后，如果你要开发作为 X 客户端运行的应用程序，你还需要安装 XFree86-devel。

### XFree86-ISO8859-2-100dpi-fonts — (Version 1.0, 1,003K)
