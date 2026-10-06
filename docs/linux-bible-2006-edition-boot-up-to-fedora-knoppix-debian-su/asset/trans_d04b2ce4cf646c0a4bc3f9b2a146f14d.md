

# 536 第四部分 ♦ 运行应用程序

## 使用 Xine 创建播放列表

点击 xine 控制窗口左侧的播放列表按钮。会出现一个播放列表编辑器（Playlist Editor），显示当前播放列表中的文件。你可以添加和删除内容，然后保存列表以供以后调用。

Xine 内容被识别为资源定位符（MRLs）。每个 MRL 被识别为文件、DVD 或 VCD。文件位于常规文件路径 (/path/file)，或以 `file://`、`fifo:/` 或 `stdin:/` 为头。DVD 和 VCD 分别以 dvd 和 vcd 为头（例如，vcd:/01）。

表 20-2 显示了 xine 播放列表编辑器的按钮。

| 按钮 | 说明 |
|---|---|
| n| CDA, DVD, or VCD | 将该 CD 或 DVD 的所有内容添加到播放列表。 |
| Add | 查看 MRL 浏览器窗口。从那里，点击 File（文件）从你的 Linux 系统选择一个文件，然后点击 Select（选择）将该文件添加到播放列表编辑器。（MRL 代表资源定位符，定义了远程和本地内容的识别形式。） |
| Move Up Selected MRL Move Down Selected MRL | 在播放列表中向上或向下移动。 |
| Play | 播放播放列表的内容。 |
| Delete Selected MRL | 移除当前项。 |
| Delete All Entries | 清空整个播放列表。 |
| Save | 将播放列表保存到家目录 ($HOME/.xine/playlist)。 |
| Load | 读取（已保存的）播放列表。 |

## Xine 提示

让音频和视频正常工作有时是一项棘手的工作。如果你在让 xine 正常工作（或根本无法工作）遇到困难，这里有几个快速技巧：

- *Xine 无法启动——为了获得最佳效果，xine 需要一个支持 xvid 的 X 驱动程序。如果你的显卡在 X 中没有 xvid 支持，xine 在尝试使用默认驱动程序时立即关闭。如果你遇到这种情况，请尝试如下所示使用 X11 视频驱动运行 xine（速度较慢，但应该可行）：
  * xine -VXSHM

- *播放卡顿——如果从硬盘播放文件时出现卡顿，你可以检查几项设置：如果硬盘支持 32 位 IO 和 DMA 功能，通常可以提高硬盘性能。以下是检查方法：

![](img/a2d958d7eab32ca5b89b2b8af808aa70_568_0.png)

不当的磁盘设置可能会导致硬盘数据损坏。此操作风险风险自负。适用于 IDE 硬盘（不适用于 SCSI）！如果你在本节中更改 DMA 或 IO 设置，请确保有最新的备份，且硬盘上没有活动。

- 1. 测试硬盘读取速度。测试第一个 IDE 驱动器 (/dev/hda)，输入：

```
# hdparm -t /dev/hda
buffered disk reads: 64 MB
19.31 seconds = 3.33 MB/sec
```

- 2. 作为 root 用户设置当前的 DMA 和 IO 设置：

```
# hdparm -c /dev/hda
/dev/hda:
/O support = 0 (default 16-bit)
using_dma = 0 (off)
```

- 3. 此结果显示 32 位 IO 和 DMA 是关闭的。要开启它们，输入：

```
# hdparm -c 1 -d 1 /dev/hda
/dev/hda:
/O support = 1 (32-bit)
using_dma = 1 (on)
```

- 4. 开启两个设置后，再次测试磁盘：

```
# hdparm -t /dev/hda
Timing disk reads: 64 MB
2.2 seconds = 28.83 MB/sec
```

在此示例中，在更改了描述参数后，64MB 的缓冲磁盘读取从 19.31 秒缩到了 2.2 秒。现在播放效果会好得多。

- *Wine 无法播放流行媒体 —— 消息“no input plug-in”意味着你尝试播放的文件格式不受支持，或者它需要额外的插件（如播放 DVD 时）。如果消息显示“xy a broken file”，则该文件可能是受支持格式的专有版本。例如，我有一个 QuickTime 视频失败了，因为它需要 SVQ3 解码器（Linux 目前不支持），尽管其他 QuickTime 文件可以正常播放。

