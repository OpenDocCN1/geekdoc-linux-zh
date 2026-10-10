

## 选项（续）

| 使用此选项 | 以执行此操作 |
| :--- | :--- |
| `--mode type` | 设置蒙太奇类型。选项包括 Frame、Unframe（默认）或 Concatenate。 |
| `-monochrome` | 将图像转换为黑白。 |
| `-page width x height [ % \ ! ]` | 设置图像画布的像素宽度和高度。追加百分号以按百分比调整宽度和高度。追加感叹号以强制使用确切尺寸。Postscript 页面的可选尺寸如下： |

| 页面尺寸 | 宽度 | 高度 |
| :--- | :--- | :--- |
| 11x17 | 792 | 1224 |
| A0 | 2380 | 3368 |
| A1 | 1684 | 2380 |
| A2 | 1190 | 1684 |
| A3 | 842 | 1190 |
| A4 | 595 | 842 |
| A4Small | 595 | 842 |
| A5 | 421 | 595 |
| A6 | 297 | 421 |
| A7 | 210 | 297 |
| A8 | 148 | 210 |
| A9 | 105 | 148 |
| A10 | 74 | 105 |
| ArchA | 648 | 864 |
| ArchB | 864 | 1296 |
| ArchC | 1296 | 1728 |
| ArchD | 1728 | 2592 |
| ArchE | 2592 | 3456 |
| B0 | 2836 | 4008 |
| B1 | 2004 | 2836 |
| B2 | 1418 | 2004 |
| B3 | 1002 | 1418 |
| B4 | 709 | 1002 |
| B5 | 501 | 709 |
| C0 | 2600 | 3677 |
| C1 | 1837 | 2600 |
| C2 | 1298 | 1837 |
| C3 | 918 | 1298 |
| C4 | 649 | 918 |
| C5 | 459 | 649 |
| C6 | 323 | 459 |
| Fisa | 612 | 936 |
| Fise | 612 | 936 |
| HalfLetter | 396 | 612 |
| Ledger | 1224 | 792 |
| Legal | 612 | 1008 |
| Letter | 612 | 792 |
| LetterSmall | 612 | 792 |

### 选项

- `-pen color`
  - 设置字体颜色或不透明颜色。
- `-pointsize point`
  - 为 PostScript 字体使用指定的磅值（point）。
- `-quality value`
  - 设置 JPEG、MIFF 或 PNG 的压缩级别。
- `-rotate degrees < | >`
  - 向左（<）或向右（>）旋转图像指定的度数。
- `-scene n`
  - 指定图像场景编号 n。
- `-shadow`
  - 在磁贴下方添加阴影以模拟深度。
- `-sharpen factor`
  - 按指定系数（0.0–99.9%）锐化图像。
- `-size width x height`
  - 当无法自动获取时，设置图像的宽度和高度。
- `-texture filename`
  - 使用指定文件名中找到的纹理作为图像背景。
- `-tile width x height`
  - 设置合成图像中磁贴的宽度和高度。
- `-transparency color`
  - 使指定颜色透明。
- `-treedepth 0 | 1`
  - 将树深度设置为 0 或 1。
- `-verbose`
  - 显示所有消息。

## 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `montage image1.jpg image2.jpg` | 创建包含 `image1.jpg` 和 `image2.jpg` 的蒙太奇。 |

## mpg123

`mpg123 [ option | filename | URL ]`

在默认音频设备上播放由 *filename* 或 *URL*（网络地址）指定的 MP3 音频文件。对于 *filename*，您可以指定由空格分隔的文件列表、shell 模式（参见第 4 章中的“Shell Patterns”部分）或 URL。要停止播放当前文件并跳至下一个，请按下 **Ctrl + C**。要停止播放并退出，请快速连续按下两次 **Ctrl + C**。要播放 WAV、AU 和其他采样声音，请参阅 *play*。要播放 MIDI 声音，请参阅 *playmidi*。

### 选项

| 使用此选项 | 以执行此操作 |
| :--- | :--- |
| `-t`, `-test` | 测试模式（无音频输出）。 |
| `@ filename`, `-list filename` | 从指定的 filename 获取输入，该 filename 可以是文件名、shell 模式（参见第 4 章中的“Shell Patterns”部分）或 URL。 |
| `-0`, `-single0`, `-1`, `-single1` | 仅播放左声道（0）或右声道（1）。仅适用于 MPEG 流。 |
| `-2`, `-2to1`, `-4`, `-4to1` | 按指定系数降低采样率。 |
| `--8bit` | 强制 8 位输出。 |
| `-a device`, `-audiodevice device` | 指定要使用的音频设备。 |
| `-b n`, `-buffer size n` | 使用大小为 n 千字节（K）的音频输出缓冲区。 |
| `-c`, `-check` | 检查滤波器范围违规。 |
| `-d n`, `--doublespeed n` | 播放每第 n 帧，跳过其他帧。 |
| `-f factor`, `--scale factor` | 更改缩放系数。默认为 32768。 |
| `-g gain`, `--gain gain` | 将输出音量设置为指定增益。 |
| `-h n`, `--halfspeed n` | 每帧播放 n 次。 |
| `-k n`, `--skip n` | 跳过前 n 帧。 |
| `-m`, `--singlemix` | 混合两个声道。仅适用于 MPEG 流。 |
| `-n n`, `--frames n` | 仅解码 n 帧。默认情况下，解码完整流。 |
| `-o h`, `--headphones` | 将音频输出直接导向耳机连接器。 |
| `-o l`, `--lineout` | 将音频输出直接导向线路输出连接器。 |
| `-o s`, `--speaker` | 将音频输出直接导向扬声器。 |
| `-p URL\|none`, `--proxy URL\|none` | 使用指定的 URL 作为 HTTP 请求的代理。 |
| `-q`, `--quiet` | 抑制消息。 |
| `--reopen` | 每首歌曲后重新打开音频设备。 |
| `-r rate`, `--rate rate` | 将采样设置为指定速率。 |
| `-s`, `--stdout` | 写入标准输出而非音频设备。 |
| `--stereo` | 强制立体声输出。 |
| `-u password`, `--auth password` | 强制指定密码进行 HTTP 身份验证。 |
| `-v`, `--verbose` | 显示更多程序消息。 |
| `-y`, `--resync` | 如果发生错误，继续解码。 |
| `-z`, `--shuffle` | 随机播放曲目。 |

