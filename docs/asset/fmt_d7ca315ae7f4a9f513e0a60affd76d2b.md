
### Meminfo

```
SUSE #      total       used     free     shared buffers  cached

Mem:             63056 61124 1932 53068 18352 27164

      by buffers/cache:     15608 47448

Swap:             125896 100
```

图 221 Meminfo

`/proc/mounts` 文件显示所有已挂载的分区。不带参数的 `mount` 命令将显示类似的信息。例如：

第 14 章 Linux 中的通用性能工具

```
root # cat /proc/mounts

/dev/root /ext2 rw 0 0

proc /proc proc rw 0 0

/dev/hda1 /ext2 rw 0 0

devpts /dev/pts rw 0 0

root # mount

/dev/hda3 on / type ext2 (rw)

proc on /proc type proc (rw)

/dev/hda on /boot type ext2 (rw)

devpts on /dev/pts devpts (rw,gid=5,mode=0620)
```

图 222 Mounts 文件

`/proc/partitions` 文件显示所有设备上的分区。你也可以使用 `fdisk -l` 来显示这些信息。例如：

```
suSE:~ # cat /proc/partitions

major blocks name

3 0 1023907 hda

3 1 6016 hda1

3 2 126000 hda2

3 3 891072 hda3

3 64 1023908 hdb

3 65 1023088 hdb1

22 0 2096
```

图 223 Partition文件

`/proc/pci` 提供了关于所有 PCI 设备的信息。注意 `/proc/pci` 更容易读。例如：

```
bash-2.04# cat /proc/pci

00:00.08 Host bridge: Intel Corporation 430TX - 82439TX MDX (rev 01)

00:07.0A ISA bridge: Intel Corporation 82371AB PIX4 ISA (rev 08)

00:07.1E IDE interface: Intel Corporation 82371AB PIX4 IDE (rev 01)

00:0F.0 Display controller: VMware Inc. Virtual SVGA

00:10.0 Ethernet controller: Advanced Micro Devices [AMD] 79c90 [PCNet_LANCE] (rev 10)
```

```bash
bash-2.04# cat /proc/version

Linux version 2.2.16 (root@premium.suse.de) (gcc version 2.95.2 19991024 (release)) #1

Wed Aug 2 20:22:26 GMT 2000

bash-2.04# uname -a

Linux kernel 2.2.16 #1 Wed Aug 2 20:22:26 GMT 2000 i686
```

图 226. 版本文件

如果你想获取更多关于 SCSI 设备的信息，必须查看位于 `/proc/scsi` 下的文件。

`vmstat` 也是一个从 `/proc` 文件系统收集信息的工具。它报告关于进程、内存、分页、块级 I/O、陷阱和 CPU 活动的信息。所产生的活动报告给出了自上次启动以来的平均值。额外的报告提供了长度为 `delay` 的采样周期信息。在这两种情况下，进程和内存报告都是瞬时的。
`vmstat` 对于记录长时间的 CPU 和内存使用情况非常有帮助。

除了配置硬盘的许多参数外，还可以使用命令 `hdparm -tT <device>` 来执行硬盘性能测试。例如：

```
SuSE-# # hdparm -tT /dev/hda

/dev/hda:

Timing buffer-cache reads: 64 MB in 0.68 seconds =94.12 MB/sec

Timing buffered disk reads: 32 MB in 29.51 seconds =1.08 MB/sec

SuSE-# # hdparm -cl /dev/hda

/dev/hda:

setting 32-bit I/O flag to 1

I/O support = 1 (32-bit)

SuSE-# # hdparm -tT /dev/hda

/dev/hda:

Timing buffer-cache reads: 64 MB in 0.67 seconds =95.52 MB/sec

Timing buffered disk reads: 32 MB in 12.92 seconds =2.48 MB/sec
```
