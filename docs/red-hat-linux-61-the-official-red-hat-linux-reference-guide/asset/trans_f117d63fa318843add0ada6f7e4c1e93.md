

# 第 5 章 proc 文件系统

- btime — 启动时间，以自 1970 年 1 月 1 日起的秒数计算，也称为*纪元*（epoch）。

## 5.2.28. /proc/swaps

此文件测量交换空间及其利用率。对于仅有一个交换分区的系统，`/proc/swap` 的输出可能如下：

```
| Filename | Type | Size | Used | Priority |
| /dev/hda6 | partition | 136512 | 20024 | -1 |
```

虽然这些信息的一部分可以在 `/proc/` 目录下的文件中找到，但 `/proc/swap` 提供了每个交换文件的快照、交换空间的类型、总大小以及该空间的使用量（单位为 KB）。当使用多个交换文件时，优先级（Priority）列非常有用。优先级越低，交换文件越可能被使用。

## 5.2.29. /proc/uptime

此文件包含有关系统自上次重启以来运行多时间的详细信息。`/proc/uptime` 的输出非常简单：

```
350735.47 234388.90
```

第一个数字是系统运行的总秒数。第二个数字是机器空闲的时间（单位为秒）。

## 5.2.30. /proc/version

此文件指定了正在使用的 Linux 内核版本和 `gcc` 版本，以及系统中安装的 Red Hat 版本：

```
Linux version 2.4.20-0.40 (user@foo.redhat.com) (gcc version 3.2.1 20021125
(Red Hat Linux 8.0 3.2.1-1)) #1 Tue Dec 3 20:50:18 EST 2002
```

此信息用于多种用途，包括用户登录时显示的版本数据。

## 5.3. /proc/ 中的目录

关于内核的常见信息组被分组在 `/proc/` 目录下的子目录下。

### 5.3.1. 进程目录

每个 `/proc/` 包含若干以数字命名的目录。列表可能如下所示：

```
dr-xr-xr-x 3 root root      0 Feb 13 01:28 1
dr-xr-xr-x 3 root root      0 Feb 13 01:28 1010
dr-xr-xr-x 3 xfs xfs        0 Feb 13 01:28 1087
dr-xr-xr-x 3 daemon daemon  0 Feb 13 01:28 1123
dr-xr-xr-x 3 root root      0 Feb 13 01:28 11307
dr-xr-xr-x 3 apache apache 0 Feb 13 01:28 13660
dr-xr-xr-x 3 rpc rpc 0 Feb 13 01:28 637
dr-xr-xr-x 3 rpcuser rpcuser 0 Feb 13 01:28 666
```

这些目录被称为进程目录，因为它们以程序的进程 ID（PID）命名，并包含该进程的特定信息。每个进程目录的所有者和组都设置为运行进程的用户。当进程终止时，其 `/proc` 进程目录就会消失。每个进程目录包含以下内容：

