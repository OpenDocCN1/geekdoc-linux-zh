
X 与苹果的 Power Mac 硬件配合得很好。目前没有关于在任何当前支持的 Power Mac 型号系列上使 X 正常工作存在重大问题的报告。这意味着如果你有一台 iBook、TiBook 或 Apple G4 Cube，你可以预期使用 X 为 Linux 配置一个可用的图形界面。如果你确实遇到问题，请查看你的 Linux 发行版供应商提供的最新更新、勘误表或 bug 修复。对于与 X 相关的任何问题，你肯定能找到答案。

## 键盘和鼠标问题

当你在 `console` 模式下使用 Linux 时，鼠标支持由通用鼠标驱动程序 `gpm` 提供。这是一个 `daemon`，即在你使用 Linux 时后台运行的程序，它提供信息的高亮、复制和粘贴支持。当你在 X 会话中使用 X 时，你的鼠标光标被称为 `pointer`，并由 XFree86 服务器支持。

你可以使用 `setfont` 和 `echo` 命令在控制台工作时更改字体和字体颜色。Linux 随附近 100 种字体安装在 `/usr/lib/kbd/consolefonts` 目录。你可以使用 `setfont` 命令来更改控制台字体，如下所示：

```
$ setfont /usr/lib/kbd/consolefonts/8x14thin
```

按回车键后，你看到了什么？

![](img/1ea833f5a3e3c1547e3dd2891f52804a_63_0.png)

> 这仅在你使用控制台运行 Linux 时有效。

要恢复默认字体，请使用 `setfont` 命令，如下所示：

```
$ setfont /usr/lib/kbd/consolefonts/default8x16
```

要更改字体颜色，请使用 `echo` 命令向屏幕输出一个特殊的字符串，如下所示：

```
$ echo -e \033[32m'
```

按回车键后，你看到了什么？要重置颜色，请使用 `echo` 命令，如下所示：

```
$ echo -e \033[0m'
```

![](img/1ea833f5a3e3c1547e3dd2891f52804a_63_1.png)

> 想使用其他颜色？请使用 `man` 命令阅读 `console_codes` 手册页。（要了解如何使用 `man` 命令，请在命令行输入 `man man`。）

### 模拟鼠标按钮

如果你的 Power Mac 只有一个按钮的鼠标（大多数都是这样），你可能需要考虑购买一个三键鼠标。Linux 和 X 的设计旨在支持和利用三键鼠标。这并不意味着你不能使用单键鼠标高效地运行 Linux 和 X，但如果你的鼠标至少有两个按钮，生活会稍微方便一些。

如果你已经在 iBook 上安装了 Linux 并且想要模拟三键功能，可以在启动时将一个称为参数的命令字符串传递给 Linux 内核。例如，在 `yaboot.conf` 文件中的以下设置会将 F11 和 F12 分别作为中间和右侧鼠标按钮启用：

```
append="adb,buttons=103,111"
```

如果你使用的是 SuSE Linux PPC 且配备一个单键 USB 鼠标（较新的台式 Power Mac 附带），向 Linux 内核 USB 驱动程序发送以下命令可启用 F11 和 F12 作为中间和右侧鼠标按钮（作为 root，你可以将这些行添加到 SuSE 系统的 `/etc/rc.d/boot.1ocal1` 文件中）：

```
echo "1" > /proc/sys/dev/mac_hid/mouse_button_emulation
echo "87" > /proc/sys/dev/mac_hid/mouse_button2_keycode #F11
echo "88" > /proc/sys/dev/mac_hid/mouse_button3_keycode #F12
```

然而，Apple TiBook 用户会发现，单独按 F12 无法用于模拟，因为它被用作媒体（CD-ROM）弹出按钮。在这种情况下，请使用上述 USB 方法。此外，将中间和右侧鼠标按钮映射到 F10 和 F11，如下所示：

```
echo "1" > /proc/sys/dev/mac_hid/mouse_button_emulation
echo "68" > /proc/sys/dev/mac_hid/mouse_button2_keycode
echo "87" > /proc/sys/dev/mac_hid/mouse_button3_keycode
```

> Yellow Dog Linux 和 TiBook 用户会发现鼠标按钮和键盘映射是自动配置的。在 X 会话中按 F11 模拟中间鼠标按钮。按 F12 模拟右侧鼠标按钮。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_64_0.png)

使用三键鼠标可能会解决使用 X11 时的一些问题。系统中三键 USB 鼠标在 XF86Config 文件中的典型条目（该文件只能由 root 编辑）如下所示：

```
Section "Pointer"
    Device      "/dev/input/mice"
    Protocol    "IMPS/2"
EndSection
```

在此示例中，指针应该被正确识别。然而，使用滚轮鼠标需要额外的设置来启用滚动，必须添加如下内容：

```
Section "Pointer"
    Device      "/dev/input/mice"
    Protocol    "IMPS/2"
    ZAxisMapping 4 5
EndSection
```

经验丰富的 Linux 用户在诊断或查找问题及解决方案时几乎没有困难。当你刚接触 Linux 时，理解系统配置文件之间的关系以及 Linux 的工作方式至关重要。

幸运的是，Apple PowerPC 用户可以借鉴他人的积累知识和解决方案来定位并解决问题。很有可能，某位使用相同型号 Power Mac 的人已经遇到并克服了当前你面临的障碍。务必花时间仔细研究任何新型号的购买，如果在 Mac 上运行 Linux 遇到麻烦，请上网查找使用你机器的 Linux 用户信息。

### 设置日期、时间和区域

在计算机上保持准确的时间非常重要。了解计算机上有两个时间也很重要：Linux 系统时间和计算机的硬件时钟。准确记录时间可能至关重要，特别是在与其他用户、客户端或远程计算机交互时。某些任务，如备份，有时必须在一天中的特定小时执行。电子邮件或文档上的时间戳在商业或法律行业中可能证明至关重要。

许多熟练的 Linux 用户将 Power Mac 的硬件时钟设置为 UTC（`协调世界时`），同时根据计算机所在位置设置系统时间（相对于 UTC 的加或减偏移量）。

由于世界被划分为许多不同的时区，每个 Linux 系统都包含一个时区信息数据库（位于 `/usr/share/zoneinfo` 目录下）。此信息与不同的命令结合使用，以帮助保持准确的时间。与 UNIX 类似，Linux 系统时间基于自 1970 年 1 月 1 日以来的秒数，许多 Linux 时间工具使用返回值作为基准来确定当前的本地时间。

显示日期和时间很容易。你只需运行 `date` 命令即可，如下所示：

```
$ date
Fri May 11 14:47:08 EDT 2001
```

在此示例中，系统的当前日期和时间是从秒数中推断出来的，并以可读格式显示。`date` 命令也可用于设置系统时间。使用 `date` 命令（作为 root）并将月、日、小时和分钟放在一个数字字符串中，如下所示：

```
$ date 06291200
Fri Jun 29 12:00:00 EDT 2001
```

另一方面，要查看计算机的硬件时钟及其时间，请使用带有 `-r` 选项的 `clock` 命令，如下所示：

```
# /sbin/clock -r

time in rtc is Fri May 11 23:07:07 2001

Fri May 11 23:07:07 2001
```

> 在基于 Intel 的 Linux 系统中，传统上使用 `hwclock` 来显示和设置系统的硬件时钟。此命令仅在 CHRP 或 PREP 工作站上支持，不支持 Apple Power Macs。请改用 `clock` 命令。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_66_0.png)

`clock` 命令的语法简短，看起来像这样：
