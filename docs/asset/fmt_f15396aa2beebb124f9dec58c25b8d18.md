
该工具扫描你的系统，试图识别已安装的视频硬件。你应该记下报告的信息，供以后与 `xf86config` 一起使用。你还应该将 `SuperProbe` 生成的信息与硬件文档进行仔细核对。`SuperProbe` 程序生成的信息将放入 `XF86Config` 文件的各个部分，具体见“剖析 XF86Config 文件”一节。

## 使用 XF86CONFIG

配置 X Server 的另一种方法是使用 `xf86config`。这个命令行程序会带你完成与 `XF86Setup` 相同的基本步骤。不过，该程序比 `XF86Setup` 需要更多关于硬件知识。

当 `xf86config` 启动时，会显示一个包含运行该程序重要信息的启动屏幕。可随时使用 `Ctrl+C` 组合键中止程序。

第二个屏幕要求你从屏幕上显示的列表中选择鼠标协议类型，输入对应编号。

根据你选择的鼠标协议，可能会出现一些补充问题，例如 `ChordMiddle`、`Emulate3Buttons` 或 `ClearDTR/RTS`。请阅读给出的说明并回答这些问题。

最后，系统会询问鼠标连接到哪个设备。如果设置了符号链接，通常是 `/dev/mouse`。否则，PS/2 鼠标为 `/dev/psaux`，连接到第一个或第二个串行（COM）端口的鼠标设备则为 `/dev/ttyS0` 或 `/dev/ttyS1`。

接下来是键盘部分。这可能是整个设置中最简单的部分。输入你的键盘类型和语言。

接下来是显示器部分，首先是一个信息屏幕，然后是一份常见显示器水平同步速率列表——你也可以自己输入。请回想之前关于选择高于显示器能力的刷新率的警告。

接下来是垂直同步范围，有常见选择或自定义输入的选项。

三个可选自由格式问题要求输入显示器定义标识符、供应商名称和显示器型号。

完成后，进入显卡选择。如果回答 `Yes`，将呈现超过 550 种不同显卡供你选择。选择显卡后，`xf86config` 会显示它打算写入 X Server 配置文件的信息。

下一个问题是显卡上的视频 RAM 大小，有标准答案，也可以自己填写。

随后是三个自由格式问题：显卡定义、供应商和型号。

最后，输入你的默认色彩深度。通常 `xf86config` 能够处理其余设置，并允许你保存配置文件。

## 使用 XVIDTUNE

在 X server 正常工作后，你可能会发现需要稍微调整同步频率，以防止屏幕看起来被拉伸、压缩、偏移或折行。注意，`xvidtune` 无法帮助不同步的模式——也就是说，你无法看到画面，因为图像是一系列（两个或更多）横条，或者屏幕上出现斜线。如果服务器以这种方式启动，你可以使用 `Ctrl+Alt+Plus`（数字键盘加号）组合键尝试找到一个可行的模式。

如果从命令行运行，`xvidtune` 会在命令行上提供一些有限的信息，说明它认为有效的水平和垂直同步范围（分别为 `hsync` 和 `vsync`）。然后它会显示一条标准免责声明，涉及程序的使用以及开发者对因使用该程序造成的损害（无）的责任。

图 5.1 显示了 `xvidtune` 程序运行时的外观。你可以使用按钮（如 `Left`、`Right` 和 `Taller`）调整各种水平和垂直条，然后测试或应用它们。你也可以先选择 `Auto`，以便在每次调整时即时看到效果。

`Show` 按钮仅在从 `xterm` 调用 `xvidtune` 时有效，因为输出将显示在那里。在您的情况下，这里显示了一个 `modeline`：

```text
"1152x864"    92.00    1152 1208 1368 1474    864 865 875 895
```

如您所见，所有数字都直接来自 `xvidtune` 显示。像这样的 `Modeline` 用于你的 `XF86Config` 文件，详见“剖析 XF86Config 文件”。通常，使用 XFree86 4 时，你永远不需要生成 `modeline`。

![](img/c741b1b6b6eccaba2ad43454c979a7f8_134_0.png)

让 `xvidtune` 保持运行，并遍历当前色彩深度可用的每种模式。你可以通过在服务器启动时使用不同色彩深度，并配合 `Ctrl+Alt+Plus` 组合键遍历各模式，为每种色彩深度重复此过程。

从命令行以非默认模式启动 X server 的最简单方法是在命令行上传递色彩深度。但是，对于 `startx` 之类的脚本，需要使用特殊语法——`startx -- -bpp 16`，其中将 `16` 替换为有效值，如 `8`、`15`、`16`、`24` 或 `32`。只有在为你的显卡和显示器找到良好的显示模式、色彩深度和 RAM 组合时，X server 才会启动。

## 剖析 XF86Config 文件

XFree86 v4.0 通过自动处理最复杂的步骤（`ModeLines`），大大简化了相对于以前版本的配置。但是，如果你有特殊的硬件，可能仍需要手动配置 XFree86。

XFree86 有一个配置文件 `/etc/X11/XF86Config`（或 `/etc/XF86Config`）。该文件按以下格式分布在各节中：

```text
Section "SectionName"
    Command1 "Option"
    Command2 "Option"
    Subsection "Subsection Name"
        Command3 "Option"
    EndSubSection
EndSection
```

### Modules 节

`Modules` 节标志着 XFree86 从 3.3 版到 4.0 版的最大变化之一。在旧版本的 XFree86 中，单体服务器提供服务，例如 `XF86_SVGA`（提供对 SVGA 设备的支持）和 `XF86_S3`（提供对 S3 设备的支持）。新模型提供了一个名为 `XFree86` 的单一服务器。对各种服务的支持现在通过动态加载模块提供。这为服务的提供方式以及用户选择实际使用的服务提供了更大的灵活性。

这也为提供诸如 `TrueType` 支持等以前由外部程序提供的服务提供了一种更通用的机制。

模块可以使用 `Load` 命令或 `SubSection` 加载。使用 `SubSection` 可以向模块传递选项：

```text
# This loads the DBE extension module.
    Load        "dbe"    # Double buffer extension
# This loads the miscellaneous extensions module, and disables
# initialisation of the XFree86-DGA extension within that module.
    SubSection  "extmod"
        Option  "omit xfree86-dga"  # don't initialise the DGA extension
    EndSubSection
```

> **提示**
>
> `omit xfree86-dga` 行会关闭 XFree86 的 DGA 扩展。这些扩展是 VMware（www.vmware.com）用来提高性能的。如果你使用该产品（或其他需要 DGA 的产品），则应注释掉此选项行。

### Files 节

此节定义 XFree86 的重要文件和目录。颜色（RGB）数据库、字体定义和模块库的路径都在这里定义。

### ServerFlags 节

此节定义各种 XFree86 选项标志。这些标志的默认值在几乎所有情况下都很好，很少需要修改。如果你确实需要研究这些选项，此节中的注释非常有用，只需查阅配置文件即可。

### InputDevice 节

`InputDevice` 是配置文件中可以重复的众多节之一。每个设备（鼠标、键盘、触摸屏、轨迹球等）都有自己的 `InputDevice` 节。例如，这是第一个鼠标节的开头：

```text
Section "InputDevice"
# Identifier and driver
    Identifier  "Mouse1"
    Driver      "mouse"
    Option      "Protocol"     "PS/2"
    Option      "Device"       "/dev/mouse"
```
