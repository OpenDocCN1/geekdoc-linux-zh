
从实际角度来看，我们可以从上述表达式中取前四项来设计一个近似方波。下面你可以看到 Matlab 程序的完整列表（列表 4.10）：

### 列表 4.10

```
cf = 500;
sf = 22050;
d = 10.0;
n = sf * d;
s = (1:n) / sf;
s = 1.3 * sin(cf * s) + 0.45 * sin(3 * cf * s) + 0.25 * sin(5 * cf * s) + 0.18 * sin(7 * cf * s);
soundsc(s, sf, 16);
```

我们将此源代码保存为 `square_wave_test.m` 文件，并与任何音频编辑器一起执行该脚本。在使用 Audacity 的情况下，将得到下面的图片（图 4.12）：

![](img/c0e2a8f44eadc53b4372ff3151186ecc_174_0.png)

图 4.12

配置好 Audacity 后，你可以启动 m 文件进行执行：

```
>> square_wave_test
```

## 第 4 章 居家项目中的声卡

使用上述程序启动 GoldWave 应用将得到如下结果（图 4.13）：

![](img/c0e2a8f44eadc53b4372ff3151186ecc_175_0.png)

图 4.13

如果你从表达式中引入第 9 次和第 11 次谐波，例如，

Square wave = 4/pi * [(sin(x)/1 + sin(3x)/3 + sin(5x)/5 + sin(7x)/7 + ...)]

将其引入列表 4.50 中合适的位置（即确定信号 `s` 的地方），你将获得对我们方波信号更好的近似。

到目前为止，我们已经了解了许多音频数据处理。剩下的唯一问题是如何将我们的声音保存到磁盘上。有各种格式的文件来存储音频数据。你可以将音频缓冲区写入二进制文件（称为“raw”文件），也可以将数据存储在特定格式（`.wav`, `mp3` 等）中，这些格式用于以某种方式组织音频数据。“纯”原始音频文件的优势是，它们可以使用音频编辑器应用程序轻松地转换为任何特定格式。为了展示音频文件的一些基本操作，开发了一个非常简单的 C++ 应用程序。

174

其源代码所示下方的列表 4.11。该程序从声卡输入端（“Line-in jack”）获取音频数据，并将数据写入 `.raw` 文件中。这里假设使用的默认音频系统是 ALSA，因此我们可以应用 ALSA API 函数来处理声音信号。让我们我们的音频文件命名为 `Sound_Test_22050.raw`（通常在写入二进制文件时可以省略 `.raw` 扩展名）。假设采样率为为 22050。

### 列表 4.11

```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include "alsa/asound.h"

int main (void) {
    int i;
    int err;
    short buf[32000];

    unsigned int rate = 22050;
    snd_pcm_t *capture_handle;
    snd_pcm_hw_params *hw_params;

    FILE *fp;
    fp = fopen("Sound_Test_22050.raw", "ab+");
    if ((err = snd_pcm_open(&capture_handle, "default", SND_PCM_CAPTURE, 0)) < 0) {
        fprintf(stderr, "cannot open audio device: %s\n", snd_strerror(err));
        exit(1);
    }
    if ((err = snd_pcm_hw_params_malloc(&hw_params)) < 0) {
        fprintf(stderr, "cannot allocate hardware structure: %s\n", snd_strerror(err));
        exit(1);
    }
```

## 第 4 章 居家项目中的声卡

```
if ((err = snd_pcm_hw_params_any(capture_handle, hw_params)) < 0) {
    fprintf(stderr, "cannot initialize hardware structure: %s\n", snd_strerror(err));
    exit(1);
}

if ((err = snd_pcm_hw_params_set_access(capture_handle, hw_params, SND_PCM_ACCESS_INTERLEAVED)) < 0) {
    fprintf(stderr, "cannot set access: %s\n", snd_strerror(err));
    exit(1);
}

if ((err = snd_pcm_hw_params_set_format(capture_handle, hw_params, SND_PCM_FORMAT_S16_LE)) < 0) {
    fprintf(stderr, "cannot set sample format: %s\n", snd_strerror(err));
    exit(1);
}

if ((err = snd_pcm_hw_params_set_rate_near(capture_handle, hw_params, &rate, 0)) < 0) {
    fprintf(stderr, "cannot set sample rate: %s\n", snd_strerror(err));
    exit(1);
}

if ((err = snd_pcm_hw_params_set_channels(capture_handle, hw_params, 1)) < 0) {
    fprintf(stderr, "cannot set channel count: %s\n", snd_strerror(err));
    exit(1);
}

if ((err = snd_pcm_hw_params(capture_handle, hw_params)) < 0) {
    fprintf(stderr, "cannot set parameters: %s\n", snd_strerror(err));
    exit(1);
}

snd_pcm_hw_params_free(hw_params);
if ((err = snd_pcm_prepare(capture_handle)) < 0) {
    fprintf(stderr, "cannot prepare audio interface for use: %s\n", snd_strerror(err));
}

for (i = 0; i < 200; i++) {
    if ((err = snd_pcm_readi(capture_handle, buf, 32000)) != 32000) {
        fprintf(stderr, "read from audio interface failed: %s\n", snd_strerror(err));
    }

    fwrite(buf, sizeof(short), 32000, fp);
    snd_pcm_close(capture_handle);
    fclose(fp);
    return 0;
}
```

