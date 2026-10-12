
## 表 8-1：Sox 实用程序支持的声音格式

| 文件扩展名或别名 | 描述 | 文件扩展名或别名 | 描述 |
| :---- | :---- | :---- | :---- |
| .8svx | 8SVX Amiga 乐器描述格式。 | .aiff | Apple IIf/IgX 和 SGI AIFF 文件。处理这些文件可能需要单独的归档工具。 |
| .au | Sun Microsystems AU 音频文件。这是一种流行格式。 | .cdr | 用于母版制作的光盘 CD-R 文件。 |
| .cvs | 连续可变斜率增量调制，用于语音信箱和其他语音压缩。 | .dat | 文本数据文件，包含声音数据的文本表示。 |
| .gsm | 有损语音压缩 (GSM 06.10)，用于缩小语音信箱和类似应用中的音频数据。 | .hcom | Macintosh HCOM 文件。 |
| .maud | Amiga 格式，用于生成 8 位线性、16 位线性、A-law 和 u-law 的单声道或立体声声音。 | .ossdp | 伪文件，用于打开 OSS /dev/dsp 文件并将其配置为使用传递给 Sox 的数据类型。用于播放或录制。 |
| .sf | IRCAM 声音文件，由 CSound 软件包和 MixView 采样编辑器使用。 | .smp | 来自 Turtle Beach 的 SampleVision 文件，用于与不同的 MIDI 采样器通信。 |
| .sunau | 伪文件，用于打开 /dev/audio 文件并将其设置为使用传递给 Sox 的数据类型。 | .txw | 来自 Yamaha 采样键盘的 Yamaha TX-16W。 |
| .vms | 用于压缩语音信箱和类似应用的语音音频。 | .voc | Sound Blaster VOC 文件。 |
| .wav | Microsoft WAV RIFF 文件。这是 MS Windows 的原生声音格式。 | .wve | 用于 Psion 掌上电脑的 8 位、a-law、8 kHz 声音文件。 |
| .raw | 原始文件（不包含头部信息，因此必须给出采样率、大小和风格）。 | .ub, .sb, .uw, .sw, .ul | 具有特定特征的原始文件。ub 是无符号字节；sb 是有符号字节；uw 是无符号字；sw 是有符号字；ul 是 ulaw。 |

如果您对音频文件的格式不确定，可以在文件名中添加 .auto 扩展名。这将触发 Sox 猜测文件中包含何种音频格式。.auto 扩展名仅可用于输入文件。如果 Sox 能够识别输入文件的内容，它会将其内容转换为您请求的输出文件的声音类型。

在最基本的形式中，您可以按如下方式将一种文件格式（例如 .wav 文件）转换为另一种格式（例如 .au 文件）：

```
sox file1.wav file1.au
```

要查看 Sox 正在执行的操作，请使用 -V 选项。例如：

```
$ sox -V file1.wav file1.voc

sox: Reading Wave file: Microsoft PCM format, 1 channel, 11025 samp/sec
sox:  11025 byte/sec, 1 block align, 8 bits/samp, 676354 data bytes
sox: Input file: using sample rate 11025
             size bytes, style unsigned, 1 channel
sox: Input file: comment "file1.wav"

sox: Output file: using sample rate 11025
             size bytes, style unsigned, 1 channel
sox: Output file: comment "file1.wav"
```

您可以在 Sox 转换过程中应用音效。以下示例展示了如何将采样率（使用 -r 选项）从 10,000 Hz 更改为 5000 Hz：

```
$ sox -r 10000 file1.wav -r 5000 file1.voc
```

为了减少噪音，您可以将文件通过低通滤波器。这里有一个例子：

```
$ sox file1.voc file2.voc lowp 2200
```

如需了解更多关于 Sox 的信息以及获取最新下载，请访问 SoX — Sound eXchange — 主页（`sourceforge.net/projects/sox/`）。

## 使用 CD 音频播放器

用于安装软件的同一个 CD-ROM 驱动器也可以用于播放音乐 CD。Red Hat 附带的两个基本 CD 播放器是 `gtcd`（基于 X 的 CD 播放器）和 `cdap`（基于文本的 CD 播放器）。

> **提示：** 在尝试任何 CD 播放器之前，请输入 `umount /mnt/cdrom` 来卸载驱动器中的 CD（如果已挂载）。然后您可以弹出旧 CD 并在驱动器中放入一张音频 CD。

