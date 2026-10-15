
e 扩展（逻辑分区容器）

选择（默认 p）：p

分区号（1-4，默认 1）：1

```bash
起始扇区 (2048-16777215, 默认 2048): 2048

最后一个扇区，+sectors 或 +size{K,M,G,T,P} (2048-1677215, 默认 1677215): +1G

创建一个类型为 'Linux' 且为 1 GiB 的分区 1。
```

```bash
Command (m for help): p

Disk /dev/sdb: 8 GiB, 8589934592 bytes, 16777216 扇

扇区大小：1 * 512 = 512 字节

扇区大小（逻辑/物理）：512 字节 / 512 字节

I/O 大小（最小/最佳）：512 字节 / 512 字节

磁盘类型：dos

标识符：0x25fd22

设备 启动 起始 结束 扇 大 大

/dev/sdb1 2048 209919 2097152 1G 83
```

```bash
Command (m for help): n

分区类型

p 主（0 个主，0 个扩展，4 空闲）

e 扩展（逻辑分区容器）

选择（默认 p）：p

分区号（1-4，默认 1）：1

起始扇区 (2048-16777215, 默认 2048): 2048

最后一个扇区，+sectors 或 +size{K,M,G,T,P} (2048-1677215, 默认 1677215): +1G

创建一个类型为 'Linux' 且为 1 GiB 的分区 1。

Command (m for help): p

Disk /dev/sdb: 8 GiB, 8589934592 bytes, 16777216 扇

扇区大小：1 * 512 = 512 字节

扇区大小（逻辑/物理）：512 字节 / 512 字节

I/O 大小（最小/最佳）：512 字节 / 512 字节

磁盘类型：dos

标识符：0x25fd22

设备 启动 起始 结束 扇 大 大

/dev/sdb1 2048 209919 2097152 1G 83
```

| 设备 | 启动 | 起始 | 结束 | 扇 | 大小 | ID | 类型 |
|---|---|---|---|---|---|---|---|
| /dev/sdb1 | | 2048 | 209919 | 2097152 | 1G | 83 | Linux |
| /dev/sdb2 | | 2099200 | 6293503 | 4194304 | 2G | 83 | Linux |
| /dev/sdb3 | | 6293504 | 16777215 | 10483712 | 5G | 83 | Linux |

```bash
Command (m for help): t

分区号（1-3，默认 3）：2

十六进制代码（输入 L 列出所有）：82

更改分区类型 'Linux' 为 'Linux swap / Solaris'。
```

```bash
Command (m for help): t

分区号（1-3，默认 3）：3

十六进制代码（输入 L 列出所有）：8e

更改分区类型 'Linux' 为 'Linux LVM'。
```

| 设备 | Boot | 开始 | 结束 | 扇区 | 大小 | Id | 类型 |
|---|---|---|---|---|---|---|---|
| /dev/sdb1 | | 2048 | 2099199 | 2097152 | 1G | 83 | Linux |
| /dev/sdb2 | | 2099200 | 6293503 | 4194304 | 2G | 82 | Linux swap / Solaris |
| /dev/sdb3 | | 6293504 | 16777215 | 10483712 | 5G | 8e | Linux LVM |

```
Command (m for帮助): : w
```

分区表已修改。
正在调用 ioctl() 重新读取分区表。
正在同步磁盘。

```bash
# fdisk -l | mail me@example.com -s "Fdisk params for server X"
```

```bash
# gdisk -l /dev/sda

GPT fdisk (gdisk) version 0.8.10
```

分区表扫描：
MBR: 仅限 MBR
BSD: 不存在
APM: 不存在
GPT: 不存在

********************************************************************

磁盘 /dev/sda: 33554432 扇区, 16.0 GiB
逻辑扇区大小: 512 
磁盘标识符 (GUID): F2A219A-E316-4A76-9AE4-986527922687
分区表最多包含 128 条目
第一个可用扇区为 34，最后一个可用扇区为 33554398
分区将按照 2048 扇区边界对齐
总空闲空间为 6077 扇区 (3.0 MiB)

| 编号 | 开始 (扇区) | 结束 (扇区) | 大小 | 代码 | 名称 |
|---|---|---|---|---|---|
| 1 | 2048 | 1026047 | 500.0 MiB | 8300 | Linux filesystem |
| 2 | 1026048 | 33550335 | 15.5 GiB | 8E00 | Linux LVM |
```

```bash
# gdisk /dev/sdb

GPT fdisk (gdisk) version 0.8.10

分区表扫描：

MBR: 不存在

