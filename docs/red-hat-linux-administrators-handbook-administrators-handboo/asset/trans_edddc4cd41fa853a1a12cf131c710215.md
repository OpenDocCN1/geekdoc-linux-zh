
```
# 1024x768 @ 70 Hz, 56.5 kHz hsync
Modeline "1024x768" 75 1024 1048 1184 1328 768 771 777 806 -hsync -vsync
```

```
# 1024x768 @ 76 Hz, 62.5 kHz hsync
Modeline "1024x768" 85 1024 1032 1152 1360 768 784 787 823
```

```
# 1280x1024 @ 61 Hz, 64.2 kHz hsync
Modeline "1280x1024" 110 1280 1328 1512 1712 1024 1025 1028 1054
```

```
# 1280x1024 @ 74 Hz, 78.85 kHz hsync
Modeline "1280x1024" 135 1280 1312 1456 1712 1024 1027 1030 1064
```

```
# 1280x1024 @ 76 Hz, 81.13 kHz hsync
Modeline "1280x1024" 135 1280 1312 1416 1664 1024 1027 1030 1064
```

EndSection

以下是在本节中的选项：

- **标识符。** 用于为显示器设置唯一标识符。每个显示器都需要有一个唯一的标识符，可以在 Screen 部分中引用。
- **厂商名称和型号名称。** 用于指定显示器的厂商名称和型号。
- **HorizSync。** 用于设置水平刷新（同步）频率，单位为 KHz。如果您想以兆赫或赫兹指定该频率，请分别在行尾使用 MHz 或 Hz。
- **VertRefresh。** 用于设置垂直刷新（同步）频率，单位为 Hz。如果您想以兆赫或千赫指定该频率，请分别在行尾使用 MHz 或 KHz。

- **ModeLine。** 用于指定视频模式。每个 ModeLine 选项具有以下格式：

```
ModeLine mode clk-rate Horizontal-timing Vertical-timing Flags
```

clk-rate 是此模式的像素时钟速率。这是一个单一的正整数。Horizontal-timing 和 Vertical-timing 各为一组四个时序整数。Flags 可选用于指定模式的额外特性。

可以使用 mode 选项将 ModeLine 写成多行。例如：

```
ModeLine "1024x768i" 45 1024 1048 1208 1264 768 776 784 817 Interlace
```

```
Mode "1024x768i"
DotClock 45
HTimings 1024 1048 1208 1264
VTimings 768 776 784 817
Flags "Interlace"
EndMode
```

前述两个视频模式描述是相同的。

- **图形设备部分。** 用于设置显卡的选项。

这里是一个示例部分：

```
# Device configured by Xconfigurator:
```

```
Section "Device"
    Identifier "Trio32/Trio64"
    VendorName "Unknown"
    BoardName "Unknown"

EndSection
```

以下是在本节中的选项：

- **标识符。** 用于为显示器设置唯一标识符。每个显示器都需要有一个唯一的标识符，可以在 Screen 部分中引用。
- VendorName。用于指定厂商名称。
- BoardName。用于指定显卡的名称。通常，X 服务器会检测您显卡上安装的功能，包括 RAM 容量、芯片组等。
- Screen 部分。用于指定 X 服务器应如何使用视频硬件（显示器和显卡）。以下是该部分的示例：

```
Section "Screen"
    Driver      "accel"
    Device      "Trio32/Trio64"
    Monitor     "My Monitor"

    Subsection "Display"
        Depth       8
        Modes       "640x480" "800x600" "1024x768"
        "1280x1024"
        ViewPort    0 0
        Virtual     1280 1024
    EndSubsection

    Subsection "Display"
        Depth       16
        Modes       "640x480" "800x600" "1024x768"
        ViewPort    0 0
        Virtual     1024 768
    EndSubsection

    Subsection "Display"
        Depth       32
        Modes       "640x480" "800x600"
        ViewPort    0 0
        Virtual     800 600
    EndSubsection
```

## EndSection

以下是在本节中的选项：

- **驱动程序。** 设置驱动程序名称。支持的驱动程序名称有 accel、mono、svga、vga2 和 vga16。
- **设备。** 设置要使用的显卡名称。
- **显示器。** 设置要使用的显示器名称。

Display 子部分用于为特定显示设备指定一组参数。Depth 选项用于设置颜色深度；Modes 选项用于设置视频模式或分辨率；ViewPort 选项用于设置初始显示的左上角；Virtual 选项用于指定虚拟视频分辨率。Screen 部分可以有多个显示子部分。

