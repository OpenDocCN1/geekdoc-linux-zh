
## XF86Config 模块部分

如你所见，X11 的其他字体安装在 `/usr/share/fonts` 目录下。ISO8859-2 字体是近 400 个中欧（或拉丁语 2）字体集合的一部分，支持近 12 种斯拉夫语和中欧语言的字符编码。

你可以使用 `xfontsel` 客户端来验证这些字体的包含情况和可用性。在终端窗口的命令行中，请像这样使用 `xfontsel`：

```
# xfontsel
```

你将看到一个窗口（如图 4.10 所示），通过点击“fmly”可以选择不同的字体厂商和字体族。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_130_0.png)

`Module` 部分用于加载服务器和渲染支持，并指定从 `/usr/X11R6/lib/modules` 目录中加载的模块名称：

```
Section "Module"
	Load "GLCore"
	Load "dbe"
	Load "dri"
	Load "extmod"
	Load "glx"
	Load "pex5"
	Load "record"
	Load "xie"
	Load "type1"
	Load "freetype"
EndSection
```

在这个示例中，几乎所有渲染和绘图支持库都被加载了，同时还包括对 Type1 和 TrueType 字体的支持。这些软件库位于 `/usr/X11R6/lib/modules/extensions` 目录下，并非所有库对于你的 X11 窗口管理器的正常窗口支持都是必需的。例如，如果你不使用加速的 3D 显卡，请不要加载 `dri` 模块。

这种以可加载模块形式为新型图形硬件提供支持的新方法已被一些制造商采用。例如，Voodoo 和 Banshee 系列显卡制造商 3dfx Interactive, Inc. 提供了许多链接和模块来支持其在 XFree86 4.0.1 下的新硬件。请访问 `http://linux.3dfx.com` 获取更多详细信息。

### XF86Config ServerFlags 部分

`ServerFlags` 部分可用于配置你的 XFree86 X 服务器允许的特殊操作。要启用某个特定操作，请包含 `Option` 关键字，后跟所需的选项。某些选项通常不应启用，例如禁用结束服务器会话的能力（`DontZap`）：

```
Section "ServerFlags"
#   Option    "DontZap"
#   Option    "DontZoom"
#   Option    "blank time"  "10"    # 10 分钟
    Option    "standby time"  "20"
    Option    "suspend time"  "30"
    Option    "off time"      "60"
#   Option    "NoPM"
    Option    "AllowMouseOpenFail"
EndSection
```

并非显示了所有可用选项。如果你在单一视频分辨率（例如 800×600 像素）下使用 X，则可能禁用 `DontZoom` 功能。然而，你应当注意控制屏幕保护（`blank time`）和 DPMS 的新选项。你可以使用这些设置来控制显示器以节省电源。`NoPM` 选项禁用 DPMS。`AllowMouseOpenFail` 选项允许服务器在没有指针设备的情况下启动。

### XF86Config InputDevice 部分

`InputDevice` 部分告知 X 服务器预期的键盘和鼠标类型。XFree86 3.3.6 格式的 Keyboard 和 Pointer 部分仍被识别以保持兼容性，但在你的 `XF86Config` 中应使用新的 `InputDevice` 部分。

```
# InputDevice (键盘)
Section "InputDevice"
    Identifier    "Keyboard0"
    Driver "keyboard"
    Option "XkbLayout" "us"
EndSection

# InputDevice (PS/2 指针)
Section "InputDevice"
Identifier "Mouse0"
Driver "mouse"
Option "auto"
Option "Device" "/dev/mouse"
Option "Protocol" "PS/2"
EndSection
```

在这个示例中，定义了一个使用美式布局的单个键盘和一个使用 PS/2 协议的单个鼠标，供 X 会话期间使用。你可以定义多个设备供使用。如果系统具有即插即用鼠标检测功能，则可以使用 `auto` 协议选项。

要定义 USB 鼠标，请使用 IMPS/2 设备选项（因为 Linux 支持 PS/2 鼠标初始化），并指向 USB 鼠标设备，如下所示：

```
Section "InputDevice"
Identifier "Mouse0"
Driver "mouse"
Option "Protocol" "IMPS/2"
Option "Device" "/dev/input/mice"
EndSection
```

请注意，你还需要在启动 X 之前以正确的设置运行 `gpm` 守护进程：

```
# gpm -t ps2 -m /dev/input/mice
```

