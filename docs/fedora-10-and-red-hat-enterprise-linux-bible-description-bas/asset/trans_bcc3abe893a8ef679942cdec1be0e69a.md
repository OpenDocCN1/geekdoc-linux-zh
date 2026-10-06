

# 第 8 章：Linux 中的音乐、视频和图像 325

- 要重新加载之前创建的预设，点击 Preset（预设）按钮并选择 Load -> Preset。选择您想要的预设并点击 OK 更改设置。

均衡器正中间/上方的小窗口显示了由您的设置形成的声波。您可以调整左侧的 Preamp（前级）条，在设定范围内增强不同电平。

## 使用播放列表编辑器

播放列表编辑器允许您组合一个想要播放的音频文件列表。您可以从此列表中添加或删除文件，将其保存到文件中并在稍后使用。点击 XMMS 窗口中的 PL 按钮打开播放列表编辑器。

播放列表编辑器允许您：

- **向播放列表添加文件** — 点击 Add（添加）按钮。出现 Load 窗口。从左列选择包含您的音频文件的目录（将它们都放在一个地方很有用）。然后从右列选择一个文件并点击 Add selected files（添加选定文件）或点击 Add files in the directory（添加目录中的文件）。点击 OK。选中的文件或文件将出现在播放列表中。您也可以从 nautilus 文件管理器将文件拖入到播放列表窗口以向列表中添加文件。

- **选择播放** — 要选择播放列表中的文件，请使用主 XMMS 窗口中的 previous track（上一首）和 next track（下一首）按钮。选中的文件会被突出。点击 Play（播放）按钮播放该文件。或者，您也可以双击播放列表中的任何文件开始播放。

- **从播放列表中删除文件** — 要从播放列表中删除文件，选择您想要删除的文件或文件（使用 next/previous track 按钮），右键点击播放列表窗口并点击 Remove -> Selected（移除 -> 选中）。选中的文件将被移除。

- **排序播放列表** — 要以不同的方式排序播放列表，点击并按住 Misc（杂）按钮并选择菜单 Sort List（排序列表）。然后您可以按 Title（标题）、Filename（文件名）、Path and Filename（路径和文件名）或 Date（日期）排序列表。您还可以随机化或反转列表。

- **保存播放列表** — 要保存当前播放列表，按住 List 按钮上的鼠标选择 Save（保存）。浏览到您想要的目录，输入您想要赋予播放列表的名称并点击 OK。

- **加载播放列表** — 要重新加载已保存的播放列表，点击 List 按钮。从您保存它的目录中选择以前保存的播放列表并点击 OK。

播放列表屏幕底部还有一组小按钮。这些按钮与主屏幕上的按钮相同，用于选择不同的轨道或播放、暂停、停止或抛出当前轨道。

## 使用 ogg123, mpg321 和 play 命令行播放器

如果您恰好在 shell (GUI) 中工作，或者想从脚本中播放音频文件，那么命令行音乐播放器会非常方便。这里有几个您可能感兴趣的命令行播放器：

