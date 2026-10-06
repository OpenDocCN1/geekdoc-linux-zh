

# 第 20 章 ♦ 播放音乐和视频

## 使用 MIDI 音频播放器

MIDI（乐器数字接口）文件由合成器和其他电子音乐设备创建。它们通常比其他音频文件小，因为它们并不存储完整的声音，而是包含播放的音符、速度和处理法的信息。你可以将 MIDI 文件视为电子乐谱。MIDI 播放器通过还原这些音符，使其听起来像各种 MIDI 乐器。

互联网上有许多下载 MIDI 文件的网站。例如尝试 Infini Music 网站（www.ifin.com），它包含了按专辑组织的披头士乐队、齐齐飞飞乐队、涅槃乐队等的歌曲。大多数 MIDI 音乐很简单，但你可以尽情玩其中的乐趣。

像 KDE 桌面（如 Fedora）这样的 Linux 发行版通常带有 kmid 播放器。Kmid 为 MIDI 音乐提供了 GUI 界面，包括实时显示卡拉歌词的能力。在 Fedora 中启动 kmid，选择声音与视频 > Kmid（或在终端窗口中输入 `kmid &`）。

## 执行音频文件转换和压缩

存储和压缩语音及音乐文件有许多不同的格式。由于音乐文件可能很大，它们通常存储在压缩格式中。虽然 MP3 是可选的压缩格式，但 Ogg Vorbis 正在迅速成为开源社区压缩音乐的首选。Ogg Vorbis 的额外优点是不会像 MP3 那样受到专利的限制。

使用 Fedora Core 进行音频文件转换和压缩的工具包括：

- sox (SOX) — 一种通用工具，用于在多种格式之间转换音频文件。
- oggenc 一种专门将音乐文件转换为 Ogg Vorbis 格式的工具。

## 使用 SoX 转换音频文件

如果你有一个格式的声音文件，但想将其转换为另一种格式，Linux 提供了一些转换工具。SoX 实用可以将并翻译到表 20-1 中列出的任何音频格式。

输入 `sox -h` 查看支持的音频类型以及支持的选项和效果。

![](img/a2d958d7eab32ca5b89b2b8af808aa70_552_0.png)

### 表 20-1：SoX 工具支持的声音格式

| 文件扩展名或别名 | 描述 | 文件扩展名或别名 | 描述 |
|---|---|---|---|
| .8svx | 8SVX Amiga 乐器描述格式 | .aiff | Apple IIc/IIgs 和 SGI AIFF 文件。可能需要归档器来处理这些文件。 |
| .au,.snd | Sun Microsystems AU 音频文件。这曾是一种流行格式。（.snd 扩展名具有歧义，因为它也用于 NeXT 格式和无头式 Mac/PC 格式。） | .avr | Audio Visual Research 格式，用于 Mac。 |
| .cdr | 用于刻录紧光盘的 CD-R 文件。 | .csv | 连续变斜率增量调制，用于语音信箱和其他语音压缩。 |
| .dat | 文本数据文件，包含声音数据的表示。 | .gsm | 有损语音压缩 (GSM 06.10)，用于缩小语音信箱和类似应用中的音频数据。 |
| .hcom | Macintosh HCOM 文件。 | .maud | Amiga 格式，用于生成 8 位线性、16 位线性、A-law 和 u-law 的单声道或立体声声音。 |
| .ogg | Ogg Vorbis 压缩音频，最适用于压缩音乐和流音频。 | .ossdsp | 伪文件，用于打开 /dev/dsp 文件并配置为使用传递给 Sox 的数据类型。用于播放或录制。 |
| .prc | Psion record.app 格式，比 WVE 格式新。 | .sf | IRCAM 声音文件，由 Csound 包和 MixView 采样编辑器使用。 |
| .sph | 来自 NIST（美国标准技术研究院）的音频 SPHERE（语音头资源）格式。 | .smp | Turtle Beach 的 SampleVision 文件，用于与不同的 MIDI 采样器通信。 |
| .sunau | 伪文件，用于打开 `/dev/audio` 文件并设置为使用传递给 SoX 的数据类型。 | .xw | 雅马采样键盘的 TX-16W。 |
| .vms | 用于语音和类似应用的压缩语音音频。 | .voc | Sound Blaster VOC 文件。 |
| .wav | Microsoft WAV RIFF 文件。这是微软 Windows 的原生生声音格式。 | .wve | 用于 Pismalt 计算机的 8 位、a-law、8 KHz 声音文件。 |
| .raw | 原始文件（不包含头部信息，因此必须给出采样率、大小和样式）。 | .ub, .sb, .uw, .sw, .ul, .al, .lu, .la, .sl | 具有特定特征的原始文件。ub 是无符号字节；sb 是符号字节；uw 是无符号字；sw 和 ul 是符号字。 |

