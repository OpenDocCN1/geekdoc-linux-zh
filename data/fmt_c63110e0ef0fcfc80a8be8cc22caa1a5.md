
`bash> lsmod|grep snd`

`snd_intel8x0`    33148  0                  ⇒ 音频控制器驱动程序

`snd_ac97_codec`   92000  1 `snd_intel8x0`     ⇒ 音频编解码器接口

`ac97_bus`         3104   1 `snd_ac97_codec`   ⇒ 音频编解码器总线

`snd_pcm_oss`      40512  0                  ⇒ OSS 仿真

`snd_mixer_oss`    16640  1 `snd_pcm_oss`      ⇒ OSS 音量控制

`snd_pcm`          73316  3 `snd_intel8x0`, `snd_ac97_codec`, `snd_pcm_oss`,

                           `snd_mixer_oss`, `snd_pcm`, `snd_timer`      ⇒ 核心层

`snd_timer`        22148  1 `snd_pcm`          ⇒ 核心层

`snd`              50820  6 `snd_intel8x0`, `snd_ac97_codec`, `snd_pcm_oss`,

                           `snd_mixer_oss`, `snd_pcm`, `snd_timer`      ⇒ 核心层

`soundcore`        8960   1 `snd`              ⇒ 核心层

`snd_page_alloc`   10344  2 `snd_intel8x0`, `snd_pcm` ⇒ 核心层

## 设备示例：MP3 播放器

图 13.4 展示了一个基于嵌入式 SoC 构建的 Linux 蓝牙 MP3 播放器的音频操作示例。您可以编写 Linux 手机的程序（我们在第 6 章“串行驱动程序”和第 12 章“视频驱动程序”中使用过），在夜间费率通常较低时从互联网下载歌曲，并通过蓝牙将其上传到 MP3 播放器的*紧凑闪存*（CF）磁盘，以便您第二天上班通勤时可以听这些歌曲。

### 图 13.4. Linux MP3 播放器上的音频。

![](img/07cc6f9c8c74622020874f66bfb53dc4_366_0.png)

我们的任务是为该设备开发音频软件。播放器上的应用程序从 CF 磁盘读取歌曲，并将其解码到系统内存中。内核 ALSA 驱动程序从系统内存收集音乐数据，并将其调度到属于 SoC 音频控制器的一部分的发送缓冲区中。此 PCM 数据被转发到编解码器，后者通过设备的扬声器播放音乐。正如在前一章讨论的导航系统的情况下，我们将假设 Linux 支持此 SoC，并且所有依赖体系结构的服务（如 DMA）均由内核支持。

因此，MP3 播放器的音频软件由两部分组成：

1. 解码从 CF 磁盘读取的 MP3 文件并将其转换为原始 PCM 的用户程序。要编写原生 ALSA 解码器应用程序，您可以利用 *alsa-lib* 库提供的辅助例程。“ALSA 编程”部分探讨了 ALSA 应用程序如何与 ALSA 驱动程序交互。
   - 您还可以选择定制公共领域的 MP3 播放器，例如 *madplay*（http://sourceforge.net/projects/mad/），以适应此设备。
2. 低级内核 ALSA 音频驱动程序。下一节将专门讨论编写此驱动程序。

图 13.4 所示设备的一种可能的硬件实现方式是使用 PowerPC 405LP SoC 和德州仪器 TLV320 音频编解码器。在这种情况下，CPU 核心是 405 处理器，片上音频控制器是编解码器串行接口（CSI）。SoC 通常具有高性能的内部本地总线，用于连接控制器（如 DRAM 和视频），以及独立的片上外设总线，用于接口低速外设，如串行端口、I²C 和 GPIO。在 405LP 的情况下，前者称为处理器本地总线（PLB），后者被称为片上外设总线（OPB）。PCMCIA/CF 控制器挂在 PLB 上，而音频控制器接口则连接到 OPB。

音频驱动器由三个主要部分构成：

- 处理播放的例程
- 处理捕获的例程
- 混音控制函数

