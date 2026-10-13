
- 1. 为 WordPerfect、Applixware 或 StarOffice 等程序创建一个新的应用程序链接，然后将图标安装到桌面面板中。 （提示：阅读“ KFM 手册”使用部分了解详细信息）。
- 2. 下载、创建、扫描并编辑您喜欢的图片以用作 KDE 桌面之一的背景，然后将图片安装为您的壁纸。
- 3. 向 KDE 的系统事件添加不同的声音。
- 4. 更改面板和任务栏的方向，以为显示器提供最大的屏幕空间。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_218_0.png)

## 第三部分

### 连接外部世界

#### 小时

- 9 使用通信程序
- 10 连接到互联网
- 11 配置互联网电子邮件
- 12 配置互联网新闻
- 13 互联网下载和浏览

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_220_0.png)

## 第 9 小时

### 使用通信程序

在本小时中，您将学习如何使用本书 CD-ROM 上安装的程序与外部世界进行通信。 您将学习如何设置串行端口或调制解调器，配置和使用两个通信程序，以及使用 Linux 发送和接收传真。

尽管您的 CD-ROM 包含运行 Linux 通信程序所需的所有软件，但您确实需要一个串行通信端口和调制解调器才能使用 Linux 系统拨号。 我假设您熟悉调制解调器、波特率、奇偶校验或停止位等通信术语，以及如何将调制解调器连接到计算机。

### 设置和测试您的调制解调器

您的第一个任务是找到备用串行端口。 您应该能够在计算机背面找到该端口，它很可能有 9 或 25 个引脚。 如果您使用笔记本电脑，您可能有一个 9 针公串行端口、用于内部调制解调器的 RJ-11 电话插孔，或带有 RJ-11 电话插孔的 PCMCIA 调制解调器卡。

您可以通过查看设备或 `/dev` 目录在 Linux 中找到串行端口。 在那里定义了许多设备，例如硬盘、软盘和打印机，但您应该查找类型为 `ttyS` 的设备，例如：

```
# ls /dev/ttyS*
/dev/ttyS0  /dev/ttyS1  /dev/ttyS2  /dev/ttyS3
```

这些设备对应于传统定义的 DOS 串行端口（地址可能与您的计算机相似或不同），如表 9.1 所示。

表 9.1 DOS 和 Linux 串行端口及地址

| DOS 端口 | Linux 设备 | 地址 |
|---|---|---|
| COM1 | `/dev/ttyS0` | 0x3F8 IRQ 4 |
| COM2 | `/dev/ttyS1` | 0x2F8 IRQ 3 |
| COM3 | `/dev/ttyS2` | 0x3E8 IRQ 4 |
| COM4 | `/dev/ttyS3` | 0x2E8 IRQ 3 |

如果您笔记本电脑上装有 PCMCIA 调制解调器卡，则在启用这些服务并告诉 Linux 在启动时查找 PCMCIA 设备之前，您无法使用调制解调器（或其他任何 PCMCIA 设备）。 要启用 PC 卡调制解调器，请确保您以 root 操作员身份登录，然后编辑 `/etc/sysconfig` 目录中名为 `pcmcia` 的文件，使其如下所示：

```
PCMCIA=yes
PCIC=182365
PCIC_OPTS=
CORE_OPTS=
```

这告诉 Linux 安装 PCMCIA 服务。 保存文件，然后重新启动 Linux。 您的 PC 卡调制解调器（如果安装了其他 PC 卡）应在重新启动期间被识别。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_222_0.png)

> 如果您在使用 PCMCIA 设备时遇到问题，请阅读 David Hinds 的 PCMCIA-HOWTO，您可以在 `/usr/doc/pcmcia` 目录下找到它。如果您想要了解 Linux 对 PCMCIA 支持的最新信息，请浏览 http://hyper.stanford.edu/HyperNews/get/pcmcia/home.html
>
> 要下载 OpenLinux 的最新驱动程序（内核模块），请访问 ftp://csb.stanford.edu/pub/pcmcia
>
> 如果您在设置串口时遇到问题，请阅读 Greg Hankins 的 Serial-HOWTO，也位于 `/usr/doc/HOWTO` 目录下。其中对设置串口和安装故障排除有完整讨论。
>
> 要阅读该文档（这是一个压缩的文本文件），请使用 `zless` 分页器，如下所示：
>
> > `zless /usr/doc/HOWTO/Serial-HOWTO.gz`

