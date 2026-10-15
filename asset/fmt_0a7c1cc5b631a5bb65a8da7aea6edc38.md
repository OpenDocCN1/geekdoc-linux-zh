
# 第 8 章：真正的多媒体

与上述格式不同，`MIDI`（乐器数字接口）不是采样数字音频的规范。相反，它是一种串行通信协议，允许在电子乐器之间传输控制数据。它已经

它被比作音乐的 PostScript 语言。由于 `MIDI` 仅包含控制设备（最常见的是电子合成器或采样器）如何以及何时产生声音的指令，因此文件体积远小于数字化音频文件。`MIDI` 制造商协会（`MMA`）是一个电子乐器制造商组成的团体，自 1983 年成立以来一直负责 `MIDI` 协议的演进。

> TIPS 有关 `MIDI` 的信息，请参阅 `MIDI` 主页：http://www.eeb.ele.tue.nl/midi/index.html。

> 提示 网络上的电子音乐软件链接可以在 Arachnaut 的互联网电子音乐软件列表中找到：http://www.web.com/~hurleyj/music/emusic-sw.html。

### 模块 (Modules)

`MIME` 类型：`audio/x-mod`

模块（Modules）通常以 `.mod` 扩展名标识，在某种程度上是 `MIDI` 文件和数字化音频文件之间的混合体。这种格式不仅仅包含采样音频或控制信息，还包含了一组数字化声音以及用于控制播放时声音排序方式的控制信息。采样数据是原始的 8 位音频数据。该格式还具有简单的数字信号处理（`DSP`）能力以添加效果。

模块起源于 Amiga 系统，但由于其较小的体积和广泛的用途，已成为网络上许多作曲家的喜爱。得益于随处可见的播放工具和网络上海量的此类文件，模块本身已经变成了一种艺术形式。

尽管我们在此条目中列出了 `MIME` 类型，但模块在网络上通常是压缩的，因此没有必要在你的 `mime.types` 文件中添加条目。

> TIPS 有关 `MOD` 文件格式的详细信息，请参阅 `MOD` 常见问题：http://www.cis.ohio-state.edu/hypertext/faq/usenet/AudioFAQ/top.html。

| 格式 | 采样率 | 优点 | 缺点 |
|---|---|---|---|
| m-law | 8kHz | 文件小，受大多数平台支持 | 质量低 |
| AIFF/AIFC | 多种速率，8kHz | 高质量，最常见 | 音频文件巨大 |
| RIFF Wave | 多种速率 | 内置于 MS Windows | 文件大 |
| MPEG | 多种速率 | 高压缩且几乎无质量损失 | 无特殊硬件或软件不支持 |
| Creative Voice | 单声道 44.1kHz，双声道 22kHz | 内置于 Soundblaster 声卡 | 专有格式 |
| snd | 5.5kHz 到 22kHz，11kHz 最常见 | 实际上可以是多种格式之一 | 软件中无头部信息，无法自动识别如何播放文件 |
| MIDI | | 非数字化音频，用于音乐创作 | 需要特殊的软件和硬件播放文件 |
| Modules | 8 位音频采样加控制数据 | 文件小，支持度广 | 需要特殊的软件和硬件播放文件 |

表 8-2：音频文件格式对比。

### 音频设备驱动程序

`UNIX` 机器上的音频硬件设置差异很大，在安装我们本节后面讨论的应用程序之前，最好先熟悉你特定的设置。配备自带音频硬件的计算机通常带有音频录制、编辑和播放工具。具有音频输入能力的机器，其 Sun OpenWindows 配备了 `AudioTool`。同样，许多 Silicon Graphics (`SGI`) 工作站配备了优秀的图形化录制器/编辑器 `Sound` 以及音频转换实用程序 `Soundfiler`。此外，`NeXT` 工作站还带有标准的 `sndplay` 应用，用于播放多种类型的音频文件。如果你的工作站自带音频卡，请检查制造商的文档，查看是否有已编译的音频工具可用。由于本文的重点是 Linux 操作系统，我们将设备驱动程序限制在 Linux 音频驱动程序上，即 `OSS/Free` 和 `OSS/Linux`。

> TIPS 如果你正在 PC 上安装 Linux 并对兼容的声卡有疑问，请参阅 Linux Sound HOWTO：http://sunsite.unc.edu/mdw/HOWTO/Sound-HOWTO.html。

本源提供了配置声音支持、选择最佳声卡、如何播放音频文件以及处理常见问题的详细说明。

`OSS/Free` 中的 `OSS` 代表 Open Sound System（开放声音系统），而 `OSS/Linux`（对应 Linux 版本）分别是适用于 Linux 的免费和商业版声音软件包。这两者都由 Hanno Savolainen 开发，`4Front Technologies` 为商业版本提供支持。这些软件包为许多声声卡提供了不同程度的设备支持。`OSS/Free` 包含在最新的 Linux 发行版中，并一直追溯到 1.2.13 内核版本（尽管当时软件包的名称不同）。在，推荐为 Linux 1.2.13 内核使用 `OSS/Free` 的 3.0.1 版本，但没有其他信息可以确定适用于后期 1.3.x 内核的 `OSS/Free` 版本。在本书出版时，大多数 Linux 发行版将处于 2.0 内核的某个水平。建议 2.0 内核使用 `OSS/Free` 的 3.5 版本，建议 2.0.1 内核使用 3.6 版本。`OSS/Free` 的主页提供了最新的内核兼容性信息。

| OSS/Free 版本 | 兼容的 Linux 内核级别 |
|---|---|
| 3.0.1 | Linux 1.2.13 |
| 3.5 | Linux 2.0 |
| 3.6 | 2.0.1 |

表 8-3：`OSS/Free` 与 Linux 内核版本的对比。

`OSS/Free` 版本安装简单。它在内核源码中解压，并使用常规内核配置机制（`make config`）进行配置。只需指定你想要声音支持即可。驱动程序会在“`make image`”（或类似）步骤与操作系统的一起安装。在构建新内核之前，请确保你已了解声卡的规格（`IRQ`、`DMA` 地址或其他功能，等等）。应该注意的是，只有当你感兴趣为新声卡添加支持（即编写代码）时，才获取 `OSS/Free` 版本。普通用户（非开发者）应获取 `OSS/Linux` 商业版本。

> TIPS `OSS/Free` 的主页为 http://personal.unet.fi/pp/software/；`4Front Technologies` 的主页（针对 `OSS` 的商业版本）为 http://www.4front-tech.com。

`OSS/Linux` 作为 `4Front Technologies` 的商业产品提供。其他系统也有 `OSS` 版本。`OSS/Linux` 支持 1.2.13 内核以及任何 2.0 内核。考虑到奇数编号内核被认为是开发发布版，这是合理的。由于 `OSS/Free` 的驱动程序在 Linux 源码发行中，所有商业分行的 Linux 版本（Red Hat、Slackware 等）都应该拥有这些驱动程序。如果你发现你的声卡在 `OSS/Free` 版本中部分或完全不支持，那么你可以考虑 `OSS/Linux` 商业版本。

### 音频播放工具

`OSS` 声音驱动程序支持 `.au` 和 `wav` 文件。要从命令行播放这些文件，只需使用 `cat` 命令并将输出重定向到音频设备 `/dev/audio`：

```
% cat file.au > /dev/audio

% cat file.wav > /dev/audio
```
