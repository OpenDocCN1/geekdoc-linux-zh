
音量控制。通常，你应该先使用查询宏来确定声音设备的功能，或者仅仅是确认其是否存在，然后再开始对其进行操作。

关于混音器，声音 API 将其功能抽象为一组通道，因此你要做的第一件事是找出有多少个可用通道以及它们是什么。表 13.1 提供了最常见通道的部分列表（完整列表包含在 `<sys/soundcard.h>` 中）。

## 表 13.1：常见混音器通道

| 通道 | 描述 |
|---|---|
| SOUND_MIXER_VOLUME | 主输出电平 |
| SOUND_MIXER_BASS | 所有输出通道的低音电平 |
| SOUND_MIXER_TREBLE | 所有输出通道的高音电平 |
| SOUND_MIXER_SYNTH | 所有合成器输入的音量控制，例如 FM 芯片或波表 |
| SOUND_MIXER_PCM | 音频设备 /dev/audio 和 /dev/dsp 的输出电平 |
| SOUND_MIXER_SPEAKER | PC 扬声器的输出电平（如果它直接连接到声卡） |
| SOUND_MIXER_LINE | 线路输入插孔的音量电平 |
| SOUND_MIXER_MIC | 麦克风输入的音量电平 |
| SOUND_MIXER_CD | 音频 CD 输入的音量电平 |
| SOUND_MIXER_ALTPCM | 备用音频设备（例如 Sound Blaster 对 PAS16 卡组的仿真）的音量电平 |
| SOUND_MIXER_RECLEV | 主录音音量电平控制 |

宏 SOUND_MIXER_NRDEVICES 报告在任意给定时刻声音驱动所知道的设备最大数量；SOUND_MIXER_READ_DEVMASK 设置一个位掩码，指示可用的通道。

SOUND_MIXER_READ_RECMASK 设置一个位掩码，指示可用的录音设备。SOUND_MIXER_READ_STEREODEVS 设置一个位掩码，指示哪些通道支持立体声输出。这些信息使你能够独立设置每个通道的音量，从而提供一种类型的平衡控制。另一个调用，SOUND_MIXER_READ_CAPS，设置一个位掩码，描述混音器的一般功能。

声音 API 的混音器部分还提供两个宏，包含可供人类阅读的字符串：SOUND_DEVICE_LABELS 和 SOUND_DEVICE_NAMES。这两者之间的唯一区别在于，SOUND_DEVICE_NAMES 中的标签没有嵌入空格或大写字母。

最后，要获取和设置混音器音量，请使用 `SOUND_MIXER_READ`(channel) 和 `SOUND_MIXER_WRITE`(channel) 宏。例如，下面的代码片段将当前混音器设备的音量设置为其最大范围的 50%：

```c
int vol = 50;

if((ioctl(fd, SOUND_MIXER_WRITE(SOUND_MIXER_MIC), &vol)) < 0)
	/* 调用失败，因此优雅地降级处理 */
else
	/* 调用成功，此处有更多代码 */
```

vol 存储要设置的音量电平（通常称为增益），而 SOUND_MIXER_MIC 则是正在设置音量的通道。第一个字节包含左通道的音量，而右通道的音量则设置在第二个字节中。调用之后，vol 包含新的值，由于硬件特性，该值与设置的音量电平略有不同。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_319_0.png)

### 示例 1

下面的程序 `mixer_status` 查询混音器设备可用的通道并显示它们的当前设置：

```c
/*
 * mixer_status.c - 显示混音器设置的示例程序。
 * 版权所有 (c) 1994-96 Jeff Tranter (jeff_tranter@xmission.com)
 * 由 Kurt Wall (kwall@xmission.com) 大幅修改
 */

#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include <sys/ioctl.h>
#include <fcntl.h>
#include <sys/soundcard.h>

/* 用于打印状态的实用函数 */
void prn_stat(int condition);

int main(void)
{
    int fd;                        /* 混音器设备的文件描述符 */
    int level;                     /* 音量设置 */
    char *device = "/dev/mixer";

    /* 设备设置的位掩码 */
    int recsrc, devmask, recmask, stereodevs, caps;
    /* 混音器通道的名称 */
    const char *labels[] = SOUND_DEVICE_LABELS;
    int i;

    /* 只读方式打开混音器设备 */
    if((fd = open(device, O_RDONLY)) < 0) {
        perror("open");
        exit(EXIT_FAILURE);
    }

    /* 获取混音器信息 */
    if((ioctl(fd, SOUND_MIXER_READ_RECSRC, &recsrc)) < 0)
        perror("SOUND_MIXER_READ_RECSRC");
    if((ioctl(fd, SOUND_MIXER_READ_DEVMASK, &devmask)) < 0)
        perror("SOUND_MIXER_READ_DEVMASK");
    if((ioctl(fd, SOUND_MIXER_READ_RECMASK, &recmask)) < 0)
        perror("SOUND_MIXER_READ_RECMASK");

    if((ioctl(fd, SOUND_MIXER_READ_STEREODEVS, &stereodevs)) < 0)
        perror("SOUND_MIXER_READ_STEREODEVS");
    if((ioctl(fd, SOUND_MIXER_READ_CAPS, &caps)) < 0)
        perror("SOUND_MIXER_READ_CAPS");

    /* 打印混音器信息 */
    printf("Status of %s:\n\n", device);
    printf("Mixer         Recording Active    Stereo\nCurrent\n");
    printf("Channel       Source    Source    Device\nLevel\n");
    printf("-----------------------------------------------------------------\n");
    printf("---------------------------\n");

    /* 遍历所有设备 */
    for (i = 0; i < SOUND_MIXER_NRDEVICES; ++i) {
        /* 只关心可用的设备 */
        if((1 << i) & devmask) {
            /* 打印通道号和名称 */
            printf("%2d %-8s", i, labels[i]);
            /* 它是录音源吗？ */
            prn_stat((1 << i) & recmask);
            /* 它是活动的吗？ */
            prn_stat((1 << i) & recsrc);
            /* 它支持立体声吗？ */
            prn_stat((1 << i) & stereodevs);
            /* 如果是立体声，显示两个电平 */
            if ((1 << i) & stereodevs) {
                if((ioctl(fd, MIXER_READ(i, &level)) < 0)
                    perror("SOUND_MIXER_READ");
                else
                    printf(" %3d%% %3d%%", level & 0xff, (level & 0xff00) >> 8);
            } else { /* 只有一个通道 */
                if((ioctl(fd, MIXER_READ(i, &level)) < 0)
                    perror("SOUND_MIXER_READ");
                else
                    printf("    %3d%%", level & 0xff);
            }
        }
        printf("\n");
    }

    /* 录音源是排他的吗？ */
    printf("\nNote: Choices for recording source are ");
    if (!(caps & SOUND_CAP_EXCL_INPUT))
        printf("not ");
    printf("exclusive.\n");

    /* 关闭 */
    close(fd);
    return 0;
}

void prn_stat(int condition)
{
    condition ? printf("  YES  ") : printf("  NO  ");
}
```

