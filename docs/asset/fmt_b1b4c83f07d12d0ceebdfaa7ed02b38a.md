
| 条目 | 目的 |
| --- | --- |
| accel | 用于加速芯片的 X 服务器 (S3, Mach32, Mach64, P9000, 8514, AGX 和 W32) |
| svga | 用于 SuperVGA 的 X 服务器 |
| vga16 | 用于 16 色 VGA 卡的 X 服务器 |
| vga2 | 用于单色卡的 X 服务器 |

每个 `Screen` 部分还列出了若干 `Display`（显示）子部分，它们指示了视频模式（使用 640×480、800×600 以及 1024×768）。每个 `Display` 子部分都有一个 `Depth` 条目，指定了每个像素使用的位数——每像素比特数。当前的 X 服务器会选择 `Driver` 条目与 X 服务器类型（例如 Super VGA 或 Accelerated）匹配的 `Screen` 部分。你在运行 `xf86config` 程序会话期间指定 X 服务器。

### 运行 X

在你拥有了一个完整的 `XF86Config` 文件后，你就可以准备好启动 X 服务器和一些应用程序了。要启动 X，运行 `startx` 脚本，这是一个包含 X 命令的文件。该脚本位于 `/usr/X11/bin` 目录，此目录应该在你的 `PATH` 变量中。运行此脚本，输入 `startx`。

`startx` 脚本会在你的主目录下查找另一个名为 `.xinitrc` 的脚本。如果发现你的主目录下没有找到任何 `.xinitrc`，它将使用默认脚本 `/usr/X11/lib/X11/xinitrc` 运行 `xinit` 命令。注意，与你主目录下的 `.xinitrc` 不同，默认脚本名的第一个字符不是点。使用此文件的默认版本，当你作为普通用户（而不是 root）运行 `startx` 时，你的屏幕应该如如图 4-1 所示。

现在，你可以在 `xterm` 窗口（屏幕中间的大窗口）的提示符处输入 Linux 命令。你将在第 5 章学习更多关于自定义 X 显示的内容。

![](img/a5afb9ccf4a12511e9fc428014e3_209_0.png)

![](img/a5afb9ccf4a12511e9fc428014e3_209_1.png)

图 4-1：初始 X 显示

当启动脚本结束时，X 服务器会退出。反之，启动脚本在其最后一个命令完成后结束。通常，窗口管理器（如 fwm）是最后一个命令，因此你可以通过退出窗口管理器来停止 X 并返回文本界面。

### 使用 Ctrl+Alt+Backspace 终止

如果你的显示器和显卡在 `XF86Config` 文件中没有正确指定，那么当你使用 `start` 命令启动 X 时，可能看不到图 4-1 所示的 X 显示。如果你遇到显示失真或系统看起来像锁死的问题，按下 `Ctrl+Alt+Backspace` 来杀死 X 服务器并返回文本显示。（在 UNIX 中，当你使用 `start` 命令启动 X 时，你可能看不到 X 所示的显示。如果你遇到显示失真或系统看起来像锁死的问题，按下 `Ctrl+Alt+Backspace` 来杀死 X 服务器并返回文本显示。）

尝试不同的显示模式

在 `XF86Config` 文件中，如果你按下 `Ctrl+Alt+Backspace` 杀死 X 服务器并返回文本显示。（在 UNIX `，` ` ` ` ，，，，，，，，，，，，，，，，， 。

尝试不同的显示模式

在 `F86Config` 文件中，， ，，显示不同的视频模式。

对于 Dell VS15X，`HorizSync` 和 `VertRefresh` 设置（来自显示器说明书）如下：

```
# 加速 (S3, Mach32, Mach64, P9000, 8514, AGX 和 W32)
Section "Screen"
  Driver      "accel"
  Device      "Number Nine GXE64 with S3-Trio6"
  Monitor     "Dell VS15X"
  Subsection "Display"
    Depth       8
    Modes       "640x480" "800x600" "1024x768"
    Viewport    0
    Virtual     1024x768
