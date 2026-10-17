
# 第20章 播放音乐和视频

对于 GNOME 用户，Grip 窗口提供了一种更图形化的方法，可以将音乐从 CD 复制到硬盘，你可以直接从硬盘播放歌曲，或将其刻录回空白 CD。除了抓取音乐外，你还可以在从 CD 提取歌曲时对每首歌进行压缩。

你可以通过红色菜单选择 `Sound & Video -> Grip`（或在终端窗口中输入 `grip`）打开 Grip。图 20-6 显示了 Grip 窗口的示例。

![](img/a2d958d7eab32ca5b89b2b8af808aa70_557_0.png)

![](img/a2d958d7eab32ca5b89b2b8af808aa70_558_0.png)

要使用 `grip` 从 CD 提取音频轨道，请执行以下操作：

1. 在 Rip 窗口打开的情况下，将 CD 插入你的 CD 驱动器。如果你连接了互联网且该 CD 在 CD 数据库中已知，标题、艺术家和轨道信息将出现在窗口中。
2. 点击你想抓取（即复制到硬盘）的每个轨道。该轨道的 Rip 列中将出现一个勾选标记。
3. 点击页面顶部的 `Config`（配置）选项卡，然后点击 `Select Encoder`（选择编码器）。
4. 你可以通过点击 Encoder 框并选择编码器来选择用于压缩音乐的编码器类型（默认情况下，`aggenc` 以 Ogg Vorbis 格式压缩文件，假设你的 Linux 发行版已安装 Ogg Vorbis）。
5. 点击页面顶部的 `Rip` 选项卡。
6. 点击以下其中之一：
   * `Rip+Encode` — 这将抓取选定的歌曲（如果你在第 4 步中保留了默认的 `aggenc` 压缩），并以 Ogg Vorbis 格式压缩它们。你需要一个 Ogg Vorbis 播放器来播放以这种格式抓取后的歌曲（Linux 有许多 Ogg Vorbis 播放器）。
   * `Rip only` — 这以 WAV 格式抓取选定的歌曲。你可以使用标准的 CD 播放器播放这些歌曲。（当我尝试时，相同的歌曲转换为 WAV 格式后比 Ogg Vorbis 文件大 12 倍。）

歌曲按你选择的格式复制到硬盘。默认情况下，文件被复制到 `$HOME/ogg` 的子目录下（例如 `/home/jake/ogg`）。子目录以艺术家和 CD 命名。例如，如果用户 `jake` 正在抓取艺术家 Mumbo 的歌曲“High Life”，那么包含抓取歌曲的目录将是 `/home/jake/ogg/mumbo/high_life`。每个文件以歌曲命名（例如 `fly_fly.wav`）。

7. 现在你可以可以使用可以播放 WAV 或 Ogg 文件的播放器（如 `XMMS`）播放任何文件。或者你可以使用 `cdrecord` 将文件复制到 CD。因为文件名是相同的，它们在 CD 上的顺序可能与在 CD 上出现的顺序不同，如果你想按原始顺序将它们复制回可写 CD，你可能需要在 `cdrecord` 命令行中输入每个文件名。例如：

```
# cdrecord -dev=/cdrom --audio fly_fly.wav
big_new.wav about_time.wav
```

Grip 窗口也可以用于播放 CD。使用显示器底部的按钮进行播放或暂停、向前或向后跳过以及停止、弹出 CD。切换轨道显示按钮可以缩小显示尺寸，使其在桌面上占用更少空间。点击 `toggle disc editor`（切换磁盘编辑器）可以查看并更改标题、艺术家和轨道信息。

## 使用 cdlabel 创建标签

`cdlabel` 可用于创建标签。它可以创建 CD  own和正面标签。`cdlabel` 收集关于 CD 的信息并生成 PostScript 输出。`cdlabel` 软件包还带有图形（位于 `/usr/share/cdlabel`），你可以将其整合。

这里有一个 `cdlabel` 命令的示例：

```
cdlabel -c "Grunge is Gone" -s "Yep HipHop" -i "If You Feed Me" -o out
```

在此示例中，CD 的标题通过 `-c "Grunge is Gone"` 确定，艺术家通过 `-s "Yep HipHop"` 确定。轨道通过 `-i` 选项指定。结果如图 20-7 所示。

![](img/a2d958d7eab32ca5b89b2b8af808aa70_560_png)

## 处理电视、视频

### 获取电视卡