在使用 Red Hat Linux 的 CD 播放器时，值得注意的一个功能是 CD 数据库（CDDB）支持。借助 CDDB，播放器可以检测加载的 CD，并从数据库中下载**标题**、**艺术家**和**曲目**名称信息。当您存储了喜爱的 CD 的信息后，您将始终能够看到播放器中放入的是什么 CD 以及每个曲目是什么。

> **注意：** 如果您尝试了这些 CD 播放器且 CD-ROM 驱动器无法工作，请参阅边栏“排查您的 CD-ROM 故障”以获取更多信息。

## 自动播放 CD

您将一张音乐 CD 插入计算机，它突然开始播放。如果您使用的是 Gnome 桌面，可以归功于 `magicdev`。`magicdev` 进程监视您的 CD-ROM 驱动器并自动启动 CD 播放器。

插入 CD 会自动启动播放器这一事实对某些人来说是美好的，但对其他人来说是恼人的。如果您只想播放 CD，这种行为是好事。然而，如果您想选择自己的 CD 播放器，或者在选择之前不播放 CD，您可能会发现自动播放很烦人。如果您插入一张数据 CD，`magicdev` 会表现出不同的行为。以下是 `magicdev` 的默认行为：

- **音乐 CD** — 当音乐 CD 插入时，`magicdev` 启动 `gtcd` 播放器来播放 CD 的第一首曲目。
- **数据 CD** — 当数据 CD 插入时，CD 挂载到文件系统中，并且会询问您是否要运行 CD 上可能存在的自动运行程序。第一个 CD-ROM 驱动器（`/dev/cdrom`）的挂载点是 `/mnt/cdrom`。如果您有两个驱动器，第二个（`/dev/cdrom1`）挂载在 `/mnt/cdrom1` 上（依此类推）。

您可以从 Gnome 控制面板更改 `magicdev` 的行为。方法如下：

1. 通过从终端窗口输入以下内容打开 Gnome 控制中心：

```
$ gnomecc &
```

2. 在“外设”标题下，单击“CD 属性”。
数据显示关于数据和音乐 CD 的 CD 属性信息。

3. 对于数据 CD，从以下选项中进行选择：

## 排查您的 CD-ROM 故障

如果您无法在 CD-ROM 驱动器上播放 CD，可以检查以下几点以纠正问题：

- 检查您的声卡是否已安装并正常工作（参见本章前面提到的“配置您的声卡”）。
- 检查 CD-ROM 和声卡之间的线缆是否已连接。
- 检查启动 Linux 时是否检测到了 CD-ROM。如果您的 CD-ROM 驱动器是 IDE 驱动器，请输入 `dmesg | grep ^hd`。您应该看到关于您的 CD-ROM 的消息，例如："hdc: CD-ROM SEU701, ATAPI CDROM drive" 或："hdc: ATAPI 14X CD-ROM drive, 128kB Cache."
- 如果您没有看到任何 CD-ROM 驱动器的迹象，请检查 CD-ROM 的电源和线缆是否已连接。为了确保硬件正常工作，您也可以启动到 DOS 并尝试访问 CD。
- 事实证明 CD-ROM 硬件在 DOS 中正常工作，但在 Linux 中仍不显示，您可能需要重新构建内核。此时，您可能会希望在 Linux 新闻组（例如 comp.os.linux.redhat）中询问有关您的特定 CD-ROM 驱动器的帮助。
- 尝试挂载软件 CD-ROM。如果您正在运行 Gnome 或 KDE 桌面，应该会出现一个窗口，指示 CD 已自动挂载。如果没有出现此类窗口，请转到终端窗口并输入 `mount /mnt/cdrom`。然后更改到 /mnt/cdrom 目录并使用命令 `cd /mnt/cdrom; ls` 列出内容。这会告诉您 CD-ROM 是否可访问。
- 如果您使 CD-ROM 能够工作，但尝试以非 root 用户身份播放音乐时出现消息 "CDROM device: Permission denied"，问题可能是 /dev/cdrom（通常是指向实际硬件设备的链接）除了 root 之外任何人都无法读取。输入 `ls -l /dev/cdrom` 查看该设备链接到什么。然后，假设该设备链接到的名称是 /dev/hdc，作为 root 用户输入 `chmod 644 /dev/hdc` 以允许所有用户读取您的 CD-ROM 并允许 root 用户写入。警告：如果其他人使用您的计算机，他们将能够读取您放入此驱动器的任何 CD。

