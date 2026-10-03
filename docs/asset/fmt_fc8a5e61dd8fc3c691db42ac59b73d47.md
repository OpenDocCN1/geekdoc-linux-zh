
`location` 对象定义了新图像如何传输到活动屏幕。`location` 的 `x` 和 `y` 值将新图像居中于屏幕。注意调用了 `SDL_BlitSurface()` 函数，使用 `SDL_UpdateRect()` 函数执行活动 `SDL_Surface` 对象的实际更新。正如提到的，如果没有必要，不需要更新整个屏幕。示例 13-5 中的快速程序演示了如何使用 SDL 将图像加载到屏幕。

## 示例 13-5：使用 SDL 显示图像

```c
/* 专业编程 - SDL test */
#include <stdio.h>
#include <SDL.h>

int main(int argc, char **argv)
{
    SDL_Surface *screen, *image1, *image2;
    SDL_Rect location1, location2;
    int delay = 4;

    if (SDL_Init(SDL_INIT_VIDEO) < 0)
    {
        perror("SDLInit");
        return 1;
    }
    printf("SDL initialized.\n");

    screen = SDL_SetVideoMode(800, 600, 0, 0);
    if (screen == NULL)
    {
        printf("Problem: %s\n", SDL_GetError());
        return 1;
    }

    printf("Video mode set.\n");

    SDL_WM_SetCaption("SDL test", "testing");
    image1 = SDL_LoadBMP("image1.bmp");
    if (image1 == NULL) {
        printf("Problem: %s\n", SDL_GetError());
        return 1;
    }
    printf("image1 loaded.\n");

    image2 = SDL_LoadBMP("image2.bmp");
    if (image2 == NULL) {
        printf("Problem: %s\n", SDL_GetError());
        return 1;
    }
    printf("image2 loaded.\n");

    location1.x = (screen->w - image1->w) / 2;
    location1.y = (screen->h - image1->h) / 2;
    location1.w = image1->w;
    location1.h = image1->h;

    location2.x = (screen->w - image2->w) / 2;
    location2.y = (screen->h - image2->h) / 2;
    location2.w = image2->w;
    location2.h = image2->h;

    if (SDL_BlitSurface(image1, NULL, screen, &location1) < 0) {
        printf("Problem: %s\n", SDL_GetError());
        return 1;
    }
    SDL_UpdateRect(screen, 1, &location1);
    SDL_Delay(delay * 1000);

    if (SDL_BlitSurface(image2, NULL, screen, &location2) < 0) {
        printf("Problem: %s\n", SDL_GetError());
        return 1;
    }
    SDL_UpdateRect(screen, 1, &location2);
    SDL_Delay(delay * 1000);

    SDL_Quit();
    return 0;
}
```

`imagetest.c` 程序使用 `SDL_SetVideoMode()` 函数请求一个 800x600 大小的区域，使用系统默认的 bpp 和屏幕图像。对于大多数系统，默认会在当前运行的 X Window 系统内产生一个窗口。如果你想在全屏模式下尝试程序，可以在 `SDL_SetVideoMode()` 的最后一个参数中添加 `SDL_FULLSCREEN` 标志。

`SDL_LoadBMP()` 函数将两个图像（image1.bmp 和 image2.bmp）加载到两个 `SDL_Surface` 对象中。执行这项工作你需要准备两个图像（命名为 image1.bmp 和 image2.bmp）。在加载完每个图像后，计算图像的 `SDL_Rect location` 以将图像放置在可视屏幕中央。然后，使用 `SDL_BlitSurface()` 和 `SDL_UpdateRect()` 函数加载它们。`SDL_Delay()` 函数提供了一个更易用的计时器。程序使用它在每个图像显示之间暂停四秒。

编译应用程序并使用几个测试图像运行它。注意两个图像之间的切换非常快速且干净（特别是当你使用高级显卡时）。不难想象在屏幕上快速传输几个图像可以实现什么。

# 播放音频文件

每个成功的游戏都需要良好的音效。在 Linux 中，将音频文件发送到音频系统有时是一件困难的事。SDL 库提供了一个优秀的接口，可以在任何音频的任何操作系统上轻松播放音频文件。

SDL 使用 `SDL_AudioSpec` 结构处理音频文件。该结构体的格式如下：

```c
typedef struct {
    int freq;
    Uint16 format;
    Uint8 channels;
    Uint8 silence;
    Uint16 samples;
    Uint32 size;
    void (*callback)(void *userdata, Uint8 *stream, int len);
    void *userdata;
} SDL_AudioSpec;
```

