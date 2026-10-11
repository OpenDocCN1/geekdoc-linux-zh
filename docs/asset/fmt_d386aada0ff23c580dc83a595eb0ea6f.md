
`lsmod` 的输出显示 `pwc` 驱动已加载并与 `videev` 模块和 `compat_ioctl32` 模块关联。

## 为 Ekika 开启防火墙

你需要在防火墙中为 Ekika 打开多个端口。特别是，你需要打开 TCP 端口 1720 和 TCP 端口 30000 到 30010。对于 UDP 端口，你必须打开 5000 到 5007 以及 5010 到 5013 端口。用于打开这些端口的精确 `iptables` 示例包含在 Ekika FAQ (www.ekika.org/faq) 中。

## 运行 Ekika

在大多数发行版中，选择“应用程序 > Ekika Softphone”来启动 Ekika。从终端启动 Ekika，输入 `ekika &`。如果没有安装，你可以在安装 GNOME 桌面时获取适用于你的 Linux 发行版的软件包。第一次运行 Ekika 时，会启动 Ekika 配置助手，允许你输入以下信息：

- 个人数据——名字、姓氏、电子邮件地址、连接方式和位置。你也可以选择在 Ekika ILS 目录中显示的内容。
- 连接类型——指示你的互联网连接速度（56K 调制解调器、ISDN、DSL/缆、T1/LAN 或自定义）。

输入数据后，Ekika 窗口打开。

## 第 4 章：播放音乐和视频

图 4-8 显示了右侧带有通讯录的 Ekiga 窗口。选择“工具 > 通讯录”打开你的 GNOME 通讯录。这你在 GNOME 中用于电子邮件和其他地址及电话信息的通讯录是同一个。在该窗口中添加 ILS 服务器和朋友，然后选择你想要联系的用户或服务器并点击“联系”。

图 4-8

连接到 ILS 服务器以使用 Ekiga 进行视频会议。

![](img/8f71f83ce3d8e208bf71b5b6c9a753bd_142_0.png)

使用视频窗口下方的标签页调整你的音频电平和视频外观。“历史”标签页显示了你的活动日志。

## 观看电影和视频

虽然 Linux 提供了相当高质量的视频播放器，但由于法律问题，在正式发行版中看到这些播放器非常罕见。Linux 中 DVD 电影编码的问题可能导致了 MPlayer (www.mplayer.hq)、Ogle (www.dtek.chalmers.se/groups/dvd) 和 xine (http://www.xine-project.org/) 等视频播放器无法进入常用 Linux 发行版的软件仓库。

## 第二部分：运行 Linux 桌面

然而，根据大多数情况，只要你不下载和使用 DeCCs（解密软件），你就可以获取并使用这些视频播放器来播放各种个人视频内容。以下章节提供了常用视频播放器的描述。

## 使用 xine 观看视频

`xine` 播放器是一个播放各种视频和音频格式的优秀应用程序。你可以从 xine.sourceforge.net 或与你的 Linux 相关的软件仓库中获取 `xine`。

对于 Fedora，`xine` 位于主仓库中。对于 Ubuntu，你还需要安装 `xine-free`（`sudo apt-get install xine-free`）。

你可以通过输入 `xine` 启动 `xine`。图 4-9 显示了 `xine` 控制的示例。

图 4-9

![](img/8f71f83ce3d8e208bf71b5b6c9a753bd_142_0.png)

## 第 4 章：播放音乐和视频

### 注意

当你尝试安装 `xine` 时，它会提示你需要以下内容：

- VCD（用于 VCD）
- DVD（用于 DVD）
- CDA（用于音乐 CD）
- MPEG（用于 MPEG）
- MP3（用于 MP3）
- AVI（用于 AVI）
- ASF（用于 ASF）
- MKV（用于 MK）
- WMV（用于 WMV）
- TS（用于 TS）
- MP4（用于 MP4）
- DTS（用于 DTS）
- Ogg（用于 Ogg）
- FLAC（用于 FLAC）
- Vorbis（用于 Vorbis）
- PartAC（用于 PartAC）
- AAC（用于 AAC）
- WAV（用于 WAV）
- QT（用于 QuickTime）

## 使用 xine 创建播放列表

点击 `xine` 窗口左侧的播放列表按钮。会出现播放列表编辑器，显示列表中的文件。你可以添加和删除内容，然后保存以后调用。

`xine` 内容被识别为媒体定位符（MRL）。每个 MRL 被识别为文件、DVD 或 VCD。文件位于路径（`/path/file`）或以 `file:`、`fifo:` 或 `stdin:` 开头。DVD 和 VCD 分别以 `dvd` 和 `vcd` 开头（例如 `vcd://0`）。

表 4-2 显示了 `xine` 播放列表编辑器的功能。

## 表 4-2

| 按钮 | 描述 |
| --- | --- |
| CDA、DVD 或 VCD | 所有 CD 或 DVD 内容被添加到播放列表。 |
| 添加 | 查看 MRL 浏览器。从该窗口点击文件从你的 Linux 文件系统中选择文件，然后点击选择添加到播放列表编辑器。（MRL 代表资源定位符，定义了远程和本地内容的标识形式。） |
| 向上移动选中 MRL | 在列表中向上移动。 |
| 向下移动选中 MRL | |
| 播放 | 播放播放列表的内容。 |
| 删除选中 MRL | 删除当前选择。 |
| 删除所有项目 | 清空播放列表。 |
| 保存 | 将播放列表保存到主目录（`$HOME/.xine/playlist`）。 |
| 加载 | 读取（保存的）播放列表。 |

## xine 技巧

让视频音频正常工作可能是一件棘手的事。如果你在让 `xine` 正常运行（或启动）时遇到困难，这里有一些技巧：

- `xine` 无法启动。为了完美运行，`xine` 需要支持 xvid 的 X 驱动。如果你的显卡在 X 中没有 xvid 支持，`xine` 在尝试打开默认 X 驱动时会立即关闭。如果你遇到这种情况，请尝试按如下方式使用 X11 驱动（速度较慢，但应该可行）启动 `xine`：

```
$ xine -VXSHM
```

## 第 4 章：播放音乐和视频

- `xine` 播放出现卡顿。如果从硬盘播放文件时出现卡顿，你可以检查几项设置：32位 I/O 和 DMA 功能，如果你的硬盘支持这些功能，它们通常会提高硬盘性能。以下是检查方法：

> 注意：不当的磁盘设置可能会导致硬盘上的数据损坏。请在执行此操作时由您自承担风险。此过程适用于 IDE 驱动器（不支持 SCSI！）！此外，如果您按照本节所述更改了 DMA 或 I/O 设置，请务必确保您的硬盘上有最新的备份，并且正在进行活动记录。

1. 测试硬盘读取速度。要测试第一个 IDE 驱动器 (`/dev/hda`)，请输入：

```bash
# hdparm -t /dev/hda
Timing buffered disk reads: 64 MB
19.31 seconds = 3.31 MB/sec
```

2. 以 root 用户身份查看当前的 DMA 和 I/O 设置：

```bash
# hdparm -c -d /dev/hda
/dev/hda:
I/O support = 0 (default 16-bit)
using_dma = 0 (off)
```

3. 该结果显示 32位 I/O 和 DMA 都是关闭的。要开启它们，请：

```bash
# hdparm -c 1 -d 1 /dev/hda
/dev/hda:
I/O support = 1 (32-bit)
using_dma = 1 (on)
```

4. 开启两个设置后，再次测试磁盘：

```bash
# hdparm -t /dev/hda
Timing buffered disk reads: 64 MB
2.2 seconds = 28.83 MB/sec
```
