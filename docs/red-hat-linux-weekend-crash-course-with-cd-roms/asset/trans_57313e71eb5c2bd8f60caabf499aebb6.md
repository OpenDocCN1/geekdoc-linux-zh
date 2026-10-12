
本节将使用 xf86config 程序引导您完成 X 配置过程，以便您能够详细了解配置选项，并理解配置文件中存储的各种信息项的格式和用途。特别是，当您使用 xf86config 配置 X 时，您会看到最新版 XFree86 支持的超过 600 种显卡列表。如果在 Red Hat Linux 安装期间 X 未正确配置，您可以从此列表中选择您的显卡并创建可用的 X 配置文件。

## 使用 xf86config 程序

xf86config 程序会向您提问，您需要回答。您需要了解有关计算机显卡和显示器的一些信息才能回答这些问题。

要运行 xf86config，请以 root 身份登录，并在 shell 命令提示符下输入 xf86config。xf86config 程序会显示一个包含一些有用信息的文本屏幕。按 Enter 继续。

xf86config 程序会要求您指定鼠标协议，该协议决定 X 服务器如何与鼠标通信。程序会显示一个编号的鼠标类型列表。输入对应您鼠标类型的号码，然后按 Enter。

xf86config 程序随后会询问以下内容：

```
Please answer the following question with either 'y' or 'n'.
Do you want to enable Emulate3Buttons?
```

如果您的鼠标有两个按钮，xf86config 会建议您启用 Emulate3Buttons。输入 y。如果启用 Emulate3Buttons，您可以通过同时按下两个按钮来模拟中间按钮点击。许多 X 应用程序假定鼠标有三个按钮，因此在通常只有两个按钮的 PC 世界中，此功能非常有用。

接下来，您必须指定鼠标的完整设备名称。在 Red Hat Linux 安装期间，您会配置鼠标，安装程序会在您的鼠标设备和标准名称 /dev/mouse 之间创建链接。因此，您可以直接按 Enter。

xf86config 程序会显示键盘类型列表，并提示您选择与键盘匹配的类型。输入列表中的号码。如果没有类型匹配，您始终可以选择 1，表示通用 101 键 PC 键盘。

xf86config 程序随后会询问键盘应配置的国家/地区。同样，您需要从程序显示的列表中进行选择。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_266_0.png)

接下来，xf86config 会通知您它需要显示器的两个关键参数：

- Horizontal synchronization frequency — the number of times per second that the monitor can display a horizontal raster line, in kilohertz (kHz)
- Vertical synchronization rate — the number of times a second the monitor can display the entire screen, in Hertz (Hz)

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_267_0.png)

**您可以在显示器手册中找到这些信息。**

按 Enter 继续。xf86config 程序会显示若干水平同步频率范围，或者您可以输入 11 来输入自己的值范围。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_267_1.png)

**请勿指定超出显示器能力的水平同步范围。错误的值可能会损坏显示器。**

要输入值范围，请输入 11 然后按 Enter。程序会提示您输入范围。以连字符（-）分隔的两个值输入范围。我的显示器文档说明水平同步范围为 30–69 kHz，因此我输入如下内容：

```
Horizontal sync range: 30-69
```

接下来，xf86config 会提示您输入垂直同步速率并提供值范围；或者您可以输入 5 来输入自己的值范围。如果您知道范围，请输入 5 然后按 Enter。在下一个提示时，输入垂直同步的范围。我的显示器文档显示该范围为 50–120 Hz，因此我输入如下内容：

```
Vertical sync range: 50-120
```

接下来，您必须为显示器定义输入一个标识符。通常，您输入显示器的品牌和型号。这里可以输入任何内容。此标识符用于在配置文件的另一部分中引用显示器。对于我系统的显示器，我的回答如下：

```
Enter an identifier for your monitor definition: Micron700FGx
```

下一个任务是配置显卡设置。xf86config 程序会显示一条说明性消息并询问以下问题：