## 第 4 章 居家项目中的声卡

先来说变量。`buf` 变量标识存储音频数据的 32000 字节数组，`rate` 变量决定采样率。`capture_handle` 变量将包含当前使用的音频设备的句柄，`hw_params` 变量指向存储音频设备所有参数的地方。

捕捉音频数据之前的准备步骤以通用方式实现。首先，程序在 Linux 系统中打开默认音频设备（`snd_pcm_open` 函数），然后在 `hw_params` 中写入相应的参数。音频设备被配置为单声道模式运行，采样率为 22050，每个样本 16 位。在将参数写入声卡（`snd_pcm_hw_params` 函数）并为数据读取准备音频接口（`snd_pcm_prepare` 函数）后，程序在一个计数为 200 的 `for()` 循环中开始捕捉音频数据。

在每次迭代之初，数据流被读入 `buf`（`snd_pcm_read` 函数），`buf` 的内容存储在之前通过写入函数 `fopen()` 打开的文件 `fp` 中：

`fp = fopen("Sound_Test_22050.raw", "ab+");`

循环结束后，音频设备描述符关闭（`snd_pcm_close` 函数）。为了将数据刷入磁盘，我们还需要关闭文件指针（`fclose` 函数）。新创建的 raw 文件可以使用 ALSA 系统中包含的标准工具 `aplay` 进行播放。你可以应用流行的软件界面来播放此文件。此外，raw 文件可以由如 GoldWave 等任何流行程序播放。请注意，通过 line-in 输入录制的音频数据可能由于输入前放大器级性能特性低而缺乏高质，因此我们通常需要通过使用 GoldWave、Audacity 等高级音频编辑器来消除噪声。你可以对这段源代码进行实验并在必要时对其进行改进。

将它们保存为 WAV 文件。我选取了两个曲目，“Pump”和“House full of bullets”，并使用 `arecord` 工具将这两个音频流都转换为两个 WAV 文件。

为了捕获音频流，我们可以应用程序混合器，它允许将音频数据从声卡的模拟数字转换器（ADC）直接传递到负责采集声音的数字模拟转换器（DAC）。然而，这适用于具有“环回（loopback）”接口的声卡，此时音频数据流可以从内部 ADC 重定向到 DAC。或者，我们可以选择另一种方法——使用音频线将“扬器输出（Speaker out）”和“线路输入（Line-In）”连接起来。在这种情况下，输出声音将直接进入线路输入。

当来自互联网的音频流到达扬器输出时，我们将使用 `arecord` 工具捕获并将其录制 WAV 文件。同样，由于音频前级放大器存在噪声，我们应该启动某些音频编辑器来消除 WAV 文件中的噪声。捕获和录制音乐时，执行 `arecord` 工具需要以下参数：

```
$ arecord -d 400 -c 2 -f dat -t wav The_Pump.wav
Recording WAVE 'The_Pump.wav' : Signed 16 bit Little Endian
Rate 48000 Hz, Stereo
```

录制完成后，当前目录将包含 `The_Pump.wav` 文件。同样的方法，音乐文件被写入：

```
$ arecord -d 400 -c 2 -f dat -t wav The_House_full_of_bullets.wav
Recording WAVE 'The_House_full_of_bullets.wav' : Signed 16 bit
Little Endian, Rate 48000 Hz, Stereo
```

要播放刚刚保存的 WAV 文件，可以使用 `aplay` 命令：

```
$ aplay -c 2 -f dat -t wav The_Pump.wav
Playing WAVE 'The_Pump.wav' : Signed 16 bit Endian,
Rate 48000 Hz, Stereo
```

注意，通过互联网传输音频流需要高网络性能。另一种录制/播放声音的方法是使用 `sox` 工具。Sox 可以读取和写入大多数流行格式的音频文件，并可以可选地对其应用效果；它可以合并多个源、合成音频，并在许多系统上作为通用音频播放器或多轨道音频录制器使用。它还具有将输入拆分为多个输出文件的能力。最后，当我们使用一些带有图形用户界流行音频编辑器（Audacity、GoldWave 等）时，可以专业地处理音频信号。

# 结论

我们讨论了 Linux 操作系统中标准声卡的一些用途。如你所见，这种流行的设备可以安装在控制或测量系统中。声卡可以成功控制外部电路，可以作为低频信号的发生器，也可以处理低级输入信号。通过将声卡与 PC 的串口或并行口等外围设备相结合，你可以设计强大的数据采集和测量系统。声卡得到了 NI LabView 和 Matlab/Simulink 等流行软件包的支持，因此使我们能够开发复杂的项目。

# 第 5 章 用于家庭和实验室的网络与无线系统

