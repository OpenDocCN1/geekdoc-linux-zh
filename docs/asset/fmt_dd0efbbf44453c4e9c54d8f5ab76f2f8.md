
| README.clkprog | 外部视频时钟设置程序的编程信息 |
| README.cyrix | 关于 Cyrix 芯片组的信息 |
| README.epson | 关于 EPSON SPC8110（笔记本）芯片组的信息 |
| README.mouse | 关于 XFree86 的 X11 鼠标支持的详细信息 |
| README.neo | 关于 NeoMagic（笔记本）芯片组的信息 |
| README.rendition | 关于 Rendition 芯片组的信息 |
| README.trident | Trident 芯片组用户的说明 |
| README.tseng | Tseng 芯片组用户的说明 |
| RELNOTES | XFree86 的权威发行说明 |
| ServersOnly | 构建 XFree86 X 服务器时目录应有的外观 |
| VGADriver.Doc | 在 XFree86 中添加 SVGA 或 VGA 驱动的 HOWTO |
| VideoModes.doc | Eric S. Raymond 关于构建 XF86Config modelines 的综合论述 |
| xinput | XFree86 中输入设备（如操纵杆）支持的一般信息 |

在使用 `xf86config` 命令重新配置 X11 之前，以 root 操作员身份登录，并先进行备份，如下所示：

```
# cp /etc/XF86Config /etc/XF86Config.org
```

然后您可以通过在终端窗口的命令行中输入以下命令来启动该命令：

```
# xf86config
```

按 Enter 后，按照提示配置您的显卡和监视器以供 X11 使用。`xf86config` 命令会在 `/etc` 目录中生成一个新的 `XF86Config` 文件。

## XF86Config 文件

`XF86Config` 文件用于将字体、键盘、鼠标、视频芯片组、监视器功能和颜色深度设置信息正确地提供给您选择的 X11 显示服务器。`XF86Config` 是一个单一的文本文件，由表 3.2 中总结的几个部分组成。

您可以使用 `less` 命令浏览系统的 `XF86Config` 文件（在第 4 小时“阅读和导航命令”中讨论）。在终端的命令行中，使用 `less`，后跟 `XF86Config` 的路径，如下所示：

```
# less /etc/XF86Config
```

然后您可以使用光标键浏览文件。阅读完毕后按 Q 键。

### 表 3.2 XF86Config 文件的主要部分

| 部分 | 用途 |
|---|---|
| Files | 告诉 X 服务器颜色、字体或特定软件模块的位置 |
| Module | 告诉 X 服务器应加载哪些特殊模块 |
| ServerFlags | 包含用于允许或禁止特殊操作的开关标志，例如核心转储、键盘服务器关闭、视频模式切换、视频调谐以及鼠标和键盘配置 |
| Keyboard | 告诉 X 服务器预期使用什么键盘以及使用什么设置 |
| Pointer | 告诉 X 服务器使用什么指针以及按钮如何处理 |
| Xinput | 用于图形板、数位笔等设备的特殊部分 |
| Monitor | 指定监视器的详细信息和设置，例如名称、水平同步范围、垂直同步范围和 modelines（每个视频分辨率一个，例如 640x480、800x600、1024x768 等） |
| Device | 提供有关视频芯片组的详细信息，例如 RAM、时钟芯片等 |
| Screen | 指定要使用的 X 服务器、颜色深度（例如每像素 8、16、24 或 32 位）、屏幕尺寸（例如 640x480、800x600、1024x768 等）以及虚拟屏幕的大小 |

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_67_0.png)

> 不要使用拥有与你不同的显卡和显示器的某人的 `XF86Config`！不正确的设置可能会损坏你的显示器。不要使用超出显示器规格的显示器设置。你已被警告！此规则的唯一例外可能是拥有完全相同组件的 PC 笔记本电脑用户。

在你尝试使用新的 `XF86Config` 设置启动 X11 会话之前，以 root 操作员身份，使用你喜欢的文本编辑器打开该文件，禁用换行，并检查设置。尤其对于笔记本电脑用户来说，执行此操作至关重要，以检查创建的设置，启用或禁用某些 X 服务器选项，输入正确的视频内存量，并微调显示器设置。

## XF86Config 文件部分

### Files 部分