在 Display 部分中作为 Modes 选项参数指定的视频分辨率，可以通过使用 Ctrl+Alt+Keypad-Plus 和 Ctrl+Alt+Keypad-Minus 键来选择或取消选择。

## 使用 X Windows

您可以以多种方式启动 X Windows。您可以运行 xinit，它会启动 X Windows 服务器并运行第一个 X 客户端应用程序。它运行的客户端应用程序取决于用户主目录中的 .xinitrc 脚本。例如，如果您以 root 身份运行 xinit，则 ~/root/.xinitrc 脚本将被用来确定 X Windows 服务器启动并运行后需要启动什么 X 客户端应用程序。如果在命令行中未指定客户端应用程序，或 ~/.xinitrc 文件不存在，它将使用以下命令作为默认值：

```
xterm -geometry +1+1 -n login -display :0
```

换句话说，它将启动一个 xterm 会话作为唯一的客户端应用程序。当此客户端应用程序退出时，X Windows 服务器也将终止。

为了提供更好的用户控制，发布了一个名为 startx 的 sh 脚本。您可以不带任何参数运行 startx 来启动 X Windows 服务器。该脚本实际上是 xinit 程序的前端。默认情况下，startx 脚本会在用户主目录中查找 .xserverrc，如果找不到，startx 会在 /usr/X11R6/lib/X11/xinit 目录中查找系统范围的 xserverrc 文件。~/.xserverrc 文件或 /usr/X11R6/lib/X11/xinit/xserverrc 文件用于确定需要启动哪个 X Windows 服务器。

startx 脚本还会查找用户主目录中的 .xinitrc，如果在那里找不到，它会在 /usr/X11R6/lib/X11/xinit 目录中查找系统范围的 xinitrc 文件。~/.xinitrc 或 /usr/X11R6/lib/X11/xinitrc 文件用于确定 X Windows 服务器启动后将运行哪些客户端应用程序。

您可以提供命令行参数来更改这些文件中找到的默认设置。但是，如果您一直覆盖默认值，不如将您选择的设置放在这些文件中，这样您在每次运行此脚本时就不必每次都输入它们。

如果您愿意，可以通过在命令行中指定颜色模式来以不同的颜色模式启动 X Windows。例如，以下命令以 256 色模式启动 X Windows：

```
startx -- -bpp 8
```

要以真彩色模式启动 X Windows，请使用以下命令：

```
startx -- -bpp 32
```

双破折号是必需的，以便将参数直接传递给 xinit 程序。

当您第一次运行 startx 时，您主目录中可能没有预安装的 .xinitrc 文件；因此，将使用系统范围的 xinitrc 文件。要创建自己的 .xinitrc 文件，请运行 locate xinitrc 命令以在 /usr/X11R6/lib/X11/xinit 或 /etc/X11/xinit 中定位该文件副本。通过将其重命名为以句点作为第一个字符，将此文件复制到您的主目录中，以便最终名称为 .xinitrc。

## 配置 .xinitrc

如前所述，.xinitrc 脚本用于根据用户的偏好启动客户端应用程序。当在用户主目录中找到此类脚本时，startx 将运行它；当 .xinitrc 脚本退出时，它将终止 X Windows 服务器。因此，您必须在脚本中调用一个客户端应用程序，以便控制不会落到脚本底部
（导致其退出）直到您终止该客户端应用程序。通常，这是通过在后台运行除最后一个客户端程序之外的所有程序来实现的。最后一个客户端程序通常是 X Windows 管理器。列表 14-1 显示了一个示例 .xinitrc 文件。

### 列表 14-1 一个示例 .xinitrc 文件

```
#
# Example .xinitrc
#
# start xclock (in the background)
xclock -geometry 50x50-1+1 &
# start two xterms (in the background)
xterm -geometry 80x50+494+51 &
xterm -geometry 80x20+494-0 &
#
# now start a window manager in
# the foreground
#
# If my favorite fvwm95 is there, start it
if [ -f /usr/X11R6/bin/fvwm95 ]; then
exec fvwm95
# Ok, no fvwm95, try fvwm2
elif [ -f /usr/X11R6/bin/fvwm2 ]; then
exec fvwm2
# Ok, no fvwm95 or fvwm2, try just fvwm
elif [ -f /usr/X11R6/bin/fvwm ]; then
exec fvwm
# Ok, no fvwm of any kind, so try afterstep
```