前五个 `ioctl` 调用在相应的整型参数（`recsrc`、`devmask`、`recmask`、`stereodevs` 和 `caps`）中设置了位掩码。在打印表格头之后，`mixer_status` 循环遍历可用的混音器通道。如果混音器具有该特定通道，则条件块执行并显示该通道的一些可用信息。

特别注意的是位掩码的测试方式：

`(1 << channel) & bitmask;`

括号内的表达式将通道号左移作用于 1，然后将结果与 `bitmask` 进行按位与运算。如果给定的通道存在，该表达式计算结果为 1。如果通道不可用，则计算结果为 0。因此，例如，如果一个通道，比如 `SOUND_MIXER_VOLUME` 支持立体声，`(1 << SOUND_MIXER_VOLUME) & stereodevs`（如程序中设置的那样）计算结果为 1。

在我拥有一块正宗 Sound Blaster 的系统中，`mixer_status` 生成了以下输出：

![](img/be588b36b489136ce784030a08a1d3d4_322_0.png)

## 输出

```
$ ./mixer_status
Status of /dev/mixer:
```

|   | 混音器通道 | 录音源 | 活动源 | 立体声设备 | 当前电平 |
|---|---|---|---|---|---|
| 0 | Vol | NO | NO | YES | 90% 90% |
| 1 | Bass | NO | NO | YES | 75% 75% |
| 2 | Trebal | NO | NO | YES | 75% 75% |
| 3 | Synth | YES | NO | YES | 75% 75% |
| 4 | pcm | NO | NO | YES | 100% 100% |
| 5 | Spkr | NO | NO | NO | 75% |
| 6 | Line | YES | NO | YES | 75% 75% |
| 7 | Mic | YES | YES | NO | 0% |
| 8 | CD | YES | NO | YES | 75% 75% |
| 9 | Mix | NO | NO | NO | 0% |
| 12 | IGain | NO | NO | YES | 75% 75% |
| 13 | OGain | NO | NO | YES | 75% 75% |

注意：录音源的选择不是排他的。

如你所见，该混音器设备缺少几个通道，例如备用音频设备（`SOUND_MIXER_ALTPCM`）。

![](img/be588b36b489136ce784030a08a1d3d4_323_0.png)

### 示例 2

下一个程序 `setvol` 允许你交互式地设置音量电平。

```c
/*
 * setvol.c - 交互式设置混音器设备的音量电平
 * 版权所有 (c) 1994-96 Jeff Tranter (jeff_tranter@mitel.com)
 * 由 Kurt Wall (kwall@mission.com) 大幅修改
 */
#include <unistd.h>

#include <stdlib.h>
#include <stdio.h>
#include <sys/ioctl.h>
#include <fcntl.h>
#include <sys/soundcard.h>

int main(int argc, char *argv[])
{
    int left, right, level;          /* 音量设置 */
    int device;                     /* 要设置的哪个混音器设备 */
    int i;                          /* 混音器的文件描述符 */
    int fd;
    /* 混音器信息的位掩码 */
    int devmask, stereodevs;
    char *dev = "/dev/mixer";
    char buf[5];

    /* 以读写方式打开混音器 */
    if((fd = open(dev, O_RDWR)) < 0) {
        perror("open");
        exit(EXIT_FAILURE);
    }

    /* 获取关于混音器的信息 */
    if((ioctl(fd, SOUND_MIXER_READ_DEVMASK,
             &devmask)) < 0)
        perror("SOUND_MIXER_READ_DEVMASK");
    if((ioctl(fd, SOUND_MIXER_READ_STEREODEVS,
```
