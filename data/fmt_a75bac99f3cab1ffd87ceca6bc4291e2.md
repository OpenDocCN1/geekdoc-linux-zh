
# MTNOP
无操作；作为副作用刷新驱动程序的缓冲区。应在通过 `IOCTL` 读取状态之前使用。

# MTTOFF
回带并使驱动器离线。

# MTRESET
回带。

# MTRETEN
回带。

# MTSEEK
寻道 `mt_count` 中指定的块号。此操作需要支持 `LOCATE` 命令（设备地址）的 SCSI-2 驱动器或兼容 Tandberg 的 SCSI-1 驱动器（Tandberg Archive Viper..）。块号应该是之前由 `MTIOCTOP` 返回的某一个，因为该数字是设备特定的。

# MTSETBLOCK
将驱动器块长度设置为 `mt_count` 中指定的值。长度为 0 则将驱动器设置为可变块大小。

# MTSETDENSITY
在代码 `mt_count` 中设置磁带密度。一些有用的密度代码：

| 代码 | 描述 |
| :--- | :--- |
| 0x08 | 隐式 |
| 0x11 | GIC-525 |
| 0x04 | GIC-11 |
| 0x12 | GIC-1350 |
| 0x05 | GIC-24 |
| 0x13 | D05 |
| 0x0F | GIC-120 |
| 0x14 | Exabye EXB-8200 |
| 0x10 | GIC-150 |
| 0x15 | Exabye EXB-8500 |

# MTEOF
写入 `mt_count` 个文件标记。

# MTWSM
写入 `mt_count` 个设置标记。

# MTSEDRNVBUFFER

根据 `nt_count` 中编码的位设置各种驱动器和驱动程序选项。这些包括驱动器的缓冲模式、布尔驱动选项以及写入阈值。这些参数仅在首次检测到设备时初始化。设置在设备关闭并重新打开时持续。单个操作可以影响缓冲模式、仅影响布尔选项，或仅影响写入阈值。

高 4 位为 0 的值将用于设置驱动器的缓冲模式。缓冲模式为：

- 0 除非实际写入介质，否则驱动器不会对写入命令报告 500 状态。
- 1 只要所有数据传输到驱动器的内部缓冲区，驱动器可能会对写入命令报告 500 状态。
- 2 只要所有数据传输到驱动器的内部缓冲区且来自不同初始化器的数据已成功写入介质，驱动器可能会对写入命令报告 500 状态。

要控制写入阈值，`nt_count` 必须包含 `ST_THRESHOLD` 以及低 28 位中的块大小。块计数指的是 1024 字节块，而不是磁带上的块大小。阈值不能超过驱动程序的缓冲区大小（见描述）。

要设置和清除缓冲区选项，`nt_count` 必须包含 `ST_BUFFER`，并将以下选项的组合进行设置。任何未指定的选项均为 false。

- 默认: false 缓冲所有写入操作。如果此选项为 false 且驱动器使用固定块大小，则所有写入必须是块大小的倍数。写入可靠的多卷归档时，必须设置此选项。
- 默认: true 当此选项为 true 时，写入操作立即返回，而不等待驱动器将数据传输到驱动程序的缓冲区。写入阈值决定缓冲区必须充满到什么程度才能发出新的 SCSI 命令。驱动器报告的任何错误将被保留。

- `MTSEDRNVBUFFER`
- `MT_ST_BUFFER`
- `MT_ST_ASYNC`
- `MT_ST_AHEAD`
- `MT_ST_TWO`
- `MT_ST_DEBUG`
- `MT_ST_FAST`
- `MT_ST_WR_PROT`
- `GMT__ONLINE`
- `GMT_DR_OPEN`
- `GMT_IM_REP_EN`

# 第四部分：特殊文件

`mt_fileno` 报告当前的文件编号（从 0 开始）。当文件编号未知（例如在执行 `MTBSD` 或 `MTSEEK` 之后），该值被设置为 -1。

`mt_blk` 报告当前文件内的块号（从 0 开始）。当块号未知（例如在执行 `MTBFS`、`MTBBSD` 或 `MTSEEK` 之后），该值被设置为 -1。

# MTIOCPOS: 获取磁带位置

