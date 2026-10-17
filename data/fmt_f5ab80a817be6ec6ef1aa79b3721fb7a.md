
# /proc 信息

## 5 /dev/tty

块设备:

1 `ramdisk`

7 `loop`

8 `sd`

9 `md`

`$ cat /proc/diskstats` 显示磁盘、分区和统计数据

1 `ram00000000000`

1 `ram1000000000000`

| 8 | 0 | sda 2228445 1032472 68692149 21672710 1098740 400314 |
| | | 4779070 10170432 1358988 12279905 |
| | | sda1 33077 13060510 188002 844328 |
| | | sda2 1491 1759 50 162 |
| 7 | | 00000000 |

在所示的 `diskstats` 输出中，你可以看到内存磁盘（`ram0`、`ram1` 等）和回环设备（`loop0`、`loop1` 等）。对于硬盘分区，示例显示了整个磁盘（`sda`）和每个分区（`sda1`、`sda2` 等）的统计数据。对于整个硬盘（从左到右）：总读取数、读取总数、合并的读取数、所有读取消耗的毫秒数、完成的写入数、合并的写入数、写入的写入器数。对于特定分区（从左到右）：读取请求数、读取扇区数、写入请求数。

`$ cat /proc/filesystems` 列出当前节点支持的文件系统类型

`nodev` `sysfs` means type is not used by any device

`nodev` `roots`

`ext3` is used on a mounted device

`iso9660` is used on a mounted device

`$ cat /proc/interrupts` 查看 IRQ 通道分配

`CPU0`: 1938091 `XT-PIC-XT` `timer`

1: 28189 `XT-PIC-XT` `i`

2: 0 `XT-PIC-XT` `cascade`

6: 3770197 `XT-PIC-XT` `Audio`

7: 660 `XT-PIC-XT` `parport0`

`$ cat /proc/meminfo` 显示物理内存地址

`00000000-09ffff` : 系统内存

`00000000-0000000` : 内内核

`009fc000-09ffff` : 预留

`00a00000-0bffff` : 显存区域

`00c0000-0c7fff` : 视频 ROM

`00c80000-0cfff` : 适配器 ROM

`000f0000-0fffff` : 系统内存

`00100000-0febfff` : 系统内存

`$ cat /proc/ioports` 显示虚拟内存地址

`0000-01df` : `dma`

`0020-0021` : `pic1`

`0040-0043` : `timer0`

`0050-0053` : `timer1`

`0060-006f` : 键盘

`0070-0077` : `rtc`

`0080-008f` : `dma`页寄存器

`00a0-00a1` : `pic2`

`00c0-00cf` : `dma2`

`00f0-00ff` : `fpu`

`$ cat /proc/keys` 显示内核保留的密钥列表

`00000001`: 1 `perm` 1f3f0000 0 `keyring` `_uid_ses.0`: 1/4

`00000002`: 7 `perm` 1f3f0000 0 `keyring` `_uid.0`: empty

`0442d29e`: 2 `perm` 1f3f0000 0 `keyring` `_ses.20729`: 1/4

`$ cat /proc/loadavg` 显示 1, 5 和 15 分钟的平均负载，

1.77 0.56 0.19 2/247 1869 运行进程/总数/最高 PID

`$ cat /proc/meminfo` 显示可用 RAM 和交换分区内存

`MemTotal`: 482992 kB

`MemFree`: 25616 kB

`Buffers`: 12204 kB

`Cached`: 64132 kB

`SwapCached`: 117472 kB

`Active`: 321344 kB

`Inactive`: 93168 kB

`HighTotal`: 0 kB

`HighFree`: 0 kB

`LowTotal`: 482992 kB

`$ cat /proc/misc` 显示设备的名称/次设备号

229 `fuse` 已注册到杂项主设备 (10)

63 `device-mapper`

175 `aspart`

144 `nvram`

`/proc/modules` Live 0xd0c5900

`ls_utf8` 6209 1 - Live 0xd0e3b000

`cifs` 213301 0 - Live 0xd0e0200

`nfs` 226861 0 - Live 0xd0e8a80

`nfsd` 208689 17 - Live 0xd0cb00

`exports` 9537 1 - Live 0xd0cf450

`lockd` 62409 3 - Live 0xd0cf50

`nfs_acl` 7617 2 - Live 0xd0c5600

`fuse` 45909 2 - Live 0xd0d2400

`vfat` 16193 0 - Live 0xd0cf600

`$ /proc/mounts` 显示已加载模块、内存大小、加载实例、加载状态和内核内存

`root` 已挂载在 `/`

`dev` 已挂载在 `/dev`

`devpts` 已挂载在 `/dev`

`sysfs` 已挂载在 `/sys`

# 修改 /proc 信息

`/proc/sys` 目录中的某些值可以动态更改。对于接受二进制值（0禁用，1 启用）的 `/proc/sys` 文件，人们只需将值重定向到任何想要更改的文件即可。例如，允许转发 IPv4 数据包（例如允许系统进行网络地址转换 (NAT) 或 IP 伪装），你可以输入：

```
# echo 1 > /proc/sys/net/ipv4/ip_forward
```

虽然你可以使用这种技术对系统进行临时更改，但修改 `/proc/sys` 信息的首选方法是使用 `sysctl` 命令。要永久更改这些设置，你应该在 `/etc/sysctl.conf` 文件中添加条目。以下是 `sysctl` 命令的一些示例：

```
# sysctl -w net.ipv4.ip_forward=1
```