`SDL_AudioSpec` 结构包含了处理音频文件所需的所有信息。结构字段如下：

| Field | Description |
|---|---|
| freq | 每秒采样数的音频频率 |
| format | 音频数据格式 |
| channels | 通道数（1 为单声道，2 为双声道） |
| silence | 音频缓冲区静音值 |
| samples | 以采样数为单位的音频缓冲区大小 |
| size | 以字节为单位的音频缓冲区大小 |
| callback | 用于填充音频缓冲区的回调函数 |
| userdata | 传递给回调函数的音频数据指针 |

## 第 13 章：图形与音频

大多数 `SDL_AudioSpec` 的值在加载音频文件时会自动填充。使用 `SDL_LoadWAV()` 函数可以将 .wav 音频文件加载到 `SDL_AudioSpec` 结构体中：

```c
SDL_AudioSpec *SDL_LoadWAV(const char *file, SDL_AudioSpec *spec,
Uint8 **audio_buf, Uint8 *audio_len)
```

`SDL_LoadWAV()` 函数将音频文件加载到 `SDL_AudioSpec` 对象 `spec` 中。它还会将 `audio_buf` 指针指向加载音频数据的缓冲区，并将 `audio_len` 参数设置为音频数据的长度。

音频数据的长度和指针是需要与 `SDL_AudioSpec` 信息同一起跟踪的重要条目。处理此类信息最常见的方法是使用另一个结构体：

```c
struct {
    SDL_AudioSpec spec;
    Uint8 *sound;
    Uint32 soundlen;
    int soundpos;
} wave;
SDL_LoadWAV("test.wav", &wave.spec, &wave.sound, &wave.soundlen);
```

该结构体在一个方便的位置提供了处理音频文件所需的所有信息。音频数据缓冲区的位置通过 `sound` 指针指向，音频缓冲区的长度保存在 `soundlen` 中。`soundpos` 变量将在播放音频文件时使用。一旦音频加载到内存中，你就可以准备播放了。

遗憾的是，事情在这里变得有点复杂了。记住，`SDL_AudioSpec` 对象指定了一个回调函数用于实际播放音频数据。回调函数就是事情变得复杂的地方。

SDL 将音频数据处理为流。在播放音频数据的持续期间，音频流必须停止并重启几次。每当流重启时，都会调用回调函数。它必须知道在音频文件中从何处停止，否则它每次都会从头开始重新播放文件。

为了处理这个问题，回调函数必须能够保留指向音频文件停止处流的指针，并使用该指针从中断的地方继续播放。这里 `soundpos` 变量就派上用场了。这是一个使用 `SDL_MixAudio()` 函数播放音频流的简短回调函数：

```c
void SDL_LCALL play(void *unused, Uint8 *stream, int len) {
    Uint32 amount = wave.soundlen - wave.soundpos;
    if (amount > len)
        amount = len;
    SDL_MixAudio(stream, &wave.sound[wave.soundpos], amount, SDL_MIX_MAXVOLUME);
    wave.soundpos += amount;
}
```

当创建 `SDL_AudioSpec` 对象时，它会将音频流及其长度传递给回调函数 `play`。局部变量 `amount` 根据 `soundpos` 变量的当前值来决定剩余多少音频需要播放。`SDL_MixAudio()` 函数用于将音频流发送到音频系统。`SDL_MixAudio()` 函数的格式为：

```c
void SDL_MixAudio(Uint8 *dst, Uint8 *src, Uint32 length, int volume)
```

调用 `SDL_MixAudio()` 会将音频文件的当前位置添加到音频流中，尝试播放所有剩余部分。最后一个参数 `volume` 指定了播放音频的相对音量。该值的范围从 `0` 到 `SDL_MIX_MAXVOLUME`。每当播放音频文件的一部分时，`soundpos` 变量就会更新为音频文件中下一个播放的位置。

一旦调用 `SDL_MixAudio()` 函数，它就会尝试将音频文件数据发送到音频系统。`SDL_PauseAudio()` 控制音频是否播放。使用参数 `1` 暂停音频播放，而使用参数 `0` 则开始播放。默认情况下，该参数设置为 `1`，暂停直到下一次调用 `SDL_PauseAudio()` 函数。

列表 13-6 所示的 `audiotest.c` 程序演示了如何使用 SDL 库播放 .wav 文件。

### 列表 13-6：使用 SDL 播放音频文件

