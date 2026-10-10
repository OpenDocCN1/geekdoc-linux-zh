
> **注意：** 如果你的声卡不包含 MIDI 支持，请使用 `timidity` MIDI 播放器（安装 `timidity++` 软件包）。它可以转换为 MIDI 输入为 WAV 文件，可以在任何声卡上播放。要启动 `timidity`，请在命令行提示符下输入 `timidity file.mid`。

要在终端窗口中启动 `kmid`，请输入 `kmid &`。

### 使用 SoX 转换音频文件

如果你有一个某种格式的音频文件，但想将其转换为另一种格式，Linux 提供了一些转换工具供你使用。`sox` 命令可以在表 7-1 中列出的任何音频格式之间进行转换。

| 文件扩展名或别名 | 描述 | 文件扩展名或别名 | 描述 |
| --- | --- | --- | --- |
| `.8svx` | 8SVX Amiga 乐器描述格式。 | `.aiff` | Apple IIf/IIs 和 SGI AIFF 文件。处理这些文件可能需要单独的归档器。 |
| `.au`, `.snd` | Sun Microsystems AU 音频文件。这是一种流行的格式。 | `.avr` | 在 Mac 上使用的 Audio Visual Research 格式。 |
| `.cdr` | 用于制作光盘母盘的 CD-R 文件。 | `.cvs` | 连续可变斜率增量调制，用于语音邮件和其他语音压缩。 |
| `.dat` | 文本数据文件，包含声音数据的文本表示。 | `.flac` | Free Lossless Audio Codec 格式，常用于发烧友。 |
| `.gsm` | 有损语音压缩（GSM 06.10），用于压缩语音邮件和类似应用中的音频数据。 | `.hcom` | Macintosh HCOM 文件。 |
| `.maud` | 用于生成 8 位线性、16 位线性、A-law 和 u-law 单声道或立体声的 Amiga 格式。 | `.ogg` | Ogg Vorbis 压缩音频，最适合压缩音乐和流式音频。 |
| `.osdsp` | 伪文件，用于打开 OSS `/dev/dsp` 文件并将其配置为使用传递给 `sox` 的数据类型。用于播放或录制。 | `.prc` | Psion record.app 格式，比 WWE 格式更新。 |
| `.sf` | IRCAM 声音文件，由 CSound 软件包和 MixView 采样编辑器使用。 | `.smp` | 来自 Turtle Beach 的 SampleVision 文件，用于与不同的 MIDI 采样器通信。 |
| `.sph` | 来自 NIST（美国国家标准与技术研究院）的语音音频 SPHERE（Speech Header Resources）格式。 | `.sunau` | 伪文件，用于打开 `/dev/audio` 文件并将其设置为使用传递给 `sox` 的数据类型。 |
| `.txw` | 来自 Yamaha 采样键盘的 Yamaha TX-16WV。 | `.vms` | 用于压缩语音邮件和类似应用的语音音频。 |
| `.voc` | Sound Blaster VOC 文件。 | `.wav` | Microsoft WAV RIFF 文件。这是 Microsoft Windows 的原声音频格式。 |
| `.wve` | 用于 Psion 掌上电脑的文件，为 8 位、A-law、8 kHz 声音文件。 | `.raw` | 原始文件（不包含头信息，因此必须给出采样率、大小和样式）。 |
| `.ub`, `.sb`, `.uw`, `.sw`, `.ul`, `.al`, `.lu`, `.la`, `.sl` | 具有特定特征的原始文件。`ub` 是无符号字节；`sb` 是有符号字节；`uw` 是无符号字；`sw` 是有符号字；而 `ul` 是 ulaw。 | | |

**提示：** 输入 `sox -h` 以查看支持的音频类型。这还会显示支持的选项和特效。

使用可选软件包，你可以转换额外的文件格式，如 AMR-WB/AMR-NB 和 MP3 文件。你需要安装额外的库。有关 `sox` 的更多信息，请参见 http://sox.sourceforge.net。

如果你不确定音频文件的格式，可以在文件名中添加 `.auto` 扩展名。这会触发 `sox` 命令猜测文件中包含的音频格式类型。`.auto` 扩展名仅可用于输入文件。如果 `sox` 能够识别出输入文件的内容，它会将内容转换为你请求的输出文件的声音类型。