## 使用 Helix Player 和 RealPlayer 10

互联网上有大量的 RealMedia 和 RealAudio 格式内容。你可以看到并听到流行音乐家和漫画人物的视频片段；观看会议、新闻报道和音乐会等直播活动；并在离开家时收听你喜喜欢的电台。

要播放 RealMedia 和 RealAudio 内容，你可能已经猜到了，是 RealPlayer。Real Networks (www.real.com) 是互联网流媒体的领导者。有超过 5000 万唯一用户在 Real Networks 及其网站注册，每天下载超过 175,000 个文件。这还不是好消息。好消息是 RealPlayer 可以在 Fedora Core 中运行。

适用于 Linux 的 RealPlayer 10 可以通过 www.download.com 和 www.tucows.com 的 Linux 区域以及 http://proforma.com/real/player/unix/html 获取。此播放器不受 Real Networks 直接支持。此外，Real 以 Helix Player 的名称开放了 RealPlayer 的源码。Fedora Core 4（包含在随附的 光盘中）包含一个预发布的 Helix Player 版本，你可以尝试一下。

配置 RealPlayer 的指令以 HTML 格式提供，因此你可以在 Mozilla 或其他浏览器中阅读。如果需要任何补丁或变通方法，你可以通过 Real Networks 知识库中查询“Linux”一词来找到。要到达那里，点击 Support（大多数 Real Networks 页面），然后点击 Knowledge Base（知识库）。

当你安装 RealPlayer 时，系统会询问你是否想将其配置为 Netscape 插件（我建议这样做，以便你可以在 Mozilla 中播放真实内容）。之后，当你在浏览器中打开任何 Real 内容时，RealPlayer 会打开处理它。或者，你也可以通过桌面的终端窗口输入以下命令启动 RealPlayer：

```
$ realplayer &
```

Real Networks 已经发展到了 S10, S45, S50, S100, S110, S120, S210, S300, S400 和 S510。

## 使用 gPhoto 使用数字相机

使用 gPhoto 允许你直接从 Linux 系统管理照片和视频。使用 gPhoto，你可以导入图像、下载视频文件并控制相机。要开始，通过 USB 或读卡器连接你的相机。连接后，使用以下命令列出相机：

```bash
gphoto2 --list
```

这将显示已连接相机列表及其支持的功能。从你的相机导入图像，使用以下命令：

```bash
gphoto2 --camera [CAMERA_ID] --dump-all [destination_directory]
```

将 `[CAMERA_ID]` 替换为找到的 ID。gPhoto2 还支持许多操作，如重命名文件、清除相机内存和提取元数据。

## 表 20-3 gPhoto2 支持的相机

| 品牌 | 型号 |
|---|---|
| AEG | Snap 300 |
| Agfa | e 307, 780, 780C, 1280, 1680 |
| Aiptek | PalmCam, PenCam |
| Apple | QuickTake 200 |
| Canon | IXY Digital, IXY Digital 300, MV630i, MVX2i, Optura 10, Optura 20, Optura 200 MC, ZR700 |
| Canon Digital | IXUS, IXUS 2, IXUS 300, IXUS 330, IXUS 400, IXUS I, IXUS II, IXUS v, IXUS v2, IXUS v3 |
| Canon EOS | 10D, 300D, D30, Digital Rebel, Kiss Digital |
| Canon PowerShot | A5, A5 Zoom, A10, A20, A50, A60, A70, A80, A200, A300, G1, G2, G3, G5, Pro70, Pro90 I5 S10, S20, S30, S40, S45, S50, S100, S110, S120, S210, S300, S400 |
| Casio | QV | 10, 104, 11, 30, 70, 100, 200, 700, and 5000SX |
| Chinin | |
| Digitalream | 200, l'elegante, l'elite, l'espion, l'esprit, and la ronde |
| Dynatron | Dynacam 800 |
| Epson PhotoPC | 300z, 500, 550, 600, 700, 800, and 850z |