BSD: 不存在

APM: 不存在

GPT: 不存在
```

正在创建新的 GPT 条目。

```bash
Command (? for帮助): p

Disk /dev/sdb: 16777216 扇区, 8.0 GiB

逻辑扇区大小: 512 

磁盘标识符 (GUID): CC47CA6B-6C9F-4C83-91CC-2FEC81254B39

分区表最多包含 128 条目

第一个可用扇区为 34，最后一个可用扇区为 16777182

分区将按照 2048 扇区边界对齐

总空闲空间为 16777149 扇区 (8.0 GiB)
```

| 编号 | 开始 (扇区) | 结束 (扇区) | 大小 | 代码 名称 |
|---|---|---|---|---|

```bash
Command (? for帮助): n

分区编号 (1-128, 默认 1): 1

第一个扇区 (34-16777182, 默认 = 2048) 或 (+)-大小{KMGTTP}: 2048

最后一个扇区 (2048-16777182, 默认 = 16777182) 或 (+)-大小{KMGTTP}: +7G

当前类型为 'Linux filesystem'

十六进制代码或 GUID (L 显示代码, Enter = 8300): 8e00

已将分区类型更改为 'Linux LVM'

Command (? for帮助): n

分区编号 (1-128, 默认 2): 2

第一个扇区 (34-16777182, 默认 = 14682112) 或 (+)-大小{KMGTTP}: 14682112

最后一个扇区 (14682112-16777182, 默认 = 16777182) 或 (+)-大小{KMGTTP}: 16777182

当前类型为 'Linux filesystem'

十六进制代码或 GUID (L 显示代码, Enter = 8300): 8200

已将分区类型更改为 'Linux swap'
```

```bash
Command (? for帮助): p

Disk /dev/sdb: 16777216 扇区, 8.0 GiB

逻辑扇区大小: 512 

磁盘标识符 (GUID): CC47CA6B-6C9F-4C83-91CC-2FEC81254B39

分区表最多包含 128 条目

第一个可用扇区为 34，最后一个可用扇区为 16777182

分区将按照 2048 扇区边界对齐

总空闲空间为 16777149 扇区 (8.0 GiB)
```

| 编号 | 开始 (扇区) | 结束 (扇区) | 大小 | 代码 |
|---|---|---|---|---|
| 1 | 2048 | 14682111 | 7.0 GiB | 8E00 | Linux LVM |
| 2 | 14682112 | 16777182 | 1023.0 MiB | 8200 | Linux swap |
```

```bash
Command (? for帮助): w

检查完成。准备写入 GPT 数据。覆盖现有分区？继续吗？ (Y/N): y

OK; 正在向 /dev/sdb 写入新分区表 (GPT)。

操作完成。
```

```bash
# parted /dev/sdb
GNU Parted 欢迎使用 Parted! 查看列表：
(parted) mkpart MyData 0 7G
警告：结果分区未针对最佳性能对齐。忽略/取消？
(parted) p
型号: ATA (scsi)
磁盘: /dev/sdb: 8590MB
扇区大小 (逻辑/物理): 512B/512B
分区表: gpt
编号 | 开始 | 结束 | 名称
1 | 0 | 7000MB | 7000MB | MyData
```

```bash
$ stat /home/sean/.bashrc
文件: /home/sean/.bashrc
文件名: '.bashrc'
大小: 966           块: 8          块: 4096
设备: /dev/sda1476d  Inode: 1527247  链接: 1
访问: (0644/-rw--)Uid: (500/sean) Gid: (500/sean)
访问: 2014-10-07 09:17:48.000000 -0500
修改: 2014-10-07 09:17:48.000000 -0500
更改: 2014-10-07 09:17:48.000000 -0500
出生: -
```

```bash
# debugfs /dev/mapper/VolGroup00-LogVol0
debugfs 1.41.4 (22-Dec-2010)
debugfs: cd /home/sean
debugfs: stat .bashrc
Inode: 1527247 类型: 普通 模式: 0644 标志: 0x0
代号: 8735284 版本: 0x000000
用户: 500 组: 500 大小: 966
文件 ACL: 0 目录 ACL: 0
链接: 1 块计数: 8
碎片地址: 0 编号: 0 大小: 0
创建时间: 2014-10-07 09:17:48.000000 -0500
访问时间: 2014-10-07 09:17:48.000000 -0500
修改时间: 2014-10-07 09:17:48.000000 -0500
块:
(0):1529149
总: 1
```