- cmdline 启动进程时发布的命令。
- cpu 提供有关系统每个 CPU 利用率的特定信息。在双 CPU 系统上运行的进程输出类似于：
```
cpu 11 3
cpu0 0
cpu1 11 3
```
- cwd 指向进程当前工作目录的符号链接。
- environ 列出进程的环境变量列表。环境变量名为大写字母，值为小写字母。
- exe 指向此进程可执行文件的符号链接。
- fd 包含进程所有文件描述符的目录。总数为：
```
lrwx------ 1 root root 64 May 08:31:00 -> /dev/null
lrwx------ 1 root root 64 May 08:31:01 -> /dev/null
lrwx------ 1 root root 64 May 08:31:02 -> /dev/null
lrwx------ 1 root root 64 May 08:31:03 -> /dev/ptmtx
lrwx------ 1 root root 64 May 08:31:04 -> socket:[7774817]
lrwx------ 1 root root 64 May 08:31:05 -> socket:[7774829]
lrwx------ 1 root root 64 May 08:31:07 -> /dev/ptmtx
```
- maps 包含与此进程相关的各种变量和库文件的映射。此文件可能更长，取决于进程的复杂性，sshd 进程的示例输出为：
```
04800480-08600880 r-x 00000000 03 03 394179 /usr/bin/sshd
08600880-08800880 rw-p 0003e00 03 03 394179 /usr/bin/sshd
08800880-08905000 rw-p 00000000 00 00 000000
40000000-40010000 r-x 00000000 03 03 239205 /lib/ld-2.2.so
40010000-40030000 rw-p 0001300 03 03 239205 /lib/ld-2.2.so
40030000-40038000 rw-p 0023282 03 03 239282 /lib/libpam.so
40038000-4003a000 rw-p 00000000 00 00 000000 /lib/libpam.so
4003a000-4003c000 r-x 00000000 03 03 239218 /lib/ld-2.2.so
4003c000-4003d000 rw-p 00010100 03 03 239218 /lib/ld-2.2.so
```
- mem 进程占用的内存。
- root 指向进程的根目录。
- stat 进程的状态。
- statm 此进程的内存状态。下面是 `/proc/stat` 示例：`263 210 5`。这七列与进程的内存统计有关。从左到右报告内存的以下方面：
1. 程序总大小，单位为 KB
2. 内存部分大小，单位为 KB
3. 共享内存页数
4. 代码页数
5. 数据/栈页数
6. 库页数
7. 脏页数
- status 比 stat 或 statm 更易读的形式显示进程状态。sshd 的示例输出类似于：
```
Name: sshd
State: S (sleeping)
Tgid: 797
Pid: 797
PPid: 1
Uid: 0 0 0
Gid: 0 0
FD: 32
Groups:
VmSize: 3072 kB
VmL: 0 kB
VmRSS: 840 kB
VmData: 104 kB
VmStk: 12 kB
VmExec: 300 kB
VmLib: 2529 kB
Vmnd: 0000000000000
VmBlk: 0000000000000
VmIgn: 0000000000001
VmCgt: 0000000000005
CapIn: 0000000000000
CapPrm: 0000000000000
CapEff: 0000000000000
```
此输出信息包含了进程名称和 ID、状态（如 S (sleeping) 或 R (running)）、组 ID 以及关于内存使用的详细数据。

## 5.3.1. /proc/self

`/proc/self/` 目录是指向当前运行进程的链接。这允许进程在不知道自己 ID 的情况下查看自己。在 shell 环境中，列出 `/proc/self/` 生成该目录的内容。

## 5.3.2. /proc/bus/

此目录包含系统中可用总线的特定信息。例如，在包含 ISA、PCI 和 USB 的标准系统中，这些总线的当前数据可以在 `/proc/bus/` 下的目录可用。子目录和文件的内容取决于系统的精确配置。然而，每种总线类型的目录至少有一个总线的目录。这些单独的总线目录用数字标记（如 00），包含指向总线上可用各种设备的二进制文件。例如，一个拥有 USB 总线但未连接 USB 设备的系统具有 `/proc/bus/usb/` 目录，其中包含几个文件：
```
total 0
dr-xr-xr-x 1 root root      0 May 3 16:25 001
--r--r--r-- 1 root root      0 May 3 16:25 devices
--r--r--r-- 1 root root      0 May 3 16:25 drivers
```

`/proc/bus/usb/` 目录跟踪任何 USB 总线上的各种设备以及使用它们所需的驱动程序。`/proc/bus/usb/001/` 目录包含第一个总线上的所有设备。通过查看 `devices` 文件的内容，可以识别主板上的 USB 根节点：

```
T: Bus=01 Lev=00 Rt=00 Cnt=00 DevB=1 Spd=12 MxCh=2
B: Alloc=0/900 us ( ) Int=0 Iso=0
D: Vendor=1.0 Cl=09(hub ) Sub=00 Prot=0 MxFS=8 Cfg=1
P: Vendor=0000 PID=0000 Rev=0
Product=USB Hub
SerialNumber=d400
C*: Ifs=1 Cfg=1 At=40 MxPwr=0Ma
I: Ifs=0 Alt=0 Efs=1 Cl=09(hub ) Sub=00 Prot=00 Driver=hub
E: Ad=81 (1) At=03 (Int.) MxFS=8 Ivl=255
```

## 5.3.3. /driver/

此目录包含内核中特定驱动程序的信息。此处的一个常见文件是 rtc，它提供系统实时时钟（RTC）驱动程序的输出，RTC 是系统关机时保持时间的设备。/proc/driver/rtc 的示例输出如下：
```
rtc_time : 01:38:43
rtc_date : 1998-02-13
rtc_epoch : 1900
alarm : 00:00:00
DST_enable : no
BCD : yes
24hr : no
square_wave : no
alarm_IRQ : no
update_IRQ : no
periodic_IRQ : no
periodic_freq : 1024
batt_status : okay
```

更多关于 RTC 的信息，请参考 /user/src/linux-2.4/Documentation/rtc.txt。

