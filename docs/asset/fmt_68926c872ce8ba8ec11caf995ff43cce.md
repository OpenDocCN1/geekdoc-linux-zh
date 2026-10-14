
```
CONSOLE=/dev/console ROOTS_FTYPE=ext3 TERM-linux SHELL=/bin/sh

ROOTS_FSK=0 crashkernel-128M-64M816M LC_ALL=POSIX

INIT_VERSION=sysinit-2.86 REDIRECT=/dev/tty COLUMNS=96 PATH=/bin:/usr/bin:/usr:/usr/sbin DO_CONFIRM= vga=0x0332 RUNLEVEL=5 SPLASHCFG=

Starting syslog servicesdone
```

在创建基准和排排除故障时，`/var/log/boot.msg` 的内容非常有用。

你可以通过启动 YaST 并选择 *Miscellaneous > Startup Log*（杂 > 启动日志）来查看文件内容。你也可以直接在终端中输入 `yast view_msg` 来启动该模块。无论哪种情况，`/var/log/boot.msg` 的内容所示：图 5-17 使用 YaST 查看 /var/log/boot.msg

```
System Log

ROOTOFS-FPYPE=shard SHELL=/bin/bash TERM=linux-root ROOTOFS FSK=0 LC_ALL=POSIX POSIX TERM_VERSION=system 2.86 REDIRECT=/dev/tty COLUMNS=96 PATH=/bin:/usr/sbin:/bin/sbin/bin/usr/bin/usr/:00000032IRMCONF======VRUN=4=0 SPLASH-INYES=splash--LINES=13 HOME=/root

SPLASH-INYES-splash-silent ROOTOFS-BLKDEV=dev/sda1/disk-by-id/Virtual_IDE_Hard_Drive_000000000000000000000000000

_root=/root

_startproc

Starting service (smartd)

console_output=/var/log/messages [/bin/syslog CONSOLE=/dev/console ROOTOFS-FPYPE=shard SHELL=/bin/bash TERM=linux-root ROOTOFS FSK=0 LC_ALL_POSIX POSIX TERM_VERSION=system 2.86 REDIRECT=/dev/tty COLUMNS=96 PATH=/bin:/usr/sbin:/bin/sbin/bin/usr/usr/bin/sbin:uuid=00032 DO_CONFIRM=YES RUNLEVEL=5

PREV_RUNLEVEL=4-MODE=0 SPLASH-INYES=splash-silent LINES=13 HOME=/root

SPLASH-INYES=splash-silent ROOTOFS-BLKDEV=dev/sda1/disk-by-id/Virtual_IDE_Hard_Drive_000000000000000000000000000

_root=/root

_startproc

Daemons

Starting daemond

console_output=/var/log/messages [/bin/syslog] CONSOLE=/dev/console ROOTOFS-FPYPE=shard SHELL=/bin/bash TERM=linux-root ROOTOFS FSK=0 LC_ALL=POSIX POSIX TERM_VERSION=system 2.86 REDIRECT=/dev/tty COLUMNS=96 PATH=/bin:/usr/sbin:/bin/sbin/bin/usr/usr/bin/sbin:uuid=00032 DO_CONFIRM=YES RUNLEVEL=5

PREV_RUNLEVEL=4-MODE=0 SPLASH-INYES=splash-silent LINES=13 HOME=/root

SPLASH-INYES=splash-silent ROOTOFS-BLKDEV=dev/sda1/disk-by-id/Virtual_IDE_Hard_Drive_000000000000000000000000000

_root=/root

_startproc

Resource Control service has been restarted

Skipped services in runlevel 5: smartd its load_balancer
```

注意：你可以使用屏幕上的下拉列表查看系统日志文件。

## 在 /proc/ 中查看硬件信息

`/proc/` 目录包含存储在运行内存中的所有硬件信息。`/proc/` 目录及其所有子目录并不是“真实”的文件。它们是在你访问时动态生成的。

然而，你可以使用 `cat` 等标准 Linux 工具查看 `/proc/` 中文件的内容。

例如，如果你输入 `/proc/cpuinfo`，将根据内核内存中的数据生成显示 CPU 名称和缓存大小等信息。下例所示：

```
dal:~ # cat /proc/cpuinfo

processor : 0

vendor_id : GenuineIntel

cpu family : 15

model : 4

model name : Intel(R) Pentium(R) 4 CPU 3.20GHz

stepping : 8

cpu MHz : 3200.116

cache size : 1024 KB

fdiv_bug : no

hlt_bug : no

f00_bug : no

coma_bug : no

fpu : yes

fpu_exception : yes

cpuid_level : 5

wp : yes

flags : fpu vme de pse tsc msr pae mce cx8 apic mtrr pge

ca cmov pat pse36 clflush dts acpl mmx fxr sse sse2 ss nx

constant_tac up pebs bts pni ds_cpl

bogomips : 6400.23

clflush size : 64

power management:
```

`/proc/` 中的一些常用文件包括：

- `/proc/devices`：显示安装在 Linux 系统中的设备信息。
- `/proc/cpuinfo`：显示处理器信息。
- `/proc/ioports`：显示 I/O 端口信息。
- `/proc/interrupts`：显示 IRQ 分配信息。
- `/proc/dma`：显示直接内存访问（DMA）通道信息。
- `/proc/bus/pci/devices`：显示外围部件接口（PCI）设备信息。
- `/proc/scsi`：显示 SCSI 设备信息。
- `/proc/partitions`：显示磁盘分区信息。
- `/proc/sys`：包含一系列子目录和文件。这些目录列如下：
    - `debug`：包含调试信息。
    - `dev`：包含特定设备的信息。
    - `fs`：包含文件系统信息。
    - `kernel`：包含内核信息。
    - `net`：包含网络相关信息。
    - `vm`：包含虚拟内存子系统的信息。

`sysctl.conf` 文件。`sysctl` 命令在启动期间被调用，并设置配置中定义的所有参数。如果未定义参数，则会设置默认值。

`sysctl` 命令可以设置 `/proc/sys/` 目录下的参数，因此所有文件都通过相对于该目录的路径进行访问。要查看当前设置的值，请使用 `-a` 选项：

```
$ # sysctl -a

...

vm.swappiness = 75

...
```

要设置参数的值，使用 `-w` 选项：

```
$ # sysctl -w vm.swappiness=80
```

要通过配置文件 `/etc/sysctl.conf` 设置这些值，可以使用与使用 `sysctl -w` 相同的语法：

```bash
# /etc/sysctl.conf

...

vm.swappiness=75
```

你现在可以通过 `sysctl -p` 手动设置这些值（如果没有提供文件名，则使用 `/etc/sysctl.conf`）。在下次重启期间，这些值将会被自动设置。

# 使用命令行实用程序收集硬件信息

除了查看 `/proc/` 中文件的内容外，你还可以使用以下实用程序来收集 Linux 系统中的硬件信息：

- `hwinfo`。显示有关系统中安装的设备的特定信息。下面是 `hwinfo` 关于 SLES 系统中安装网卡的示例输出：

```
dal:~ # hwinfo

45: None 01.0: 10701 Ethernet

[Created at net.124]
