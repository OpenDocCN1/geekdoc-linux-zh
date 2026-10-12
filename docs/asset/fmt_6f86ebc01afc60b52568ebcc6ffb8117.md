
| `'m'` | 将当前内存信息转储到控制台。 |
| `'v'` | 将 Voyager™ SMP 处理器信息转储到控制台。 |
| `'e'` | 向除 init 外的所有进程发送 SIGTERM。 |
| `'i'` | 向除 init 外的所有进程发送 SIGKILL。 |
| `'I'` | 向包括 init 在内的所有进程发送 SIGKILL。 |
| `'0-8'` | 设置控制台日志级别，控制哪些内核消息将打印到控制台。（例如，设置 `'0'` 将使只有紧急消息（如 PANIC 或 OOPS）才能到达控制台。） |

### 表 3-5 Sysrq 日志级别

| 级别 | 说明 |
|---|---|
| 0 | KERN_EMERG<br>系统无法使用 |
| 1 | KERN_ALERT<br>需要立即采取行动 |
| 2 | KERN_CRIT<br>危急情况 |
| 3 | KERN_ERR<br>错误情况 |
| 4 | KERN_WARNING<br>警告情况 |
| 5 | KERN_NOTICE<br>正常情况 |
| 6 | KERN_INFO<br>通知 |
| 7 | KERN_DEBUG<br>调试 |

**注意：** 有报告指出，使用 SysRq 按键会导致内核恐慌（`kernel panic`）的一些问题。内核已修复这些问题，并且它们在以下版本中不再出现：

- SLES9: `2.6.5-7.252` 及更高版本
- RHEL4: `2.6.9-35` 及更高版本

使用 SysRq 生成的堆栈跟踪有助于分析系统中的异常行为，例如当多个用户空间程序停止响应且键盘输入仍然可用时。通常，SysRq 跟踪会与其他独立转储和核心转储一起使用。

![](img/f332344337ca8bf6846cb313a66ee0b3_119_0.png)

图 3-13 Sysrq 报告示例

#### 3.3.5 s390dbf

`s390dbf` 调试功能可以跟踪内核组件（如设备驱动程序）。它生成跟踪日志，当特定组件显示错误时，这些日志可能很有用。然而，并非所有组件都会生成日志。组件必须注册该功能才能生成跟踪数据。

`/proc` 目录保存了来自 `s390dbf` 工具的调试日志。在路径 `/proc/s390dbf` 下，每个注册的组件都有一个目录。目录条目的名称对应于组件注册时的名称。事件（和异常）调用有三个版本：一个用于记录原始数据，一个用于文本，一个用于数字。每个调试条目包含以下数据：

- 时间戳
- 调用任务的 CPU 编号
- 调试条目级别 (`0..6`)
- 调用者的返回地址

根据要调查的区域选择文件，并选择 `/proc` 目录下的文件：

- `/proc/s390dbf/cio_*` : 通用 I/O
- `/proc/s390dbf/qdio_*` : qdio
- `/proc/s390dbf/qeth_*` : qeth
- `/proc/s390dbf/zfcp_*` : zfcp
- `/proc/s390dbf/dasd_` : DASD
- `/proc/s390dbf/0.0.xxxx` : 每个 DASD 设备

所有调试日志都有一个实际的调试级别（范围从 0 到 6）。默认级别为 3。事件和异常函数具有级别参数。通过向为每个调试日志提供的 `'level'` debugfs 文件写入数字字符串 `"x"`，可以利用 debugfs 文件系统更改实际调试级别。

##### 示例 3-46 s390dbf 日志级别

```
1nx02:/ # cat /proc/s390dbf/qeth_trace/level
2
```

现在，根据所需的跟踪级别，设置日志值，如示例 3-47 所示。

##### 示例 3-47 设置日志级别

```
1nx02:/ # echo 6 > /proc/s390dbf/qeth_trace/level
1nx02:/ # cat /proc/s390dbf/qeth_trace/level
6
```

一旦达到适当的跟踪级别，重现问题以保存 `s390dbf` 跟踪输出。

