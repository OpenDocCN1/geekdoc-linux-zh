

因此，你可以使用 TVtime 来查看网络摄像头以及接收电视频道。下面的章节描述了如何选择电视采集卡并使用 TVtime 在桌面上观看电视。

> **注意：** TVtime 无法显示某些低质量网络摄像头的输出。若需使用网络摄像头，请考虑获取 `xawtv` 软件包，可以通过键入 `yum install xawtv` 来安装。

## 获取受支持的电视卡

Video4Linux 是 Fedora 自带的视频接口。它支持多种电视采集卡和摄像头。

要查看可以与 TVtime 一起使用的受支持电视卡列表，请参考 `CARDLIST` 和 `Cards` 文件。要查看这些文件，你需要安装 kernel-doc 软件包。你可以在 Linux 系统的以下位置找到 `CARDLIST.tuner` 文件：

```
/usr/share/doc/kernel-4-doc*/Documentation/video4linux/
```

`CARDLIST.bttv` 文件适用于 Video4Linux bttv 驱动，它按卡号、名称列出许多电视采集卡，有时还会按芯片组列出。此外，`CARDLIST.tuner` 列出了可能与不同电视卡相关的调谐器类型。

Video4Linux 旨在自动检测你的电视采集卡并加载正确的模块以激活它。因此，请物理安装电视卡硬件（连接到相应的电视接收设备），启动 Fedora，并按照下一节所述运行 `tvtime` 命令。你应该能够看到视频显示在 TVtime 窗口中。

如果你的卡似乎没有工作，以下是一些你可以尝试的方法：

- 要检查你的电视卡是否已正确插入插槽并被 Linux 检测到，请输入以下内容：

```
$ /sbin/lspci | less
```

这将显示你计算机上所有有效 PCI 卡的列表。如果没有显示类似“Multimedia video controller”的内容对应你的卡，你很可能遇到了硬件问题。我的 Hauppauge WinTV Go 卡（支持 Brooktree 芯片组）显示为：

```
Multimedia video controller: Brooktree Corporation Bt878 Video Capture
```

- 卡可能存在，但未检测到正确的卡类型。如果卡有多个修订版本，且每个版本都需要不同的驱动，则检测不当最可能是问题所在。如果你认为你的卡未被正确检测，请在 `CARDLIST` 文件中找到你的卡。然后，将相应的行添加到 `/etc/modprobe.conf` 文件中。例如，要添加 Prolink PV-BT878P 修订版 9B 卡，请将以下行添加到 `/etc/modprobe.conf`：

```
options bttv card=72
```

你还可以添加 *Insmod-options* 文件中列出的 bttv 驱动的其他选项。如果你仍然遇到问题，无法让卡正常工作，可以参考关于 Video4Linux 问题的邮件列表提出问题：

```
http://listsman.redhat.com/mailman/listinfo/video4linux-list
```

当你尝试运行 TVtime 或其他视频应用程序时，看不到视频的一个可能原因是其他用户或视频应用程序已经打开了视频驱动。在 Fedora 中，一次只能有一个应用程序使用视频驱动。Video4Linux 的一个怪癖是，系统上第一个打开设备的人成为该设备的所有者。因此，你可能需要打开设备文件（如 /dev/video0）的权限，以便除第一个人以外的其他人也能访问 video4linux 驱动（例如，使用 `chmod 666 /dev/video0`）。

## 启动 TVtime

要启动 TVtime 查看器，只需从“声音和视频”菜单中选择“TVtime 电视查看器”选项。或者，在桌面的终端窗口中输入以下内容：

```
$ tvtime &
```

桌面上应出现一个包含视频屏幕的窗口。单击窗口上的鼠标左键可查看当前频道号、当前时间和当前视频源（如 Television、Composite1 等）。单击鼠标右键可查看屏幕上的 Setup 菜单。如果你的卡似乎已被检测到且所需的模块已正确加载，但你没有看到任何视频，请尝试使用键盘方向键逐步前进，直到找到有效频道。如果这不起作用，请尝试进行以下调整（最重要的是视频源和电视标准），以使 TVtime 正常工作：