`Files` 部分告诉 X 服务器颜色名称数据库和系统字体的位置。

### XF86Config ServerFlags 部分

本节的几个部分可用于配置由你的 XFree86 X 服务器启用的特殊操作。通过删除特定标志前面的井号（`#`）来启用某个操作。大多数用户不会禁用 `DontZap` 功能，因为它提供了一种快速退出 X 会话的方法。如果你在单一视频分辨率下使用 X，例如 800x600 像素，则可以禁用 `DontZap` 功能。

### XF86Config Keyboard 部分

`Keyboard` 部分告诉 X 服务器期望使用何种类型的键盘以及使用的设置，例如语言类型、键字符布局和制造商。

### XF86Config Pointer 部分

`Pointer` 部分告诉 X 服务器使用什么指针或鼠标以及按钮如何处理。某些 `Protocol` 设置对于串行鼠标为 `Auto`，对于总线鼠标为 `BusMouse`。`Device` 条目 `/dev/mouse` 是指向实际设备（如串行鼠标的 `/dev/ttyS0`）的符号链接。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_67_1.png)

> 双按钮鼠标用户 definitely 希望启用三按钮仿真器，其中同时按下两个按钮会模拟按下中间按钮或按钮 2。按钮 2 的常见用途是粘贴文本或图形。有关配置鼠标的更多信息，请参阅 `/usr/X11R6/lib/X11/doc` 目录下的文件 `README.mouse`。

### XF86Config Monitor 部分

尽管 `XF86Config` 文件的前几个部分很容易理解，如果你是 XFree86 用户，其初始 `XF86Config` 文件无法工作，请特别注意 `Monitor` 部分、`Device` 部分和 `Screen` 部分。`Monitor` 部分包含有关你的显示器的具体细节和设置，例如显示器的名称、其水平和垂直同步范围以及关键的 `modelines`（每个视频分辨率一个，例如 640×480、800×600、1024×768 等）。理解 `modeline` 是微调 X11 显示的关键。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_68_0.png)

> 在微调 `XF86Config` 文件中的 `modelines` 之前，请先参阅 `/usr/X11R6/lib/X11/doc` 目录下的文件 `VideoModes.doc` 和 `README.Config` 以获取最佳细节。另一个不错的教程是 `/usr/doc/HOWTO` 目录下的 `XFree86-Video-Timings-HOWTO`。

`modeline` 的基本部分是 10 个不同的值，表示以下内容（从左到右）：

- 屏幕分辨率的标签，例如 800×600
- 视频频率，单位为 MHz
- 显示器每行可见的点数
- 开始水平回扫值（视频同步脉冲开始前脉冲数）
- 结束水平回扫值（同步脉冲结束）
- 显示器上可见和不可见点的总数
- 垂直显示结束值，或显示器上可见的点行数
- 开始垂直回扫值（同步脉冲开始前行数）
- 结束垂直回扫值（同步脉冲结束时的行数）
- 垂直总计值，或显示器上可见和不可见行的总数

### XF86Config Device 部分

`Device` 部分包含有关你的视频芯片组的详细信息，例如 RAM、时钟芯片等。请注意，即使你告诉 `xf86config` 或 `XF86Setup` 你有两兆字节的视频 RAM，这些值也会用井号（`#`）注释掉。要正确配置 X，你需要在 `XF86Config` 文件的这一部分中删除 `VideoRam` 设置前面的井号。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_69_0.png)

> 你 `XF86Config` 文件的这一部分至关重要。设备定义用于告诉 X 服务器确切支持何种类型的视频芯片组和选项。有关设备标识符和选项的列表，请参阅与你的芯片组对应的 `/usr/X11R6/lib/X11/doc` 目录下的 README 文件。

### XF86Config Screen 部分

`Screen` 部分说明使用哪个 X 服务器、颜色深度（例如每像素 8、16、24 或 32 位）、屏幕尺寸（例如 640×480、800×600 或 1024×768 等）以及虚拟屏幕的大小。

本节包含对你选择的 X 服务器（`XF86_SVGA` 或其他彩色服务器、4 位和 16 色的 `XF86_VGA16` 服务器，或单色服务器 `XF86_Mono`）的说明，说明应支持哪些分辨率和虚拟屏幕大小。
