
如果你使用过其他线程编程库（如 Win32 线程或 POSIX 线程库），你会发现 SDL 的线程 API 相当不完整。例如，SDL 不允许程序更改线程的调度优先级或其他低级属性。这些功能高度依赖于操作系统，要在跨平台的情况下以一致的方式支持它们是非常困难的。如果你的游戏需要完整的线程能力，你可能考虑使用依赖于平台的线程工具包，但这将使你的游戏移植到其他平台变得更加困难。尽管如此，SDL 的线程 API 对于游戏可能任何需求都足够。

## SDL 音频编程

游戏编程中一个经常被忽视但关重要的领域是声音。计算机声音处理与计算机图形一样是一门科学，格式转换、混和和播放的基本原理非常简单。本节讨论了计算机音频的基础知识，并研究了 SDL 的音频编程接口。

### 使用 PCM 表示声音

计算机声音基于脉冲编码调制，或 PCM。如你所知，视频源中的像素以固定间隔编码光学图像的平均颜色强度，更多的像素允许更接近地表示原始图像。PCM 数据具有相同的目的，只是它代表的是声波中连续间隔的平均强度。PCM 数据的每个“像素”被称为采样。这些样本发生的速率是采样率或声音数据的频率。采样率用标准的国际制频率单位赫兹（Hz）表示。较高的采样率允许更接近地表示原始声波。

单个 PCM 样本通常为每个通道 8 位或 16 位（1 或 2 字节）（单声道一个通道，立体声两个通道），游戏级声音通常以 22,050 Hz 或 44,100 Hz 的频率采样。样本可以表示为有符号或无符号数。16 位样本可以比 8 位样本精确得多的表示声音的强度，但它涉及两倍的数据。在 44,100 Hz 下使用 16 位样本，每秒钟的声音数据将消耗近 90 千字节的存储空间，立体声则是双倍。游戏

| | 单声道 | 立体声 |
|---|---|---|
| | 8 bit | 16 bit | 8 bit | 16 bit |
| 11025 Hz | 11,025 | 22,050 | 22,050 | 44,100 |
| 22050 Hz | 22,050 | 44,100 | 44,100 | 88,200 |
| 44100 Hz | 44,100 | 88,200 | 88,200 | 176,400 |

表 4-1：各种声音格式消耗的存储（每秒字节）程序员必须在声音质量和磁盘空间之间做出权衡。随着廉价互联网连接的出现和 CD-ROM 驱动器的普及，这种权衡已不再是问题。正如原始像素数据通常存储在 `.bmp` 文件中，原始 PCM 样本通常存储在 `.wav` 文件中。SDL 可以 `SDL_LoadW` 函数 读取这些文件。

## Function `SDL_LoadWAV(file, spec, buffer, length)`

摘要：将 RIFF `.wav` 文件加载到内存。

返回值：成功返回非空，失败返回 NULL。指定的 `SDL_AudioSpec` 结构包含相关信息，将 `*buffer` 设置为新分配的缓冲区，并设置 `*length` 为缓冲区的大小。

参数：
- `file`—要加载的文件名。更通用的 `SDL_LoadWAV_RW` 提供从非文件源加载 `.wav` 数据的方法（事实上，`SDL_LoadWAV` 只是 `SDL_LoadWAV_RW` 的封装）。
- `spec`—指向接收加载采样率和格式的 `SDL_AudioSpec` 结构。
- `buffer`—指向接收新分配样本缓冲区的 `Uint8 *`。
- `length`—指向接收缓冲区的 `Uint32`。

### Function `SDL_FreeWAV(buffer)`

摘要：释放之前 `SDL_LoadWAV` 分配的内存。这是必要的，因为数据可能不是通过 `malloc` 分配的，或者可能受到其他考虑。仅使用此函数释放 SDL 分配的样本数据；释放自己的声音缓冲区使用 `free`。

参数：
- `buffer`—要释放的样本数据。

### Structure `SDL_AudioSpec`

摘要：包含特定声音格式的信息：频率、采样大小等。用于 `SDL OpenAudio` 等函数。

成员：
- `freq`—每秒采样频率。对于立体声，这意味着每个通道每秒一个样本（即，立体声 44,100 Hz 实际上是每秒 88,200 个样本）。
- `format`—样本格式。可能值为 `AUDIO_S16` 和 `AUDIO_U8`。（还有其他格式，但它们并不常见且未完全支持——我是惨痛得来的。）
- `silence`—对应静音的 PCM 样本值（对于16 位有符号格式通常为 0，对于8 位无符号格式为 128）。由 SDL 计算。只读。
- `channels`—交错通道的数量。这通常为一（单声道）或二（立体声）。

`samples`—音频传输缓冲区中的样本数。典型值为 4,096。

