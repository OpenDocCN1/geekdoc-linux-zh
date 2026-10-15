
| DontZoom | 通常，组合键 `Ctrl+Alt+KeypadPlus` 会在你的 X 服务器可用的配置屏幕分辨率之间循环，每次点击都会增加分辨率，而 `Ctrl+Alt+KeypadMinus` 同样被用于降低分辨率。如果应用程序由于其他目的需要这些组合键，请取消此项的注释，以让 X Windows 忽略这些组合键并将它们传递给你的应用程序。 |

| DisableVidModeExtension | 该指令防止使用 `xvidtune` 客户端对你的视频显示进行调优（我们未在书中讨论该客户端；可以在打开的窗口中输入 `man xvidtune` 查找该程序的文档）。无需取消此项的注释，你可以默认保持其注释。 |

| AllowNonLocalXvidtune | 与前面的指令相关，这允许非本地（换句话说，在网络某处的）`xvidtune` 客户端访问你的 X Windows 系统。出于安全考虑，最好保持此指令禁用状态。 |

| DisableModInDev | 通过启用此指令，在 X 运行时将无法动态更改键盘和鼠标设置。 |

| AllowNonLocalModInDev | 取消此指令的注释允许非本地计算机更改你的键盘和鼠标设置。除非你有需要，否则启用此指令是不明智的。 |

## Keyboard

正如所预期的，Keyboard 节指定了与键盘功能相关的信息，包括键盘类型和协议。示例部分如下：

### "Keyboard*" 节

+ *Protocol "Standard*"

* AutoRepeat 500 5

* ServerNumLock

* Xleds 1 2 3

## The XF86Config 文件 201

```
# LeftAlt Meta
# RightAlt ModeShift
# RightCtl Compose
# ScrollLock ModeLock
```

```
XkbDisable
```

```
# XkbModel "pc102"
# XkbModel "microsoft"
```

```
# XkbLayout "de"
```

```
# XkbOptions "ctrl:swapcaps"
```

```
# XkbModel "pc101"
# XkbLayout "us"
# XkbOptions ""
```

```
XkbKeymap "free86(us)"
```

EndSection

这看起来是一个复杂的节，但正如表 9.3 所示，实际上非常简单：

## 表 9.3：Keyboard 指令

| Directive | 效果 |

| --- | --- |

| Protocol | 在 Red Hat Linux 5 中此指令只有一个有效值：Standard。在其他 Linux 版本中，此指令可以取其他值。确保此指令已取消注释并分配了值。 |

| AutoRepeat | 该指令用于指定按住键在开始自动重复之前等待多久，以及键重复的频率。在我们的示例中，`AutoRepeat 500 5` 意味着所有值都是毫秒。这意味着在按键按住 500 毫秒（半秒）后开始自动重复，然后按键每 5 毫秒重复一次。 |

| ServerNumLock | 通常，此指令可以保持注释状态。它指定由服务器而非应用程序来处理 NumLock 键。该指令仅对于某些需要它的 X Windows 应用程序是必要的。在标准的 Linux 发行版中，你不需要它。 |

## 表 9.3 继续：Keyboard 指令

| Directive | 效果 |

| :--- | :--- |

| Xleds | 该指令指定用户可以使用 `xset` 命令控制哪些键盘 LED。保持其注释状态可能可能是个好主意，这也是默认设置。 |

| LeftAlt, RightAlt, RightCtrl, and ScrollLock | Windows 最初运行在 Unix 工作站上，其键盘与标准 PC 键盘不同。这些键盘包含了 Meta、RightShift、Compose 和 Model 等特殊键。如果你发现你的应用程序需要使用这些键（这对于大多数标准应用程序来说不太可能），那么请取消这些指令的注释。 |

| XkbDisable | 该指令用于禁用 XKB 扩展。如果你不使用 XKB，可以保持其注释状态。 |

## Pointer

Pointer 节处理鼠标相关的配置。在这里你设置鼠标的类型、鼠标连接的端口以及与按钮相关的行为。

### "Pointer*" 节

+ * Protocol "PS/2"

* BaudRate 9600

+ * Device "/dev/psaux"

+ * XkbModel "pc102" 

+ * XkbLayout "us"

+ * XkbOptions "ctrl:swapcaps"

+ * XkbKeymap "free86(us)"

* SampleRate 150

Emulate3Buttons

Emulate3Timeout 50

# ChordMiddle

EndSection

## 表 9.4：Pointer 指令

| Directive | 效果 |

| --- | --- |

| Protocol | 该指令指定你使用的鼠标类型。可能的值包括用于总线鼠标的 BusMouse、用于 PS2 的 PS2，以及一系列串口鼠标：GlidePoint、IntelliMouse、Logitech、Microsoft 等。通常今天常见的类型是 PS2 和 Microsoft。 |

| Device | 该指令用于指定鼠标连接的设备端口。对于大多数 Linux 发行版，如果你在安装发行版时正确配置了鼠标，`/dev/mouse` 将指向你的鼠标并可以使用它。如果 `/dev/mouse` 未指向你的鼠标，请为 PS2 端口指定 `/dev/psaux`，为 Windows 的 COM1 指定 `/dev/ttyS0`，为 COM2 指定 `/dev/ttyS1`。 |

