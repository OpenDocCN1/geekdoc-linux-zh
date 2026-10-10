
在指定的 `filename` 中搜索指定的 `string`（一个由换行符分隔的一个或多个搜索词列表），其中 `filename` 是用 `gzip` 创建的压缩文件（参见第 6 章）。你可以在空格分隔的列表或通过使用 shell 模式指定多个文件名（参见第 4 章中的“Shell 模式”部分）。有关可用选项，请参见 `fgrep`。

### zgrep

`zgrep [ 选项 ] regexp filename`

在指定的 `filename` 中搜索 `regexp`（一个基本正则表达式），其中 `filename` 是用 `gzip` 创建的压缩文件（参见第 6 章）。你可以在空格分隔的列表或通过使用 shell 模式指定多个文件名（参见第 4 章中的“Shell 模式”部分）。有关可用选项，请参见 `grep`。

### zmore

`zmore filename`

显示 `filename`（一个用 `gzip` 或 `compress` 创建的压缩文件），而不解压缩文件。（有关 `gzip` 和 `compress` 的更多信息，请参见第 6 章。）你可以在空格分隔的列表或通过使用 shell 模式指定多个文件名（参见第 4 章中的“Shell 模式”部分）。如果省略 `filename`，该实用程序从标准输入接受输入。

#### 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| `=` | 显示当前行号。 |
| `.` | 重复上一条命令。 |
| `:q`, `:Q`, `q`, `Q` | 退出。 |
| `[ *n* ] regexp` | 搜索 `regexp`（正则表达式）的第 `n` 次出现。默认情况下，`n` 为 1，因此搜索找到下一次出现。 |
| `[ *n* ] Ctrl + D`, `[ *n* ] d` | 显示 `n` 更多行。默认值为 11。 |
| `! command` | 运行指定的 shell 命令。 |
| `*n*` | 显示 `n` 更多行。在输入数字后按下空格键。 |
| `*nf*` | 跳过 `n` 屏并打印一屏的行。 |
| `*nn*` | 搜索最后输入的正则表达式的第 `n` 次出现。 |
| `*ns*` | 跳过 `n` 行并打印一屏的行。 |
| `s` | 跳到下一个文件。 |

# 第 9 章

![](img/e85417bb52fc523c6fc7b3b77b124ecb_402_0.png)

处理声音和图形文件

本章涵盖了能够处理声音和图形文件的实用程序。这些实用程序可以制作 CD-ROM 音频轨道的磁盘录音，播放 MP3 和 MIDI 音频文件，将几乎所有类型的计算机图形文件转换为另一种图形格式，等等。

> 提示 本章讨论的一些命令在大多数 Linux 发行版中默认未安装。有关从互联网下载这些命令的信息，请参见简介。

#### 概览

| 如何操作 | 参见此条目 | 示例 |
| :--- | :--- | :--- |
| 将图形文件从一种格式转换为另一种格式？ | `convert` | `convert jpeg image1.bmp image1.jpg` |
| 创建工作目录中所有图形文件的缩略图索引？ | `convert` | `convert \`vid:*\.jpg\` catalog.jpg` |
| 为刚刚刻录的 CD-ROM 创建印刷版珠宝盒标签？ | `cdlabelgen` | `cdlabelgen -c \`My Favorites\` -s \`2000\` -i \`Blues%Jazz%Rock%Alternative Rock%Techno%Industrial\` -e images/mp3.eps > cover.ps` |
| 播放音频 CD-ROM？ | `cdp` | `cdp` |
| 对音频 CD-ROM 上的所有音频轨道制作 WAV 录音？ | `cdparanoia` | `cdparanoia -B \`1\`` |
| 使用特效创建两个或更多图形文件的合成图像？ | `combine` | `combine -compose bumpmap image1.jpg image2.jpg combined.jpg` |
| 查看图形文件的详细信息？ | `identify` | `identify -verbose image1.jpg` |

### 声音和图形文件

本节详细介绍以下内容：

- 声音文件类型
- 图形文件类型

### 声音文件类型

下表列出了你通常在 Linux 系统上遇到的声音文件类型，按后缀（扩展名）组织。

#### 常见声音文件格式

