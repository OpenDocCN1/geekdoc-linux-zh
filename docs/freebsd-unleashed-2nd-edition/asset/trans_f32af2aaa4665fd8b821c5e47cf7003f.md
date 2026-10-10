

一旦你确定了想要运行的默认颜色深度，你就需要对该颜色深度的模式行进行修改（除非你计划默认运行 640×480 分辨率，在这种情况下你无需进行任何更改）。

选择你想要修改的模式行的编号，然后按 Enter 键。例如，如果你计划默认运行 24 位颜色，你应该选择之前示例屏幕中给出的**3**。这将带你进入一个类似于以下内容的屏幕。

从以下列表中选择模式：

- 1 "640×400"
- 2 "640×480"
- 3 "800×600"
- 4 "1024×768"
- 5 "1280×1024"
- 6 "320×200"
- 7 "320×240"
- 8 "400×300"
- 9 "1152×864"
- a "1600×1200"
- b "1800×1400"
- c "512×384"

请输入对应你想要选择的模式的数字。
例如，**432** 将选择 "1024×768" "800×600" "640×480"，其中默认模式为 1024×768。

哪些模式？

选择对应你想要在 X-Windows 首次启动时使用的默认分辨率的数字。例如，如果你希望 X-Windows 默认以 1024×768 分辨率启动，请选择 **4**。

如果你希望能够在不同分辨率之间切换，你可以在这里输入多个数字。第一个数字将是默认分辨率，随后列出的数字将在你发出更改屏幕分辨率的命令时，按照列出的顺序循环切换。例如，如果你希望默认分辨率为 1024×768，循环时显示的下一个分辨率为 800×600，循环时显示的最后一个分辨率为 640×480，你应该在此处输入 **432**。

大多数人一旦设置了初始分辨率，就没有改变屏幕分辨率的习惯。如果你从未更改过 Windows 或 Macintosh 系统上的屏幕分辨率，那么在 FreeBSD 中你可能也不会更改。除非你预计出于某种原因需要在各种分辨率之间来回切换，否则你可能只需在此处设置一个分辨率即可。

当你为当前颜色深度选择了所需的分辨率后，按 Enter 键继续。接下来系统会询问你关于虚拟屏幕的问题：

你可以拥有一个**虚拟屏幕（桌面）**，即比物理屏幕更大的屏幕区域，通过将鼠标移动到屏幕边缘进行平移。如果你不希望某个分辨率下拥有虚拟桌面，那么你不能列出比该分辨率更大的模式。每种颜色深度都可以拥有不同大小的虚拟屏幕。

请用 'y' 或 'n' 回答以下问题。
你想要一个比物理屏幕更大的虚拟屏幕吗？

比物理屏幕更大的虚拟屏幕会导致桌面的部分区域位于屏幕边缘之外。要查看桌面的不同部分，你需要通过将鼠标指针拖出屏幕末端来向上、下、左、右滚动。

> **注意**
> 在我看来，虚拟屏幕非常令人厌烦且难以操作。它们唯一可能合理的场景是当你被迫使用非常低的分辨率（640x480 或更低）时。即使在那种情况下，你很可能也会发现虚拟屏幕令人无法忍受且极难操作。因此，我强烈建议你在此处选择 N。

如果你决定想要一个虚拟屏幕，系统将询问你希望屏幕的分辨率是多少。选择所需的分辨率并按 Enter。

如果你决定不想要虚拟屏幕，你将返回到之前显示的模式行配置屏幕。这里显示了另一个示例屏幕：

对于每种颜色深度，都定义了一个模式（分辨率）列表。服务器启动时的默认分辨率将是显示器和显卡支持的第一种列出的模式。
当前设置为：

```
"640x480" "800x600" "1024x768" "1280x1024" for 8-bit
"640x480" "800x600" "1024x768" "1280x1024" for 16-bit
"1024x768" for 24-bit
```

由于显示器或时钟限制而无法支持的模式将被服务器自动跳过。

- 1. 更改 8 位（256 色）的模式
- 2. 更改 16 位（32K/64K 色）的模式
- 3. 更改 24 位（24 位色）的模式
- 4. 模式没问题，继续。

输入你的选择：

注意，24 位颜色的模式行已发生变化。它现在只有 1024×768 分辨率。

除非你计划运行多种颜色深度，否则你可以保持其他颜色深度不变。如果你确实计划在颜色深度之间切换，只需选择下一个要配置的颜色深度的编号，并重复前面的步骤来配置该颜色的分辨率。

当你完成所有想要配置的模式设置后，选择 **4**（模式没问题，继续）以进入下一节。