| BaudRate | 该指令仅用于少数 Logitech 鼠标。查看你的鼠标文档。 |

| SampleRate | 该指令仅用于少数 Logitech 鼠标。查看你的鼠标文档。 |

| Emulate3Buttons | 该指令应用于兼容双键的鼠标。取消注释后，同时点击左键和右键将模拟三键鼠标的中间键。由于 Windows 依赖于三个键的存在，因此对于双键协议鼠标启用此项是明智的。 |

| Emulate3Timeout | 该指令用于指定两个鼠标键点击的时间间隔必须多近才能被算作同时点击；此值仅在 Emulate3Buttons 启用时有效。默认设置为 50。如果很难同时按下两个鼠标键，可以通过分配更高的值来延长时间。该指令假设单位是毫秒，并且你应该只指定数值，而不包含单位（换句话说，`Emulate3Timeout 100 ms` 是无效的）。 |

| ChordMiddle | 该指令用于启用某些三键 Logitech 鼠标的中间键。如果你有一个 Logitech 鼠标且中间键不起作用，请尝试启用此指令。 |

## Monitor 显示器

到目前为止，我们看到的配置指令大多是自解释其义的，并不使用。当涉及到配置显示器等视频硬件时，情况就会变得复杂。让我们来看示例配置中的 Monitor（Monitor）部分：

Section "monitor"

Identifier "monitor"

VendorName "LG"

ModelName "StudioWorks"

HorizSync 30-70

VertRefresh 50-160

```
# 640x400 @ 70 Hz, 31.5 kHz hsync
Multiline "640x400" 25.175 664 760 800 400 409 411 450
# 640x400 @ 60 Hz, 31.5 kHz hsync
Multiline "640x480" 25.175 664 760 800 480 491 493 525
# 800x600 @ 56 Hz, 35.15 kHz hsync
Multiline "800x600" 36 800 824 896 1024 600 601 603 625
# 1024x768 @ 87 Hz interlaced, 35.5 kHz hsync
Multiline "1024x768" 44.9 1024 1048 1208 1264 768 776 784 817
```

```
# 640x400 @ 85 Hz, 37.86 kHz hsync
Multiline "640x400" 31.5 640 672 736 832 400 401 404 455
-VSync
# 640x480 @ 72 Hz, 36.5 kHz hsync
Multiline "640x480" 31.5 640 680 720 864 480 488 491 521
# 640x480 @ 75 Hz, 37.50 kHz hsync
Multiline "640x480" 31.5 640 656 720 840 480 481 484 500
-VSync
# 800x600 @ 60 Hz, 37.8 kHz hsync
Multiline "800x600" 40 800 840 968 1056 600 601 605 628
+vsync
```

