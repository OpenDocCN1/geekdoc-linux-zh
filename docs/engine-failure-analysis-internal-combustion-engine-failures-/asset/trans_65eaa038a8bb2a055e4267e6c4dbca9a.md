
## 选项（续）

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| **gsm** | 用于语音压缩的全局移动通信标准（GSM）电信文件。 |
| **hcom** | Macintosh 压缩音频文件。 |
| **maud** | Amiga 声音文件。 |
| **ossdsp** | OSS 设备驱动程序 |
| **sb** | 有符号字节 RAW 声音文件。 |
| **sf** | IRCAM 声音文件，用于 Csound 和 Mix/View 应用程序。 |
| **smp** | Turtle Beach SampleVision 声音。 |
| **sunau** | Sun/NeXT AU 声音文件。 |
| **txw** | Yamaha TX-16W 采样器。 |
| **ub** | 无符号字节 RAW 声音文件。 |
| **ul** | Ulaw RAW 声音文件。 |
| **uw** | 无符号字声音文件。 |
| **vms** | 压缩语音文件。 |
| **voc** | Sound Blaster VOC 声音。 |
| **wav** | Microsoft WAV 声音。 |
| **-v** *volume* | 将音频输出更改为指定音量。 |
| **--volume=***volume* | （小于 1.0 减小，大于 1.0 增大）。 |
| **--version** | 显示 play/rec 的版本。 |
| **-x**, **--xinu** | 反转样本的字节顺序。 |

## 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| `rec - -format gsm mygreeting.gsm` | 使用 GSM 声音格式将麦克风输入录制到指定文件（*mygreeting.gsm*）中。 |

## SOX

`sox [选项] 输入文件 输出文件 [效果]`

将输入文件指定的采样声音格式转换为另一种格式，并存储到输出文件中，可附带可选效果。此命令最常用于 shell 脚本中，或作为两个其他命令之间的过滤器。要播放采样声音，请使用 `play`。要播放 MP3，请使用 `mpg123`。要播放 MIDI 文件，请使用 `playmidi`。

## 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| **-a** | 将数据格式类型设置为 ADPCM。 |
| **-A** | 将数据格式类型设置为 Alaw（对数）。 |
| **-b** | 使用字节来描述样本的大小。 |
| **-c n**, **--channels=n** | 定义文件的通道数（n）。 |
| **-d** | 使用 64 位双浮点记法来描述样本的大小。 |
| **-D** | 使用 80 位 IEEE 浮点记法来描述样本的大小。 |
| **-f** | 使用 32 位浮点记法来描述样本的大小。 |
| **-f format**, **--format=format** | 指定样本的位格式。可用选项有：<br> **a** ADPCM。<br> **A** Alaw（对数）。<br> **g** GSM。<br> **s** 有符号线性（二进制补码）。<br> **U** Ulaw（对数）。<br> **u** 无符号线性。 |
| **-g** | 将数据格式类型设置为 GSM。 |
| **-h**, **--help** | 显示可用选项。 |
| **-I** | 使用 32 位字来描述样本的大小。 |
| **-P** | 以预览模式运行。 |

## 选项（续）

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| **-r rate**, **--rate=rate** | 使用指定的采样率解码音频数据。 |
| **-S** | 将数据格式类型设置为有符号线性（二进制补码）。 |
| **-t type** | 指定要使用的音频文件格式类型。选项有：<br> **8svx** Amiga 乐器描述格式。<br> **aiff** Apple/Silicon Graphics AIFF 声音。<br> **au** Sun/NeXT AU 声音。<br> **auto** 自动检测声音文件类型。这是默认值。<br> **cdr** RAW，CD-ROM 音频的无符号样本。<br> **cvs** 连续可变斜率调制；用于语音压缩。<br> **dat** 包含样本数据文本表示的文本数据文件。<br> **gsm** 用于语音压缩的全局移动通信标准（GSM）电信文件。<br> **hcom** Macintosh 压缩音频文件。<br> **maud** Amiga 声音文件。<br> **ossdsp** OSS 设备驱动程序。<br> **sb** 有符号字节 RAW 声音文件。<br> **sf** IRCAM 声音文件，用于 Csound 和 Mix/View 应用程序。<br> **smp** Turtle Beach SampleVision 声音。<br> **sunau** Sun/NeXT AU 声音文件。<br> **txw** Yamaha TX-16W 采样器。<br> **ub** 无符号字节 RAW 声音文件。<br> **ul** Ulaw RAW 声音文件。<br> **uw** 无符号字声音文件。<br> **vms** 压缩语音文件。<br> **voc** Sound Blaster VOC 声音。<br> **wav** Microsoft WAV 声音。 |
| **-U** | 将数据格式类型设置为无符号线性。 |

