
## 3.4.5 串口端口：`/dev/ttyS*`

旧的 RS-232 类型和类似的串口是特殊终端设备。你无法在命令行对串口设备做很多，因为有很多设置需要考虑，例如波特率和流控。

名为 `/dev/ttyS0` 的端口，COM2 为 `/dev/ttyS1`，依此类推。USB 串口适配器以 USB 和 ACM 命名为 `/dev/ttyUSB0`、`/dev/ttyACM0`、`/dev/ttyUSB1`、`/dev/ttyACM1` 等。

## 3.4.6 并口端口：`/dev/lp0` 和 `/dev/lp1`

代表一种大部分被 USB 取代的接口，单向并行口设备 `/dev/lp0` 和 `/dev/lp1` 对应 Windows 中的 LPT1 和 LPT2。你可以使用 `cat` 命令将文件（例如要打印的文件）直接发送到并行端口，但之后可能需要给打印机一个额外的格式。这样的服务器能更好地处理与打印机的交互。双向并行端口为 `/dev/parport0` 和 `/dev/parport1`。

## 3.4.7 音频设备：`/dev/snd/*`、dev/dsp、dev/audio 等

Linux 有两套音频设备。高级 Linux 架构 `ALSA` 系统和开放声音系统 `OSS` 有各自独立的设备。`ALSA` 设备位于 `/dev/snd/`，而 `OSS` 设备为 `/dev/dsp` 和 `/dev/audio`。

`ALSA` 系统是现代标准，而 `OSS` 是遗留。大多数 Linux 发行版使用 `ALSA`。但某些应用程序仍然需要 `OSS`，可以通过兼容层提供。

## 3.4.8 创建设备文件

在现代 Linux 中，`udev` 处理设备节点的创建。`udev` 监听内核事件并在 `/dev` 中创建或删除相应的设备节点。这取代了手动使用 `mknod` 手动创建节点的需要。关于 `udev` 的更多信息，请参阅第 3.5 节。

你不需要了解这些内容也可以继续阅读这本书。事实上，如果这是你第一次查看 Linux 设备，建议跳到下一章开始学习如何使用磁盘。

## 3.5.2 udev 操作与配置

`udev` 守护进程的工作机制如下：

- 内核通过内部网络链路向 `udev` 发送名为 `uevent`（内核事件）的通知。
- `udev` 载入 `uevent` 中的所有属性。
- `udev` 解析其规则，并根据这些规则采取操作或设置更多属性。

你可以看到这里设备发生了变化。在接收到 `uevent` 后，`udev` 知道了 `sysfs` 设备路径以及与这些属性相关的其他属性，现在它已准备好开始处理。

规则位于 `/lib/udev/rules.d` 和 `/etc/udev/rules.d` 目录。`/lib` 中的规则是默认的，而 `/etc` 中的规则会覆盖它们。对规则进行完整的解释会非常冗燥，但让我们看看第 3.5.1 节中 `/dev/sda` 示例的符号链接。这些链接是由 `/lib/udev/rules-storage.rules` 中的规则定义的。在文件中你会看到以下几行：

这些规则匹配由内核 SCSI 子系统提供的 `udev` 磁盘（第 3.6 节）。你可以看到有几个规则用于捕捉设备可能的不同表示方式，但核心思想是 `udev` 将尝试匹配带有 `sd` 或 `sr` 但没有数字的设备（使用 `KERNEL="sd[0-9]|sr*"`），以及子系统（`SUBSYSTEM="scsi"`），最后是其他属性。如果所有这些表达式为真，`udev` 将执行下一个表达式：

`IMPORT(program)=@ata_id --export $tempnode`

这不是一个条件判断，而是一个从 `/lib/udev/ata_id` 命令导入变量的指令。如果你有一个磁盘，尝试在命令行中试一下：

```
$ sudo /lib/udev/ata_id --export /dev/sda
ID_ATA=1
ID_TYPE=bus
ID_BUS=ata
MODEL=WDC_WD3200AASJS-22L7AO
MODEL_ENC=WDC_WD3200AASJS-22L7AO\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20
ID_REVISION=01.3E10
ID_SERIAL=WDC_WD3200AASJS-22L7AO_WD-WAV2FU80671
--snip--
```

