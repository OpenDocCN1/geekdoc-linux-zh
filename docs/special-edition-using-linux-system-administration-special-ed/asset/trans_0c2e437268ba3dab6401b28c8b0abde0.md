

```text
raid5: 正在测量校验和计算速度
  8regs  : 337.947 MB/秒
  32regs : 242.316 MB/秒
使用函数 : 8regs (337.947 MB/秒)
scsi : 0 个主机
scsi : 检测到总数。
md.c: sizeof(md_super_t) = 4096
分区检查：
RAMDISK：在块 0 处发现压缩映像
自动检测 RAID 阵列
自动运行 ...
... 自动运行完成。
VFS：已挂载根文件系统（ext2 文件系统）。
ncr53c8xx: 使用 PCI 总线 1，设备 4，功能 0
ncr53c8xx: 检测到 53c875
ncr53c875-0: rev=0x03, base=0x40101000, io_port=0x7000, irq=9
ncr53c875-0: ID 7, Fast-20, 奇偶校验
ncr53c875-0: 片上 RAM 位于 0x40100000
ncr53c875-0: 重启（scsi 复位）
ncr53c875-0: 正在下载 SCSI SCRIPTS。
scsi0 : ncr53c8xx - 修订版 3.1h
scsi : 1 个主机。

  厂商: FUJITSU   型号: M2954Q-512       修订版: 0153
  类型:   直接访问                          ANSI SCSI 修订版: 02
在 scsi0，通道 0，id 0，lun 0 处检测到 SCSI 磁盘 sda
  厂商: FUJITSU   型号: M2954Q-512       修订版: 0153
  类型:   直接访问                          ANSI SCSI 修订版: 02
在 scsi0，通道 0，id 1，lun 0 处检测到 SCSI 磁盘 sdb
  厂商: FUJITSU   型号: M2954Q-512       修订版: 0153
  类型:   直接访问                          ANSI SCSI 修订版: 02
在 scsi0，通道 0，id 2，lun 0 处检测到 SCSI 磁盘 sdc
  厂商: SONY      型号: SDX-300C        修订版: 0400
  类型:   顺序访问                          ANSI SCSI 修订版: 02
在 scsi0，id 6，lun 0 处检测到 SCSI 磁带机 st0
ncr53c875-0-<0,0>: 标记命令队列深度设置为 8
ncr53c875-0-<0,1>: 标记命令队列深度设置为 8
ncr53c875-0-<0,2>: 标记命令队列深度设置为 8
ncr53c875-0-<0,*>: FAST-20 WIDE SCSI 40.0 MB/s (50 ns, offset 15)
SCSI 设备 sda: 硬件扇区= 512 字节. 扇区数= 8498506 [4149 MB] [4.1 GB]
  sda: sda1 sda2 < sda5 sda6 sda7 sda8 >
ncr53c875-0-<1,*>: FAST-20 WIDE SCSI 40.0 MB/s (50 ns, offset 15)
SCSI 设备 sdb: 硬件扇区= 512 字节. 扇区数= 8498506 [4149 MB] [4.1 GB]
  sdb: sdb1 sdb2
ncr53c875-0-<2,*>: FAST-20 WIDE SCSI 40.0 MB/s (50 ns, offset 15)
SCSI 设备 sdc: 硬件扇区= 512 字节. 扇区数= 8498506 [4149 MB] [4.1 GB]
  sdc: sdc1 sdc2
自动检测 RAID 阵列
自动运行 ...
... 自动运行完成。
VFS：已挂载根文件系统（ext2 文件系统）为只读。
切换根目录：旧根目录的 d_count=1
尝试卸载旧根目录 ... 成功
释放未使用的内核内存：释放了 68k
添加交换空间：530108k 交换空间（优先级 -1）
```

## 特殊内核线程的启动

内核启动的第一个进程是 init。init 的进程 ID 为 1。内核本身的进程 ID 为 0，但用 `ps` 命令是看不到的。可以通过运行 `ps` 命令并查找 init 的父进程 ID（PPID）来间接推断，如下所示：

```text
UID       PID  PPID  C STIME TTY          TIME CMD
root        1     1  0 2:17:38 ?      00:00:03 init [S]
```

init 进程会启动一些特殊的系统进程：kflushd、kpiod、kswapd 和 mdrecoveryd。这些都是内核线程。kflushd 是一个内核线程，取代了以前称为 bdflush 的用户空间进程。它负责将脏缓冲区写回磁盘。kpiod 是一个负责页面输入和输出的内核线程。kswapd 是内核交换守护进程，当内存碎片化或已满时负责释放内存。mdrecoveryd 是一个监控 RAID 元设备的内核线程。

至此，内核本身的启动已经完成。但是，接受用户登录的进程或其他守护进程尚未启动。

## LINUX 运行级别

Linux 的启动过程之所以复杂，是因为它可以启动到多种不同的状态。这些操作模式被称为 init 状态或运行级别，由 init 程序维护。表 4.1 总结了 Linux 的不同运行级别。

| 运行级别 | 描述 |
|---|---|
| 0 | 关闭机器电源 |
| 1 或 S | 单用户模式 |
| 2 | 无 NFS 的多用户模式 |
| 3 | 完整的多用户模式 |
| 4 | 未使用 |
| 5 | 带 X-Windows 的完整多用户模式 |
| 6 | 关闭并重新启动 |