`size`—音频传输缓冲区的大小（单位为字节）。由 SDL 计算。只读。

`callback`—指向 SDL 应该调用的函数，该函数用于检索更多用于播放的样本数据。

PCM 数据处理起来非常方便，尽管需要考虑大小问题。关键在于意识到 PCM 仅仅是一组近似能量波的测量值。强声波会产生较大的 PCM 样本值，而弱声波则会产生较小的值。要增加或减少 PCM 声波的音量，只需将每个样本乘以一个常数即可。要创建音量衰减效果，将每个样本乘以一个逐渐增大或减小的值。要在两个样本之间进行淡出，只需进行带权重变化的平均值计算。波是可叠加的；程序可以通过简单地相加（或取平均）样本来组合（混合）声音。记住，二进制数字是有限的；将样本乘以一个很大的常数或相加过多样本可能会导致溢出，从而引起声音失真。

### 为声卡提供数据

声卡在概念上非常简单：它接受连续的 PCM 样本流，并通过一组扬声器或耳机重建原始声波。你的基本任务是为声卡提供 PCM 样本。这有点技巧。如果你想要 44.1 千赫兹 (kHz) 的音频（音频 CD 上存储的音频质量），你需要每通道每向声卡提供 44,100 个样本。使用 16 位样本和双通道（立体声），这将产生 176,400 字节的音频数据（见表 4！）。此外，这一点至关重要。数据的任何中断都会导致明显的杂音。

如果让游戏每秒停止 44,100 次来为声卡获取更多数据，将是既困难又极其愚蠢的。幸运的是，计算机给了我们一点帮助。大多数现代计算机架构都包含一种称为直接内存访问（或 DMA）的特性。DMA 为高速后台内存传输提供了支持。这些传输用于多种用途，但最常见的用途是向声卡、硬盘和视频加速器传输大量数据。你可以定期地给计算机的 DMA 控制器提供几千个 PCM 样本的缓冲区来传输声音，DMA 控制器会在传输完成后通知程序，以便其发送下一块样本。

操作系统的驱动程序会为你处理 DMA；你只需要确保你生成音频的速度足够快。这有时通过回调函数实现。每当计算机声学硬件快速等待更多音频数据时，SDL 就会相应调用你的音频回调函数。回调函数必须将更多音频数据拷贝到给定的缓冲区。这通常涉及将几种声音混合在一起。

这种方案有一个小问题：由于你是分块向声卡发送数据，因此在播放任何新声音之前总会有轻微的延迟。例如，假设我们的程序需要播放射枪声。它可能会将该声音添加到内部声音列表中，以混合到输出流中。然而，声卡可能还没有准备好接收更多数据，因此混合后的样本必须等待。这种现象被称为延迟（latency），你应该尽可能将其最小化。你可以通过在初始化声卡时指定较小的声音缓冲区来减少延迟，但从现实来看你无法消除它（这在真实性方面通常不是问题；现实生活中也存在延迟，因为光的传播速度比声音快得多）。

## SDL 音频播放示例

我们已经讨论了足够声音编程的细节；现在是时候举个例子了。这个例子比之前的示例要长一点，但代码非常直观。

### 代码列表 4–12 (`audio-sdl.c`)

```c
/* 使用 SDL 进行音频混合的示例。 */

#include <SDL/SDL.h>

#include <stdio.h>

#include <stdlib.h>

#include <assert.h>
```

```c
/* 加载声音的结构体。 */

typedef struct sound_s {

    Uint8 *samples;      /* 原始 PCM 样本数据 */

    Uint32 length;       /* 数据的字节大小 */

} sound_t, *sound_p;
```

```c
/* 正在播放的结构体。 */

typedef struct playing_s {

    int active;            /* 如果应该播放此声音则为 1 */

    sound_p sound;         /* 要播放的声音数据 */

    Uint32 position;      /* 缓冲区中的当前位置 */

} playing_t, *playing_p;
```

```c
/* 所有激活音效的数组。 */

#define MAX_PLAYING_SOUNDS 10

playing_t sounds[MAX_PLAYING_SOUNDS];
```

```c
/* 此值越高，每个正在播放的声音就越大。

   然而，如果播放的声音过多，高值可能会导致失真。

   请对此进行实验。 */

#define VOLUME_PER_SOUND      SDL_MIX_MAXVOLUME / 2
```

```c
/* 每当声卡需要更多样本进行播放时，SDL 就会调用此函数。

   它可能从单独线程调用，因此我们应该小心处理所接触的内容。 */

void AudioCallback(void *user_data, Uint8 *audio, int length)

{

    /* 清空音频缓冲区，以便我们将样本混合其中。 */

    memset(audio, 0, length);
```

```c
printf("%s" was loaded and converted successfully.\n",

    filename);

return 0;

}
```