End
```

当 X 服务器启动时，它根据 `Modes` 条目中的第一个模式配置显卡（在此情况下，为 640×480，即水平 640 像素，垂直 480 像素）。

#### Monitor（显示器）部分

...在这两个关键值之后，你会看到大量的 `Modeline` 条目。该列表是一组标准模型；X 服务器会从该集合中选择最佳的标准模式。你不需要编辑那些行。

#### Device（设备）部分

`Device`（设备）部分指定了显卡并通过 `Identifier` 条目为其命名。`xf86config` 程序会生成一个包含 VGA 显卡标准 `Device` 部分的配置文件。你应该检查根据你提供给 `xf86config` 的输入而创建的 `Device` 部分。该部分应该包含一个正确的 `Identifier` 条目，如下：

- Identifier "Number Nine GXE64 with S3-Trio6"

## 第 4 章：Linux 下 X 的秘密

`Screen` 部分通过 `Identifier` 条目中显示的名称引用此显卡。对于许多显卡，此部分可能不会包含更多信息，因为 X 服务器（针对该显卡）可以自动配置并正确使用该显卡。

对于显卡，`XF86Config` 文件的 `Device` 部分需要一个 `Clock` 条目，其值为一组浮点数。这些时钟是最难找到的参数之一（尽管某些视频芯片组——如 S3-Trio64——不需要时钟）。获取时钟的一种方法是用命令 `X -probeonly` 运行 X 服务器。事实上，`xf86config` 程序正是这样运行 X 并为你获取时钟的。你只需要在看到以下问题时按 y 即可：

Do you want me to run 'X probeonly'?

如果你的显卡在 `Device` 部分需要时钟，这种方法是获取所需值最简单的方法。

### Screen（屏幕）部分

每个 `Screen` 部分指定了与特定 X 服务器配合 `Monitor`（显示器）和 `Device`（设备）。你通过 `Identifier` 条目中显示的名称指定 `Monitor` 和 `Device`。`Driver` 条目标识 X 服务器。`xf86config` 程序在配置文件中生成多个 `Screen` 部分。每个 `Screen` 部分对应一个由 `Driver` 条目标识的不同 X 服务器。表 4-2 列出了这些选项。

| 条目 | 目的 |
| --- | --- |
| accel | 用于加速芯片的 X 服务器 (S3, Mach32, Mach64, P9000, 8514, AGX 和 W32) |
| svga | 用于 SuperVGA 的 X 服务器 |
| vga16 | 用于 16 色 VGA 卡的 X 服务器 |
| vga2 | 用于单色卡的 X 服务器 |

每个 `Screen` 部分还列出了若干 `Display`（显示）子部分，它们指示了视频模式（使用 640×480、800×600 以及 1024×768）。每个 `Display` 子部分都有一个 `Depth` 条目，指定了每个像素使用的位数——每像素比特数。当前的 X 服务器会选择 `Driver` 条目与 X 服务器类型（例如 Super VGA 或 Accelerated）匹配的 `Screen` 部分。你在运行 `xf86config` 程序会话期间指定 X 服务器。

### 运行 X

在你拥有了一个完整的 `XF86Config` 文件后，你就可以准备好启动 X 服务器和一些应用程序了。要启动 X，运行 `startx` 脚本，这是一个包含 X 命令的文件。该脚本位于 `/usr/X11/bin` 目录，此目录应该在你的 `PATH` 变量中。运行此脚本，输入 `startx`。

`startx` 脚本会在你的主目录下查找另一个名为 `.xinitrc` 的脚本。如果发现你的主目录下没有找到任何 `.xinitrc`，它将使用默认脚本 `/usr/X11/lib/X11/xinitrc` 运行 `xinit` 命令。注意，与你主目录下的 `.xinitrc` 不同，默认脚本名的第一个字符不是点。使用此文件的默认版本，当你作为普通用户（而不是 root）运行 `startx` 时，你的屏幕应该如如图 4-1 所示。

现在，你可以在 `xterm` 窗口（屏幕中间的大窗口）的提示符处输入 Linux 命令。你将在第 5 章学习更多关于自定义 X 显示的内容。

![](img/a5afb9ccf4a12511e9fc428014e3_209_0.png)

![](img/a5afb9ccf4a12511e9fc428014e3_209_1.png)

图 4-1：初始 X 显示
