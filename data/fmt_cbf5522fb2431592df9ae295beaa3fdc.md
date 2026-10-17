
```c
int setup_buffer(unsigned char **buffer, size_t *buffersize,
int play_format,
int channels,
int sample_frequency)
unsigned char *walker = 0; /* 用于遍历
 * 我们将分配的内存缓冲区
 */
int seconds
    = 2;
int needed = bytes_needed(play_format,
channels,
sample_frequency,
seconds);
int i;
if ((needed == 0) || (!buffer) || (!buffersize))
return 0;

walker = malloc(needed);
if (!walker)
{
*buffersize = 0;
return 0;
}

*buffer = walker; /* 保存缓冲区的起始 */
*buffersize = needed;
needed /= channels;
for (i = 0; i < needed; ++i)
{
int j;
channels = <<j
/* 以下公式生成锯齿波形 */
walker = -(1 << (j+1)) & 0xff
}
return 1;
}
```

# 第 19 章

我们已经尽力让这个函数尽可能通用，以便你可以尝试不同数量的通道和不同的格式。我们现在可以在主程序中使用它；我们需要一个缓冲区来存储数据，因此我们将其添加到变量部分：

```c
channels = 1;
int play_format = AFMT_UB;
int sample_frequency = 48000;
* 如果你的声卡不支持如此高的
* 频率，请将其改为 44100 或 22050。
```

```c
unsigned char *buffer = 0;
size_t buffersize = 0;
```

一旦我们设置了各种参数，我们就创建缓冲区：

```c
printf(stdout,
"该设备现在已好播放以下组合：\n
  "Format: %d\n"
  "Channels: %d\n"
  "Frequency: %d\n",
  play_format, channels, sample_frequency);
```

> /* 使用所需的播放格式初始化缓冲区 */

```c
if (setup_buffer(&buffer, &buffersize, 
play_format, channels, sample_frequency))
  { /* 播放缓冲区的代码在此处 */
```

```c
close(device_fd);
```

最后，这里是播放缓冲区并在完成后清理它的实际代码：

```c
/* 播放缓冲区的代码在此处 */
size_t bytes_written = 0;
printf(stdout,
"正在向设备写入 %d 字节。\n",
  buffersize);
bytes_written = write(device_fd, buffer, buffersize);
```

```c
fprintf(stdout, 
    "成功向设备写入了 %d 字节。\n",
    bytes_written);

reset_device(device_fd);

free(buffer);
}
close(device_fd);
```

# 清理

有多种方法可以将设备恢复到已知状态，这在结束长时间音频文件的播放时可能是必要的。一种方法是关闭设备（通过调用 `close` 函数）；另一种方法是等待直到设备的所有内部缓冲区刷新：

## wait_till_finished

```c
int wait_till_finished(int device_fd)
{
    if (ioctl(device_fd, SNDCTL_DSP_SYNC, 0) == -1)
    {
        return -1; /* 设备不支持该格式（或 ioctl()） */
    }
    return 1; /* 所有声音已播放完毕 */
}
```

另一种可能性是重置设备；这会停止正在播放的内容并准备好设备播放更多内容，而 `close` 函数会先让设备完成它正在执行的操作。在重置之后，你可以为设备设置不同的参数。

我们在上面的代码中使用了以下函数，以确保设备在退出程序之前停止——我们为声卡使用了一个早期驱动程序，如果不这样做，它有时会挂起：

## reset_device

```c
int reset_device(int device_fd)
{
    if (ioctl(device_fd, SNDCTL_DSP_RESET, 0) == -1)
    {
        return -1; /* 设备不支持该格式（或 ioctl()） */
    }
    return 1; /* 音设备已重置 */
}
```

# 动态图像

Linux 对视频和动画的支持大致可以分为三类：

- 软件播放器
- 硬件播放器（由薄软件层辅助的硬件驱动程序）
- 混合型（由软件模块辅助的硬件播放器）

我们将逐一查看这些类别。

## 软件播放器

## xanim

一直在维护的软件播放器无疑是 `xanim`，虽然它目前无人维护，但它支持许多文件。特别是，它在 Linux 上可用。

*(注：提供的 OCR 文本存在大量重复和错误，已根据逻辑结构进行了清理和提取。)*

# 第 19 章

## 如何获取

由于 OMS 的不断发展，获取它的最佳方法是通过 CVS，这意味着你需要安装一个 CVS 程序包：

```bash
mkdir ~/livid
cd ~/livid
export CVSROOT=server:anonymous@cvs.linuxvideo.org:/cvs/livid
cvs login
Logging as anonymous@cvs.linuxvideo.org
CVS password:
```

现在没有设置密码，直接按回车即可。你现在可以下载软件了：

```bash
cvs -x3 co -P ac3dec oms mpeg2dec mgadvid
```

请注意，除非你拥有带有硬件 DVD 解码器的 Matrix G200/G400 显，否则不需要指定 `mgadvid`。

工具现在将下载到各自的目录中。

> 请记住这是一个正在开发的项目，因此你从网站获取的构建可能无法正常编译。

OMS 有一些先决条件，例如各种开发工具的存在，包括：

- GNU autoconf 和 automate
- GTK+ 和 imlib

`configure` 脚本会告诉你它们需要的版本。

现在进入各个目录，并使用 `configure` 来配置、构建和安装包。以 root 身份执行最为简单，因为安装需要必要的权限。

```bash
cd ac3dec; ./configure; make; make install
cd ../mpeg2dec; ./configure; make; make install
```

你需要对 `oms` 执行 `make install`，否则它将无法从两个程序找到库例程。最后，配置 `oms` 本身：

```bash
cd ../oms; ./configure; make; make install
```

`oms` 的构建很可能因为找不到头文件而失败。如果发生这种情况，进入该目录执行 `make` 和 `make install`，然后在顶层目录重试。不要忘记在 `oms` 目录中执行最后的 `make install`，否则程序将无法找到它所需的各种插件。

现在，唯一要做的工作就是运行 `oms`：

```bash
$ oms
```

如果一切顺利，你将看到一个类似于这样的界面：

![](img/930f7611cac03a5cd5573f4bb94fd7b9_752_0.png)

现在向你的 DVD 播放器中插入 DVD，点击 PlayList 并获取你 DVD 的播放列表。然后按下播放按钮并点击播放图标（如上图高所示）。然后坐下来享受吧！

## 政治与法律问题

多媒体世界被法律战所包围；我们每天都会听到针对涉及网络分发和多媒体工具的项目的诉讼（例如 Napster、Scour、DeCSS 等）。

其中最后一项最近让 Linux 处于了舆论焦点——取决于你询问谁，它要么是一种在 Linux 上查看 DVD 的无辜手段，要么是为了破解内置的物理版权保护并为广泛的 DVD 盗版开辟道路的协同努力。

关于多媒体分发（法律上或其他），已经有（并将继续有）书籍著作。著作法一直是先例和细微技术问题的雷区，我们不会试图代表对这一极其广泛的问题所表达的各种观点。然而，如果你想对 DeCSS 案例有一个有趣的视角，你可能想查看 http://www.opendvd.org。

# 第 19 章

## 参考文献

Linux Video, OMS 以及其他 DVD 相关链接：

http://www.linuxvideo.org

Video4Linux API:
