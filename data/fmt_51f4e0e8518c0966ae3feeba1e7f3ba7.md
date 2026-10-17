
以下代码显示了如何在标准设备上报告能力。注意为了清晰起见，我们将报告代码与错误检查代码分开。此外，注意我们在修订部分做了一些处理，假装它是一个位掩码并仅在它有值时打印。

## sound_capability

```c
typedef struct {
    int scBitmask; /* 对应此能力的位掩码 */
    const char *scName; /* 此能力的可读表示形式 */
    struct capability;
};
```

- `list_capabilities(FILE output, int capability_mask)`

```c
static const sound_capability capability_list[] = {
    (DSP_CAP_REVISION, "revision"),
    (DSP_CAP_DUPLEX, "full duplex"),
    (DSP_CAP_REALTIME, "real-time processing"),
    (DSP_CAP_BATCH, "batching"),
    (DSP_CAP_COPROC, "co-processing"),
    (DSP_CAP_TRIGGER, "trigger"),
    (DSP_CAP_MMAP, "mmap()"),
};
```

```c
int i;

for (i = 0; capability_list[i].scBitmask != 0; ++i)
{
    if (capability_mask & capability_list[i].scBitmask)
    {
        printf(output,
               "设备具有 %s 能力 (%x -> %x)\n",
               capability_list[i].scName,
               capability_list[i].scBitmask,
               capability_mask & capability_list[i].scBitmask);
    }
}
```

## report_capacabilities

```c
int report_capacabilities(FILE *output, const char *device_name, int device_fd)
{
    int capability_mask = 0;

    if (ioctl(device_fd, SNDCTL_DSP_GETCAPACS, &capability_mask) == -1)
    {
        /* 设备不支持此调用 */
        int reason_why_GET_CAPACS_failed = errno;

        printf(output,
               "设备 <%s> 报告了错误 %d (%s)\n",
               "等待其能力报告时。\n",
               device_name,
               reason_why_GET_CAPACS_failed,
               strerror(reason_why_GET_CAPACS_failed));

        return 0;
    }
    else /* 我们现在应该能够列支持的能力： */
    {
        printf(output,
               "设备 <%s> 报告以下能力：(%d %x)\n",
               device_name,
               capability_mask,
               capability_mask);

        list_capabilities(output, capability_mask);
    }

    return 0;
}
```

## 支持的格式

最后，我们可以使用以下调用来获取支持的格式：

```c
ioctl(device_fd, SNDCTL_DSP_GETFS, &format_mask)
```

对应的位掩码如下：

| 位掩码 | 格式 |
|---|--- |
| AFMT_MU_LAW | mu-law |
| AFMT_A_LAW | a-law |
| AFMT_IMA_ADPCM | IMA ADPCM |
| AFMT_U8 | 8 bit |
| AFMT_S16_LE | signed 16 bit |
| AFMT_S16_BE | signed 16 bit |
| AFMT_MPEG | MPEG audio |

驱动程序可能支持比这里列出的更多的格式。然而，这里可以使用更高效的方式列出支持的格式。以下代码将列出支持的格式，与上面报告能力的方式类似：

## list_formats

```c
void list_formats(FILE output, int mask) {
    static const sound_capability capability_list[] = {
        (DSP_CAP_REVISION, "revision"),
        (DSP_CAP_DUPLEX, "full duplex"),
        (DSP_CAP_REALTIME, "real-time processing"),
        (DSP_CAP_BATCH, "batching"),
        (DSP_CAP_COPROC, "co-processing"),
        (DSP_CAP_TRIGGER, "trigger"),
        (DSP_CAP_MMAP, "mmap()"),
    };

    int i;
    for (i = 0; capability_list[i].scBitmask != 0; ++i)
    {
        if (mask & capability_list[i].scBitmask)
        {
            printf(output,
                 "设备支持 %s。\n",
                 capability_list[i].scName);
        }
    }
}
```

## Multimedia and Linux

我们将通过向我们的 `main` 函数添加适当的调用，来看如何使用描述的函数。首先，我们需要一些额外的变量，用于存储每次调用的结果：

```c
int main(int argc, char *argv[]) /* 标准命令行参数 */
{
    const char *device = "/dev/dsp/"; /* 标准音频设备名称。 */

    int device_fd = -1; /* 我们还没有打开任何东西 */
    int version = 0; /* OSS 驱动程序的版本 */
    int capability_mask = 0; /* 设备的能力。 */
    int format_mask = 0; /* 设备可以播放的格式 */
}
```

## 第 19 章

接下来，我们添加对上面定义的各种函数的调用：

```c
device_fd = open_device(stderr, device, O_WRONLY);
```

```c
if (device_fd == -1)
    /* 如果为真，则 open 调用失败并已给出一个错误。 */
        exit(EXIT_FAILURE);
```

我们已经成功打开了设备。现在报告它能做什么：

```c
version = report_version(stdout, device, device_fd);
capability_mask = report_capabilities(stdout, device, device_fd);
format_mask = report_formats(stdout, device, device_fd);
```