> **注意**
>
> 表 4.1 中所示的运行级别在大多数 UNIX 系统（包括 Linux）中被普遍接受为标准。对于运行级别 2-5，可以任意选择在这些 init 状态下运行的服务。上述 init 状态是一个很好的经验法则。

运行级别由一个 init 读取的配置文件 `/etc/inittab` 控制。默认运行级别始终是完整的多用户操作模式，即运行级别 3 或 5。下面显示了一个示例 `/etc/inittab` 文件：

```text
#
# inittab       此文件描述了 INIT 进程应如何在某个运行级别
#               设置系统。
#
# 作者:          Miquel van Smoorenburg, <miquels@drinkel.nl.mugnet.org>
#               由 Marc Ewing 和 Donnie Barnes 为 RHS Linux 修改
#
# 默认运行级别。RHS 使用的运行级别为：
#   0 - 停机（不要将 initdefault 设置为此值）
#   1 - 单用户模式
#   2 - 多用户，不带 NFS（如果没有网络，则与 3 相同）
#   3 - 完整的多用户模式
#   4 - 未使用
#   5 - X11
#   6 - 重启（不要将 initdefault 设置为此值）
#
id:3:initdefault:
# 系统初始化。
si::sysinit:/etc/rc.d/rc.sysinit
l0:0:wait:/etc/rc.d/rc 0
l1:1:wait:/etc/rc.d/rc 1
l2:2:wait:/etc/rc.d/rc 2
l3:3:wait:/etc/rc.d/rc 3
l4:4:wait:/etc/rc.d/rc 4
l5:5:wait:/etc/rc.d/rc 5
l6:6:wait:/etc/rc.d/rc 6
# 在每个运行级别都要运行的内容。
ud::once:/sbin/update
# 捕获 CTRL-ALT-DELETE
ca::ctrlaltdel:/sbin/shutdown -t3 -r now
# 当 UPS 告知电源出现故障时，假定我们还有几分钟
# 的电力。安排从现在起 2 分钟后关机。
# 当然，这需要你安装了电源并且你的
# UPS 已连接且工作正常。
pf::powerfail:/sbin/shutdown -f -h +2 "电源故障；系统正在关机"
# 如果在关机执行前电源已恢复，则取消关机。
pr:12345:powerokwait:/sbin/shutdown -c "电源已恢复；关机已取消"
# 在标准运行级别下运行 getty
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6
# 在运行级别 5 下运行 xdm
# xdm 现在是一个单独的服务
x:5:respawn:/etc/X11/prefdm -nodaemon
```

只要系统在运行，init 进程就会保持活动状态。它确保所有守护进程都已启动。例如，当你登录时，监控终端的 getty 进程（在 Linux 中为 `/sbin/mingetty`）会被你的登录 shell 替换。因此，该终端的 getty 进程不再存在。然而，当你注销时，shell 退出，留下一个无法使用的死终端端口。init 进程会检测到 shell 何时结束，并为该终端端口生成另一个 getty 进程。这就在终端上提供了 `login:` 提示符。

正如我们之前所述，init 进程从文件 `/etc/inittab` 获取关于需要运行哪些守护进程的指令。inittab 文件是一个典型的面向行的 UNIX 控制文件，包含几个条目，每个条目由四个以冒号分隔的字段组成。以 `#` 符号开头的行是注释行，会被忽略。这些字段的用法如下：

- 每行的第一个字段是一个标识符，用于命名该行，并且必须唯一。
- 第二个字段定义该行有效的运行级别。它可以指定多个运行级别，例如 2345，表示该条目在运行级别 2、3、4 和 5 下有效。如果此字段为空，则它在所有运行级别下均有效。例如，示例 inittab 文件中的 `si`（系统初始化）、`ud`（更新）、`ca`（control-alt-delete）和 `pf`（电源故障）行的运行级别列表都为空，因此适用于所有运行级别。
- 第三个字段描述当 init 处于第二个字段指定的某个运行级别时应采取的操作。此字段的一些典型值是 once、respawn、wait 和 initdefault。`once` 告诉 init 在进入指定运行级别时执行该程序，但不等待其完成。而 `wait` 则告诉 init 在继续之前，要等到指定程序的执行完成。`respawn` 指示 init 在进入相应运行级别时启动指定程序，并且每当 init 检测到该程序未运行时，就重新启动它。最后，`initdefault` 值具有特殊含义，包含此值的条目在第三个字段中不包含第四个字段。它指定系统默认的运行级别，并指示 init 在系统首次启动时进入此运行级别。
- 最后一个字段指定当系统处于第二个字段指定的运行级别时，init 要执行的命令行。这可以是一个 shell 脚本或一个可执行程序，并且支持命令行参数和 shell 重定向。

在上面显示的示例 inittab 文件中，默认运行级别是 3。这指示 init 在首次启动时将系统带到运行级别 3，除非通过传递给 LILO 的命令覆盖，要求系统启动到单用户模式。

## 运行 `/etc/rc.d` 目录中的初始化脚本

系统初始化脚本位于 `/etc/rc.d` 目录中。init 程序首先运行名为 `rc.sysinit` 的脚本。`rc.sysinit` 设置各种系统变量并执行其他启动初始化功能。接下来，init 运行为默认运行级别指定的所有脚本。最后，init 运行名为 `rc.local` 的脚本。

以下是 `/etc/rc.d` 目录内容的典型列表：

```text
 # ls -l
 total 25
 drwxr-xr-x  2 root     root          1024 Nov 30 19:14 init.d
 -rwxr-xr-x  1 root     root          2722 Apr 15  1999 rc
```

