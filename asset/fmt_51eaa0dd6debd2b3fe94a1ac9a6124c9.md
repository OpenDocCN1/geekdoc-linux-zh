
播放列表编辑器让您组合想要播放的音频文件列表。您可以从此列表中添加和删除文件，将其保存到文件中并在稍后再次使用。点击 `XMMS` 窗口中的 `PL` 按钮打开播放列表编辑器。

播放列表编辑器允许您通过以下方式操作文件：

- 添加文件到播放列表 — 点击“添加”按钮。出现“加载文件”窗口。选择包含文件的目录。点击确定。文件将出现在播放列表中。
- 选择文件进行播放 — 要选择文件，使用播放列表中的上一曲/下一曲按钮。文件将高亮。点击播放按钮播放该文件。
- 从播放列表中删除文件 — 要从播放列表中删除文件，右键点击列表并选择移除 -> 已选中。
- 在播放列表上排序 — 要以不同方式对播放列表排序，按住鼠标并按标题、文件名、路径排序。您也可以随机或反转列表。
- 保存播放列表 — 要保存当前播放列表，按住列表按钮并选择保存。浏览到您所在的目录，然后输入想要赋予播放列表的名称并点击确定。
- 加载播放列表 — 要重新加载保存的播放列表，点击列表。从您保存它的目录选择播放列表并点击确定。

播放列表底部有一组小按钮。这些按钮与主屏幕上的相同，用于选择轨道、播放、暂停或弹出当前轨道。

## 第 8 章：Linux 中的音乐、视频和图像

### 使用 `ogl23`、`mpg321` 和 `play` 命令行

命令行音乐播放器如果您在 shell（无图形界面）工作或想从脚本播放音频文件，将非常方便。这里是一些可能您感兴趣的命令行播放器：

- `ogl23` — 从命令行播放 Ogg Vorbis 或 FLAC 音文件的良好方法。从命令行，您可以播放文件（`--abc.ogg`）、包含多个文件的列表（`--list=/tmp/myownlist`）或 HTTP 或 FTP 地址（`http://example.com/song.ogg`）。以下是 `ogl23` 从当前目录播放 Ogg Vorbis 文件的示例：

```
$ ogl23 01-Rhapsody_in_Blue.ogg
Audio Device: Advanced Linux Sound Architecture (ALSA) output
Ogg Vorbis stream: 2 channel, 44100 Hz
Title: Rhapsody in Blue
Artist: George Gerswin
Track number: 1
Tracktotal: 8
Album: Rhapsody in Blue
Genre: Instrumental
Time: 20:03.36 [15:29.65] of 15:50.01 (181.6 kbps) Output Buffer 96.9%
```

要停止 `ogl23` 播放单曲，按 `Ctrl+C`。当有多个轨道排队时，两次 `Ctrl+C` 退出 `ogl23`。

- `play` `play` 命令可以用于播放 `sox` 支持的各种音频格式。语法简单为 `play file.xx`。要查看 `play` 命令可以播放哪些文件格式，输入 `play -h` 查看列表。如果您正在查找包含音效、语音内容或其他音频文件的目录，`play` 命令将非常有用。

### 第二部分：使用 Fedora 和 RHEL

这些不是典型的主流多媒体音频类型。（你需要安装 `so` 包，该包随 Fedora 和 RHEL 提供，才能进行播放。）

- `mpg321` — 这类似于 `ogg123` 命令，但它（正如你可能猜的那样）使用解压来播放 MP3 音频文件。像 `ogg123` 一样，你可以播放一个文件 (`abc.mp3`)、一个包含多个文件的列表 (`--list /tmp/myplaylist`)，或者一个 HTTP 或 FTP 位置 (`http://example.com/song.mp3`)。与 `ogg123` 不同，`mpg321` 不随 Fedora 或 RHEL 提供。你可以从 Livna.org 网站获取 `mpg321` 包。

#### 使用 MIDI 播放器

`MIDI` 代表乐器数字接口（Musical Instrument Digital Interface）。`MIDI` 文件由合成器和其他电子设备创建。`MIDI` 文件通常比其他音频文件小，因为它们存储的是播放的音符而不是完整的声音。`MIDI` 播放器重放音符，使其听起来像各种 `MIDI` 乐器。

网上有很多网站可以下载 `MIDI` 文件。尝试 Ifni `MIDI` Music 网站 (`www.ifni.com`)，其中包含按专辑分类的披士乐队、齐飞飞乐队、涅槃和其他乐队的歌曲。大多数 `MIDI` 音乐非常简单，但你可以尝试播放一下。