如果你不确定音频文件的格式，可以在文件名后添加 `.auto` 扩展名。这将触发 SoX 猜测文件中包含什么种音频格式。`.auto` 扩展名只能用于输入文件。如果 SoX 确定了输入文件的内容，它将为你翻译成声音类型。在最基本的形式下，你可以如下将一种文件格式（如 WAV 文件）转换为另一种格式（如 AU 文件）：

```
$ sox file1.wav file1
```

要查看 SoX 正在做什么，请使用 -V 选项。例如：

```bash
$ sox -V file1.wav file1.voc
# Reading file: file1.wav: PCM format, 2 channel, 44100 samples/sec
# Input: 176400 bytes/sec, block align, 16 bits/sample, unsigned, 1 channel
# Input file: file1.wav
# Output file: file1.voc: using sample rate 44100, size 176400 bytes/sec, encoding signed (2'complement), 2 channels
# Output file: file1.wav
```

你可以在转换过程中应用效果。以下示例显示了如何使用 `-r` 选项将采样率从 10000 Hz 更改为 5000 Hz：

```bash
$ sox -r 5000 file1.wav file2.wav lowpass
```

为了减少噪声，你可以将文件通过低通滤波器。这是一个示例：

```bash
$ sox file1.wav file2.wav lowpass
```

欲了解更多关于 SoX 的信息请访问 SoX 主页（https://sourceforge.net/projects/sox/）。

## 使用 ogg 压缩音乐文件

ogg 命令将音乐或其他 AIFF 转换为 Ogg Vorbis 格式。通过 Ogg Vorbis，音频可以在不明显损失质量的情况下显著缩小。在最基本的形式下，你可以使用 oggenc 一个或多个 WAV 文件。例如：

```
$ oggenc *.wav
```

此命令会将当前目录下所有以 .wav 结尾的文件转换为 Ogg 格式。OGG 文件可以在许多音频播放器中播放，包括之前提到的 XMMS。

> 如果你想从 CD 刻录并压缩音乐文件，可以使用 Grip（后文将介绍）。该工具也可用于复制音频 CD。

![](img/a2d958d7eab32ca5b89b2b8af808aa70_555_png)

## 录制和刻录音乐

可写光驱是计算机的标准设备。以前你曾不得不使用软磁盘（1.44MB）或 Zip 磁盘（100MB）存储个人数据，光驱刻录机让你存储超过 660MB 的数据，并可以使用与其他计算机交换的格式。

在 Linux 上既有图形和命令行工具用于创建 CD。cdrecord 命令允许你从命令行向可刻录（CD-R）和可重写（CD-RW）驱动器创建音频和数据 CD。该命令将在下一节中讨论。

## 使用 cdrecord 创建音频 CD

你可以使用 cdrecord 命令创建数据 CD 或音乐 CD。你可以通过设置单独的文件系统并将该映像复制到系统来创建数据 CD。创建音频 CD 包括选择你想复制的音频轨道并将它们全部复制到 CD。

本节重点介绍使用 cdrecord 创建音频 CD。cdrecord 可以使用 .au、wav 和 .cdr 格式的音频文件，并在必要时进行翻译。如果你使用其他格式的音频文件，可以使用 sox 命令（在本章之前介绍）将其转换为支持的格式之一。

创建音频 CD 的一种方法是 cdda2wav 将音乐轨道提取（复制）到目录，然后使用 cdrecord 从目录将其写入 CD。这是一个示例：

> 如果你更倾向于使用图形工具复制和刻录 CD 和 DVD，请参考附录 A，它描述了如何使用 K3B Kreator 刻录 镜像。该工具也可用于复制音频 CD。

- 1. 创建一个存放音频文件的目录，并进入该目录。（确保目录可以容纳 660MB 数据——如果你刻的歌曲较少则更小）。例如：

```bash
mkdir /tmp/cd
cd /tmp/cd
```

![](img/a2d958d7eab32ca5b89b2b8af808aa70_556_png)

