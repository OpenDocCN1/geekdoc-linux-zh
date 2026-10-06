
```c
#include <unistd.h>
#include <fcntl.h>
#include <sys/types.h>
#include <sys/ioctl.h>
#include <stdlib.h>
#include <stdio.h>
#include <linux/soundcard.h>
#include <math.h>

#define FREQUENCY 1000 // frequency = 1000Hz
#define DURATION 5 // 存储多少秒的语音
#define RATE 11025 // 采样率
#define SIZE 8 // 采样大小：8 或 16 位
#define CHANNELS 1 // 1 = 单声道 2 = 立体声

int main()
{
int fd; // 声设备文件描述符
int param; // ioctl 用的参数
int status; // 系统调用的返回状态

int il;
int nl;
nl = DURATION * RATE;

// 此缓冲区持有数字化的音频

char buf[nl];
double x;

// 打开声设备

fd = open("/dev/dsp", O_RDWR);
if (fd < 0)
{
  perror("open of /dev/dsp failed");
  exit(1);
}

// 设置采样参数
param = SIZE; // 采样大小
status = ioctl(fd, SOUND_PCM_WRITE_BITS, &param);
if (status == -1)
  perror("SOUND_PCM_WRITE_BITS ioctl failed");
if (param != SIZE)
  perror("unable to set sample size");

param = CHANNELS; // 单声道或立体声
status = ioctl(fd, SOUND_PCM_WRITE_CHANNELS, &param);
if (status == -1)
  perror("SOUND_PCM_WRITE_CHANNELS ioctl failed");
if (param != CHANNELS)
  perror("unable to set number of channels");

param = RATE; // 采样率
status = ioctl(fd, SOUND_PCM_WRITE_RATE, &param);
if (status == -1)
  perror("SOUND_PCM_WRITE_RATE ioctl failed");

// 用样本填充缓冲区
for (il = 0; il < nl; il++) {
  x = sin(il * 2.0 * M_PI * FREQUENCY / (double) RATE);
  buf[il] = (char)(int)(x+128);

  status = write(fd, buf, sizeof(buf)); // 播放声音缓冲区
  if (status != sizeof(buf))
    perror("wrote wrong number of bytes");
  status = ioctl(fd, SOUND_PCM_SYNC, 0);
  if (status == -1)
    perror("SOUND_PCM_SYNC ioctl failed");
  close(fd);
  return 0;
}
```

# 第 4 章 家庭项目中的声卡

注意我们通过程序方式创建正弦波，因此我们需要包含定义该函数的 `math.h` 头文件。此外，我们还需要（专门针对 gcc）使用以下命令编译此源码：

```bash
$ gcc playsound.c -o playsound
```

## 使用 OSS 编程音频

这些默认值。默认参数如下：8 位无符号采样、单通道（单声道）和 8 kHz 采样率。

如你所知，向 DSP 设备写入一系列数字样本会产生声音。再次强调，音频信号的格式通过调用带有适当参数的 `ioctl()` 来设置，但默认设置与输入信号定义的设置相同（8 位无符号数据、单声道和 8kHz 采样率）。

如果数据写入太慢，声音输出将出现断断或停顿。写入速度快于采样率将导致内核驱动程序阻塞调用者，直到音频硬件准备好处理新数据。与捕获输入数据一样，你可以使用 `ioctl()` 调用更改默认参数。通常情况下，你应该在打开设备之后、任何读/写操作之前设置参数。注意，你还应该按照下面列出的顺序设置参数。

如果参数超出范围，驱动程序将将其设置为最接近的值。例如，尝试在 8 位声卡上使用 16 位采样将导致驱动程序选择 8 位，但不会返回错误。值得验证返回的值对你的应用程序是否是可以接受的。用于 DSP 设备的所有 `ioctl()` 调用都采用以 `SOUND_PCM` 开头的参数名称。与 `SOUND_PCM_READ_XXX` 类似的参数用于返回参数的当前值。要更改值，`ioctl()` 调用应采用类似于 `SOUND_PCM_WRITE_XXX` 的参数。如上所述，这些调用还会返回所选的值，该值不一定是传递给音频驱动程序的值。

`ioctl()` 常量定义在 `linux/soundcard.h` 头文件中。让我们详细检查每一个常量。

- `SOUND_PCM_WRITE_BITS` 设置采样大小，以位为单位。有效选项是 8 和 16，但注意某些声卡不支持 16。
- `SOUND_PCM_READ_BITS` 返回当前采样大小，应为 8 位或 16 位；
- `SOUND_PCM_WRITE_CHANNELS` 设置通道数——1 为单声道，2 为立体声。在立体声模式下运行时，数据在读写时是交错的，格式为左-右-右。注意某些声卡不支持立体声模式，因此你必须检查调用返回的实际通道数；
- `SOUND_PCM_READ_CHANNELS` 返回当前通道数，1 或 2；
- `SOUND_PCM_WRITE_RATE` 设置每秒采样数的采样率。记住，所有声卡对采样率都有限制；内核驱动程序会将速率舍入到硬件支持的最最近速率，并返回实际的（舍入后的）速率。典型的下限为 4 kHz；上限为 13、15、22 或 44 kHz；
- `SOUND_PCM_READ_RATE` 返回当前采样率。这是内核使用的速率，由于之前讨论的舍入问题，该速率可能与之前调用 `SOUND_PCM_WRITE-RATE` 给出的速率不完全相同。