Video4Linux (`V41/V42`) 是 Linux 可用的视频接口。它支持多种电视卡和摄像头，并包含在某些发行版中。如果你的发行版没有包含 V4L 或 V42，你可以自行安装，尽管这并不是一项容易的任务。有关 V4L 的安装的更多信息，请访问 http://linux.bytex.org/v42/index.html。

Video4Linux 设计用于自动检测你的电视卡并加载相应的模块以激活它。安装电视卡硬件（连接到电视接收机），启动 Linux，并按照下节运行 `vptime` 命令。在你的窗口中查看视频。

### 使用 vptime 观看电视

`vptime` 程序（`vtime` 命令）允许你在桌面上显示输出——特别是电视节目。你可以更改频道、调整音量并调优图像。

`vptime` 不显示某些低质量摄像头的输出。要使用摄像头，可以考虑获取 `xawt` 包。

### 显卡配置

显卡未被正确检测，请在 `CARDLIST` 文件中查找您的显卡。然后在 `/etc/modprobe.conf` 文件中添加相应的行。例如，要添加 Prolink VK-BT878P（9B 版本）显卡，请向文件中添加以下行：

```
options bttv card=72
```

你还可以为 `bttv` 驱动程序添加 `insmod-options` 文件中列出的其他选项。如果你在让显卡工作方面仍然遇到问题，可以使用邮件列表，可以在那里提问关于 Video4Linux 的问题：http://listman.redhat.com/mailing/listinfo/video4linux-list。虽然这是针对 Red Hat 的列表，但相关信息适用于大多数发行版。

当你运行 `vttime` 或其他视频应用程序时看不到视频，一个可能的原因是其他其他人或其他视频应用程序已经打开了视频驱动程序。一次只能有一个应用程序使用视频驱动程序。video4linux 的另一个特性是，系统中第一个打开设备的人将成为其所有者。因此，你可能需要打开驱动程序的权限，允许第一个人之外的人访问 video4linux 驱动程序。

### 运行 vttime

要启动 `vttime` 查看器，只需从 `Sound & Video`（音频视频）菜单选择 `TVtime Television`（取决于你的 Linux 发行版），或在桌面的终端窗口中输入以下内容：

```
$ vttime &
```

桌面上应该弹出一个视频窗口。点击该窗口可以查看电台列表。右键点击查看 `Setup`（设置）菜单。

你可以通过 `vttime` 屏幕显示执行以下一些操作：

* 配置输入 — 更改视频源，选择电视标准（美国默认为 NTSC），并更改输入的分辨率。
* 设置画面 — 调整亮度、对比度和色调。
* 调整视频处理 — 控制尝试的帧率，配置去隔行器或添加输入过滤器。
* 调整输出 — 控制宽高比（例如，针对 16:9 输出），应用遮幅（matte），或查看过扫描模式（overscan）。

## 使用 GnomeMeeting 进行视频会议

`GnomeMeeting` 窗口让你通过网络通过视频、音频和打字消息与其他通信。由于 `GnomeMeeting` 支持 H323 协议（一种多媒体通信标准），你可以使用它与使用其他流行视频会议客户端的人通信，例如 Microsoft NetMeeting、Cu-SeeMe 和 Intel VideoPhone。

`GnomeMeeting` 不支持 NetMeeting 的共享白板功能，仅支持视频会议。

为了能够发送，你需要一个 Linux 支持的摄像头（Webcam）——你会找到几十种型号供选择。接下来的章节将向你展示如何设置摄像头以及使用 `GnomeMeeting`。

### 获取支持的摄像头

与视频采集卡一样，摄像头支持是通过 video4 接口提供的。如果你想查看你的摄像头是否被支持，请检查 `/src/linux/Documentation`。video 子目录下描述了几种并行摄像头；然而，大多数支持的摄像头列在该目录中。

经过研究，我购买了一个罗技 QuickCam Pro。该摄像头的驱动程序是为 Philips 的，但也适用于罗技、三星、Creative Labs 和 Apex 的摄像头。购买后，我在 www.linux.org 查看了驱动描述。

支持的 USB 摄像头应该会被自动检测，这样当你插入它们时，就会加载必要的模块。启动 `GnomeMeeting` (`gnomemeeting`)，你应该能看到来自 Linux 桌面的视频。

你可以通过输入以下内容来检查摄像头是否正常工作：

```
$ lsmod | grep pwc
pwc 512
usbcore 590
```
