

# 查看电视和网络摄像头

在 Linux 中让视频播放起来仍然是一次冒险。大多数电视卡和摄像头制造商并没有费心去开发 Linux 驱动程序。因此，大多数为 Linux 桌面带来视频功能的驱动程序都是通过逆向工程（即，由观察视频设备发送和接收内容的软件工程师创建的，而不是通过查看运行该设备的实际代码）得到的。

第一个，也可能是最大的一招，就是获取一块在 Linux 下受支持的电视卡或摄像头。一旦你从该设备获取了视频输出（通常可从 `/dev/video0` 获得），你就可以尝试几个应用程序来开始使用它。本节描述用于观看电视的 Xawtv 程序和用于视频会议的 GnomeMeeting 程序。

## 使用 Xawtv 观看电视

Xawtv 程序允许你在桌面上显示视频输出，特别是电视频道。你可以切换频道、调整音量，并对图像进行精细调整。附加功能允许你抓取 PBM 或 JPEG 格式的静态图像，或以 AVI 格式捕获视频片段。

默认情况下，Xawtv 会显示任何在 `/dev/video0` 设备上产生视频的设备。因此，你可以使用 Xawtv 来查看摄像头以及接收电视频道。下面的部分描述了如何选择电视采集卡并使用 Xawtv 在桌面上观看电视。

### 获取受支持的电视卡

Video4Linux 是红帽 Linux 中包含的视频接口。它支持各种电视采集卡和摄像头。对于电视采集卡，Video4Linux 依赖于 bttv 驱动程序。

要查看您可以与 Xawtv 一起使用的受支持电视卡列表，请参阅 `Cards` 文件。要查看该文件，您需要安装 kernel-source 软件包。您可以在 Linux 系统的以下位置找到 `Cards` 文件：

```text
/usr/src/linux*/Documentation/video4linux/bttv/Cards
```

该目录中还有 `CARDLIST` 和 `Insmod-options` 文件。`CARDLIST` 文件列出了每个受支持卡片的卡片编号。`Insmod-options` 文件描述了您在加载电视卡驱动程序时可能想添加的选项。

Video4Linux 旨在自动检测您的电视采集卡并加载适当的模块来激活它。因此，安装电视卡硬件（连同适当的电视接收连接），重启红帽 Linux，并按照下一节所述运行 xawtv 命令。您应该能够在 Xawtv 窗口中看到视频显示。

如果您的卡似乎没有工作，以下是您可以尝试的一些事项：

1.  要检查您的电视卡是否正确插入插槽并被 Linux 检测到，请输入以下内容：

    ```bash
    $ lspci
    ```

    这将显示计算机上所有有效 PCI 卡的列表。如果没有显示该卡的内容，您可能存在硬件问题。

2.  有可能卡在那里，但没有检测到正确的卡片类型。如果您拥有具有多个修订版的卡片，且每个版本都需要不同的驱动程序，则误检测的可能性最大。如果您认为您的卡片没有被正确检测到，请在 CARDLIST 文件中找到您的卡片。然后将适当的行添加到 `/etc/modules.conf` 文件中。例如，要添加一张 Prolink PV-BT878P，修订版 9B 的卡片，请将以下行添加到 `/etc/modules.conf`：

    ```text
    options    bttv   card=72
    ```

    您还可以添加 Insmod-options 文件中列出的其他选项。如果您仍然遇到卡片无法正常工作的问题，有一个邮件列表可供您询问关于 video4linux 的问题。其位置是：

    ```text
    http://listman.redhat.com/mailman/listinfo/video4linux-list
    ```

    您看不到视频运行 Xawtv 或其他视频应用时的另一个可能原因是 `/dev/video0` 的权限未开放。默认情况下，该设备仅对 root 用户开放。要在计算机上开放权限，以便任何用户都可以查看视频，请以 root 用户身份从终端窗口输入以下命令：

    ```bash
    # chmod 777 /dev/video0
    ```

### 运行 xawtv

要启动 Xawtv 查看器，只需在桌面的终端窗口中输入以下内容：

```bash
$ xawtv &
```

桌面窗口中应出现一个视频屏幕。单击窗口上的鼠标左键以查看电台列表。单击鼠标右键以查看设置窗口。图 8-6 显示了 Xawtv 窗口的示例，左侧是控制窗口，右侧是电台列表。

![](img/1744bde8c889adfab3fc911e1687fecf_324_0.png)

现在您可以使用电视窗口做以下几件事：

-   切换频道 — 使用上下箭头切换频道。
-   设置电台 — 为不同频道分配名称，以便按下 E 键时它们出现在频道列表中。您可以更改每个频道的名称（Station ID）和热键。
-   抓取图像 — 如果您在屏幕上看到喜欢的图像，请键入 Ctrl+J。JPEG 图像（以单词 snap 开头）将出现在您启动 Xawtv 的目录中。
-   调整图像和音频 — 使用功能键 F6–F12 更改图像质量。使用加号 (+) 和减号 (-) 键分别调高或降低音量。

表 8-2 列出了您可以在 Xawtv 中用于不同功能的按键列表。