```c
/*
 * Professional Linux Programming - SDL audio test
 */
#include <stdio.h>
#include <SDL/SDL.h>
#include <SDL/SDL_audio.h>

struct {
    SDL_AudioSpec spec;
    Uint8 *sound;
    Uint32 soundlen;
    int soundpos;
} wave;

void SDL_CALL playit(void *unused, Uint8 *stream, int len) {
    Uint32 amount = wave.soundlen - wave.soundpos;
    if (amount > len) {
        amount = len;
        SDL_MixAudio(stream, &wave.sound[wave.soundpos], amount, SDL_MIX_MAXVOLUME);
        wave.soundpos += amount;
    }
}

int main(int argc, char **argv) {
    char name[32];

    if (SDL_Init(SDL_INIT_AUDIO) < 0) {
        perror("Initializing:");
        return 1;
    }

    if (SDL_LoadWAV(argv[1], &wave.spec, &wave.sound, &wave.soundlen) == NULL) {
        printf("Problem: %s\n", SDL_GetError());
        return 1;
    }
    // ... rest of code omitted for brevity
}
```

## 访问 CD

在当今的多媒体世界中，许多系统包含 CD-ROM 驱动器。SDL 库允许你访问 CD。`SDL_CDOpen()` 函数返回一个 `SDL_CD` 对象。该对象是一个包含 CD 信息的结构体：

```c
typedef struct {
    int id;
    CDStatus status;
    int numtracks;
    int cur_track;
    int cur_frame;
    SDL_Track track[MAX_TRACKS+1];
} SDL_CD;
```

`CDstatus` 返回 CD-ROM 驱动器的当前状态：

- `CD_TRAYEMPTY`
- `CD_STOPPED`
- `CD_PLAYING`
- `CD_PAUSED`
- `CD_ERROR`

`numtracks` 和 `cur_track` 字段显而易见，显示了 CD 中的轨道数和当前轨道编号。`cur_frame` 字段并不那么显而易见。当前轨道内的帧位置是 CD 的基本单位。它等于音频的一个单位。你可以使用 `FRAMES_TO_MSF()` 函数将帧值转换为分钟、秒和帧。

一旦 CD 加载到 CD-ROM 驱动器中，播放轨道只需使用 `SDL_CDPlayTracks()` 函数即可：

```c
int SDL_CDPlayTracks(SDL_CD *cdrom, int start_track, int start_frame, int ntracks, int nframes)
```

其中 `cdrom` 是由 `SDL_CDOpen()` 函数打开的 `SDL_CD` 对象，`start_track` 是开始播放的轨道，`start_frame` 是开始播放的偏移量，`ntracks` 是从开始要播放的轨道数，`nframes` 是从最后一个轨道开始停止播放的帧数。

在默认 CD-ROM 驱动器中打开 CD 并播放第一轨道所示：

```c
SDL_CD *cdrom;
cdrom = SDL_CDOpen(0);
SDL_CDPlayTracks(cdrom, 0, 0, 1, 0);
```

就这些了！从 CD 播放音乐没有这更简单的了。SDL 还整合了一些函数来帮助清理有关 CD 的信息。

列表 13-7 所示的 `cdtest.c` 程序演示了如何使用几个 SDL 函数播放 CD 中的音乐曲目。

### 列表 13-7：使用 SDL 播放音乐 CD

```c
/*
 * Professional Linux Programming - SDL CD test
 * */
#include <stdio.h>
#include <SDL/SDL.h>

int main()
{
    SDL_CD *cdrom;
    // ... rest of code
}
```

```c
int track, i, m, s, f;

if (SDL_Init(SDL_INIT_CDROM) < 0) {
  perror("*track");
  return 1;
}

cdrom = SDL_CDOpen(0);
if (cdrom == NULL) {
  perror("*open");
  return 1;
}

if (CD_INDRIVE(cdrom->numtracks)) {
  printf("CD tracks: %d\n", cdrom->numtracks);
  for (i = 0; i < cdrom->numtracks; i++) {
    FRAMES_TO_MSF(cdrom->track[i].length, &s, &f);
    if (f > 0) {
      s++;
      printf("*Track %d: %d.2f\n", cdrom->track[i].id, m, s);
    }
  }
} else {
  printf("*Sorry, no CD detected in default drive\n");
  return 1;
}

while(1) {
  printf("*Please select track to play: *\n");
  scanf("%d", &track);
  if (track == -1) {
    break;
  }
  printf("*Playing track %d\n", track);
  if (SDL_CDPlayTracks(cdrom, track, 0, 1, 0) < 0) {
    printf("*Problem: %s\n", SDL_GetError());
    return 1;
  }
  SDL_Delay((m * 60 + s) * 1000);
}

SDL_CDClose(cdrom);
SDL_Quit();
return 0;
```
