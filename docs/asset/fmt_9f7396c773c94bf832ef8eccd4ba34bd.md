
```
[root@centos65 ~]# dmesg | grep sd[a-z] | head
sd 0:0:0:0: [sda] 83886080 512-byte logical blocks: (42.9 GB/40.0 GIB)
sd 0:0:0:0: [sda] Write Protect is off
sd 0:0:0:0: [sda] Mode Sense: 00 3a 00 00
sd 0:0:0:0: [sda] Write cache: enabled, read cache: enabled, doesn't support \
DPO or FUA
sda: sda 0:0:0:0: [sda] Attached SCSI disk
s 3:0:0:0: [sdb] 150994944 512-byte logical blocks: (77.3 GB/72.0 GIB)
sd 3:0:0:0: [sdb] Write Protect is off
sd 3:0:0:0: [sdb] Mode Sense: 00 3a 00 00
sd 3:0:0:0: [sdb] Write cache: enabled, read cache: enabled, doesn't support \
DPO or FUA
```

这是带有 200GB `ata` 磁盘的计算机上 `dmesg` 的另一个示例。

```
paul@barry:$# dmesg | grep -i "ata disk"
[ 2.624149] hda: ST360021A, ATA DISK drive
[ 2.904150] hdb: Maxtor 6Y0800, ATA DISK drive
[ 3.472148] hdc: WD2000GB-9WA0, ATA DISK drive
```

这是 RHEL5 上运行 `dmesg` 的第三也是最后一个示例。

```
root@rhel5 ~# grep -i "scsi disk"
sd 0:0:2:0: Attached scsi sda
sd 0:0:3:0: Attached scsi sdb
sd 0:0:6:0: Attached scsi sdc
```

### 4.3.3. `/sbin/lshw`

`lshw` 工具将列出硬件。通过正确的选项 `lshw` 可以显示关于磁盘（分区）的信息。以下是 Debian 6 的截屏：

```
root@debian6:~# lshw -class | grep -B2 scsi
description: Linux autodet
physical id: 1
bus info: scsi@0.0,1
logical name: /dev/sdb
description: Linux autodet partition
physical id: 1
bus info: scsi@2.0,1
logical name: /dev/sdc
description: Linux autodet partition
physical id: 1
bus info: scsi@3.0,1
logical name: /dev/sdd
description: Linux autodet partition
physical id: 1
bus info: scsi@4.0,1
logical name: /dev/sde
description: Linux
physical id: 1
bus info: scsi@0.0,1
logical name: /dev/sda1
description: Extended partition
physical id: 2
bus info: scsi@0.0,2
logical name: /dev/sda3
```

Redhat 和 CentOS 没有这个工具（除非你将其添加到仓库）。

### 4.3.4. `/sbin/lsscsi`

`lsscsi` 命令为所有 scsi（以及模拟 scsi）设备提供了良好的可读输出。第一个截图是 SPARC 系统上的 `lsscsi`。

```
root@shaka:~ lsscsi
[0:0:0:0] disk Adaptec RAID5 V1.0 /dev/sda
[1:0:0:0] disk SEAGATE ST3360FSUN36G04 /dev/sdb
```

NAS 上的 `lsscsi` 截图（拥有 750GB 磁盘并从 USB 棒启动）。

```
root@debian6# lsscsi
[0:0:0:0] disk SanDisk Cruzer Edge 1.19 /dev/sda
[1:0:0:0] disk ATA ST37503AS SD04 /dev/sdb
[2:0:0:0] disk ATA ST37503AS SD04 /dev/sdc
[3:0:0:0] disk ATA ST37503AS SD04 /dev/sdd
[4:0:0:0] disk ATA ST37503AS SD04 /dev/sde
```

这个截图显示了 `lsscsi` 的经典输出。

```
root@debian6# lsscsi -c
Attached devices:
Host: scsi0 Channel: Target: 00 Lun: 00 Rev: 1.19
  Vendor: SanDisk Model: Cruzer Edge
  Type: Direct-Access  ANSI SCSI revision: 02
Host: scsi1 Channel: Target: 00 Lun: 00 Rev: SD04
  Vendor: ATA Model: ST37503AS
  Type: Direct-Access  ANSI SCSI revision: 05
Host: scsi2 Channel: Target: 00 Lun: 00 Rev: SD04
  Vendor: ATA Model: ST37503AS
  Type: Direct-Access  ANSI SCSI revision: 05
Host: scsi3 Channel: Target: 00 Lun: 00 Rev: SD04
  Vendor: ATA Model: ST37503AS
  Type: Direct-Access  ANSI SCSI revision: 05
Host: scsi4 Channel: Target: 00 Lun: 00 Rev: SD04
  Vendor: ATA Model: ST37503AS
  Type: Direct-Access  ANSI SCSI revision: 05
```

### 4.3.5. 磁盘设备

定位 scsi（或 sd）设备的另一种方法是通过 `/proc/scsi/scsi`。

这个截图来自一台带有 adaptec RAID5 的备用计算机。

```
root@shaka:~# cat /proc/scsi/scsi
Attached devices:
Host: scsi0 Channel: 0 Id: 00 Lun: 00
  Vendor: Adaptec Model: RAID5 Rev: V1.0
  Type: Direct-Access
Host: scsi1 Channel: 0 Id: 00 Lun: 00
  Vendor: SEAGATE ST3360FSUN36G04
  Type: Direct-Access
```

这里我们在 QNAP（带有 Debian）上运行 `/proc/scsi/scsi`。

```
root@debian6# cat /proc/scsi/scsi
Attached devices:
Host: scsi0 Channel: Target: 00 Lun: 00
  Vendor: SanDisk Cruiser Edge 1.19
  Type: Direct-Access  ANSI SCSI revision: 02
Host: scsi1 Channel: Target: 00 Lun: 00
  Vendor: ATA ST37503AS SD04
  Type: Direct-Access  ANSI SCSI revision: 05
Host: scsi2 Channel: Target: 00 Lun: 00
  Vendor: ATA ST37503AS SD04
  Type: Direct-Access  ANSI SCSI revision: 05
Host: scsi3 Channel: Target: 00 Lun: 00
  Vendor: ATA ST37503AS SD04
  Type: Direct-Access  ANSI SCSI revision: 05
Host: scsi4 Channel: Target: 00 Lun: 00
  Vendor: ATA ST37503AS SD04
  Type: Direct-Access  ANSI SCSI revision: 05
```

## 4.4. 擦除硬盘