您可以通过使用 `dmesg` 命令检查 Linux 启动消息的部分内容来确认串口是否已启用。将 `dmesg` 命令的输出通过 `less` 分页器管道传输以显示启动消息并查找类似以下的 Serial driver 消息（完成后按 Q 键退出）：

```
# dmesg | less
```

```
Serial driver version 4.13 with no serial options enabled
ttyS0 at 0x03f8 (irq = 4) is a 16550A
ttyS3 at 0x02e8 (irq = 3) is a 16550A
```

这里复制了 `dmesg` 文件的一部分，以便您可以看到需要查找的内容。此处的输出表明系统具有 MS-DOS 等效的 COM1 和 COM4 串口，其 IRQ 在括号中列出。如果您看不到串行驱动程序或串口列表，则必须确保为 Linux 内核启用了串行线支持。默认情况下，OpenLinux 自带串行支持，因此这可能不是问题。

使用本节“使用通信程序拨号”中讨论的 `minicom` 程序与调制解调器进行交互测试。

### 使用 lisa 命令创建 `/dev/modem`

使用 `lisa` 命令设置您的调制解调器。`lisa` 命令在您选择调制解调器类型和调制解调器串口后创建一个符号链接 `/dev/modem`。确保您以 root 操作员身份运行，或使用 `su -` 命令，然后使用其 `--modem` 选项启动 `lisa`，如下所示：

```
# su -c "lisa --modem"
```

按 Enter 后，您会看到 `lisa` 对话框，如图 9.1 所示。

#### 图 9.1

`lisa` 管理程序配置所选调制解调器。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_223_0.png)

滚动选项列表以突出显示与计算机一起使用的调制解调器类型（如今几乎所有调制解调器都兼容 Hayes），然后按 Enter。`lisa` 命令会要求您选择调制解调器使用的串口，如图 9.2 所示。

#### 图 9.2

滚动串口列表，然后按 Enter 选择调制解调器的串口。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_223_1.png)

滚动串口列表以突出显示调制解调器的串口。按 Enter 后，`lisa` 会要求您选择调制解调器使用的最高速度。如果您使用的是 33.6 调制解调器，请选择 57600 bps。如果您使用的是 56K 调制解调器，请选择 115200 bps（如图 9.3 所示）。

#### 图 9.3

滚动串口速度列表并按 Enter 选择调制解调器串口的最高速度。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_224_0.png)

按 Enter 后，您将被要求输入传真号码。输入传真号码并按 Enter，或直接按 Enter 完成调制解调器的配置。`lisa` 命令退出并从所选设备创建一个符号链接（在第 5 小时“操作和搜索命令”中讨论）到名为 `/dev/modem` 的文件。

您可以通过使用 `ls` 命令列出文件 `/dev/modem` 来验证此操作，如下所示：

```
# ls -l /dev/modem
```

`lrwxrwxrwx 1 root root 5 Dec 29 15:43 /dev/modem -> ttyS0`

> 您也可以从命令行使用 `ln` 命令自行创建符号链接，就像 `lisa` 所做的那样。例如，如果您的调制解调器连接到 COM2，请确保您以 root 身份运行，然后输入以下内容：
>
> ```
> # ln -s /dev/ttyS1 /dev/modem
> ```
>
> 这会创建一个符号链接 `/dev/modem`，指向连接到调制解调器的串口。

### 使用通信程序拨号

本节介绍随 OpenLinux 发行版提供的两个通信程序：`minicom` 和 `seyon`。`minicom` 程序可以在不运行 X11 的情况下使用，也可以与 X11 一起使用。`seyon` 程序必须在运行 X Window System 时使用。

在 `/usr/bin` 目录下还有一个旧的通信程序，称为 `cu`。该程序不如 `minicom` 或 `seyon` 友好，但如果您有兴趣设置和尝试此程序，请阅读 `cu` 手册页，并务必阅读 `/usr/doc/uucp` 目录下的 `uucp` 软件文档。

### 使用 minicom 设置和拨号
