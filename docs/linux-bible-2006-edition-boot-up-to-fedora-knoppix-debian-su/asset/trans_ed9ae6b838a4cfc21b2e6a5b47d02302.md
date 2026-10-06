
2. 将音乐 CD 插入你的 CD-ROM 驱动器。（如果桌面上打开了 CD 播放器，请将其关闭。）

3. 使用 `cddawav` 命令提取你想要的音乐轨道。例如： 

```
# cddawav -D /dev/cdrom -B
```

这会从 CD-ROM 驱动器中读取所有音乐轨道。-B 选项表示将每个轨道输出到单独的文件。默认情况下，`cddawav` 命令将文件输出为 WAV 格式。

与其提取所有歌曲，你也可以选择单个轨道或一个轨道范围进行提取。例如，提取第 3 到第 5 个轨道，添加 `-t3+5` 选项。提取第 9 个轨道，添加 `-t9+9`。提取从第 7 个轨道到 CD 结束，添加 `-7`。

如果你使用的是低质量 CD 驱动器或有缺陷的 CD，`cddawav` 可能不是最好的抓取工具。你可以尝试使用 `cdparanoia -B` 将歌曲从 CD 提取到硬盘。

4. 当 `cddawav` 运行时，将一张空白 CD 插入可写 CD 驱动器。

5. 使用 `cdrecord` 命令将音乐写入 CD。例如：

```
# cdrecord -v /dev/cdrom -audio *.wav
```

`cdrecord` 选项告诉你在位于 /dev/cdrom 的可写 CD 设备上创建一个音频 CD (`-audio`)。`cdrecord` 命令会将当前目录下的所有 `.wav` 文件写入。`-v` 选项会导致详细输出。

6. 如果你想更改轨道的顺序，可以按照你想要的顺序输入名称（而不是 `*.wav`）。如果你的 CD 刻录机支持更高速度，你可以使用 `speed` 选项将写入速度翻倍（`speed=2`）或四倍（`speed=4`）。

创建音乐 CD 后，在标签上标明 CD 的内容。现在它可以在任何标准音乐 CD 播放器上播放了。

## 使用 Grip 抓取 CD

对于 GNOME 用户，Grip 窗口提供了一种更图形化的方法，可以将音乐从 CD 复制到硬盘，你可以直接从硬盘播放歌曲，或将其刻录回空白 CD。除了抓取音乐外，你还可以在从 CD 提取歌曲时对每首歌进行压缩。

你可以通过红色菜单选择 `Sound & Video -> Grip`（或在终端窗口中输入 `grip`）打开 Grip。图 20-6 显示了 Grip 窗口的示例。

![](img/a2d958d7eab32ca5b89b2b8af808aa70_557_0.png)

![](img/a2d958d7eab32ca5b89b2b8af808aa70_558_0.png)

要使用 grip 从 CD 提取音频轨道，请执行以下操作：

- 1. 在 Rip 窗口打开的情况下，将 CD 插入你的 CD 驱动器。如果你连接了互联网且该 CD 在 CD 数据库中已知，标题、艺术家和轨道信息将出现在窗口中。
2. 点击你想抓取（即复制到硬盘）的每个轨道。该轨道的 Rip 列中将出现一个勾选标记。
3. 点击页面顶部的 Config（配置）选项卡，然后点击 Select Encoder（选择编码器）。
4. 你可以通过点击 Encoder 框并选择编码器来选择用于压缩音乐的编码器类型（默认情况下，`aggenc` 以 Ogg Vorbis 格式压缩文件，假设你的 Linux 发行版已安装 Ogg Vorbis）。
5. 点击页面顶部的 Rip 选项卡。
6. 点击以下其中之一：
   * Rip+Encode — 这将抓取选定的歌曲（如果你在第 4 步中保留了默认的 `aggenc` 压缩），并以 Oggbis 格式压缩它们。你需要一个 Ogg Vorbis 播放器来播放以这种格式抓取后的歌曲（Linux 有许多 Ogg Vorbis 播放器）。
   * Rip only — 这以 WAV 格式抓取选定的歌曲。你可以使用标准的 CD 播放器播放这些歌曲。（当我尝试时，相同的歌曲转换为 WAV 格式后比 Ogg Vorbis 文件大 12 倍。）

歌曲按你选择的格式复制到硬盘。默认情况下，文件被复制到 $HOME/ogg 的子目录下（例如 /home/jake/ogg）。子目录以艺术家和 CD 命名。例如，如果用户 jake 正在抓取艺术家 Mumbo 的歌曲“High Life”，那么包含抓取歌曲的目录将是 /home/jake/ogg/mumbo/high_life。每个文件以歌曲命名（例如 fly_fly.wav）。

- 7. 现在你可以可以使用可以播放 WAV 或 Ogg 文件的播放器（如 XMMS）播放任何文件。或者你可以使用 `cdrecord` 将文件复制到 CD。因为文件名是相同的，它们在 CD 上的顺序可能与在 CD 上出现的顺序不同，如果你想按原始顺序将它们复制回可写 CD，你可能需要在 `cdrecord` 命令行中输入每个文件名。例如：

```
# cdrecord -dev=/cdrom --audio fly_fly.wav
big_new.wav about_time.wav
```

Grip 窗口也可以用于播放 CD。使用显示器底部的按钮进行播放或暂停、向前或向后跳过以及停止、弹出 CD。切换轨道显示按钮可以缩小显示尺寸，使其在桌面上占用更少空间。点击 toggle disc editor（切换磁盘编辑器）可以查看并更改标题、艺术家和轨道信息。

## 使用 cdlabel 创建标签

`cdlabel` 可用于创建标签。它可以创建 CD  own和正面标签。`cdlabel` 收集关于 CD 的信息并生成 PostScript 输出。`cdlabel` 软件包还带有图形（位于 /usr/share/cdlabel），你可以将其整合。

这里有一个 cdlabel 命令的示例：

```
cdlabel -c "Grunge is Gone" -s "Yep HipHop" -i "If You Feed Me" -o out
```

在此示例中，CD 的标题通过 `-c "Grunge is Gone"` 确定，艺术家通过 `-s "Yep HipHop"` 确定。轨道通过 `-i` 选项指定。结果如图 20-7 所示。

![](img/a2d958d7eab32ca5b89b2b8af808aa70_560_png)

## 第20 章 播放音乐和视频

## 处理电视、视频

### 获取电视卡

Video4Linux (V41/V42) 是 Linux 可用的视频接口。它支持多种电视卡和摄像头，并包含在某些发行版中。如果你的发行版没有包含 V4L 或 V42，你可以自行安装，尽管这并不是一项容易的任务。有关 V4L 的安装的更多信息，请访问 http://linux.bytex.org/v42/index.html。

Video4Linux 设计用于自动检测你的电视卡并加载相应的模块以激活它。安装电视卡硬件（连接到电视接收机），启动 Linux，并按照下节运行 `vptime` 命令。在你的窗口中查看视频。

### 使用 vptime 观看电视

vptime 程序（vtime 命令）允许你在桌面上显示输出——特别是电视节目。你可以更改频道、调整音量并调优图像。

vptime 不显示某些低质量摄像头的输出。要使用摄像头，可以考虑获取 xawt 包。