Fedora 和 RHEL 带了 `kmid` 播放器。`Kmid` 默认不安装（在 DVD 的 `kdeutimedia` 包中可以找到）。`Kmid` 为 `MIDI` 音乐提供了图形界面，包括实时显示卡拉歌词的功能。还有 `timidity` `MIDI` 播放器（来自 DVD 上的 `timidity++` 包），它可以让你从终端窗口运行 `MIDI` 音频。

> 注意：如果你的声卡不支持 `MIDI`，请使用 `timidity` `MIDI` 播放器。它可以将 `MIDI` 输入转换为可以在任何声卡上播放的 `WAV` 文件。要启动 `timidity`，请在命令行输入 `timidity file.mid &`。

要启动 `kmid`，从终端窗口输入 `kmid &`。

#### 使用 SoX 转换音频文件

如果你有一个某种格式的音频文件，但想将其转换为另一种格式，Linux 提供了一些你可以使用的工具来转换文件。`sox` 工具可以在表 8-1 列出的任何音频格式之间进行相互转换。

> 提示：输入 `sox -h` 查看支持的音频类型。这还会显示支持的选项和效果。

### 表 8-1：`sox` 工具支持的音频格式

| 文件扩展名或伪名 | 描述 | 文件扩展名或伪名 | 描述 |
|--- | --- | --- | --- |
| `.8svx` | 8SVX Amiga 乐器描述格式。 | `.aiff` | Apple IIc/IIgs AIFF 文件。可能需要单独的归档程序。 |
| `.au`, `.snd` | Sun Microsystems AU 音频文件。这是一个流行的格式。 | `.avr` | Audio Visual Research 格式，用于 Mac。 |
| `.cdr` | 用于刻制紧光盘的 CD-R 文件。 | `.cvs` | 连续变增量调制，用于语音信箱和其他语音压缩。 |
| `.dat` | 文本数据文件，包含声音数据的表示。 | `.gsm` | 有损语音压缩 (GSM 06.10)，用于缩减语音信箱及类似应用程序中的音频数据。 |
| `.hcom` | Macintosh HCOM 文件。 | `.maud` | Amiga 格式，用于产生 8 位线性、A 波和单声道或立体声 u 波声音。 |
| `.ogg` | Ogg Vorbis 压缩音频，最适合压缩音乐和流媒体音频。 | `.ossdsp` | 伪文件，用于打开 OSS `/dev/dsp` 文件并配置使用传递给 Sox 的数据类型。用于播放或录制。 |
| `.prc` | Psion 记录格式，比 WVE 格式新。 | `.sf` | IRCAM 音文件，用于 CSound 包和 MixView 采样编辑器。 |
| `.sph` | 来自 NIST（美国国立标准技术研究院）的语音音频 SPHERE（语音头资源）格式。 | `.smp` | Turtle Beach 的 SampleVision 文件，用于与不同的 MIDI 采样器通信。 |
| 文件扩展名或伪名 | 描述 | 文件扩展名或伪名 | 描述 |
| :--- | :--- | :--- | :--- |
| `.sunau` | 伪文件，用于打开 `/dev/audio` 文件并设置使用传递给 Sox 的数据类型。 | `.txw` | Yamaha 音频采样键盘的 TX-16W。 |
| `.vms` | 用于语音信箱及类似应用程序的语音压缩。 | `.voc` | Sound Blaster VOC 文件。 |
| `.wav` | Microsoft WAV RIFF 文件。这是 Microsoft 原生声音格式。 | `.wve` | 8 位、A 波、8 kHz音频文件，用于 Psion 掌上电脑。 |
| `.raw` | 原始文件（不包含头部信息，因此必须给出采样率、大小和样式）。 | `.ub`, `.sb`, `.uw`, `.sw`, `.ul`, `.al`, `.la`, `.sl` | 具有特定特征的原始文件。`ub` 是无符号字；`sb` 是符号字；`uw` 是无符号字；`sw` 是符号字；`ul` 是无符号字。 |

如果你不确定音频文件的格式，可以在文件名后添加 `.au` 扩展名。这会触发 `Sox` 猜测文件中包含的是哪种音频格式。`.auto` 扩展名只能用于输入。如果 `Sox` 能识别文件内容，你就可以将轨道编码为另一种格式。例如，你可以将轨道转换为 `WAV`：

```
sox input.au output.wav
```

要查看 `Sox` 正在做什么，使用 `-V` 选项：

```
sox -V input.au output.wav
```

将轨道转换为 Ogg 格式，示例所示：

```
sox input.wav output.ogg
```

要减少噪声，可以将文件通过低通滤波器。示例：

```
sox input.wav output.wav low 2200
```

要更改采样率，使用 `-r` 选项：
