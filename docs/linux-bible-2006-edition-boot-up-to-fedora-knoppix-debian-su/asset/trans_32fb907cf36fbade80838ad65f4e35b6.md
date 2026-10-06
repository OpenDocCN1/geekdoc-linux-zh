

# 512 第四部分 ♦ 运行应用程序

- * /dev/dsp, /dev/dsp1—数字采样设备，许多音频应用程序通过识别这些设备来访问您的声卡。在 Udev 下，这些设备分别符号化为 /dev/sound/dsp 和 /dev/sound/dsp1。

- * /dev/mixer, /dev/mixer1—音频混器设备。在 Udev 下，这些设备是指向 /dev/sound/mixer 和 /dev/sound/mixer1 的符号链接。

- * /dev/sequencer—为 MIDI、FM 和 GUS 提供低级接口。在 Udev 下，这些设备是指向 /dev/sound/sequencer 和 /dev/sound/sequencer 的符号链接。

- * /midi100—提供对 MIDI 端口的访问。在 Udev 下，对 MIDI 端口的访问通过指向 /dev/snd 中名为 `midiC[0-9]` 的设备特殊文件的符号链接来处理。例如，/dev/midi100 将是指向 /dev/midiCD 的符号链接。

关于 Linux 音频的通用信息，请参阅关于声卡的 Sound-HOWTO 以及关于不同类型音频文件播放软件的 Playing-HOWTO。您可以在 http://tldp.org  Linux HOTWs。

# 选择 CD 播放器

GNOME CD 播放器 (gnome-cd) 是 GNOME 桌面系统的默认 CD 播放器。事实上，如果启用了 HAL (halid)(如 Fedora 系统所示)，当您插入 CD 时，gnome-cd 会在 GNOME 桌面上自动弹出。它具有标准的播放按钮，并允许您自动从 CD 数据库（如 freeped.org）获取曲目信息（如果数据库中没有找到您的 CD，您可以输入自己的曲目信息）。

各种 CD 播放器随 Linux 发行版一起提供，也可以下载并安装。以下是您使用 Linux 播放 CD 的几种选择：

- * Rhythmbox (rhythmbox)—使用用于 GNOME 的 Rhythmbox 管理和播放软件导入并管理您的 CD 收藏。它在音频后端使用 GStreamer，并使用 Ogg Vorbis 音频格式压缩音乐。除了允许您创建音乐库的播放列表外，Rhythmbox 还具有播放网络电台的功能。

- * KcSD 播放器 (ksc)—该 CD 播放器随 KDE 自带。要使用它，必须安装多媒体包。从 KDE 桌面的主菜单中，选择 Multimedia: KcSD（或在终端窗口中输入 ksc）。像 gnome-cd 一样，此播放器允许您从 CD 数据库中查看曲目和艺术家信息。然而，KcSD 还允许您向 CD 数据库提交信息（如果未找到您的 CD）。

Grip (grip)—Grip 主要用作 CD 刻录器（ripper），也可以播放 CD。选择 Multimedia Grip（或在终端窗口中输入 grip）。它包含了从收集数据到向 CD 数据库提交数据的工具。它包含了复制（刻录）CD 曲目并将其转换为不同格式（编码）的工具。自然地，必须安装 grip 包才能使用此命令。

CDPlay (cdp)—如果您无法访问桌面，可以使用基于文本的 cdp 命令。此播放器使用键盘键来播放 CD、选择曲目、向前或后退或退出。根据您的 Linux 发行版，必须安装 cdp 或 cdplay 包才能使用此命令。

X 多媒体系统 (xmms)—XMMS 播放器可以播放多种音频格式，也可以直接从 CD 播放。

如果您尝试使用某些 CD 播放器但 CD-ROM 驱动器无法工作，请查看侧边栏“排除 CD-ROM 故障”获取更多信息。

# 排除 CD-ROM 故障

如果您无法在 CD-ROM 驱动器上播放 CD，可以检查以下几点以修复问题：

- 验证您的 CD 卡已安装并正常工作。
- 验证在启动 Linux 时检测到了 CD-ROM 驱动器。如果您的 CD-ROM 驱动器是 IDE 驱动器，输入 `dmesg | grep`。
- 检查 CD-ROM 驱动器的电缆连接和电源。
- 检查 CD 驱动器是否损坏。
- 尝试在其他电脑上播放该 CD。
- 尝试在其他驱动器上播放 CD。
- 尝试使用其他 CD。
- 检查 CD 驱动器是否被只读。
- 检查 驱动程序是否已正确加载。
- 检查驱动程序是否损坏。
- 尝试使用其他 CD 播放器。
- 检查 CD 驱动器是否被其他进程占用。
- 检查内核模块是否加载。
- 检查 `dmesg` 输出。
- 检查 `/dev/cdrom` 是否存在。
- 检查 `/dev/sr0` 是否存在。
- 检查 `ls -l /dev/cdrom`。
- 检查 `lsmod | grep cd`。
- 检查 `udev` 规则。
- 检查 `/etc/udev/rules.d/` 中的规则。

