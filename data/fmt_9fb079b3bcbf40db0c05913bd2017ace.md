
参数分别为：步骤 1 中创建的声卡实例、标识符字符串、设备索引、支持的播放流数量、支持的捕获流数量（在示例中为 0）、用于存储分配的 PCM 实例的指针。分配的 PCM 实例在 `include/sound/pcm.h` 中定义如下：

```c
struct snd_pcm {
  struct snd_card *card; /* 关联的 snd_card */
  /* ... */
  struct snd_pcm_str streams[2]; /* 此 PCM 组件的播放和捕获流。如果硬件支持，每个流可以支持子流 */
  /* ... */
  struct device *dev; /* 关联的硬件设备 */
};
```

`snd_device_new()` 例程位于 `snd_pcm_new()` 和其他类似组件实例化函数的核心。`snd_device_new()` 将组件和一组操作与关联的 `snd_card` 绑定（参见步骤 3）。

### 设置播放操作

通过调用 `snd_pcm_set_ops()` 将播放操作与步骤 2 中创建的 PCM 实例连接起来。`snd_pcm_ops` 结构指定了向编解码器传输 PCM 音频的 These 操作。列表 13.1 通过以下方式实现：

```c
/* PCM 播放流的操作符 */
static struct snd_pcm_ops mycard_playback_ops = {
  .open = mycard_pb_open, /* 打开 */
  .close = mycard_pb_close, /* 关闭 */
  .ioctl = snd_pcm_lib_ioctl, /* 用于处理特殊命令，否则指定通用 ioctl 处理器 snd_pcm_lib_ioctl() */
  .hw_params = mycard_hw_params, /* 当高层设置硬件参数（如音频格式）时调用。DMA 缓冲区分配也从此处进行 */
  .hw_free = mycard_hw_free, /* 释放 mycard_hw_params() 中分配的资源 */
  .prepare = mycard_pb_prepare, /* 准备传输音频流。设置音频格式如 S16_LE（稍后解释），使能中断，... */
  .trigger = mycard_pb_trigger, /* 当 PCM 引擎启动、停止或暂停时调用。第二个参数指定调用原因。此函数不能进入睡眠状态 */
};

/* 将操作与 PCM 实例连接 */
snd_pcm_set_ops(pcm, SNDRV_PCM_STREAM_PLAYBACK, &mycard_playback_ops);
```

在列表 13.1 中，`mycard_pb_prepare()` 将采样率配置到 `SAMPLING_RATE_REGISTER`，时钟源配置到 `CLOCK_INPUT_REGISTER`，并将传输完成中断使能配置到 `CONTROL_REGISTER`。`trigger()` 方法 `mycard_pb_trigger()` 使用 `dma_map_single()` 实时映射由 ALSA 框架填充的音频缓冲区。（我们在第 10 章“外围组件互连”中讨论过流式 DMA。）映射的 DMA 缓冲区地址被编程到 `DMA_ADDRESS_REGISTER`。与之前位于编解码器内部的寄存器不同，该寄存器是 SoC 中音频控制器的一部分。音频控制器将 DMA 数据转发给编解码器以进行播放。

### 硬件能力

另一个相关对象是 `snd_pcm_hardware` 结构，它宣布 PCM 组件的硬件能力。对于我们的示例设备，这在列表 13.1 中定义如下：

```c
/* PCM 播放流的硬件能力 */
static struct snd_pcm_hardware mycard_playback_stereo = {
    .info = (SNDRV_PCM_INFO_MMAP | SNDRV_PCM_INFO_PAUSE |
             SNDRV_PCM_INFO_RESUME); /* 支持 mmap()。流具有暂停/恢复功能 */
    .formats = SNDRV_PCM_FMTBIT_S16_LE, /* 每通道 16 位有符号，小端 */
    .rates = SNDRV_PCM_RATE_8000_48000, /* DAC 采样率范围 */
    .rate_min = 8000, /* 最小采样率 */
    .rate_max = 48000, /* 最大采样率 */
    .channels_min = 2, /* 支持左声道和右声道 */
    .channels_max = 2, /* 支持左声道和右声道 */
    .buffer_bytes_max = 32768, /* 最大缓冲区大小 */
};
```

此对象通过 `open()` 操作符 `mycard_playback_open()` 与关联的 `snd_pcm` 绑定，使用 PCM *运行时* 实例。每个打开的 PCM 流都有一个称为 `snd_pcm_runtime` 的运行时对象，包含管理该流所需的所有信息。这是一个包含软件 and 硬件配置的巨大结构，定义在 `include/sound/pcm.h` 中，并包含 `snd_pcm_hardware` 作为其组件字段之一。

### 缓冲区预分配

使用 `snd_pcm_lib_preallocate_pages_for_all()` 预分配缓冲区。随后，`mycard_hw_params()` 使用 `snd_pcm_lib_malloc_pages()` 从此预分配区域获取 DMA 缓冲区，并将其存储在步骤 3 中提到的 PCM 运行时实例中。`mycard_pb_trigger()` 在启动 PCM 操作时映射此缓冲区，在停止 PCM 操作时取消映射。

### 混音控制

使用 `snd_ctl_add()` 将混音控制元素与声卡关联，用于全局音量控制：

```c
snd_ctl_add(card, snd_ctl_new1(&mycard_playback_vol, &myctl_private));
```

`snd_ctl_new1()` 接受 `snd_kcontrol_new` 结构作为其第一个参数，并返回指向 `snd_kcontrol` 结构的指针。列表 13.1 将其定义如下：

## 6. 将声卡注册到 ALSA 框架

```c
snd_card_register(card);
```

`snd_kcontrol` 结构体描述了一个控制元素。我们的驱动程序将其用作通用音量控制的旋钮。`snd_ctl_add()` 将一个 `snd_kcontrol` 元素注册到 ALSA 框架中。当用户应用程序（如 `alsamixer`）运行时，会调用相应的控制方法。在列表 13.1 中，`snd_kcontrol_put()` 方法（`mycard_playback_volume_put()`）将请求的音量设置写入解码器的 `VOLUME_REGISTER`。

`codec_write_reg()`（在列表 13.1 中使用了但未实现）通过连接 SoC 中音频控制器和外部解码器的总线通信来向解码器寄存器写入值。例如，如果底层总线协议是 I2C 或 SPI，`codec_write_reg()` 使用第 8 章“The Inter-Integrated Circuit Protocol”中讨论的接口函数。

如果您希望在驱动程序中创建一个 `/proc` 接口用于在调试期间转储寄存器或在正常操作期间导出参数，请使用 `snd_card_proc_new()` 及其相关服务。列表 13.1 没有使用 `/proc` 接口文件。

如果您构建并加载列表 13.1 中的驱动模块，您将在 MP3 播放器上看到两个新的设备节点：`/dev/snd/pcmC0D0p` 和 `/dev/snd/controlC0`。前者是音频播放的接口，后者是混音器控制的接口。MP3 解码应用程序在 `alsa-lib` 的帮助下，通过在这些设备节点上进行操作来流式传输音乐。

# 列表 13.1. Linux MP3 播放器的 ALSA 驱动程序

```c
#include <linux/platform_device.h>
#include <linux/soundcard.h>
#include <sound/driver.h>
#include <sound/core.h>
#include <sound/pcm.h>
#include <sound/initval.h>
#include <sound/ctls.h>
/* 解码器支持的播放速率 */
static unsigned int mycard_rates[] = {
    8000,
    48000,
};
/* 播放通道的硬件约束 */
static struct snd_pcm_hw_constraint_list mycard_playback_rates = {
    .count = ARRAY_SIZE(mycard_rates),
```
