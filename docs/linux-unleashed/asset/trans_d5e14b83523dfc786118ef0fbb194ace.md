

## 详解 Xconfig 和 XF86Config 文件

ConfigFX86 和 fx86config 都有可用的文档，通常与可执行文件一起放置在 /usr/X386/bin 目录下。不过，某些版本的 Linux 和 XFree86 并不提供这些文档。文档通常以多种格式提供。有一个 ASCII 版本名为 ConfigFX86.txt，还有一个 PostScript 版本名为 ConfigFX86.ps（或 fx86config 的对应版本）。

当您运行 ConfigFX86 或 fx86config 时，系统会显示一些通用信息，然后提示您输入之前收集的关于系统的信息。在大多数情况下，系统会显示一个受支持值的列表，并要求您选择其中一个。按顺序完成这些选择后，该工具就会获得构建 Xconfig 文件所需的正确信息。

例如，xf86config 工具会询问您的鼠标类型、是否要启用鼠标的特殊功能（如三键鼠标的中键）、鼠标连接的设备、显示器的水平和垂直同步范围、显示器的名称、视频卡使用的芯片组、要运行的服务器、链接到服务器的文件位置、视频卡上安装的 RAM 量、是否要设置时钟芯片，以及视频卡支持的分辨率顺序。在您回答了所有问题后，xf86config 会询问该工具是否应创建 XF86Config 文件。

使用脚本创建 XF86Config 或 Xconfig 文件后，您应该克制立即启动 X 的冲动。相反，请花点时间手动检查该文件，以防止因设置不正确而对硬件造成任何潜在损坏。接下来关于手动配置 Xconfig 或 XF86Config 文件的章节将解释所有设置。当您对一切都满意后，使用命令 startx 启动 X。

如果您手动将配置信息输入 Xconfig 或 XF86Config 文件，您需要了解这些文件的布局以及如何输入您的具体细节。所有版本的 XFree86 都至少有一个示例配置文件，通常名为 Xconfig.sg 或 XF86Config.sg，位于 lib 目录中。您应该使用此文件作为创建自己配置文件的模板。将示例文件复制到一个不带 .eg 扩展名的新文件中，并进行以下描述的更改。

Xconfig 和 XF86Config 文件并不短，但其中散布着大量注释。配置文件的格式是一组部分，每个部分对应 XFree86 配置的各个方面。部分的一般顺序如下：

-   二进制文件和屏幕字体的路径名
-   键盘信息
-   鼠标信息
-   服务器文件
-   视频信息

让我们更详细地查看每个部分。如果您已运行过自动配置文件生成工具（如 xf86config 或 XF86Config），请检查生成文件中的条目。如果您正在手动编辑文件，请缓慢且有条理地进行操作，以防止出错。

**注意**

本节其余部分显示的代码摘录来自 XFree86 版本 3.X 创建的 XF86Config 文件，因为它是最新版本，并且通常包含在新的软件发行版中。XFree86 版本 2.X 的 Xconfig 文件类似，通过检查 Xconfig 文件，您在执行相同步骤时不应遇到任何问题。

请注意，Xconfig 或 XF86Config 文件中的每个部分都以关键字 "section" 开头，随后是该部分的名称。部分以关键字 "EndSection" 结束。这使得查找您要操作的部分更容易。文件中的注释都以井号（#）开头。

### 路径名

在大多数情况下，除非您将 XFree86 安装在默认值以外的目录中，否则配置文件中提供的路径名无需更改。XFree86 用于屏幕字体和其他文件的路径在配置文件的以下部分中给出：

```
Section "Files"

# The location of the RGB database. Note, this is the name of the
# file minus the extension (like ".txt" or ".db"). There is normally
# no need to change the default.

RgbPath "/usr/X11R6/lib/X11/rgb"

# Multiple FontPath entries are allowed (which are concatenated together),
# as well as specifying multiple comma-separated entries in one FontPath
# command (or a combination of both methods)
	FontPath 	"/usr/X11R6/lib/X11/fonts/misc/"
	FontPath 	"/usr/X11R6/lib/X11/fonts/Type1/"
	FontPath 	"/usr/X11R6/lib/X11/fonts/Speedo/"
	FontPath 	"/usr/X11R6/lib/X11/fonts/75dpi/"
	FontPath 	"/usr/X11R6/lib/X11/fonts/100dpi/"

EndSection
```

