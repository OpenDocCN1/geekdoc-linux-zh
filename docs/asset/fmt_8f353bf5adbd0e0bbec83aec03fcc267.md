
Playing: `01-Rhapsody_in_Blue.ogg`

Ogg Vorbis stream: 2 channel, 44100 Hz

Title: Rhapsody in Blue

Artist: George Gershwin

Track number: 1

Total: 8

Album: Rhapsody in Blue

Genre: Instrumental

Time: 00:20.36 [15:29.65] of 15:50.01 (181.6 kbps) Output Buffer 96.9%

要停止 `ogg123` 播放单曲，请按 `Ctrl+C`。当队列了多个轨道时，按两次 `Ctrl+C` 退出 `ogg123`。这是 `vorbisistools` 包的一部分，您可以使用 `yum` 安装它。

- `play` — `play` 命令可用于播放 `sox` 支持的各种音频格式。语法为 `play file.xx`。要查看 `play` 命令可以播放哪些文件格式，请输入 `-h` 查看列表。如果您正在查找音效目录、语音内容或其他非典型多媒体音频类型的音频文件，`play` 命令将非常有用。（您需要安装 `sox` 包，它随 Fedora 和 RHEL 自带，才能播放。）

- `mpg321` — 这类似于 `ogg123`，但正如您所料的，它用于播放 MP3 文件。像 `ogg123` 一样，您可以播放文件 `[abc.mp3]`、一个包含多个音乐文件的播放列表 (`--list=/tmp/mownlist`)，或者一个 HTTP 或 FTP 位置 (`http://example.com/song.mp3`)。`mpg321` 不随 Fedora 或 RHEL 带。您可以从 Livna.org 网站获取 `mpg321` 包。

## 使用 MIDI 播放器

`MIDI` 代表 Musical Instrument Digital Interface（乐器数字接口）。`MIDI` 文件由合成器和其他音乐设备创建。`MIDI` 文件通常比其他类型的音频文件小，因为它们存储的是所播放音符的内容。`MIDI` 播放器重现这些音符使其听起来。

### 第 8 章：Linux 中的音乐、视频和图像 374

`MIDI` 代表 Musical Instrument Digital Interface。`MIDI` 文件由合成器和其他音乐设备创建。`MIDI` 文件通常比其他类型的音频文件小，因为它们存储的是所播放音符的内容。`MIDI` 播放器重现这些音符使其听起来。

`MIDI` 代表 Musical Instrument Interface。`MIDI` 文件通常比其他类型的音频文件小，因为它们存储的是所播放音符的内容。`MIDI` 播放器重现这些音符使其听起来。

## 使用 SoX 转换音频

如果您有一种格式的声音并想转换为另一种格式，`sox` 可以进行翻译。以下是表 8-1 列出的格式之间转换的列表。

### 表 8-1：sox 支持的音频格式

| 文件扩展名或别名 | 描述 | 文件扩展名或别名 | 描述 |
|---|---|---|---|
| `.svx` | Amiga 格式 | `.aiff` | Apple AIFF 文件 |
| `.au` | Sun AU | `.snd` | 音频文件 |
| `.cdr` | CD-R 文件 | `.cvs` | 连续变化率 |
| `.dat` | 文本数据 | `.gsm` | 有损压缩 |

### 第二部分：使用 Fedora 和 RHEL

| 文件扩展名或别名 | 描述 | 文件扩展名或别名 | 描述 |
| --- | --- | --- | --- |
| `.hcom` | Macintosh HCOM 文件 | `.maud` | Amiga 格式 |
| `.ogg` | Ogg Vorbis 压缩音频 | `.ossdsp` | OSS DSP |
| `.prc` | Psion 记录格式 | `.sf` | IRCAM 音频文件 |
| `.sph` | 语音音频（头部） | `.smp` | SampleVision 文件 |
| `.sunau` | Sun 音 | `.txw` | Yamaha TX-16W |
| `.vms` | 用于压缩 | `.voc` | Sound Blender VOC |
| `.wav` | Microsoft WAV 文件 | `.wwe` | 8位、A-law |
| `.raw` | 原始文件 | `.ub`, `.sb`, `.uw`, `.sw`, `.ul`, `.al`, `.lu`, `.la`, `.sl` | 原始文件 |

> 提示：输入 `sox -h` 查看支持的音频类型。

如果不确定音频文件的格式，可以为文件名添加 `.auto` 扩展名。这将触发 `sox` 猜测文件中包含哪种音频格式。

# 第 8 章：Linux 中的音乐、视频和图像 329

`.auto` 扩展只能用于输入文件。如果 `sox` 能够识别输入文件的内容，它就会将内容翻译为输出文件请求所需的音频类型。

在最基本的形式，你可以将一种文件格式（如 WAV 文件）转换为另一种格式（如 AU 文件）：

```
$ sox file.wav file1.au
```

要查看 `sox` 正在做什么，请使用 `-V` 选项。例如：

```
$ sox -V file.wav file1.voc
```

`sox`: Reading Wave: Microsoft PCM format, 2 channel, 44100 samp/sec
`sox`: 176400/bit/sec, 4 block align, 16 bits/sec, 50266944 data bytes
`sox`: Input file: using sample rate 11025
size bytes, style unsigned, 1 channel
`sox`: Input file.wav: comment "file.wav"

你可以在 SoX 转换过程中应用效果。下面的示例显示了如何使用 `-r` 选项将采样率从 10,000 kHz 更改为 5,000 kHz：

```
$ sox -r 10000 file.wav -r 5000 file.voc
```

为了减少噪声，你可以将文件通过低通滤波器发送。这里有一个示例：

```
$ sox file1.voc file2.voc lowp 2200
```