##### 示例 3-48 将 s390dbf 跟踪保存到文件

```
cat /proc/s390dbf/qeth_trace/hex_ascii > output_file
```

一旦保存了来自 `s390dbf` 设施的跟踪信息，请恢复旧的跟踪级别（示例 3-49）。

##### 示例 3-49 将跟踪级别重置为默认值

```
1nx02:/ # echo 2 > /proc/s390dbf/qeth_trace/level
```

![](img/f332344337ca8bf6846cb313a66ee0b3_121_0.png)

图 3-14 重置

`s390dbf` 对于与硬件设备相关的问题确定很有用，它还可以跟踪设备驱动程序与硬件设备之间的通信。通过 `s390dbf` 跟踪，我们可以确认设备之间存在通信（例如，发往 DASD 设备的 I/O 请求及其返回的状态）。

#### 3.3.6 zFCP/SCSI

zFCP 跟踪功能启用对 `zfcp` 设备驱动程序和光纤通道协议流的调试。在进行任何调试时，zFCP 跟踪应与 SCSI 跟踪一起使用。

可以根据问题目标区域选择以下跟踪信息：

- `loglevel_erp`
- `loglevel_fsf`
- `loglevel_fc`
- `loglevel_qdio`
- `loglevel_cio`
- `loglevel_scsi`
- `loglevel_other`

在示例 3-50 中，我们将启用 zFCP 驱动程序，并将 `loglevel_erp` 的日志级别设置为 1。

##### 示例 3-50 启用 zfcp

```
echo 1 > /sys/bus/ccw/drivers/zfcp/loglevel_erp
```

zFCP 跟踪的日志级别有四个不同的级别，从 0 到 3。数值越大，获取的信息越详细。所有区域的日志级别默认设置为 0，仅输出最少信息。通过设置 `zfcp` 的日志级别，调试消息将写入 `/var/log/messages`。要停止 zFCP 跟踪，请参阅示例 3-51。

##### 示例 3-51 禁用 zfcp

```
echo 0 > /sys/bus/ccw/drivers/zfcp/loglevel_erp
```

示例 3-52 显示了 zFCP 驱动程序的输出。

##### 示例 3-52 loglevel_erp 的 zFCP 跟踪

```
Mar 5 10:56:36 linuxx kernel: zfcp: zfcp_fsf_req_send(4926): calling do_QDIO adapter 0.0.f441, flags=0x2, queue_no=0, index_in_queue=42, count=1, buffers=000000000d5a2260
Mar 5 10:56:36 linuxx kernel: zfcp: zfcp_fsf_req_send(4933): free_count=127
Mar 5 10:56:36 linuxx kernel: zfcp: zfcp_fsf_send_fcp_command_task(3757): Send FCP Command initiated (adapter 0.0.f441, port 0x5005076300cf9b9e, unit 0x5501000000000000
Mar 5 10:56:36 linuxx kernel: zfcp: zfcp_qdio_request_handler(310): adapter 0.0.f441, first=42, elements_processed=1
Mar 5 10:56:36 linuxx kernel: zfcp: zfcp_qdio_zero_sbals(866): zeroing BUFFER 42 at address 000000000d59fa00
Mar 5 10:56:36 linuxx kernel: zfcp: zfcp_qdio_request_handler(326): free_count=128
Mar 5 10:56:36 linuxx kernel: zfcp: zfcp_qdio_request_handler(329): elements_processed=1, free count=128
Mar 5 10:56:36 linuxx kernel: zfcp: zfcp_qdio_response_handler(376): first BUFFERE flags=0x40000000
```

##### SCSI 跟踪

使用 SCSI 跟踪，我们可以获得有关 SCSI 层的重要调试信息。如前所述，将其与 zFCP 跟踪一起使用是有效的。示例 3-53 显示了用于设置 SCSI 跟踪日志级别的命令。

###### 示例 3-53 SCSI 日志级别设置

```
echo 0x9249249 > /proc/sys/dev/scsi/logging_level
```

示例 3-54 显示了一个 SCSI 跟踪示例。