上述代码定义了屏幕字体和 RGB 数据库的搜索路径。如果您将 XFree86 安装到默认目录，或让安装例程使用默认值继续，则此处不应更改任何内容。

请注意，此 XF86Config 文件中引用的目录遵循 X 的正式命名约定，使用 /usr/X11R6。然而，由于在大多数安装中，这些目录链接到 /usr/X11、/usr/X386，以及潜在的其他目录，因此可以沿链接到达目标文件。请通过依次进入每个目录并检查其中包含的文件，以验证这些目录是否确实指向屏幕字体。如果目录不存在或为空，XFree86 将无法正确加载字体，并可能崩溃或生成错误消息。

如果您向 XFree86 安装中添加新字体，它们应放在 XF86Config 文件中指定的某个字体目录中。

### 键盘设置

在大多数安装中，键盘设置默认为标准的美国 101 键键盘及其标准键映射。这对大多数计算机系统都是有效的。不过，对文件进行一些微调有助于简化您的生活，因此不应完全忽略键盘部分。以下代码显示了 XF86Config 文件中的键盘部分：

```
Section "Keyboard"

	Protocol 	"Standard"

# when using XQUEUE, comment out the above line, and uncomment the
# following line

# Protocol 	"Xqueue"

	AutoRepeat 	500 5

# Let the server do the NumLock processing. This should only be required
# when using pre-R6 clients
#	ServerNumLock

# Specify which keyboard LEDs can be user-controlled (eg, with xset(1))
# Xleds			1 2 3
# To set the LeftAlt to Meta, RightAlt key to ModeShift,
# RightCtl key to Compose, and ScrollLock key to ModeLock:

#	LeftAlt	Meta
#	RightAlt	ModeShift
#	RightCtl	Compose
#	ScrollLock	ModeLock

EndSection
```

Protocol 应保留为 “standard”。Xqueue 行被注释掉，除非您为 XFree86 实现了一个 Xqueue，否则应保持这种状态。autorepeat 设置告诉 XFree86 在生成多个按键动作之前等待按键按下的时长（例如，如果您按住 “x” 键超过一定毫秒数，它将开始打印多个 x）。

ServerNumLock 控制 XFree86 启动时 NumLock 键是开还是关。ServerNumLock 选项在大多数示例配置文件中默认是注释掉的。如果您正在运行 XFree86 版本 2.X（或更早版本），取消注释该行是个好主意。这有助于使您的键盘在 XFree86 下更好地工作。对于 XFree86 版本 3.X，您可以保持其注释状态，因为服务器将处理 NumLock 行为。

理论上，您可以使用 Xleds 设置来允许编程大多数键盘上的 LED 按钮（用于 Num Lock、Caps Lock 和 Scroll Lock）。由于 LED 很少用于用户反馈，因此请保持其注释状态。

该部分的其余内容控制 Alt、Ctrl 和 Shift 键的行为。某些 UNIX 应用程序期望称为 “meta” 键的特殊按键组合，即按住一个特殊键同时按下另一个键（如在 DOS 或 UNIX 中的 Ctrl+C）。这些条目让您控制哪些键被解释为 Alt、Meta、Control 和 ModeLock。大多数安装中这些行都被注释掉是没有问题的，因为需要特殊按键的 Linux 应用程序数量很少（且这些应用程序分布有限）。

您可以使用 XFree86 自动将按键转换为国际字符。在大多数情况下，键盘布局由 XFree86 从内核读取，尽管您可以覆盖此设置。X11 标准仅允许修改四个键表，远少于 Linux。

### 鼠标定义

XFree86 大量使用鼠标，因此您必须指定系统上的鼠标类型及其连接方式。XFree86 支持大多数流行版本的鼠标，并且任何类型的