此请求接受一个类型为 `(struct mt *)` 的参数，并报告驱动器认为的当前磁带块号，这并不是 `MTIGET` 报告的 `mt_blk`。该驱动器必须是支持 `READ POSITION` 命令（设备特定地址）的 SCSI-2 驱动器或连接了 Tandberg 的 SCSI-1 驱动器（Tandberg, Archive Viper, Wangtek...）。

```c
/* 用于 MTIOCPOS 的结构体 */
struct mt {
 long mt_blk; /* 当前块号 */
};
```

# 返回值

无法完成请求的操作。

- 无法完成写入操作，因为磁带已到达介质末尾。
- 尝试写入或擦除写保护的磁带。（这在 `open()` 期间不会检测）。
- 打开期间，设备不存在。
- 驱动器已在使用中或无法分配缓冲区。
- 尝试读取或写入大于驱动器内部缓冲器的变长度块。
- `ioctl()` 具有非法参数，或请求的块大小非法。
- 未知的 `ioctl()`。
- `EIO`
- `ENOSPC`
- `EACCES`
- `ENIO`
- `EBUSY`
- `EOVERFLOW`
- `EINVAL`
- `ENOSYS`

# 版权

Copyright 1995, Robert K. Nichols.

在所有副本上均保留版权声明和许可声明的情况下，允许制作并分发本手册的逐副本。额外的权限包含在源文件的头部。

## 参见

`mt(1)`

Linux 1.1.86, 1995年1月31日

# tty

`tty`—控制终端。

## 描述

文件 `/dev/tty` 是主号为 5、设备号为 0 的字符文件，通常模式为 0666，所有者/组为 root.tty。它是进程控制终端（如果有）的同义词。

除了 `tty` 所指设备支持的 `ioctl()` 请求外，还支持以下 `ioctl()` 请求：

# VCS, VCSa

# 1101

`TIOCNOTTY`

将当前进程从其控制终端分离，并将其从当前进程组中移除（即将其进程组 ID 设置为零）。此 `ioctl(1)` 调用仅对连接到 `/dev/tty` 的文件描述符有效；这通常用于守护进程在被用户从终端调用用时。进程尝试打开 `/dev/tty`；如果用户成功，它将使用 `TIOCNOTTY` 从终端检测到自己，但如果打开失败，显然它没有连接到终端，不需要将自分离。

# 文件

`/dev/tty`

## 参见

`mkod(1)`, `chown(1)`, `getty(1)`, `termios(2)`, `console(4)`, `tty(4)`

Linux, 1月21日

# ttys

`ttys`—串口终端线。

## 描述

`ttys[-3]` 是串口线路的字符设备。

它们通过以下方式创建：

```
mkod -m 668 /dev/ttys0 c 4 64 # 基地址 0x03f8
mkod -m 668 /dev/ttys1 c 4 65 # 基地址 0x02f8
mkod -m 668 /dev/ttys2 c 4 66 # 基地址 0x03e8
mkod -m 668 /dev/ttys3 c 4 67 # 基地址 0x02e8
chown root.tty /dev/ttys[-3]
```

# 文件

`/dev/ttys[-3]`

## 参见

`mkod(1)`, `chown(1)`, `getty(1)`, `tty(4)`

Linux, 12月19日

# VCS, VCSa

`vcs`, `vcsa`—虚拟控制内存。

## 描述

`/dev/vcs0` 是主号为 7、设备号为 0 的字符设备，通常模式为 0644，所有者为 root.tty。指向当前虚拟控制终端。

`/dev/vcs[1-63]` 是虚拟控制终端的字符设备；它们的主号为 7，设备号为 1 到 63，通常模式为 0644，所有者为 root.tty。...dev/vcsa[-63] 与它们相同，但包含四个字节的前缀，给出屏幕尺寸和光标位置：lines, columns, y（屏幕左角 y=0）。它们替换了 `console(4)` 的 screendump ioctl，因此系统管理员可以使用文件权限进行控制。前八个虚拟控制台设备可以通过以下方式创建：

```
for x in 0 1 2 3 4 5 6 7; do
  mknod -n 644 /dev/vcsx c 7
  /dev/vcsax c 7;
done
chown root.tty /dev/vcs*
```

支持 `ioctl(1)` 请求。

# 示例

你可以通过切换到 v3 并输入 `/dev/vcs3 >foo` 在 v3 上执行 screendump。此程序显示第二个虚拟控制台光标下的字符和屏幕属性，并更改背景颜色：