导入设置了环境，使得输出中的所有变量名都被设置为显示的值。例如，随后的任何规则都会识别 `ENV(ID_TYPE)`。

特别需要注意的是 `ID_SERIAL`。在每条规则中，这个条件都出现在第二个：

```
ENV{ID_SERIAL}!="*"
```

这意味着只有在 `ID_SERIAL` 未设置时它才为真。因此，如果它为假，则当前规则无效，`udev` 将移动到下一条规则。

那么意义何？这两个规则（以及文件中周围的规则）的目的是找到磁盘设备的序列号。通过 `ENV(ID_SERIAL)`，`udev` 可以评估以下内容：

你可以看到这条规则要求 `ENV(ID_BUS)` 必须设置，并且它有一条指令：

当遇到此指令时，`udev` 会为接入的设备创建一个符号链接。现在你知道符号链接是从哪里来的了！

你可能想知道如何区分条件表达式和指令。条件用两个等号（`==`）或非等号（`!=`）表示，而指令用单个等号（`=`）、加等号（`+=`）或冒号等号（`:`）表示。

## 3.5.3 udev

`udev` 程序是 `udev` 的管理工具。你可以重载 `udev` 规则并触发事件，但 `udevadm` 最强大的功能是搜索和探索系统，以及在 `udev` 从内核接收 `uevent` 时对其进行监控。唯一的技巧之处在于命令语法变得有点复杂。

让我们从检查一个系统设备开始。回到第 3.5.2 节的示例，为了查看与 `/dev/sda` 等设备的规则一起生成的所有 `udev` 属性，请运行以下命令：

```
$ udev info --query=all --name=/dev/sda
```

输出如下：

- P: /devices/pci0000:00:00:01.2/host/target:0:0:0:0:0:0:0/block
N: sda
S: disk/by/id-ata-WDC_WD30200AAJ5-22L7AO_WD-MAV2FU80671
S: disk/by/id-scsi-SATA_WDC_WD3020AAJ5-_WD_MAV2FU80671
S: disk/by/id/wn-050014ee057faef84
S: disk/path-pci-0000:00:01.2f-scsi-0:0:0
E: DEVLINKS=/dev/disk/by/id-ata-WDC_WD3020AAJ5-22L7AO_WD-MAV2FU80671 /dev/disk/by-id-scsi-SATA_WDC_WD3020AAJ5-_WD_MAV2FU80671 /dev/disk/by/id/wn-050014ee057faef84/path/pci-0000:00:01.2f-scsi-0:0:0
E: DEVNAME=dev/sda
E: DEVPATH=/devices/pci0000:00:01.2/host/target:0:0:0:0:0:0/block
E: TYPE=disk
E: ID=ATA
E: ID_DOWNLOADCODE=1
E: ID_FEATURE_SET=AAM
--snip

每个前缀表示一个属性或特性。`P:` 是 `sysfs` 设备路径，`N:` 是赋予 `/dev` 的名称，`S:` 是根据规则放置在 `/dev` 中的符号链接，`E:` 是来自 `udev` 的设备信息（输出比需要的多得多；你可以自己运行命令感受一下）。

## 3.5.4 监控设备

使用 `udevadm` 监控事件：

```
$ udevadm monitor
```

输出（例如当你插入闪存媒体时）如下简化示例：

```
KERNEL[65829.569485] add /devices/pci0000:0000:1d.0/usb2-1/2.2-1.0 (usb)
KERNEL[65829.569667] add /devices/pci0000:0000:1d.0/usb2-1/2.2-1.0 (usb)
KERNEL[65829.570614] add /devices/pci0000:0000:1d.0/usb2-1/2.2-1.0/host15(scsi)
KERNEL[65829.570645] add /devices/pci0000:0000:1d.0/usb2-1/2.2-1.0:host15/scsi_host/scsi
UDEV[65829.622579] add /devices/pci0000:0000:1d.0/usb2-1/2.2-1.0 (usb)
UDEV[65829.623014] add /devices/pci0000:0000:1d.0/usb2-1/2.2-1.0 (usb)
```