然后系统会要求你指定想要使用的默认颜色深度：

```
Please specify which color depth you want to use by default:

1 1 bit (monochrome)
2 4 bits (16 colors)
3 8 bits (256 colors)
4 16 bits (65536 colors)
5 24 bits (16 million colors)

Enter a number to choose the default depth.
```

选择你之前决定的颜色深度的编号，然后按 Enter。

在你选择所需的颜色深度后，系统会询问你是否要保存更改：

```
I am going to write the XF86Config file now. Make sure you don't accidentally overwrite a previously configured one.

Shall I write it to /etc/X11/XF86Config?
```

选择 **Y** 以写入新的 XF86Config 文件。如果你已经有一个 XF86Config 文件，它将被新文件覆盖。

一旦你在此处选择了 **Y**，xf86config 将响应以下内容：

```
File has been written. Take a look at it before running 'startx'. Note that the XF86Config file must be in one of the directories searched by the server (e.g. /etc/X11) in order to be used. Within the server press ctrl, alt and '+' simultaneously to cycle video resolutions. Pressing ctrl, alt and backspace simultaneously immediately exits the server (use if the monitor doesn't sync for a particular mode).
```

如需进一步配置，请参阅 /usr/X11R6/lib/X11/doc/README.Config。

此时，你将返回到命令提示符。你可以跳过下一节，并继续阅读紧随其后的“测试 X-Windows 设置”部分。

## 配置不在数据库中的显卡并保存配置文件

如果你没有从显卡列表数据库中选择其中一个显卡，系统将首先询问你想要使用什么默认颜色深度：

```
Please specify which color depth you want to use by default:

1 1 bit (monochrome)
2 4 bits (16 colors)
3 8 bits (256 colors)
4 16 bits (65536 colors)
5 24 bits (16 million colors)

Enter a number to choose the default depth.
```

选择对应你想要使用的默认颜色深度的编号并按 Enter。然后系统会询问你是否要保存更改：

```
I am going to write the XF86Config file now. Make sure you don't accidentally overwrite a previously configured one.

Shall I write it to /etc/X11/XF86Config?
```

在此处选择 Y 以写入配置文件。这将覆盖你现有的任何配置文件。一旦你写入了更改，xf86config 将响应以下消息并退出：

```
File has been written. Take a look at it before running 'startx'. Note that the XF86Config file must be in one of the directories searched by the server (e.g. /etc/X11) in order to be used. Within the server press ctrl, alt and '+' simultaneously to cycle video resolutions. Pressing ctrl, alt and backspace simultaneously immediately exits the server (use if the monitor doesn't sync for a particular mode).
```

如需进一步配置，请参阅 /usr/X11R6/lib/X11/doc/README.Config。

默认情况下，X-Windows 将以 640×480 分辨率启动。你可能希望将其更改为更高的分辨率。你需要手动编辑 XF86Config 配置文件才能做到这一点。XF86Config 文件将在下一节中介绍。

## 理解 XF86Config 文件

与配置 FreeBSD 的其他大多数方面类似，X-Windows 的配置由一个纯文本配置文件控制。主要的 X-Windows 配置文件位于 /etc/X11 目录下，名为 XF86Config。该文件由 xf86cfg（X-Windows 配置的图形用户界面）创建和/或修改，也由 xf86config（在本章前面部分介绍的基于文本的 X-Windows 配置界面）进行修改。这些配置工具使得 X-Windows 的配置比过去需要手动编辑文件时容易得多。

然而，仍然有一些情况你需要手动修改配置文件。例如，如果你的显卡未列在显卡数据库中，你可能需要手动修改此文件。另一种可能需要手动修改的情况是，如果你使用 xf86config 配置了 X-Windows，并希望更改鼠标设置（例如鼠标速度）。如果你只是想对 X-Windows 进行一两项小更改，手动编辑文件可能比通过 xf86config 进行完整配置更可取。

要修改 XF86Config 文件，首先制作该文件的备份副本，以便在更改导致问题时可以轻松撤销更改。例如，你可能希望将 /etc/X11/XF86Config 复制到 /etc/X11/XF86Config.bak。一旦你有了备份副本，使用你喜欢的文本编辑器打开 /etc/X11/XF86Config 文件（如果你需要了解如何使用 FreeBSD 附带的某个文本编辑器，请参阅第 6 章）。

> 请记住，FreeBSD（以及其他类 Unix 操作系统）是区分大小写的。不要将基于文本的配置程序（xf86config）与实际配置文件（XF86Config）混淆。由于区分大小写，它们是完全不同的两个文件。