**表 8-2：看电视时的快捷键 (xawtv)**

| 按键 | 描述 |
| :-------- | :---------- |
| A | 音频。静音和取消静音音频。 |
| F | 全屏。在标准大小和全屏之间切换。 |
| G | 抓取 PPM。以 PPM 格式捕获当前图像。（使用 Ctrl+G 抓取视频大小，而不是 PPM 格式的整个窗口。） |
| H | 获取帮助。调出首次打开 xawtv 时出现的帮助屏幕。 |
| J | 抓取 JPEG。以 JPEG 格式捕获当前图像。（使用 Ctrl+J 抓取视频大小，而不是 JPG 格式的整个窗口。） |
| R | 录制电影。调出允许您以 AVI 格式捕获视频片段的窗口。 |
| O | 设置窗口。打开设置窗口，允许您使用鼠标而不是键盘按键来选择选项。 |
| C | 频道窗口。打开频道窗口，以便您可以切换频道。 |
| E | 频道编辑器。打开频道编辑器，以便您可以添加电台和热键。 |
| Z | 频道跳跃。每隔几秒跳转到一个新的电台。 |
| T | 置顶。使显示窗口保持在顶部。 |
| 上/下箭头 | 切换频道。向上或向下切换频道。 |
| 左/右箭头 | 调谐。微调图像。 |
| 上页/下页 | 收藏夹。基于配置文件中保存的喜爱电台列表向上或向下切换频道。 |
| 功能键 (F5-F12) | 图像。调整亮度 (F5 和 F6)、色度 (F7 和 F8)、对比度 (F9 和 F10) 和颜色 (F11 和 F12)。 |
| +/- | 音量。调高或调低音量。 |
| Enter | 静音。开启或关闭音量。 |
| Q | 退出 |

您在使用 Xawtv 过程中更改的设置将存储在您的 `$HOME`/`.xawtv` 文件中。要创建频道列表，您可以运行 *scantv* 命令。它将询问您的电视和频率表，然后扫描频道并根据结果创建一个 `.xawtv` 文件。

## 使用 GnomeMeeting 进行视频会议

GnomeMeeting 窗口允许您通过网络通过视频、音频和键入消息与其他人进行通信。由于 GnomeMeeting 支持 H323 协议，您可以使用它与使用其他流行视频会议客户端（如 Microsoft NetMeeting、Cu-SeeMe 和 Intel VideoPhone）的人进行通信。

为了能够发送视频，您需要一个在 Linux 中受支持的摄像头。虽然并非所有摄像头都在 Linux 中受支持，但您仍有几十种型号可供选择。以下部分向您展示如何设置摄像头并使用 GnomeMeeting 进行视频会议。

### 获取受支持的摄像头

与电视采集卡的支持类似，摄像头支持通过 video4linux 接口提供。一些受支持的摄像头具有并行端口接口，尽管目前 Linux 支持的大多数摄像头都需要 USB 端口。

要检查您的摄像头是否受支持，请查看 /usr/src/linux*/Documentation 目录。并行端口视频摄像头中的一些在 video4linux 子目录中有描述；但是，大部分受支持的摄像头列在 usb 目录中。

> **提示：** 经过一番研究，我购买了一款 Logitech QuickCam Pro 3000。该摄像头的驱动程序是为 Philips USB 摄像头制作的，但它也适用于 Logitech、Samsung、Creative Labs 和 Askey 的摄像头。在购买之前，我在 www.smc.c.demon.nl/webcam 上查看了驱动程序的描述。

受支持的 USB 摄像头应被自动检测，以便在插入时自动加载必要的模块。只需启动 gnomemeeting 或 xawtv 命令，如果一切正常，您应该在 Linux 桌面上看到来自摄像头的视频。以下是我输入的一些用于检查摄像头是否正常工作的命令：

```bash
# lsmod
pwc
43392 1
videodev
5120 2 [pwc]
usbcore
59072 1 [audio pwc usb-uhci]
```

lsmod 的输出显示 pwc 驱动程序已加载，并与 videodev 模块和 usbcore 模块相关联。要查看关于 pwc 模块（特定于此摄像头）的信息，我输入了以下 modinfo 命令：

```bash
# modinfo -p pwc
filename:
/ lib/modules/2.4.18-0.13/kernel/drivers/usb/pwc.o
description: "Philips USB webcam driver"
author: "Nemosoft Unv. <nemosoft@smcc.demon.nl>"
license: "GPL"
parm:
size string, description "Initial image size. One of sqcif, qcif, qcif, sif, cif, vga"
parm:
fps int, description "Initial frames per second. Varies with model, useful range 5-30"
parm:
fbufs int, description "Number of internal frame buffers to reserve"
parm:
m buffs int, description "Number of external (mmap(ed) image buffers"
parm:
trace int, description "For debugging purposes"
parm:
power_save int, description "Turn power save feature in camera on or off"
parm:
compression int, description "Preferred compression quality. Range 0 (uncompressed) to 3 (high compression)"
parm:
leds int array (min = 2, max = 2), description "LED on,off
```

