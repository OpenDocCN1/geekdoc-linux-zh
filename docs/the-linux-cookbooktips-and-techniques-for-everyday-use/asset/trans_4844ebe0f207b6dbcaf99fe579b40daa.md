

$ amixer set Master 75% RET

+   • 要将 PCM 音量设置为 30，请输入：

```
amixer set PCM 30 RET
```

## 22.2.3 静音音频设备

使用特殊的 `mute` 和 `unmute` 参数来静音给定设备的音量。在你录制之前，必须取消静音你想要录制的输入设备。录制完成后，记得也将麦克风静音，以避免在调高扬声器时产生回授。

+   • 要取消麦克风静音并打开以便录制，请输入：

```
amixer set MIC unmute capture RET
```

+   • 要静音麦克风，请输入：

```
amixer set MIC mute RET
```

+   • 要取消主音量静音并将其设置为 80% 音量，请输入：

```
amixer set Master 80% unmute RET
```

## 22.2.4 选择音频录制源

要选择录制设备，请使用 set 后跟设备名称和 `capture` 参数，后者指定该组为用于录制的捕捉声音的组。

+   • 要将 LINE IN 插孔选为录制源，请输入：

```
amixer set Line capture RET
```

+   • 要将麦克风插孔选为录制源，请输入：

```
$ amixer set MIC capture RET
```

NOTE: 你一次只能选择一个组进行捕捉，并且当你将一个组选为录制输入源时，你只是打开了麦克风或其他输入；直到你使用录制工具，录制才开始。

## 22.3 播放声音文件

@sf(Debian): `sox`
@sf(WWW): http://home.sprynet.com/~cbagwell/sox.html

随 sox 分发的 play 工具（一种声音文件转换工具）可以识别并播放许多音频格式，包括 WAV、VOC、AU、AIFF 和 SND 格式文件，以及音频 CD 格式文件和各种原始二进制文件；它几乎不能处理的唯一常见音频格式是 MP3 和 MIDI 文件，这些将在后面的章节中讨论。

+   • 要播放文件 `pentastar.aiff`，请输入：

```
$ play pentastar.aiff RET
```

NOTE: 在开始播放声音之前，请确保你已使用混音器设置了主音量和 PCM 音量级别（参见章节 调整音频控件）。尝试播放声音时没有声音输出的最常见原因是音量未调高！

ALSA 附带了 aplay，这是一个用于播放声音文件的工具，与 play 类似，但识别的格式较少。

+   22.3.1 播放 MP3 文件    播放 MP3 文件。
+   22.3.2 播放 MIDI 文件    播放 MIDI 文件。

### 22.3.1 播放 MP3 文件

@sf(Debian): `mpg321`
@sf(WWW): http://freshmeat.net/projects/mpg321/

要播放 MP3 文件，将其名称作为参数传递给 mpg321。

+   - 要播放 MP3 文件 `september-wind.mp3`，请输入：

```
$ mpg321 september-wind.mp3 RET
```

要缓冲音频，在系统运行许多进程或活动较多的情况下很有用，请将缓冲大小（以千字节为单位）作为 `-b` 选项的参数。默认值为 0（无缓冲）；如果你需要此选项，请使用至少 1024KB（即 1MB）的大小，或约六秒的 MP3 音频。

你也可以使用 mpg321 播放来自网络的“流式”MP3 音频；只需将 MP3 流的 URL 作为参数给出即可。

+   - 要播放 http://example.net/broadcast/live.mp3 处的 MP3 流，请输入：

```
$ mpg321 http://example.net/broadcast/live.mp3 RET
```

+   - 要使用 2MB 音频缓冲播放 http://example.net/broadcast/live.mp3 处的 MP3 流，请输入：

```
$ mpg321 -b 2048 http://example.net/broadcast/live.mp3 RET
```

NOTE: mpg321 工具是 mpg123 的自由软件替代品，mpg123 是另一个命令行 MP3 播放器，但不是自由软件。

但还有许多其他 MP3 播放器可用；其中一些列在 其他声音文件工具 中。

### 22.3.2 播放 MIDI 文件

@sf(Debian): `playmidi`
@sf(WWW): http://playmidi.openprojects.net/

playmidi 工具用于播放 MIDI 文件；将要播放的 MIDI 文件的名称作为参数给出。

+   - 要播放 MIDI 文件 `copa-cabana.mid`，请输入：

```
$ playmidi copa-cabana.mid RET
```

如果你有非 MIDI 声卡，仍然可以通过给出 `-f` 选项来播放 MIDI 文件，该选项将 MIDI 输出发送到声卡上的 FM 合成器，后者使用随 playmidi 分发提供的 FM 补丁来播放。

+   - 要在非 MIDI 声卡上播放 MIDI 文件 `copa-cabana.mid`，请输入：

```
$ playmidi -f copa-cabana.mid RET
```

## 22.4 录制声音文件

```
@sf(Debian): `sox`
@sf(WWW): http://home.sprynet.com/~cbagwell/sox.html
```

要录制声音，首先选择一个输入设备作为录制源。声卡可能具有 MIC 和 LINE IN 插孔，以及连接到 CD-ROM 驱动器的连接，所有这些都是可以作为录制源的声音输入。当你为捕捉选择一个设备时，你的录制将来自此源。

录制从当前活动的输入开始，如果有的话，必须使用混音器设置；开始录制前取消静音并设置其音量级别。（务必将扬声器的音量调到最低，否则会产生回授。）

要将音频录制到文件，请使用 rec 工具。它可以写入许多音频文件格式，要么使用 `-t` 选项指定的格式，要么根据你为输出文件提供的文件名扩展名确定要使用的格式（参见章节 声音文件格式）。输入 C-C 以停止录制。

给出要录制的声音文件的名称作为参数；如果指定了 `.wav` 文件，则默认情况下会录制简单的单声道、低保真声音样本。

+   - 要从麦克风录制一个简单的 WAV 样本并保存到名为 `hello.wav` 的文件，请输入：

```
$ rec hello.wav RET
```

此命令开始向文件 `hello.wav` 录制 8,000 Hz、单声道 8 位 WAV 录制，直到你使用 C-C 中断它。默认情况下会制作低保真录制——8,000 Hz、单声道 8 位样本——你可以指定制作高保真录制。（但请记住，高保真录制会占用更多磁盘空间。）

要制作立体声录制，请使用 `-c` 选项指定通道数，给出 2 作为

