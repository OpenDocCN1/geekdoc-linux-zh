
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

内核启动的第一个进程是 `init`。`init` 的进程 ID 为 1。内核本身的进程 ID 为 0，但用 `ps` 命令是看不到的。可以通过运行 `ps` 命令并查找 `init` 的父进程 ID（PPID）来间接推断，如下所示：

```text
UID       PID  PPID  C STIME TTY          TIME CMD
root        1     1  0 2:17:38 ?      00:00:03 init [S]
```

`init` 进程会启动一些特殊的系统进程：`kflushd`、`kpiod`、`kswapd` 和 `mdrecoveryd`。这些都是内核线程。`kflushd` 是一个内核线程，取代了以前称为 `bdflush` 的用户空间进程。它负责将脏缓冲区写回磁盘。`kpiod` 是一个负责页面输入和输出的内核线程。`kswapd` 是内核交换守护进程，当内存碎片化或已满时负责释放内存。`mdrecoveryd` 是一个监控 RAID 元设备的内核线程。

至此，内核本身的启动已经完成。但是，接受用户登录的进程或其他守护进程尚未启动。

## LINUX 运行级别

Linux 的启动过程之所以复杂，是因为它可以启动到多种不同的状态。这些操作模式被称为 init 状态或运行级别，由 `init` 程序维护。表 4.1 总结了 Linux 的不同运行级别。

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

运行级别由一个 `init` 读取的配置文件 `/etc/inittab` 控制。默认运行级别始终是完整的多用户操作模式，即运行级别 3 或 5。下面显示了一个示例 `/etc/inittab` 文件：