在其最基本的形式中，你可以如下将一种文件格式（如 WAV 文件）转换为另一种格式（如 AU 文件）：

```
$ sox file1.wav file1.au
```

要查看 `sox` 正在做什么，请使用 `-V` 选项。例如：

```
$ sox -V file1.wav file1.voc

sox: Reading Wave file: Microsoft PCM format, 2 channel, 44100 samp/sec
sox: 176400 byte/sec, 4 block align, 16 bits/samp, 50266944 data bytes
sox: Input file: using sample rate 11025
sox: size bytes, style unsigned, 1 channel
sox: Input file.wav: comment "file1.wav"

sox: Output file1.voc: using sample rate 44100
sox: size shorts, encoding signed (2's complement), 2 channels
sox: Output file: comment "file1.wav"
```

你可以在 `sox` 转换过程中应用声音特效。以下示例展示了如何使用 `-r` 选项将采样率从 10,000 kHz 更改为 5,000 kHz：

```
$ sox -r 10000 file1.wav -r 5000 file1.voc
```

为了减少噪音，你可以让文件通过低通滤波器。这里有一个示例：

### 提取和编码音乐

将您的音乐收藏存储到计算机的硬盘上，可以让您更轻松管理和播放音乐。使用抓轨（ripping）软件，您可以将音乐 CD 上的曲目复制到您的硬盘。作为同一过程的一部分（或作为一个独立的步骤），您可以将每个曲目编码为其他形式。通常进行编码是为了减少音频文件的大小。

Fedora 附带的用于从 CD 中提取音频曲目并将其复制到硬盘的工具包括 Sound Juicer 窗口和 `cdparanoia` 命令。Fedora 附带并通常用于编码音乐的编码器包括 `oggenc` 和 `flac`。虽然编码通常是在提取过程中的一部分完成的（例如在 Sound Juicer 中），但我提供了一个示例，说明如何在命令行中使用 `oggenc` 将 WAV 文件编码为 Ogg Vorbis 格式。

#### 使用 Sound Juicer 提取音乐 CD

Sound Juicer 是一个直观的图形工具，用于从商业音乐 CD 中提取音乐曲目。它可以读取音乐 CD 的曲目；获取 CD 专辑、艺术家和曲目信息（前提是您拥有互联网连接）；并将曲目保存到您的硬盘。在这个过程中，您还可以让 Sound Juicer 将曲目编码为 Ogg Vorbis、FLAC 或语音质量 WAV 格式。

**注意：** 您可以使用本章前面描述的 Fluendo 编解码器来获得 MP3 播放支持。购买 MP3 解码软件需要付费。

要启动 Sound Juicer，请选择 应用程序 → 声音和视频 → 音频 CD 提取器。（或者您也可以通过输入 `sound-juicer` 或从 Rhythmbox 中选择 音乐 → 导入音频 CD 来启动它。）图 7-6 显示了 Sound Juicer 窗口的示例。

以下是如何使用 Sound Juicer 从音频 CD 中提取歌曲并将其编码为任何支持的编码类型：

- 1. 启动 Sound Juicer 后，将音频 CD 插入计算机的 CD 驱动器，并在 Sound Juicer 窗口中选择 重新读取光盘。（如果启动了另一个音频播放器，您可以将其关闭。）
- 2. 选择 编辑 → 首选项。出现首选项窗口，如图 7-6 所示。
- 3. 设置以下首选项：

![](img/c78bdcb5b7842a0d73dcc98921f872a2_299_0.png)

**图 7-6：** 使用 Sound Juicer 从音乐 CD 中提取歌曲并对其进行编码。

- **CD 驱动器** — 如果您有多个 CD 驱动器，请选择要从中提取的驱动器。
- **音乐文件夹** — 选择将写入音乐曲目的文件夹。确保包含该文件夹的磁盘分区有足够的空间来存储您的音乐收藏。正如我之前提到的，对于大型收藏，使用单独的分区是个好主意。
- **曲目名称** — 这里是您确定用于存储音乐的文件名的地方。文件夹层次结构设置为艺术家姓名，后跟专辑标题。因此，同一艺术家的多个专辑将位于同一文件夹中。曲目本身（由“文件名”框指示）按曲目号和歌曲标题存储，中间用破折号分隔。您可以选择指示用于存储音乐的 文件名 和文件夹名称的不同方式。
