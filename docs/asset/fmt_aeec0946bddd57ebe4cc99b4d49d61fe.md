
## `ogg123`

`ogg123` 是从命令行播放 ogg Vor 或 FLAC 音频文件的良好方法。在命令行中，你可以播放文件 (`abc.ogg`)、包含多个音乐文件的播放列表 (`--list=/tmp/mynplaylist`)，或者 HTTP 或 FTP 路径 (`http://example.com/song.ogg`)。以下是使用 `ogg123` 命令播放当前目录下 ogg Vor 文件的示例：

```
$ ogg123 0-Rhapsody in Blue.ogg
Audio Device: Advanced Linux Sound Architecture (ALSA) output
Playing: 0-Rhapsody in Blue
Ogg Vor stream: channel 2, 44100 Hz
Title: Rhapsody in Blue
Artist: George Gershwin
Track number: 1
Track total: 8
Album: Rhapsody in Blue
Genre: Instrumental
Time: 00:20:36 [15:29.65] of 15:50.01 (181.6 kbps) Output Buffer 96.9%
```

要停止 `ogg123` 播放单曲，请按 Ctrl+C 键；当队列队列时，按键退出 `ogg123`。

## `play`

`play` 命令可播放 sox 支持的各种音频格式。语法简单为 `play file.xx`。要查看 `play` 命令可以播放哪些文件格式，请输入 `sox -h` 查看列表。如果你正在寻找音效、语音内容或其他非典型多媒体音频类型的音频文件，`play` 命令非常有用。（你需要安装 sox 软件包，Fedora 和 RHEL 自带该包，才能使用 `play`。）

## `mpg321`

这与 `ogg123` 命令类似，但正如你所猜的那样，它被用于播放 MP3 音频文件。与 `ogg123` 一样，你可以播放文件 (`abc.mp3`)、包含多个文件的播放列表 (`--list=/tmp/mynplaylist`)，或者 HTTP 或 FTP 路径 (`http://example.com/song.mp3`)。与 `ogg123` 不同，`mpg321` 不随 Fedora 或 RHEL 附。你可以从 Linux 源获取 `mpg321` 软件包。

### 使用 MIDI 播放器

MIDI 代表乐器数字接口（Musical Instrument Digital Interface）。MIDI 文件由合成器和其他电子音乐设备创建。MIDI 文件比其他音频文件小，因为它们存储的是播放的音符，而不是完整的声音。MIDI 播放器通过各种 MIDI 乐器重现声音。

## 第二部分：使用 Fedora 和 RHEL

互联网上有许多下载 MIDI 文件的网站。尝试 Ifni Music 网站 (`www.ifnimidi.com`)，它包含了披头士、齐兹齐飞、涅槃等人的歌曲，并按专辑分类。大多数 MIDI 音乐非常简单，你可以尝试玩玩。

Fedora 和 RHEL 带有 `kmidi` MIDI 播放器。`Kmidi` 默认不安装（可以在 DVD 中的 `kmultimedia` 软件包中找到）。`Kmidi` 为 MIDI 音乐提供了 GUI 界面，包括实时显示歌词的能力。还有 `timidity` 播放器（来自 DVD 上的 `timidity++` 软件包），它可以让你从终端窗口运行 MIDI 音频。

> 注意：如果你的声卡不支持 MIDI，请使用 `timidity` MIDI 播放器（安装 `timidity` 软件包）。它可以将 MIDI 输入转换为可以在任何声卡上播放的 WAV 文件。要启动 `timidity`，在命令行提示符处输入 `timidity file.mid`。

要启动 `kmidi`，从终端窗口输入 `kmidi &`。

### 使用 SoX 转换音频文件

如果你有一个格式的音频文件，但希望将其转换为另一种格式，Linux 提供了一些你可以用来转换文件的工具。`sox` 可以在表 8-1 中列出的任何音频格式之间进行转换。

#### 表 8-1：Sox 工具支持的音频格式