```bash
$ df -i
文件系统 Inode 已用 空闲 Inode用% 挂载在
/dev/mapper/VolGroup00-LogVol00 60686336 1500786 59185550 3% /
```

```bash
# mkfs.ext3 -b 4096 -m 2 -L data -O sparse_super /dev/sdb1
mke2fs 1.42.11 (09-Jul-2014)
/dev/sdb1 包含 ext4 文件系统
创建于 Thu 2015年2月19日 00:27:24
坚持吗？(y,n) y
创建文件系统 1708980 个 4k 块和 427392 个 inode
文件系统 UUID: 2d6f6a18-77f9-47f3-b6ad-e36026da3a9
超级块备份存储在块：
32768, 98304, 163840, 229376, 294912, 819200, 884736
```

```bash
# dumpefs /dev/sdb1
dumpefs 1.42.11 (09-Jul-2014)
设备: /dev/sdb1
文件系统类型: ext4
UUID=2d6f6a18-77f9-47f3-b6ad-e36026da3a9
标签=data
块大小 = 4096
inode 计数 = 2
特征 = (has_extent ext4_feature_compat_dir__sum ext4_feature_compat_inode_size)
块_inode_计数 = 427392
块_计数 = 1708980
空闲块 = 59185550
空闲 inode = 59185550
```

```
# mkfs -t xfs -f /dev/sdb1 isize=256 agcount=4, agsize=427245
meta-data=/dev/sdb1 sectsz=512 attr=2, projid32bit=1
blks = crc=0 finobt=0
 = =
data = bsize=4096 blocks=1708980, imaxpct=25 unit=0 swidth=0 blks
naming =version 2 bsize=4096 ascii-ci=0 ftype=0
log =internal log bsize=4096 blocks=2560, version=2
 = =
count=1 sectsz=512 unit=0 blks, lazy-realtime =none extsz=4096 blocks=0, rtextents=0
```

```bash
# blkid
/dev/sda1: UUID="4d2b8b91-9666-49cc-a23a-1a183ccd2150" TYPE="ext4"
/dev/sda3: LABEL="flubbers" UUID="bab04315-389d-42bf-9efa-b25c2f39b7a0" TYPE="ext4"
/dev/sda4: UUID="18d6e8bc-14a0-44a0-b82b-e69b4469b0ad" TYPE="ext4"
```

```bash
$ mount
/dev/sda1 on / type ext4 (rw,errors=remount-ro)
proc on /proc type proc (rw,noexec,nosuid,nodev)
sysfs on /sys type sysfs (rw,noexec,nosuid,nodev)
udev on /dev type devtmpfs (rw,mode=0755)
devpts on /dev/pts type devpts (rw,noexec,nosuid,gid=5,mode=0620)
tmpfs on /run type tmpfs (rw,noexec,nosuid,size=10%,mode=0755)
/dev/sda3 on /mnt/data type ext4 (rw)
/dev/sda4 on /mnt/timemachine type ext4 (rw)
```

```bash
$ cat /etc/mtab
/dev/sda1 / ext4 rw,errors=remount-ro 0 0
proc /proc rw,noexec,nosuid,nodev 0 0
sysfs /sys sysfs rw,noexec,nosuid,nodev 0 0
udev /dev devtmpfs rw,mode=0755 0 0
devpts /dev/pts devpts rw,noexec,nosuid,gid=5,mode=0620 0 0
tmpfs /run tmpfs rw,noexec,nosuid,size=10%,mode=0755 0 0
/dev/sda3 /mnt/data ext4 rw 0 0
/dev/sda4 /mnt/timemachine ext4 rw 0 0
```

```bash
$ cat /proc/mounts
rootfs / rootfs rw 0 0 suid,nodev,noexec,relat 0 0
sysfs /sys sysfs rw,nosuid,nodev,noexec,relat 0 0
proc /proc rw,nosuid,nodev,noexec,relat 0 0
udev /dev devtmpfs rw,relat,size=1980172k,nr_inodes=495043,mode=755 0 0
devpts /dev/pts devpts rw,nosuid,noexec,relat,gid=5,mode=620,ptmx_mode=000 0 0
tmpfs /run tmpfs rw,nosuid,noexec,relat,size=404804k,mode=755 0 0
/dev/disk/by-uuid/30b3416-5a59-4954-b4a6-f2c105d9aac5 / ext4 rw,relat,errors=remount-ro,data=ordered 0 0
/dev/sda3 /mnt/data ext4 rw,relat,data=ordered 0 0
/dev/sda4 /mnt/timemachine ext4 rw,relat,data=ordered 0 0
```