## 选项（续）

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| **-U** | 将数据格式类型设置为 Ulaw（对数）。 |
| **-V** | 打印详细的程序消息。 |
| **-W** | 使用 16 位字来描述样本的大小。 |
| **-x**, **-Xinu** | 反转样本的字节顺序。 |

## 效果

| 使用此效果 | 执行此操作 |
| :--- | :--- |
| **avg [l \| r]** | 对通道取平均值，或者可选地复制左通道（l）或右通道（r）。 |
| **band [~n] center [width]** | 应用带通滤波器。可选地指定噪声因子（n）和下降斜率的宽度。 |
| **deemph** | 使用高音衰减搁架滤波器衰减高音。 |
| **echo *delay decay*** | 以指定的延迟和衰减（均以毫秒为单位）为声音样本添加**回声**。 |
| **flanger *delay decay speed*** | 以指定的延迟、衰减和速度（以毫秒为单位）为声音样本添加**扫频效果**。 |
| **highp *center*** | 应用具有指定中心频率的高通滤波器。 |
| **lowp *center*** | 应用具有指定中心频率的低通滤波器。 |
| **mask** | 向信号添加掩蔽噪声。 |
| **phaser *delay decay speed*** | 以指定的延迟、衰减和速度（以毫秒为单位）为声音样本添加移相器。 |
| **reverb *delay*** | 以指定的延迟为声音样本添加混响。 |

## 效果（续）

| 使用此效果 | 执行此操作 |
| :--- | :--- |
| **reverse** | 通过倒放声音消息来检测其中可能存在的撒旦主义潜意识信息。 |
| **split** | 将单声道输入转换为模拟立体声。 |
| **vibro *speed depth*** | 以指定的速度和深度为声音添加 Fender Vibro-Champ 效果。 |

![](img/e85417bb52fc523c6fc7b3b77b124ecb_462_0.png)

## 处理字体

本章详述了有助于在 X 窗口系统环境中使用字体的实用工具。它将讨论从二进制发行版安装新字体以及将 TrueType 字体转换为 X 服务器可以显示的 PostScript 字体的实用工具。还将介绍安装新字体并使其可供 X 服务器使用所需的基本实用工具。

## 概览

| 如何操作 | 参见此条目 | 示例 |
| :--- | :--- | :--- |
| 如何将二进制发行版格式（BNF）字体转换为 X 服务器可用的格式？ | **bdtopcf** | `bdtopcf -o myfont.pcf myfont.bdf` |
| 如何让新字体对 X 服务器可用？ | **mkfontdir**, **ttmkdir** | `mkfontdir -e > fonts.dir` |
| 如何将 Type 1 PFB 字体转换为 Type 1 PFA 字体？ | **t1ascii** | `t1ascii myfont.pfa myfont.pfb` |
| 如何将 Type 1 PFA 字体转换为 Type 1 PFB 字体？ | **t1binary** | `t1binary myfont.pfb myfont.pfa` |
| 如何将 TrueType 字体转换为 Type 1 字体，以便无需运行 TrueType 字体服务器即可使用？ | **ttf2pt1** | `ttf2pt1 -A myfont.ttf` <br> `ttf2pt1 -e myfont.ttf` |
| 如何让 TrueType 字体对字体服务器可用？ | **ttmkdir** | `ttmkdir -o fonts.scale` |
| 如何查看和搜索当前可供 X 服务器使用的字体列表？ | **xlsfonts** | `xlsfonts` |
| 如何向 X 服务器路径添加新的字体目录？ | **chkfontpath**, **xset** | `xset fp+ '/usr/fonts/newfonts'` |

## 字体基础

本节涵盖以下内容：

- X 环境中的字体名称
- 字体别名
- Linux 系统中发现的字体类型
- 字体编码
- Linux 发行版通常提供的位图字体
- Linux 发行版通常提供的可缩放字体

### 字体名称

为了被 X 字体服务器识别，字体必须通过有效的字体名称完整描述，该名称由 X 逻辑字体描述（XLFD）标准定义。符合 XLFD 的名称看起来如下：

`-b&h-lucida-medium-r-normal-sans-20-140-100-100-p-114-is08859-1`

此名称由固定数量的字段组成，字段之间用连字符分隔，用于描述以下类型的信息（从左到右）：

Family 设计该字体的公司或组织。

Family 当前字体所属字体家族的名称，例如 Helvetica 或 Times Roman。

Weight 字体的黑度。设置包括 light、medium、bold、demibold 和 extra bold。

Slant 字体的垂直方向。设置包括 -r（roman，垂直方向）、-o（oblique，像*斜体*一样倾斜，但倾斜方向向左）和 -i（italic）。

Set Width 字符的相对宽度。设置包括*超窄*（非常窄）、*窄*（窄）、*正常*（正常宽度）、*宽*（宽）和*超宽*（非常宽）。
