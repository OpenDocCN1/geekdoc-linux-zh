
Grip 窗口可以播放 CD。使用显示器上的按钮播放或暂停、向前或后跳、停止和退出 CD。切换轨道显示按钮可以缩小显示尺寸，使其在桌面上占用更少空间。点击磁盘编辑器查看并更改标题、艺术家和轨道信息。

# 使用 cdlabelagen 创建 CD 标签

`cdlabelagen` 命令可用于创建适用于 CD 盒的内托卡（tray cards）和封面卡。你收集有关 CD 的信息，`cdlabelagen` 会生成一个 PostScript 输出文件，你可以将其发送到打印机。`cdlabelagen` 软件包还自带了一些图形资源（位于 `/usr/share/cdlabelagen/`），你可以将其整合其中。

以下是一个 `cdlabelagen` 命令行示例，它可以生成 PostScript 格式的 CD 标签文件——你可以将其写在同一行，或者如所示所示使用反斜杠将其分为多行：

```
$ cdlabelagen -c cdlabelagen -c "20th Century Collection" \\
-s "Jon Negus" \\
-i "Heart of Mine%20th Century Man%Swing. Swing, Swing%I \\
write the songs%Oh Mistress Mine%Turns%Winter Solstice" \\
-o cover.ps
```

在此示例中，`-c "20th Century Collection"` 标识 CD 的标题，`-s "Jon Negus"` 指定艺术家。曲目输入在 `-i` 选项之后，每行之间用 % 符号分隔。输出文件通过 `-o` 选项发送到 `cover.ps`。要查看并打印结果，请如下所示使用 `evince` 命令：

```bash
$ evince cover.ps
```

此示例的结果如图 4-7 所示。

图 4-7

使用 `cdlabelagen` 生成 CD 盒标签并使用 `evince` 打印。

![](img/7021538f323e6521c571e727b770a451_134_0.png)

你需要编辑 `cdlabelagen` 命令行以包含 CD 标签的标题和歌曲名称，并重新运行程序几次以获得正确的标签。当你准备好打印标签时，点击“全部打印”（Print All）。

# 电视、视频和数字图像的使用

在 Linux 中让电视采集卡、网络摄像头和其他视频设备运行起来仍然像是一场冒险。大多数电视采集卡和摄像头的制造商并不会为了生产 Linux 驱动程序而彻夜难眠。因此，大多数将视频带到 Linux 桌面的驱动程序都是通过反向工程实现的（也就是说，它们是由软件工程师通过观察视频设备的发送和接收创建的，而不是通过查看运行设备的实际代码）。

第一个可能也是最大的技巧是获取一个 Linux 支持的电视采集卡或摄像头。一旦你从该设备获取到视频输出（通常从 `/dev/video0` 获取），你就可以尝试一些应用程序开始使用它。

本节将探索用于看电视的 `tvtime` 程序和用于视频会议的 `Ekika` 程序。

## 使用 tvtime 看电视

`tvtime` 程序（`tvtime` 命令）允许你在桌面上显示视频输出——特别是电视节目。你可以切换频道、调整音量并精调图像。此外，`tvtime` 支持流畅的屏幕上显示和宽屏显示支持。

接下来的章节描述了如何选择电视采集卡以及使用 `tvtime` 在桌面上看电视。

### 获取支持的电视采集卡

`Video4Linux` (`V4L2`) 是 Linux 可用的视频接口。它支持多种电视采集卡和摄像头，并包含在某些发行版中。如果你的发行版不包含 V4 或 `V4L2`，你可以自行安装它，尽管这并不是最容易完成的任务。有关安装和使用 V4L 以及相应驱动程序的更多信息，请访问 http://linux.org/v4wiki/index.html。MythTV 项目提供了关于 Linux 电视采集卡的见解（www.myhtv.org/wiki/index.php/Video_capture_card）。

`Video4Linux` 设计用于自动检测你的电视采集卡并加载相应的模块来激活它。安装电视采集卡硬件（并连接到你的电视接收设备），启动 Linux，并按照下一节描述运行 `tvtime` 命令。你应该能在 `tvtime` 窗口中看到视频显示。

如果你的卡看起来不起工作，这里有你可以尝试的几种方法：

- 检查电视采集卡是否正确插入插槽并通过输入以下命令被 Linux 检测到：

```
$ /sbin/lspci | grep -i video

00:09.0 Multimedia video.controller: Brooktree Corporation Bt878
    00:09.0 Multimedia video.controller: Brooktree Corporation Bt878
```

- 将以下内容添加到 `/etc/modprobe.conf` 文件中。例如，添加：

```
options bttv card=7
```

### 运行 tvtime

要启动 `tvtime`，只需从以下处选择视频：

```
$ tvtime
```