```
# 1024x480 @ 85 Hz, 43.27 kHz hsync
Multiline "1024x480" 36 640 696 752 832 480 481 484 509
-VSync
# 1152x864 @ 89 Hz interlaced, 44 kHz hsync
ModelLine "1152x864" 65 1152 1168 1384 1480 864 865 875 985
Interlace

# 80600 @ 72 Hz, 48.0 kHz hsync
ModelLine "800x600" 50 800 856 1040 1000 637 643 666
+hsync +vsync
# 1024x768 @ 60 Hz, 48.4 kHz hsync
ModelLine "1024x768" 65 1024 1032 1176 1344 768 771 777 806
-hsync -vsync

# 640x480 @ 100 Hz, 53.01 kHz hsync
ModelLine "640x480" 45.8 640 672 768 864 480 488 494 530
-Hsync -Vsync
# 1152x864 @ 60 Hz, 53.5 kHz hsync
ModelLine "1152x864" 89.9 1152 1216 1472 1680 864 868 876 892
-Hsync -Vsync

# 80600 @ 70 Hz, 56.5 kHz hsync
ModelLine "800x600" 60.75 800 864 9028 1088 600 616 621 657
-Hsync -Vsync
# 1024x768 @ 75 Hz
ModelLine "1024x768" 45 1024 1048 1184 1328 768 771 777 806
-hsync -vsync
# 1280x1024 @ 87 Hz interlaced, 51 kHz hsync
ModelLine "1280x1024" 80 1280 1296 1512 1568 1024 1037 1165
Interlace

EndSection

表 9.5 讨论了各种指令。

### 表 9.5：显示器

| 指令 | 说明 |
| :--- | :--- |
| Identifier | 该指令用用户指定的名称标识显示器。 |
| VendorName | 该指令标识显示器的厂商。此值对 XFree86 的运行没有影响，最好分配一个有意义的值以便以后识别。 |
| ModelName | 该指令标识显示器的型号。此值对 XFree86 的运行没有影响，最好分配一个有意义的值以便以后识别。 |

### 表 9.5：继续：显示器

| 指令 | 说明 |
| :--- | :--- |
| HorizSync | 该指令指定显示器的水平同步频率范围（kHz）。你可以像示例那样指定范围，也可以提供逗号分隔的离散值。参考显示器文档并提供正确的值很重要。在这里输入错误的值，可能会损坏显示器。 |
| VertRefresh | 该指令指定显示器支持的垂直刷新率（Hz）。你可以像示例那样指定范围，也可以提供逗号分隔的离散值。参考显示器文档并提供正确的值。。输入错误的值，可能会损坏显示器。 |
| ModelLine | 该指令指定显示器可能的模式。模式将分辨率与点钟以及时序相结合，以确定如何显示。XF86Config 中的任何不兼容的模式在服务器加载时都会被删除。最情况下，通常最好让 XFree86 配置为你创建这些行，而不是修改它们。 |

## Device 设备

XF86Config 通常包含多个 Device 部分。Device 部分描述了服务器可以使用显卡。通常服务器可以填充大部分信息，但手动提供这些信息以避免出错是明智的。因为这些信息包含了关于视频硬件的高度技术规范，除非你确实需要进行这些更改，否则应该让 XFree86 配置处理此部分。

让我们看一个 Device 示例：

Section "Device"
  Identifier "Generic VGA*"
  VendorName "Unknown"
  BoardName "Unknown"
  Chipset "generic"
  VideoRam 256
  Clocks 25.2 28.3
EndSection

在表 9.6 中，我们看到了 Device 部分使用的条目：

### 表 9.6：设备指令

| 指令 | 影响 |
| :--- | :--- |
| Identifier | 与 Monitor 部分一样，该指令提供了一个可以在F86Config 文件其他地方使用的名称。 |
| VendorName | 该指令不影响 X 服务器的运行，但有助于你以后识别硬件。 |
| BoardName | 该指令同样不影响运行，有助于识别设备。 |
| Chipset | 该指令标识你的视频芯片组。如果 XFree86 不支持硬件，将使用通用芯片组。 |
| VideoRam | 该指令指定可用显存的大小（单位为 KB）。如果你不提供此信息，服务器将尝试直接从显卡获取。 |
| Clocks | 该指令指定视频硬件的时钟设置。不要手动编辑它，而是让你的配置软件来设置。 |
| ClockChip | 该指令指定视频硬件使用的时钟芯片（如果有）。如果有，则不需要指定 Clocks 行，因为时钟芯片将提供所有信息 |

## Screen 屏幕

Screen 部分用于汇总 Monitor 和 Device 部分包含的信息。你可以有多个 Screen 部分。

这是一个 Screen 部分示例：

```
Section "ACCEL"

  Driver "ACCEL"

  Device "VideoCard"

  Monitor "monitor"

  Subsection "Display"

    Depth 24

    Modes "1024x768"

    ViewPort 0

EndSubsection
```

### Subsection 'Display' 子部分

| Depth | 32 |
| :--- | :--- |
| Modes | *800x600* |
| ViewPort | 0 0 |

EndSubsection

Screen 部分连接设备和显示器，然后定义显示。表 9.7 显示了 Screen 部分使用的主要指令：

### 表 9.7：屏幕指令

| 指令 | 影响 |
| :--- | :--- |
| Driver | 该指令指定四种驱动之一：SVGA（用于通用 VGA）、MONO（用于单色）或 ACCEL（用于加速 X 服务器）。 |
| Device | 该指令指定设备的名称。 |
| Monitor | 该指令指定显示器的名称。 |
| Depth | 在未指定 Display 部分时使用的色彩深度。 |

除了这些指令，还会使用一个名为 Display 的子部分。我们指定了三个，如表 9.8 所示：

### Display 子部分

| 指令 | 影响 |
| :--- | :--- |
| Depth | 该指令指定显示色彩深度，单位为每个像素的位数。例如，8 位允许 256 色，16 位允许 65536 色，24 位允许 1670 万色。 |
| Modes | 该指令指定显示分辨率。常见的分辨率有 1024x768、800x600 和 640x480。 |
| ViewPort | 该指令指定可能的虚拟桌面的大小。例如，你的 640x480 屏幕可能是更大的 1024x768 虚拟桌面的窗口。ViewPort 条目指定虚拟桌面的水平和垂直维度（像素像素），但值之间用空格而不是 x 分隔。这里的输入 ViewPort 0 表示没有虚拟桌面。 |

`xinitrc` `.xinitrc` 文件是一个可执行的 shell 脚本。我们将在第 13 章“理解 shell”中学习关于 shell。因此，我们在这里不会进入 shell 或 shell 脚本的细节；而是将快速查看来自 Red Hat Linux 5 的默认 `xinitrc` 文件，以了解它的作用。（这里标记了行号是为了方便我们做决定。行号不属于文章的一部分。）

```
1: #!/bin/sh

2: # $ConfigSource:xinitrc.cpp,v 1.4 91/08/22 11:41:34 rws Exp $\n

3:

4: /usr/bin/X11/xhost +

5:

6: userresources=$HOME/.Xresources

7: usermodmap=$HOME/.Xmodmap

8: sysresources=/usr/X1R6/lib/X11/xinit/.Resources

9: sysmodmap=/usr/X1R6/lib/X11/xinit/.Xmodmap

10:

11: # merge in defaults and keymaps

12:
```
