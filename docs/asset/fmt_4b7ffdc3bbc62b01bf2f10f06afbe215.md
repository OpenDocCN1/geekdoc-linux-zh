
这是我们 `main` 函数的骨架代码；注意我们是以写入模式打开设备的。如果我们想让它尽可能万无一失，我们将使用 `stat` 或 `fstat` 调用来检查传递的文件名是否实际上是一个设备。如果不是，我们必须小心，因为引用的文件将被创建为空。因此，在接下来的代码中，我们首先以只读模式打开设备，然后尝试确保它是一个音频设备；只有在我们确定后，才会重新打开设备。

```c
int main(int argc, const char *argv[])
{
    const char *device = "/dev/dsp";
    int device_fd = -1;
    switch (argc)
    {
        case 2: device = argv[1];
            if (strcmp(device,"*") == 0) {
                Usage(stdout, argv[0]);
                exit(EXIT_SUCCESS);
            }
            break;
        case 1: break;
        default:
            Usage(stderr, argv[0]);
            exit(EXIT_FAILURE);
    }
```

我们知道要播放某些内容，只需要向设备写入；同样，如果我们只想录制，可以指定 `O_RDONLY`。然而，写入错误的位置可能是危险的，因此 `open_device` 调用必须检查传递的文件名是否指向设备：

```c
device_fd = open(device, O_WRONLY);

if (device_fd == -1) {
    exit(1);
}

/* 播放代码将在此此处 */
close(device_fd);

return 0;
}
```

# 第 19 章

`open_device` 调用简单地打开设备并将错误消息写入指定的日志 - 在这种情况下我们使用 `stderr` 流并返回已打开设备的句柄（或文件描述符），或者如果设备未成功打开则返回 `-1`。出于安全考虑，我们还包含了一个 `stat` 调用来检查文件名是否指向设备。`stat` 和相关常量定义在 `stat.h` 中：

```c
int open_device(FILE *errorlog, const char *device_name, int open_flags)
{    struct stat device_info;
    int audio_fd;
    if (stat(device_name,&device_info) == -1) /* 文件不存在 */
        fprintf(errorlog,
               "ERROR: device %s could not be opened: it does not exist.\n",
               device_name);
        return -1;
    if ((device_info.stat_mode & S_IFCHR) != S_IFCHR) /* 这是设备吗？ */
        fprintf(errorlog,
               "ERROR: filename %s is not a devicefile.\n",
               device_name);
        return -1;
    audio_fd = open(device_name, open_flags, 0);
    if (audio_fd == -1) // 打开设备失败
        int reason_for_failure = errno;
        fprintf(errorlog,
               "ERROR: device %s could not be opened with flags %d.\n",
               device_name, open_flags);
        return -1;
    fprintf(errorlog,
               "The reason given was: %s.\n",
               strerror(reason_for_failure));
    return audio_fd;
}
```

# Determining 声卡设备的能力

不同声卡的特性多种且多样。在某些设备（特别是旧设备）中，硬件层面存在根本性的限制；新的卡也可能受限于不成熟驱动。音频 API 提供了三个 `ioctl` 调用来帮助你确定声卡的能力，每个调用都接受一个整数指针作为参数。返回时，`ioctl` 将为此整数分配一个值，可以是根据支持的功能或格式设置的位掩码，也可以是一组组合在整数中的字节，甚至可能是两者的结合。

以下调用将返回设备所使用的 OSS API 版本，或者（在 ALSA 的情况下）兼容层试图模拟的 OSS 版本。注意，OSS API 在 3.6.1 版本之前不支持此调用。

```c
ioctl(device_fd, OSS_GETVERSION, &version)
```

接下来的代码段应插入到 `open_device` 函数之后，展示了此调用的用法：

## decode_version

```c
int decode_version(FILE *output, int version)
{
    int major_version = (version >> 16) & 0xff;
    int minor_version = (version >> 8) & 0xff;
    int revision = (version) & 0xff;

    fprintf(output,
        "The此设备驱动程序的 OSS 版本为 %d.%d.%d\n",
        major_version,minor_version,revision);

    return (major_version << 16) |
           (minor_version << 8) |
           revision);
}
```

## report_version

```c
int report_version(FILE *output, const char *device_name, int device_fd)
{
    int version = 0;

    if (ioctl(device_fd, OSS_GETVERSION, &version) == -1)
    {
        /* 设备不支持此调用 */
        int reason_why_GET_VERSION_failed = errno;

        fprintf(output,
            "设备 <%s> 报告了错误 %d (%s),\n",
            "等待其 OSS 驱动版本时。\n",
            device_name,
            reason_why_GET_VERSION_failed,
            strerror(reason_why_GET_VERSION_failed));
    }

    if (reason_why_GET_VERSION_failed == EINVAL) /* 可能是旧驱动程序*/
        return 0x03000000; /* 构造一个合理的最近版本号 */

    else /* 我们现在应该能够解码支持的版本： */
    {
        return decode_version(output, version);
    }
}
```

## 第 19 章

如你所见，版本号由一个主版本字节、一个次版本字节和一个修订字节组成，所有内容都封装在返回的整数中。

## 设备能力

```c
ioctl(device_fd, SNDCTL_DSP_GETCAPS, &capability_mask);
```

此调用返回设备的能力。目前定义了以下能力：

| 位掩码 | 含义 |
|---|---|
| `DSP_CAP_REVISION` | 驱动程序/卡的修订版本 - `capability_mask` 的部分实际上是一个数字，而不是位掩码。 |
| `DSP_CAP_DUPLEX` | 驱动程序/卡全双工 - 它可以同时录制和播放。 |
| `DSP_CAP_REALTIME` | 驱动程序/卡具备实时处理能力。 |
| `DSP_CAP_BATCH` | 驱动程序/卡支持批处理 - 它有多个内部缓冲区。 |
| `DSP_CAP_COPROC` | 驱动程序/卡有一个协处理器。 |
| `DSP_CAP_TRIGGER` | 驱动可以为应用程序提供触发。 |
| `DSP_CAP_MMAP` | 驱动可以使用 `mmap` 调用将内存空间映射到其缓冲区，从而加速操作。 |
