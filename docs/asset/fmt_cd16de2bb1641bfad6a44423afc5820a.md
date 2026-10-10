
> 在我看来，虚拟屏幕非常令人厌烦且难以操作。它们唯一可能合理的场景是当你被迫使用非常低的分辨率（640x480 或更低）时。即使在那种情况下，你很可能也会发现虚拟屏幕令人无法忍受且极难操作。因此，我强烈建议你在此处选择 `N`。

如果你决定想要一个虚拟屏幕，系统将询问你希望屏幕的分辨率是多少。选择所需的分辨率并按 `Enter`。

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

当你完成所有想要配置的模式设置后，选择 `4`（模式没问题，继续）以进入下一节。

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

选择你之前决定的颜色深度的编号，然后按 `Enter`。

在你选择所需的颜色深度后，系统会询问你是否要保存更改：

```
I am going to write the XF86Config file now. Make sure you don't accidentally overwrite a previously configured one.

Shall I write it to /etc/X11/XF86Config?
```

选择 `Y` 以写入新的 `XF86Config` 文件。如果你已经有一个 `XF86Config` 文件，它将被新文件覆盖。

一旦你在此处选择了 `Y`，`xf86config` 将响应以下内容：

```
File has been written. Take a look at it before running 'startx'. Note that the XF86Config file must be in one of the directories searched by the server (e.g. /etc/X11) in order to be used. Within the server press ctrl, alt and '+' simultaneously to cycle video resolutions. Pressing ctrl, alt and backspace simultaneously immediately exits the server (use if the monitor doesn't sync for a particular mode).
```

如需进一步配置，请参阅 `/usr/X11R6/lib/X11/doc/README.Config`。

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

选择对应你想要使用的默认颜色深度的编号并按 `Enter`。然后系统会询问你是否要保存更改：

```
I am going to write the XF86Config file now. Make sure you don't accidentally overwrite a previously configured one.

Shall I write it to /etc/X11/XF86Config?
```

在此处选择 `Y` 以写入配置文件。这将覆盖你现有的任何配置文件。一旦你写入了更改，`xf86config` 将响应以下消息并退出：

```
File has been written. Take a look at it before running 'startx'. Note that the XF86Config file must be in one of the directories searched by the server (e.g. /etc/X11) in order to be used. Within the server press ctrl, alt and '+' simultaneously to cycle video resolutions. Pressing ctrl, alt and backspace simultaneously immediately exits the server (use if the monitor doesn't sync for a particular mode).
```

如需进一步配置，请参阅 `/usr/X11R6/lib/X11/doc/README.Config`。

默认情况下，X-Windows 将以 640×480 分辨率启动。你可能希望将其更改为更高的分辨率。你需要手动编辑 `XF86Config` 配置文件才能做到这一点。`XF86Config` 文件将在下一节中介绍。

## 理解 XF86Config 文件

与配置 FreeBSD 的其他大多数方面类似，X-Windows 的配置由一个纯文本配置文件控制。主要的 X-Windows 配置文件位于 `/etc/X11` 目录下，名为 `XF86Config`。该文件由 `xf86cfg`（X-Windows 配置的图形用户界面）创建和/或修改，也由 `xf86config`（在本章前面部分介绍的基于文本的 X-Windows 配置界面）进行修改。这些配置工具使得 X-Windows 的配置比过去需要手动编辑文件时容易得多。

然而，仍然有一些情况你需要手动修改配置文件。例如，如果你的显卡未列在显卡数据库中，你可能需要手动修改此文件。另一种可能需要手动修改的情况是，如果你使用 `xf86config` 配置了 X-Windows，并希望更改鼠标设置（例如鼠标速度）。如果你只是想对 X-Windows 进行一两项小更改，手动编辑文件可能比通过 `xf86config` 进行完整配置更可取。

要修改 `XF86Config` 文件，首先制作该文件的备份副本，以便在更改导致问题时可以轻松撤销更改。例如，你可能希望将 `/etc/X11/XF86Config` 复制到 `/etc/X11/XF86Config.bak`。一旦你有了备份副本，使用你喜欢的文本编辑器打开 `/etc/X11/XF86Config` 文件（如果你需要了解如何使用 FreeBSD 附带的某个文本编辑器，请参阅第 6 章）。

> 请记住，FreeBSD（以及其他类 Unix 操作系统）是区分大小写的。不要将基于文本的配置程序（`xf86config`）与实际配置文件（`XF86Config`）混淆。由于区分大小写，它们是完全不同的两个文件。

# XF86Config 语法

`XF86Config` 文件分为多个部分。每个部分都与特定的设备或配置问题相关。每个部分以关键字 `Section` 开始，后跟带引号的节名称。每个部分以关键字 `EndSection` 结束。部分正文为了便于阅读进行了缩进。注释以井号（`#`）开始，并持续到行尾。以下是 `XF86Config` 文件中某部分的示例：