现在我们将考虑一个编程 DSP 设备的简单示例。程序将使用 `/dev/dsp` 设备创建 1000 Hz 的声音。声音将持续 5 秒。你可以看到下面的源代码（列表 4:1）：

### 列表 4.2

```c
#include <unistd.h>
#include <fcntl.h>
#include <sys/types.h>
#include <sys/ioctl.h>
#include <stdlib.h>
#include <stdio.h>
#include <string.h>
#include <linux/soundcard.h>
```

```c
#define DURATION 5 // 存储多少秒的（话语）声音
#define RATE 11025 // 采样率
#define SIZE 16 // 采样大小：8 或 16 位
#define CHANNELS 2 // 1 = 单声道 2 = 双声道
```

```c
int main()
{
 int fd; // 声学设备文件描述符
 int param; // ioctl 调用的参数
 int status; // 系统调用的返回状态

int nl;

// 打开声音设备

nl = DURATION * RATE * CHANNELS; // 内存缓冲区大小
char buf[nl]; // 此缓冲区持有数字音频数据

fd = open("/dev/dsp", O_RDWR);
if (fd < 0)
{
 perror("open of /dev/dsp failed");
 exit(1);
}
```

```c
// 设置采样参数
```

```c
param = SIZE;                      // 采样大小
status = ioctl(fd, SOUND_PCM_WRITE_BITS, &param);
if (status == -1)
    perror("SOUND_PCM_WRITE_BITS ioctl failed");
if (param != -1)
    perror("unable to set sample size");
```

```c
param = CHANNELS;                  // 单声道或立体
status = ioctl(fd, SOUND_PCM_WRITE_CHANNELS, &param);
if (status == -1)
    perror("SOUND_PCM_WRITE_CHANNELS ioctl failed");
if (param != CHANNELS)
    perror("unable to set number of channels");
```

```c
param = RATE;                        // 采样率
status = ioctl(fd, SOUND_PCM_WRITE_RATE, &param);
if (status == -1)
    perror("SOUND_PCM_WRITE_RATE ioctl failed");
```

```c
while (1)
{
    // 循环直到按下 Control-C

    printf("Say something:\n");
    status = read(fd, buf, sizeof(buf)); // 制声音
    if (status != sizeof(buf))
        perror("read wrong number of bytes");
    printf("Received:\n");

    status = write(fd, buf, sizeof(buf)); // 回放
    if (status != sizeof(buf))
        perror("wrote wrong number of bytes");

    // 在录音前等待播放完成
    status = ioctl(fd, SOUND_PCM_SYNC, 0);
    if (status == -1)
        perror("SOUND_PCM_SYNC ioctl failed");
}
close(fd);
return 0;
}
```

让我们深入研究源代码。按照惯例，我们必须为音频数据分配内存缓冲区。缓冲区（`buf`）的大小存储在 `nl` 变量中。程序打开 `/dev/dsp` 设备并使用 `ioctl()` 函数配置其参数。之后，程序进入一个无限 `while()` 循环，从输入读取数据并传递到输出。数据的读取是通过 `read()` 调用完成的，写入则通过调用 `write()` 函数完成。

将此源代码保存为 `record_play_sound.c` 并使用以下命令进行编译：

```bash
gcc record_play_sound.c -lm -o record_play_sound
```

成功编译后，你就可以启动程序。程序启动后，它会等待你读出某段短语，然后重放你刚刚保存的音频缓冲区。

### 使用 ALSA 进行编程

使用 ALSA 进行音频编程为开发者提供了优于 OSS 的关键优势。通过 ALSA，你被允许配置大多数音频参数，并在处理信号时提供更大的活性和创造力。此外，开发者从应用程序中获得了对音频处理的极大程度的控制。如果你想与 ALSA 声音系统工作，你应该意识到 ALSA 是在系统内核中配置的。安装 ALSA 后，会创建 `/proc/asound` 目录，因此你只需要在文件系统中检查它的是否存在即可。

如果你由于某些原因没有找到 `asound`，你可以自己下载并配置 ALSA。最新版本的 ALSA 声音系统软件可以在 `www.alsa-project.org` 找到。下载并解压此库后，你应该通过输入以下命令进行安装：

```bash
configure
make install
```

当你成功配置 ALSA 系统后，紧接着要做的事情是检查已安装声卡（s）的信息是否可用。要此操作，你可以查看 `/proc/asound/cards` 文件的内容。

```c
exit (1);
}
}
```

```c
snd_pcm_close (handle);
exit (0);
}
```

此应用程序生成一个正弦波信号，表示为 $\sin(2\pi F)$，其中 $F$ 是频率。为了访问 ALSA API 函数，我们需要放置一个带有适当头文件的包含指令：

```c
#include <alsa/asoundlib.h>
```

在这个程序中，我们定义了一些变量。`double` 类型变量 `frequency` 包含我们的频率值（在本例中为 500 Hz）。`int` 类型变量 `rate` 表示采样率，我们将将其设置为 44100 `samples/s`。我们还需要分配一些缓冲区来存储播放的音频数据。`buf` 变量是程序移动的地方。我们将形成 16 位采样，因此 `buf` 将包含 2 字节（`short`）值。`buf` 的大小被选择为 2048，尽管你也可以选择其他值。`double` 类型变量 `x` 将保存 `for` 循环中带符号标记的离散值。

为了给流设置硬件参数，我们需要分配一个 `snd_pcm_hw_params_t` 类型的 `hw params`。`handle` 变量将包含指向声设备的句柄，并在后续调用中用于操作音频流。
