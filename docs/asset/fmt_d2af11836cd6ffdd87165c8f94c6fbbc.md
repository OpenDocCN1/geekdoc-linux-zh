
## XF86Config 示例

```
Section "Keyboard"

Protocol "Standard"

XkbRules "xfree86"

XkbModel "pc101"

XkbLayout "us"

EndSection
```

```
Section "Pointer"

Protocol "microsoft"

Device "/dev/tty0"

Emulate3Buttons

EndSection
```

```
Section "Monitor"

Identifier "Primary Monitor"

VendorName "Typical monitors"

Name "800x600, 60Hz"

HorizSync 31.5-90

VertRefresh 55-90

Modeline "800x600/60Hz" 40 800 840 968 1056

600 601 605 628

+HSync +VSync

EndSection
```

```
Section "Device"

Identifier "Primary Card"

VendorName "Unknown"

BoardName "None"

VideoRam 2048

EndSection
```

```
Section "Screen"

Driver "VGA16"

Device "Primary Card"

Monitor "Primary Monitor"

SubSection "Display"

Depth 4

Modes "640x480/60Hz"

EndSubSection

EndSection
```

```
Section "Screen"

Driver "SVGA"

Device "Primary Card"

Monitor "Primary Monitor"

DefaultColorDepth 16

Subsection "Display"

Depth 8

Modes "800x600/60Hz"

Virtual 800 600

EndSection

Subsection "Display"

Depth 15

Modes "800x600/60Hz"

Virtual 800 600

EndSection

Subsection "Display"

Depth 16

Modes "800x600/60Hz"

Virtual 800 600

EndSection

Subsection "Display"

Depth 24

Modes "800x600/60Hz"

Virtual 800 600

EndSection

SubSection "Display"

Depth 32

Modes "800x600/60Hz"

Virtual 800 600

EndSubSection

EndSection
```

自动生成的文件结束

请注意，`XF86Config` 文件包含了显示字体规范、键盘和鼠标的使用说明、关于显示器和显卡能力的详细信息，以及关于结合显卡和显示器详情以创建特定视图（例如 256 色的 1024 × 768 分辨率）的信息。

上述的示例文件不包含注释，你可以在许多 `XF86Config` 文件中找到这些注释。这些注释可以帮助你理解配置文件的不同部分，并提供替代配置的示例。

商业 X 服务器并不依赖于 `XF86Config` 文件。每个服务器都使用具有不同格式的配置文件。例如，来自 Xi Graphics 的 Accelerated-X 服务器使用 `/etc/Xaccel.ini` 配置文件。为了方便配置工作，商业 X 服务器包含了与本章描述的 XFree86 工具相似的配置工具。其中一个为 Accelerated-X 提供配置选项的工具如图 5-6 所示。通常情况下，在操作商业 X 服务器时，您在准备配置文件之前，应该审阅随附的文档，以学习如何使用产品配置实用。

![](img/0de795a4f3f708f3baad48fd57def247_187_0.png)

图 5-6 Accelerated-X 的配置工具

# 运行 X 系统

## 使用 Xconfigurator

`Xconfigurator` 程序是一个为你的 Free86 服务器创建 `XF86Config` 文件的实用。它由 Red Hat Software 开发，作为 Red Hat Linux 安装的一部分自动执行。你也可以在安装完成后运行此程序，以调整或重新进行 X 配置。要启动程序，请在命令行中输入程序名称（注意大写的 X）：

```
Xconfigurator
```

如果你已经安装了 Red Hat Linux，`Xconfigurator` 的界面将让你感到熟悉。`Xconfigurator` 允许你从列表中选择显卡，并提供手动设置额外选项或让 `Xconfigurator` 探测显卡以确定最佳设置的选项。图 5-7 显示了 `Xconfigurator` 的示例屏幕，你可以在其中选择在不同颜色深度下使用的屏幕分辨率。使用 `Xconfigurator` 的详细步骤已作为第 3 章安装说明的一部分提供。

![](img/0de795a4f3f708f3baad48fd57def247_188_0.png)

图 5-7 在 Xconfigurator 中选择屏幕分辨率

尽管 `Xconfigurator` 是一个很有用的工具，但它并不总是设置 X 的最佳方法，因为它可能无法提供你需要的所有选项。因此，你可能会发现在系统中选择了显卡并选取了看似正确的选项后，X 仍然无法运行。（参见本章稍后的“启动 X”部分）。`Xconfigurator` 的问题在于，它没有提供足够的配置细节来让你选择出能够使 X 服务器正常运行的选项；它同样不具备在不提问大量问题的情况下设置显卡的能力。如果 `Xconfigurator` 未能成功设置 X，请尝试使用后续章节描述的其他工具。

## 使用 x86config

XFree86 软件带有一个名为 `x86config` 的命令行配置实用工具。启动此实用工具后，你必须阅读屏幕上显示的信息并回答问题。如果你花时间阅读屏幕上的信息并了解硬件细节（例如 RAM 的容量），`x86config` 很有可能正确配置任何显卡。

`x86config` 实用工具包含在 Red Hat Linux 中。许多其他发行版也包含此工具。要启动 `x86config`，请在任何命令行输入该工具的名称（注意它是小写的）：

```
x86config
```