```
Do you want to look at the card database? y
```

输入 y 然后按 Enter。程序随后会显示数百张显卡的列表。（编号从零开始，一直超过 600。）按 Enter 查看每一屏以查看完整列表。显卡的品牌、型号和芯片组是您选择正确的 XFree86 X 服务器并正确配置它所需的重要信息。

通过输入适当的号码选择您的显卡。例如，我的一台 PC 配备了带有 S3 ViRGE/DX 芯片组的 Diamond Stealth 3D 2000 PRO 显卡。我在其中一屏上注意到以下行：

```
240 Diamond Multimedia Stealth 3D 2000 PRO      S3 ViRGE/DX
```

我输入 240 — 对应我的显卡的号码 — 然后按 Enter。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_268_0.png)

XFree86 的每个新版本都支持更多显卡。例如，XFree86 4.0.1 支持 749 张显卡。（作为参考，版本 3.1.2 仅支持 124 项；版本 3.3.1 支持 382 张显卡；版本 3.3.6 支持 671 张显卡。）如果您的显卡的厂商和型号未出现在列表中，但您知道视频芯片组，请尝试选择对应通用芯片组的条目。

在您输入选择后，xf86config 会显示有关您所选显卡的一些信息（以及任何适当的说明）。

按 Enter 继续后，xf86config 会询问您的显卡有多少视频内存。大多数当前显卡的视频内存从 4MB（4,096KB）到 32MB（32,768KB）不等。您至少需要 1MB 视频内存才能以 1,024×768 分辨率（水平 1,024 像素 × 垂直 768 像素）显示 256 种颜色。输入对应您显卡内存量的号码，然后按 Enter。

现在您必须为显卡提供一个标识符。输入适用于您显卡的信息。以下是我的 PC 显卡的输入内容：

```
Enter an identifier for your video card definition: Diamond Stealth 3D 2000 PRO
```

程序接下来会要求您输入默认颜色深度，以每像素位数计。选项从单色（每像素 1 位）到数百万色（每像素 24 位）。输入对应您想要的深度的号码，然后按 Enter。

此步骤完成了您与 xf86config 的会话。程序会显示以下消息，询问是否可以将 XF86Config 文件写入当前目录：

```
I am going to write the XF86Config file now. Make sure you don't accidentally overwrite a previously configured one.

Do you want it written to the current directory as 'XF86Config'? n

Please give a filename to write to: /etc/X11/XF86Config
```

对第一个问题回答 n；然后输入 /etc/X11/XF86Config 并按 Enter。xf86config 程序写入配置文件并退出。

![](img/eef64cc01382a4448bc55a2ee7dcc4ca_269_0.png)

## 运行和控制 X Window 系统

在您拥有完整的 XF86Config 文件后，您的 X 服务器应该可以运行。通常，您在 Red Hat 安装期间选择图形登录选项，因此 X 在系统每次重启时都会自动启动。

如果您未选择图形登录选项，您可以通过运行 startx 脚本来启动 X 服务器，该脚本是一个包含 shell 命令的文件。此 shell 脚本位于 /usr/X11R6/bin 目录中，但该目录应位于您的 PATH 环境变量中。因此，要运行该脚本，请在 shell 提示符下输入 startx。

有一些特殊的按键组合可用于控制 X 服务器。以下各节描述了这些控制 X 的方法。

### 使用 Ctrl+Alt+Backspace 中止 X

如果您创建新的 XF86Config 文件以尝试一些新的视频模式，您可以通过按 Ctrl+Alt+Backspace 来中止 X 服务器，从而终止 X 服务器。（在 UNIX 中，术语 kill 指异常退出程序。UNIX 甚至有一个 kill 命令可停止出错的程序。）

如果您在安装 Red Hat Linux 时选择图形登录选项，X 服务器会立即重新启动 — 但这次使用的是新 XF86Config 文件中的配置选项。如果您的系统未设置为图形登录屏幕，您将返回到文本显示。