- **配置输入** — 此选项允许你更改视频源、选择电视标准（在美国默认为 NTSC）以及更改输入分辨率。要将视频源更改为 Composite1、S-Video、Television 或其他输入源，请右键单击 TVtime 窗口，选择 Input configuration → Change video Source。要更改电视标准，请选择 Television standard 并选择 NTSC (U.S.)、PAL (Europe) 或其他可用设置。

- **设置图像** — 调整亮度、对比度、颜色和色调。右键单击 TVtime 窗口，选择 Picture settings，然后选择 Brightness、Contrast、Saturation 或 Hue 来调整这些属性。

- **调整视频处理** — 你可以控制尝试的帧速率、配置去交错器或添加输入滤镜。右键单击 TVtime 窗口，选择 Video processing，然后选择 Attempted framerate（以降低帧速率）或 Deinterlacer 选项（以更改其他处理功能）。你还可以尝试 Input filters 来做一些有趣的事情，如反转颜色、像镜像一样翻转视频，或将视频变为黑白（使用 Chroma killer）。

如果你经常从计算机观看电视，请考虑在面板上添加一个图标（右键单击面板并选择 Add to Panel Application Launcher Sound & Video TVtime）。在 TVtime 运行时，你可以通过右键单击标题栏并选择 On Top 将其置于顶层。

## 在 TVtime 中选择频道

当视频输入工作正常且图像已按你的喜好调整后，你应该设置频道。右键单击 TVtime 窗口，选择 Channel management Scan channels for signal。TVtime 将扫描所有可用频道并记录哪些有活动信号。一旦频道扫描完成，你可以使用鼠标滚轮在活动频道之间切换。如果 TVtime 错过了某个活动频道，请使用键盘方向键前往该错过的频道，并选择 Channel management Current channel active in list。

> **提示：** xmrlv 项目提供了一种识别和下载你所在地区电视指南的方法。TVtime 包含对 xmrlv 指南文件的支持，允许你在浏览 TVtime 频道时显示当前电视节目和电视台名称。启动 xmrlv 可能有点棘手。如果你感兴趣，我建议从 XMLTV 项目网站开始（http://xmltv.org/index.php/Main_Page）。

## 使用 Ekiga 进行视频会议和 VOIP

Ekiga 应用程序（原名 GnomeMeeting）使你可以通过网络使用视频、音频和输入消息与其他人通信。由于 Ekiga 支持 H323 协议，你可以使用它与其他使用视频会议客户端的人通信，例如 Microsoft NetMeeting、Cu-SeeMe 和 Intel VideoPhone。除了视频会议，Ekiga 还支持 VOIP 和 IP 电话，以便通过互联网拨打电话。

要能够发送视频，你需要一个在 Linux 中受支持的网络摄像头。虽然并非所有网络摄像头都受 Linux 支持，但你仍有几十个型号可供选择。下面的章节将展示如何设置你的网络摄像头并使用 Ekiga 进行视频会议。

## 获取受支持的网络摄像头

与对电视采集卡的支持一样，网络摄像头支持是通过 Video4Linux 接口提供的。一些受支持的摄像头具有并口接口，但目前 Linux 支持的大多数网络摄像头都需要 USB 端口。

在 Linux 中寻找一个可用的网络摄像头有点像冒险。很少有（甚至没有）网络摄像头附带 Linux 驱动或规格，以便开源开发者创建这些驱动。已创建的网络摄像头驱动通常功能有限，有时还会随着新内核的发布而失效。此外，网络摄像头供应商有时会更换使用的芯片组而不更改网络摄像头的名称。而且，有时相同的网络摄像头会以不同的名称进行市场推广。