我们的驱动器实现了播放，但不支持录音，因为示例中的 MP3 播放器没有麦克风。该驱动器还简化了混音功能。它没有提供全套音量控制（如扬声器、耳塞和线路输出），而是仅允许单一的通用音量控制。

表 13.1 中所示的 MP3 播放器音频硬件的寄存器布局反映了这些假设和简化，并不符合 AC'97 等此前提到的标准。因此，编解码器有一个 `SAMPLING_RATE_REGISTER` 用于配置播放（数模转换）采样率，但没有寄存器用于设置捕获（模数转换）速率。`VOLUME_REGISTER` 配置单一的全局音量。

### 表 13.1. 图 13.4 中音频硬件的寄存器布局

| 寄存器名称 | 描述 |
|---|---|
| `VOLUME_REGISTER` | 控制编解码器的全局音量。 |
| `SAMPLING_RATE_REGISTER` | 设置编解码器用于数模转换的采样率。 |
| `CLOCK_INPUT_REGISTER` | 配置编解码器的时钟源、分频器等。 |
| `CONTROL_REGISTER` | 使能中断，配置中断源（例如缓冲区传输完成），复位硬件，使能/禁用总线操作等。 |
| `STATUS_REGISTER` | 编解码器音频事件的状态。 |
| `DMA_ADDRESS_REGISTER` | 示例硬件支持单个 DMA 缓冲区描述符。现实中的声卡可能支持多个描述符，并可能有额外的寄存器来保存参数，例如当前正在处理的描述符、当前样本在缓冲区中的位置等。DMA 操作针对音频控制器中的缓冲区执行，因此该寄存器位于控制器的内存空间中。 |
| `DMA_SIZE_REGISTER` | 保存与 SoC 之间 DMA 传输的大小。该寄存器也位于音频控制器内部。 |

列表 13.1 是针对 MP3 播放器的骨架 ALSA 音频驱动器，并大量使用伪代码（在注释中）以省去冗余细节。ALSA 是一个复杂的框架，符合规范的音频驱动器通常有几千行代码。列表 13.1 只能让你开始探索音频驱动器。继续学习请回退到顶层 `sound/` 目录内强大的 Linux-Sound 源代码。

### 驱动器方法和结构

我们的示例驱动器实现为平台驱动器。让我们来看一下平台驱动器的 `probe()` 方法 `mycard_audio_probe()` 执行的步骤。我们将在每一步下稍微展开，解释我们遇到的相关概念和重要数据结构，这将把我们带到驱动器的其他部分，并有助于将事物联系起来。

`mycard_audio_probe()` 执行以下操作：

- 通过调用 `snd_card_new()` 创建声卡实例：

```c
struct snd_card *card = snd_card_new(-1, id[dev->id], THIS_MODULE, 0);
```

`snd_card_new()` 的第一个参数是卡索引（用于识别系统中多个声卡中的该卡），第二个参数是将被存储在当前返回的 `snd_card` 结构 `id` 字段中的 ID，第三个参数是属主模块，最后一个参数是私有数据字段的大小，该字段将通过当前返回的 `snd_card` 结构的 `private_data` 字段提供（通常用于存储芯片特定数据，如中断级别和 I/O 地址）。

`snd_card` 表示创建的声卡，在 `include/sound/core.h` 中定义如下：

```c
struct snd_card {
  int number;         /* 卡索引 */
  char id[16];       /* 卡 ID */
  /* ... */
  struct module *module;   /* 属主模块 */
  void *private_data;      /* 私有数据 */
  /* ... */
  struct list_head controls;
                    /* 此卡的所有控制 */
  struct device *dev;      /* 分配给此卡的设备 */
  /* ... */
};
```

`probe` 方法的对应移除方法 `mycard_audio_remove()` 使用 `snd_card_free()` 从 ALSA 框架释放 `snd_card`。

- 使用 `snd_pcm_new()` 创建 PCM 播放实例并将其与步骤 1 中创建的卡关联：

```c
int snd_pcm_new(struct snd_card *card, char *id,
                int device,
                int playback_count, int capture_count,
                struct snd_pcm **pcm);
```