当然，安装 USB 鼠标的最佳解决方案是使用 `mouseconfig` 命令。双键鼠标用户肯定想要启用三键模拟功能，该功能通过同时按下两个按键来模拟中间键（或按键 2）的按压。按键 2 的一个常见用途是粘贴文本或图形。有关配置鼠标的更多信息，请查看 `/usr/X11R6/lib/X11/doc` 目录下的 `README.mouse` 文件。有关 USB 输入设备的信息可以在 `/usr/share/doc/kernel-doc-2.2.16/usb` 目录下的 `input.txt` 文件中找到。

## XF86Config 监视器部分

监视器部分包含详细信息，如监视器的标识符、制造商名称、型号名称以及水平和垂直同步范围。请注意，旧的模型行（每个视频分辨率一个）不再需要！XFree86 服务器应自动计算正确的时序和频率！

```
Section   "Monitor"
    Identifier "LCD Panel 1024x768"
    VendorName "Unknown"
    ModelName  "Unknown"
    HorizSync  31.5-48.5
    VertRefresh 60
EndSection
```

然而，如果你需要在监视器部分中包含模型行，你可以这样做。这在需要支持非品牌监视器或微调你的设置时特别有用。

模型行的基本部分代表不同的值（从左到右）：

- 屏幕分辨率的标签，例如 800x600
- 以 MHz 为单位的视频频率（DotClock）
- 显示器上每行可见点数
- 水平消隐开始值（视频同步脉冲开始前的脉冲数）
- 水平消隐结束值（同步脉冲的结束）
- 显示器上可见和不可见的总点数
- 垂直显示结束值（显示器上可见的行数）
- 垂直消隐开始值（同步脉冲开始前的行数）
- 垂直消隐结束值（同步脉冲结束处的行数）
- 垂直总数值（显示器上可见和不可见的总行数）

```
Mode     "1024x768"
        DotClock    45
        HTimings    1024 1048 1208 1264
        VTimings    768 776 784 817
EndMode
```

此示例定义了一个用于 1024×768 显示器的模型行（可能是笔记本电脑或 LCD 面板监视器）。当需要为超出常规显示器范围的监视器或显示设备制作自定义模型行时，可能会出现一些问题。例如，如果你的显示器是 1024×480（例如用于索尼 ClXS 笔记本电脑）怎么办？在这种情况下，你可以尝试使用 Andreas Bohne 基于 Web 的模型行计算器，地址为 http://www.dkfz-heidelberg.de/spec/linux/modeline/。另一个可能更灵活的工具是 Anders Ostreim 的模型行命令，可在 http://home.kvalito.no/~bagnthor/files/files.shtml 找到。

## XF86Config 设备部分

设备部分详细说明了你的视频芯片组、用于芯片组支持的适当驱动程序、显卡内存、时钟芯片的频率设置以及其他选项。你的 `XF86Config` 文件中的此部分至关重要——设备定义用于告知 X 服务器确切支持何种类型的视频芯片组和选项。请注意，你的计算机的设备部分和驱动项肯定会与此（针对 NeoMagic 笔记本电脑）不同：

```
# 设备
Section "Device"
    Identifier    "NeoMagic Corporation||MagicMedia 256AV"
    Driver        "neomagic"
#   VideoRam      2048
#   Option      "intern_disp"
#   Option      "extern_disp"
#   Option      "lcd_center"
#   Option      "no_stretch"
EndSection
```

你的 `XF86Config` 中可能还定义了多个设备部分。当你系统中安装了多于一张显卡并希望使用一个或多个显示器时，会使用这种方法。还要注意，设备部分中可能包含各种 Option 条目。

根据指定的驱动程序和你的图形芯片组，你可能会发现有许多可用选项。在示例中，`extern_disp` 选项可用于启用将 X 会话显示在外部监视器上（很可能是通过启用到监视器端口的信号）。你应始终查阅驱动程序文档，位于 `/usr/X11R6/lib/X11/doc` 目录下的 README 文件、手册页或通过 http://www.xfree86.org。

XFree86 4.0.1 附带的一些驱动程序列在表 4.2 中（该表源自名为 Status 的文件，位于 `/usr/X11R6/lib/X11/doc` 目录下）。请注意，该表反映的是 4.0.1 版本的卡片支持情况。更多卡片的支将在后续版本中提供。

**表 4.2 XFree86 4.0.1 驱动程序和受支持的显卡**

| 驱动程序 | 显卡 |
| :--- | :--- |
| apm | Alliance AT24, 25, 3D |
| ati | ATI Mach64 显卡及其他 |
| chips | C&T 65520, 65525, 65530, 65535, 65540, 65545, 65546, 65548, 65550, 65554, 69000, 64200, 64300 |
| cirrus | Cirrus Logic Alpine 和 Laguna 芯片组 |