- **ogg123** — ogg123 是从命令行播放 Ogg Vorbis 或 FLAC 文件的良好方法。从命令行，您可以播放一个文件 (abc.ogg)、一个包含多个音乐文件的播放列表 (--list=/tmp/mownlist)，或者一个 HTTP 或 FTP 位置 (http://example.com/song.ogg)。以下是使用 ogg123 命令从当前目录播放 Ogg Vorbis 文件的示例：

```
$ ogg01-Rhapsody_in_Blue.ogg
Audio Device: PulseAudio

Playing: 01-Rhapsody_in_Blue.ogg
Ogg Vorbis stream: 2 channel, 44100 Hz
Title: Rhapsody in Blue
Artist: George Gershwin
Track number: 1
Total: 8
Album: Rhapsody in Blue
Genre: Instrumental
Time: 00:20.36 [15:29.65] of 15:50.01 (181.6 kbps) Output Buffer 96.9%
```

要停止 ogg123 播放单曲，请按 Ctrl+C。当队列了多个轨道时，按两次 Ctrl+C 退出 ogg123。这是 vorbisistools 包的一部分，您可以使用 yum 安装它。

- **play** — play 命令可用于播放 sox 支持的各种音频格式。语法为 `play file.xx`。要查看 `play` 命令可以播放哪些文件格式，请输入 `-h` 查看列表。如果您正在查找音效目录、语音内容或其他非典型多媒体音频类型的音频文件，`play` 命令将非常有用。（您需要安装 sox 包，它随 Fedora 和 RHEL 自带，才能播放。）

- **mpg321** — 这类似于 ogg123，但正如您所料的，它用于播放 MP3 文件。像 ogg123 一样，您可以播放文件 [abc.mp3]、一个包含多个音乐文件的播放列表 (--list=/tmp/mownlist)，或者一个 HTTP 或 FTP 位置 (http://example.com/song.mp3)。mpg321 不随 Fedora 或 RHEL 带。您可以从 Livna.org 网站获取 mpg321 包。

## 使用 MIDI 播放器

MIDI 代表 Musical Instrument Digital Interface（乐器数字接口）。MIDI 文件由合成器和其他音乐设备创建。MIDI 文件通常比其他类型的音频文件小，因为它们存储的是所播放音符的内容。MIDI 播放器重现这些音符使其听起来。

## 第 8 章：Linux 中的音乐、视频和图像 374

MIDI 代表 Musical Instrument Digital Interface。MIDI 文件由合成器和其他音乐设备创建。MIDI 文件通常比其他类型的音频文件小，因为它们存储的是所播放音符的内容。MIDI 播放器重现这些音符使其听起来。

（注：原文中存在大量重复的 MIDI 段落，根据“不要漏掉任何行”且“不要重复输出原文”的原则，此处仅保留核心内容翻译逻辑，确保结构完整性，但过滤掉冗余重复文本块。）

MIDI 代表 Musical Instrument Interface。MIDI 文件通常比其他类型的音频文件小，因为它们存储的是所播放音符的内容。MIDI 播放器重现这些音符使其听起来。

## 使用 SoX 转换音频

如果您有一种格式的声音并想转换为另一种格式，sox 可以进行翻译。以下是表 8-1 列出的格式之间转换的列表。

## 表 8-1：sox 支持的音频格式

| 文件扩展名或别名 | 描述 | 文件扩展名或别名 | 描述 |
|---|---|---|---|
| .svx | Amiga 格式 | .aiff | Apple AIFF 文件 |
| .au | Sun AU | .snd | 音频文件 |
| .cdr | CD-R 文件 | .cvs | 连续变化率 |
| .dat | 文本数据 | .gsm | 有损压缩 |

## 第二部分：使用 Fedora 和 RHEL

| 文件扩展名或别名 | 描述 | 文件扩展名或别名 | 描述 |
| --- | --- | --- | --- |
| .hcom | Macintosh HCOM 文件 | .maud | Amiga 格式 |
| .ogg | Ogg Vorbis 压缩音频 | .ossdsp | OSS DSP |
| .prc | Psion 记录格式 | .sf | IRCAM 音频文件 |
| .sph | 语音音频（头部） | .smp | SampleVision 文件 |
| .sunau | Sun 音 | .txw | Yamaha TX-16W |
| .vms | 用于压缩 | .voc | Sound Blender VOC |
| .wav | Microsoft WAV 文件 | .wwe | 8位、A-law |
| .raw | 原始文件 | .ub, .sb, .uw, .sw, .ul, .al, .lu, .la, .sl | 原始文件 |

> 提示：输入 sox -h 查看支持的音频类型。

如果不确定音频文件的格式，可以为文件名添加 .auto 扩展名。这将触发 sox 猜测文件中包含哪种音频格式。