| 扩展名 | 描述 |
| :--- | :--- |
| `.aiff` | Apple/Silicon Graphics AIFF 声音 |
| `.au` | Sun/NeXT AU 声音 |
| `.cdr` | RAIW，CD-ROM 音频的无符号样本 |
| `.cvs` | 连续可变斜率调制，用于语音压缩 |
| `.voc` | Sound Blaster VOC 声音 |
| `.wav` | Microsoft WAV 声音 |
| `.mp3` | MP3 压缩数字音频 |
| `.mid .midi` | MIDI 声音 |

### 图形文件类型

下表列出了你在 Linux 系统上可能会遇到的图形文件格式，按后缀（扩展名）排列。

#### 常见图形文件格式

| 扩展名 | 描述 |
| :--- | :--- |
| `.bmp`, `.dib` | Microsoft Windows 位图图像文件 |
| `.cgm` | 计算机图形元文件 |
| `.eps` | Adobe 封装的 PostScript 文件 |
| `.gif` | CompuServe 图形交换格式 |
| `.hpgl` | 惠普（Hewlett Packard）绘图仪文件 |
| `.ico` | Microsoft Windows 图标 |
| `.jpg`, `.jpeg`, `.jfif` | 联合图像专家组 JFIF 格式 |
| `.pbm` | 可移植位图格式文件 |
| `.pcd` | 柯达（Kodak）光碟文件 |
| `.pcx` | PC Paintbrush 文件 |
| `.pgm` | 可移植灰度图格式（灰度） |
| `.pict` | Apple Macintosh QuickDraw/PICT 文件 |
| `.png` | 可移植网络图形 |
| `.pnm` | 可移植任意图 |
| `.tga` | Truevision Targa 图像文件 |
| `.tiff` | 标记图像文件格式 |
| `.xbm` | X Windows 系统位图 |
| `.xpm` | X Windows 系统点画文件 |
| `.xwd` | X Windows 系统窗口转储文件 |

### 字母顺序命令参考

本节详细介绍用于以下任务的命令：

- 播放、录制和操作声音文件（`aumix`, `mikmod`, `mpg123`, `play`, `playmidi`, `rec`, `sox`）。
- 播放音频 CD（`cdp`）。
- 转换和处理图形文件（`combine`, `convert`, `identify`, `mogrify`, `montage`）。
- 将 CD 音轨录制为 WAV 文件（`cdda2wav`, `cdparanoia`）。
- 为 CD 珠宝盒创建标签（`cdlabelgen`）。

#### aumix

`aumix [选项]`

如果不带参数输入此命令，它将启动一个基于文本的交互式程序，用于控制音频设备的各种设置。请参阅本节的命令表，了解你在交互模式下可以使用的命令。

##### 选项

| 使用此选项 | 目的 |
| :--- | :--- |
| `-b[ + | - ] [ n ]` | 设置低音增益。指定以下任一选项：+ 增加一级，- 降低一级，`n` 设置特定级别（10–100）。 |
| `-C filename` | 指定包含颜色方案的 `filename`。 |
| `-cl[ + | - ] [ n ]` | 设置 CD 增益。指定以下任一选项：+ 增加一级，- 降低一级，`n` 设置特定级别。 |
| `-d device` | 使用指定的设备而不是默认设备。 |
| `-f filename` | 将设置保存到指定的 `filename`。 |
| `-i[ + | - ] [ n ]` | 设置线路输入增益。指定以下任一选项：+ 增加一级，- 降低一级，`n` 设置特定级别（10–100）。 |
| `-l[ + | - ] [ n ]` | 设置线路增益。指定以下任一选项：+ 增加一级，- 降低一级，`n` 设置特定级别（10–100）。 |
| `-L` | 从 `$HOME/.aumixrc` 加载设置，如果前者不可访问，则从 `/etc/aumixrc` 加载。 |
| `-m [+\|-][n]` | 设置麦克风级别。指定以下任一选项：+ 增加一级，- 降低一级，`n` 设置特定级别（10-100）。 |
| `-o [+\|-][n]` | 设置线路输出级别。指定以下任一选项：+ 增加一级，- 降低一级，`n` 设置特定级别（10-100）。 |