| 文件扩展名或别名 | 描述 | 文件扩展名或别名 | 描述 |
|---|---|---|---|
| `.8svx` | 8SVX Amiga 音乐乐器描述格式。 | `.aiff` | Apple II/IIgs 和 SGI AIFF 文件。处理这些文件可能需要单独的归包。 |
| `.au, .snd` | Sun Microsystems 音频文件。这是一个流行的格式。 | `.avr` | Audio Visual Research 格式，用于 Mac。 |
| `.cdr` | 用于刻录光盘的 CD-R 文件。 | `.csv` | 连续变化增量调制，用于语音信箱和其他语音压缩。 |
| `.dat` | 文本数据文件，包含声音数据的文本表示。 | `.gsm` | 损性语音压缩 (GSM 06.10)，用于缩小语音信箱和类似应用程序中的音频数据。 |
| `.hcom` | Macintosh HCOM 文件。 | `.maud` | Amiga 格式，用于产生 8 位的声音。 |
| `.ogg` | Ogg Vorbis 压缩。 | `.mp3` | MPEG-1 Audio Layer III。 |
| `.wav` | Wave 音频格式。 | `.raw` | 未压缩的 PCM 数据。 |
| `.flac` | 免费无损音频编码器。 | `.aacac` | 高级音频编码 (Advanced Audio Coding)。 |

## 第 8 章：Linux 中的音乐、视频和图像 337

### 使用 Sound Juicer 提取 CD

Sound Juicer 是一个直观的图形工具，用于从商业音乐 CD 中提取音乐轨道。它可以读取音乐 CD 的轨道；获取 CD 专辑、艺术家和 CD 轨道信息（前提是你已连接到互联网）；并将轨道保存到硬盘上。在此过程中，你还可以让 Sound Juicer 将轨道编码为 Ogg Vorbis、FLAC 或音质级 WAV 格式。

> 注意：你可以使用本章之前介绍的 Codeina 功能来支持 MP3 播放。购买 MP3 解码软件需要付费。

启动 Sound Juicer，选择应用程序 -> 声音 -> Sound Juicer CD 提取器。（你也可以通过输入 `sound-juicer` 或通过 Rhythmbox 中的 音乐 -> 导入音频 CD 来启动它。）图 8-8 显示了 Sound Juicer 的界面。

![](img/6a8f767dda2519b458f97c2e7f586576_378_0.png)

图 8-8：使用 Sound Juicer 从音乐 CD 提取歌曲并进行编码。

以下是使用 Sound Juicer 从音频 CD 提取歌曲并将其编码为任何支持类型的方法：

- 1. 启动 Sound Juicer 后，将音频 CD 插入电脑的 CD 驱动器，并在 Sound Juicer 窗口中选择“重新读取”（如果启动了其他音频播放器，你可以将其关闭）。
- 2. 选择编辑 -> 首选项。出现首选项窗口，如图 8-8 所示。
- 3. 设置以下首选项：
    - CD 驱动器 —— 如果你有多个 CD 驱动器，选择你想要提取的一个。
    - 音乐文件夹 —— 选择写入音乐轨道的文件夹。确保包含文件夹的磁盘分区有足够的空间存储你的收藏。正如我之前提到的，对于大型收藏，使用独立分区是个好主意。
    - 轨道名称 —— 在此处标识用于存储音乐的名称。文件夹层级设置为艺术家名称，随后是专辑标题。同一艺术者的同一文件夹下可能有多个专辑。轨道本身（由文件名框指定）按轨道编号和标题存储，中间用破折号分隔。你可以选择不同的方式对文件和文件夹名称进行编码以存储音乐。
    - 输出 —— 这设置每个轨道的编码类型。你的可选有 FLAC、Ogg Vorbis 和 WAV。如果安装了 `streamer-plugins-mp3` 包，你应该会有 MP3 选项。我通常使用 Ogg Vorbis，因为它的质量良好且占用空间较小。在某些情况下，我需要更高的输出（带某些压缩），我倾向于使用 FLAC。选择 WAV 则无压缩存储文件（最高质量，体积最大）。
- 4. 关闭首选项窗口，并在 Sound Juicer 中选择“提取”。轨道将被提取，并存储在硬盘上你选择的文件夹中。

### 通过命令行提取和编码音乐 CD

与其使用图形工具（如 Sound Juicer）来提取和编码音乐 CD，你也可以使用命令。这里描述的命令在大多数 Linux 系统上都可用，而这些系统可能提供不同的图形工具。使用这些命令，你在设置用于编码的选项时也拥有更大的活性。

此过程将引导你完成从 CD 提取轨道（`cdparallax`）并将其编码为 Ogg Vorbis（`oggenc`）。

- 1. 创建一个存放音频文件的目录并切换到该目录。确保该目录可以容纳 660MB 的数据（如果你刻制的歌曲较少）。例如：

```
# mkdir /tmp/cd
# cd /tmp/cd
```

- 2. 将音乐 CD 插入 CD-ROM 驱动器（如果桌面打开了 CD 播放器，请关闭）。