```c
/* 停止所有正在播放的声音。 */

void ClearPlayingSounds(void)

{

    int i;

    for (i = 0; i < MAX_PLAYING_SOUNDS; i++) {

        playing[i].active = 0;

    }

}
```

```c
/* 将声音添加到当前播放的声音列表中。 */

AudioCallback 将在被调用时开始将此声音混合到流中

（可能在几秒钟的一小部分内）。 */

int PlaySound(sound_p sound)

{

    int i;

    /* 为此声音寻找一个空槽位。 */

    for (i = 0; i < MAX_PLAYING_SOUNDS; i++) {

        if (playing[i].active == 0)

            break;

    }

    /* 如果没有空槽位，则报告失败。 */

    if (i == MAX_PLAYING_SOUNDS)

        return 1;

    /* 音频回调会访问 'playing' 结构体，

    所以我们在访问它们之前应该获取锁。 */

    SDL_LockAudio();

    playing[i].active = 1;

    playing[i].sound = sound;

    playing[i].position = 0;

    SDL_UnlockAudio();

    return 0;

}
```

# 第 4 章

```c
int main()

{

    SDL_Surface *screen;

    SDL_Event event;

    int quit_flag = 0; /* 我们在想要退出时设置此标记。 */

    /* 音频格式规范。 */

    SDL_AudioSpec desired, obtained;

    /* 我们加载的声音及其格式。 */

    sound_t cannon, explosion;

    /* 初始化 SDL 的视频和音频子系统。

    视频系统对于接收事件是必要的。 */

    if ((SDL_INIT(SDL_INIT_VIDEO) | SDL_INIT_AUDIO) != 0) {

        printf("无法初始化 SDL: %s\n", SDL_Error());

        return 1;

    }

    /* 确保在程序退出时调用 SDL_Quit。 */

    atexit(SDL_Quit);

    /* 我们还需要退出前调用此函数。SDL_Quit

    没有为我们正确关闭音频设备。 */

    atexit(SDL_CloseAudio);

    /* 尝试设置 256x256 彩色（16位）视频模式。 */

    screen = SDL_SetVideoMode(256, 256, 16, 0);

    if (screen == NULL) {

        printf("无法设置视频模式: %s\n", SDL_Error());

        return 1;

    }

    /* 打开音频设备。声音驱动程序将尝试提供

    请求的格式，但可能不会成功。

    'obtained' 结构体将被填充实际的    格式数据。 */

    desired.freq = 44100;          /* 期望输出率 */

    desired.format = AUDIO_S16;    /* 请求有符号 16 位采样 */

    desired.samples = 4096;      /* 这是任意的 */

    desired.channels = 2;         /* 请求立体声 */

    desired.callback = AudioCallback;

    desired.userdata = NULL;      /* 我们不需要这个 */

    if (SDL_OpenAudio(&desired, &obtained) < 0) {

        printf("无法打开音频设备: %s\n", SDL_Error());

        return 1;

    }

    /* 加载我们的声音文件并转换为

    声卡的格式。 */

    if (LoadAndConvertSound("cannon.wav", &obtained, &cannon) != 0) {

        printf("无法加载声音。\n");

        return 1;

    }

    if (LoadAndConvertSound("explosion.wav", &obtained, &explosion) != 0) {

        printf("无法加载声音。\n");

        return 1;

    }

    /* 清空正在播放的声音列表。 */

    ClearPlayingSounds();

    /* SDL 的音频初始处于暂停状态。启动它。 */

    SDL_PauseAudio(0);

    printf("按 'Q' 退出。C 和 E 声音。\n");

    /* 开始事件循环。持续读取事件，直到发生

    错误或退出标记被设置。 */

    while (SDL_WaitEvent(&event) != 0 && quit_flag == 0) {

        SDL_Keyym keysym;

        switch (event.type) {

            case SDL_KEYDOWN:

                keysym = event.key.keysym;

                /* 如果用户按下 Q，退出。 */

                if (keysym.sym == SDL_q) {

                    printf("按了 Q，正在退出。\n");

                    quit_flag = 1;

                }

                /* 'C' 射击大炮。 */

                if (keysym.sym == SDL_c) {

                    printf("发射大炮!\n");

                    PlaySound(&cannon);

                }

                /* 'E' 播放爆炸。 */

                if (keysym.sym == SDL_e) {

                    printf("轰！\n");

                    PlaySound(&explosion);

                }

                break;

            case SDL_QUIT:

                printf("退出事件 再见。\n");

                quit_flag = 1;

                /* 停止正在播放的声音。 */

                SDL_PauseAudio(1);

                /* 释放锁。 */

                SDL_LockAudio();

                /* 释放声音。 */

                free(cannon);

                free(explosion);

                /* 释放锁。 */

                SDL_UnlockAudio();

                return 0;

        }

    }

}
```