## 示例

| **此命令** | **执行以下操作** |
| :--- | :--- |
| `mpg123 "mp3"` | 播放工作目录中的所有 MP3 文件。 |
| `mpg123 --auth mypassword http://www.sounds.org/sample.mp3` | 播放可从互联网 http://www.sounds.org 获取的指定 MP3 文件 (sample.mp3)，并提供指定密码 (mypassword)。 |

## play

`play [ option ] filename | effect`

播放由 *filename* 指定的音频文件。通常，实用程序会自动检测声音文件类型和其他文件参数，因此，除非实用程序未能正确检测文件类型，否则您不需要使用选项。您还可以使用 "sox" 部分中效果表指定的效果之一。此实用程序是 sox 实用程序的前端。

要播放 MIDI 声音，请参阅 **playmidi**。要播放 MP3，请参阅 **mpg123**。

### 选项

| **使用此选项** | **以执行此操作** |
| :--- | :--- |
| `-c *n*, --channels=*n*` | 定义文件的通道数 (*n*)。 |
| `-d *device*, --device=*device*` | 指定除默认输出设备以外的设备。 |
| `-f *format*, --format=*format*` | 指定采样的位格式。可用选项如下： |
| | - a ADPCM。 |
| | - A Alaw（对数）。 |
| | - g GSM。 |
| | - s 有符号线性（二进制补码）。 |
| | - U Ulaw（对数）。 |
| | - u 无符号线性。 |
| `-h, --help` | 显示可用选项。 |
| `-r rate, --rate=rate` | 使用指定的采样率解码音频数据。 |
| `-s size, --size=size` | 使用指定大小描述采样大小。可用选项如下： |
| | - b 字节。 |
| | - d 64 位双精度浮点数。 |
| | - D 80 位 IEEE 浮点数。 |
| | - f 32 位浮点数。 |
| | - l 32 位字。 |
| | - w 16 位字。 |
| `-t type, --type=type` | 指定要使用的音频文件格式类型，如下所示： |
| | - 8svx Amiga 乐器描述格式。 |
| | - aiff Apple/Silicon Graphics AIFF 声音。 |
| | - au Sun/NEXT AU 声音。 |
| | - auto 自动检测声音文件类型（默认）。 |
| | - cdr RAW，CD-ROM 音频的无符号采样。 |
| | - cvs 用于语音压缩的连续斜率调制。 |
| | - dat 包含采样数据文本表示的文本数据文件。 |
| | - gsm 用于语音压缩的全球移动通信系统 (GSM) 电信文件。 |
| | - hcom Macintosh 压缩音频文件。 |
| | - maud Amiga 声音文件。 |
| | - ossssp OSS 设备驱动程序。 |
| | - sb 有符号字节 RAW 声音文件。 |
| | - sf 由 CSound 和 MixView 应用程序使用的 IRCAM 声音文件。 |
| | - smp Turtle Beach SampleVision 声音。 |
| | - sna Sun/NeXT AU 声音文件。 |
| | - txw Yamaha TX-16W 采样器。 |
| | - ub 无符号字节 RAW 声音文件。 |
| | - ul ULaw RAW 声音文件。 |
| | - uw 无符号字声音文件。 |
| | - vms 压缩语音文件。 |
| | - voc Sound Blaster VOC 声音。 |
| | - wav Microsoft WAV 声音。 |
| `-v volume, --volume=volume` | 将音频输出更改为指定音量（小于 1.0 降低，大于 1.0 增加）。 |
| `--version` | 显示 play/rec 的版本。 |
| `-X, --xinu` | 反转样品的字节顺序。 |

## 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `play mysound.wav` | 播放指定的声音文件 (mysound.wav)。 |
| `play mysound.wav echo 40 12` | 播放指定的声音文件 (mysound.wav) 并带有回声效果（40 毫秒延迟和 12 毫秒衰减）。 |

## playmidi

`playmidi [ option ] [ filename ]`

播放由 filename 指定的 MIDI 文件。可用选项允许您播放或抑制指定的 MIDI 通道（参见本节中的 MIDI 通道表）。要播放 WAV、AU 和其他波形表声音，请参阅 play。要播放 MP3，请参阅 mpg123。