到目前，我们讨论了在桌面电脑或笔记本电脑上本地运行的嵌入式项目。但现在你通常也希望控制你的硬件或从某些远程获取数据。例如，当你想从工作场所操作家中的系统或反之亦然时，就需要这样做。在这些情况下，你需要构建由一些相对独立的部分（子系统）组成的分布式系统，每个部分都可以在单机 PC 上运行。你可能还希望修改已经构建的嵌入式项目，以便将数据传递给另一个应用程序，例如 MySQL、OpenOffice 或运行在同一台机器或互联网某处的文本编辑器。将你的本地应用程序放在某些分布式环境中可能会为你的系统提供新的便利。例如，你可以安排你的分布式系统，使一个应用程序执行高级操作，如结果的可视化和/或提供良好的图形用户界面。上面的示例仅说明了你可能开始考虑构建分布式系统的若干许多情况。本章将帮助你理解在 Linux 中设计分布式系统的许多方面。

总的来说，在 Linux 中开发分布式系统有一些常用方法——我们将在本章开始讨论其中两种，其余部分将致力于设计分布式系统的实际方面。文中的方法基于使用 Linux 的网络功能。这些常用特性是构成网络基础的 TCP/IP 和本地套接字（local sockets）。

现在，当我们提到“分布式应用”时，我们指的是“网络应用”，反之亦然。构建分布式系统需要大量的网络编程以及对网络应用程序开发的基本概念的了解。网络编程中的关键术是“套接字（socket）”，因此在详细介绍我们的应用程序之前，我们将详细考虑它。“套接字”一词可以被视为分配给网络应用的“地址”或“端点”。TCP/IP 套接字由两个基本参数决定：IP 地址和端口。两个网络应用程序只能通过套接字相互交互。

IP 地址识别网络上的 PC，并且对于特定网络应该是唯一的。端口是一个数字，它与 IP 地址结合，用于标识特定网络应用程序的套接字。这是一个非常简单的描述，尽管如此，它有助于事情变得清晰。两个网络应用程序之间的交互可以用图 5.1 所示。

# 第 5 章 用于家庭和实验室的网络与无线系统

| 图 5.1 两个网络应用程序之间的交互 |

| :--- |

| ![Fig 5.1](img/c0e2a8f44eadc53b4372ff315183_0.png) |

| 用于家庭和实验室的网络与无线系统 |

你可以看到“网络应用程序 1”通过网络与“网络应用程序 2”通信。“网络应用程序 1”想要与“网络应用程序 2”通信，因此它必须知道 IP 地址和端口。否则，“网络应用程序 2”在处理“网络应用程序 1”时应该知道 IP 地址和端口。执行发生的网络接口。

让我们详细讨论 IP 地址和端口。

IP 地址是分配给网络接口或一组接口的标识符。从第一个角度看，网络接口似乎是你的 PC 的网卡，加上相应的软件控制数据传输。每个 IP 地址可以识别 IP 包（在网络传输的数据块）的源或目的。现在许多 IP 地址根据 IPv4 标准形成，尽管未来 IPv4 将被 IPv6 代替。原因显而易见：IPv4 地址长度为 32 位，但 IPv6 的出现允许我们大幅扩展即将过载的互联网地址空间。

在网络接口上启用 TCP/IP 时，我们应该为其分配一个或多个逻辑 IPv4 地址，自动或手动分配。表示为 0 和 1 组成的 32 位字符串，但由于这非常常见，引入了点十进制表示法，点表示 0 到 255 的四个十进制数字。每个数字（字节）代表 32 位地址中的 8 位或 1 字节。例如，IPv4 地址 11000010000010001111000100000010 用点十进制表示法表示为 194.15.28.10。

除了 IP 地址之外，应用程序必须提供目标应用程序的 TCP 端口号。端口提供了发送段的位置。每个端口必须通过其唯一编号进行标识。1024 以下的端口号是由互联网分配数字机构（IANA）分配给预定义网络应用程序的常用端口。例如，端口号 23 预留给 Telnet；端口 80 留给 HTTP，等。

## 家庭和实验室的网络与无线系统

到此时，我们已经知道了网络应用程序之间是如何通信的。下一个问题是如何编写网络应用程序来传输或接收某些数据。为了清晰起见，查看网络应用程序的层级结构将很有帮助。你每天都会面对各种类型的应用程序。广泛使用的网络浏览器就是此类应用程序的一个示例。作为编写网络应用程序的一般规则，引入了一种被称为 DARPA 模型的特殊四层概念模型。

该模型映射了 TCP/IP 协议族，包括应用层、传输层、网络层和网络接口层（图 5.2）：

![](img/c0e2a8f44eadc53b4372ff3151186ecc_184_0.png)

图 5.2

该模型使我们理解网络应用程序是如何相互交互的。网络接口层（也称为网络访问层）负责在网络介质上发送 TCP/IP 数据包并接收网络介质上的 TCP/IP 数据包。注意，TCP/IP 协议族的设计独立于网络访问方法、帧格式和介质。因此，我们可以使用 TCP/IP 在使用各种局域网技术（以太网、802.11 无线局域网、WAN 技术）的不同网络类型之间通信。由于其独立于任何特定的网络技术，TCP/IP 也可以很容易适应新技术。

网络层负责地址、封装和路由。其中，网络层包含了网协议（IP），它对数据包进行地址、路由、分片和重组。
