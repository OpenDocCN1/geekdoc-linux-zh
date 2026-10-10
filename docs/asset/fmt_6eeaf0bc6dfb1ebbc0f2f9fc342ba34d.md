
Fedora 和 RHEL 中有多种音频播放器可以播放各种格式的音乐和声音文件。在不添加任何软件的情况下，你可以播放商业音乐 CD 和 Ogg Vorbis 音频（你可以自行进行刻录和编码）。其中某些播放器可以添加 MP3 支持，红帽之外也有 MP3 播放器可用。

- `Ks Player (kscd)` — KcSD 播放器随 KDE 桌面一起。要使用 KcSD，必须安装 `kdemimedia` 包。从应用程序菜单（KDE 桌面）选择 Sound & Video（或从终端窗口输入 `kscd`）。此播放器可以从 CD 数据库获取标题、轨道和艺术家信息，并允许你将输入的信息提交到 CD 数据库（如果你的 CD 未被找到）。

- `Rhythmbox (rhythmbox)` — 使用用于 GNOME 的 Rhythmbox 音乐管理播放软件导入并管理你的音乐收藏。Rhythmbox 使用 Gstreamer 和 Sound Juicer 从 CD 中提取音乐，并使用 Ogg Vorbis、FLAC 或低质量 WAV（用于语音）音频格式压缩音乐。除了允许你为音乐库创建播放列表外，Rhythmbox 还有播放互联网广播电台的功能。通过从应用程序菜单中选择 Sound → Music Player 启动 Rhythmbox。

- `XMMS (xmms)` — 多媒体系统 `XMMS` 为播放 Ogg Vorbis、FLAC 和其他格式提供了图形界面。如果你正在运行 GNOME 或 KDE 桌面，应该会出现一个桌面图标显示 CD 已挂载。如果没有出现此类图标，进入终端并输入 `/media/cdrecorder`。然后使用 `ls /media/cdrecorder` 列出内容。

## 自动播放 CD

当你将 CD 插入驱动器时，你可能希望它自动播放。你可以在 Nautilus 中更改此行为。

> 提示：如果你有多个声卡，每块声卡由一个数字标识，0 代表第一块声卡。例如，要为第二块声卡启动 `alsamixer`，输入 `alsamixer -c 1`

## 故障 CD-ROM

如果你无法播放 CD，这里是可以检查的几点：

- 验证你的声卡已安装并正常工作（见前面的“配置声卡”）。
- 验证启动时是否检测到 CD-ROM。输入 `dmesg | grep -i`。你应该看到关于 CD-ROM 的信息，如 `ata2:0: ATAPI: HL-DT-STCD-RW/DVD DRIVE GCC424N, 0 UDMA/33`。
- 验证 CD-ROM 的电源和线已连接。为了确保硬件正常，你也可以进入 DOS 并尝试访问 CD。
- 如果没有出现图标，进入终端并输入 `/media/cdrecorder`。
- 检查你的 CD-ROM 驱动器是否因为固件 Bug 或问题被列名单。访问 tldp.org/HOWTO/Hardware-HOWTO/cdrom.html。
- 如果 CD-ROM 正常工作，但在作为非 root 用户尝试播放音乐时出现 `CDROM device: Permission denied` 错误，问题可能是与介质相关的设备 root 以外的用户无法读取。例如，作为 root 用户，驱动器输入 `mount |grep media` 查看哪个设备名称代表驱动器。然后输入 `chmod 644 /dev/scd0` 以允许所有用户读取你的 CD-ROM，并允许 root 用户对其写入。警告：如果其他人使用你的电脑，他们将能够读取放入该驱动器的任何 CD。
- 如果 CD 不工作，尝试另一张 CD。
- 如果 CD 未被识别，它可能被划伤或脏了。清洁表面。

## 使用 Rhythmbox 播放和管理音乐

Rhythmbox 是一个从一个应用程序收集、管理和播放音乐收藏的工具。如果你需要导入音乐（来自 CD、URL 或文件夹），你可以在 Rhythmbox 窗口中根据专辑、艺术家、标题或其他变量选择并排序你的音乐。Rhythmbox 还允许你播放广播电台。

从 CD 中提取音乐，并使用 Ogg Vorbis、FLAC 或低质量 WAV（用于语音）音频格式压缩音乐。

第一次运行 Rhythmbox 时，考虑通过选择 Edit -> Preferences 设置一些 Rhythmbox 偏好。在 Music 选项卡中，你可以告诉 Rhythmbox 存储音乐文件的文件夹，如图 8-5 所示。（记住这个文件夹。稍后配置 Juice 刻录 CD 时会需要它。

## 第 8 章：Linux 中的音乐、视频和图像

> 提示：你为音乐收藏选择的位置可能会占用大量磁盘空间。有些人会添加一个硬盘，或者至少准备一个大容量专用磁盘分区来存储他们的音乐和其他多媒体内容。拥有这个独立区域对于以后进行备份非常有帮助。此外，如果你以后想重新安装操作系统，可以在不损坏音乐收藏的情况下进行操作。

![](img/ec54a77854df1c8d0311d04a1e6b8d3c_368_0.png)

图 8-5：使用 Rhythmbox 定义你存储音乐的位置。

设置好“音乐”文件夹和其他偏好后，关闭偏好设置菜单并开始使用主音乐播放器（见图 8-6）。

> 注意：要让 Rhythmbox 支持 MP3，你可以使用本章前面介绍的解码器（Codec）功能。

以下是使用 Rhythmbox 的几种方法：

- `扫描可移动介质`：通过选择音乐 → 扫描可移动介质，从音频 CD 中提取曲目。如果找到音频 CD，Sound Juicer 将启动并刻录和压缩 CD 中的音乐（更多刻录音频 CD 信息请参阅“使用 Sound Juice 提取音乐 CD”章节）。
