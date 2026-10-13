
### 8. 在 `/dev/db` 存储设备上创建物理资源

#### 8.1. 创建一个 512 MiB 的额外分区并将其设置为 LVM 类型。使用 `third` 作为该分区的名称

```
[root@servera]# parted /dev/db mkpart 514MiB 1026MiB
[root@servera]# parted /dev/db set 3 lvm on
```

#### 8.2. 向内核注册新分区

```
[root@servera]# udevadm settle
```

#### 8.3. 将新分区作为 PV 添加

```
[root@server ~]# pvcreate /dev/vdb3
Physical volume "/dev/vdb3" successfully created.
```

### 9. 使用新创建的磁盘空间，通过 `server_volume` 扩展文件系统到总大小为 700 MIB

#### 9.1. 使用新的 `/dev/vdb3` PV 扩展 `server_group` VG

```
[root@server ~]# vgxtend server_group /dev/vdb3
Logical volume "server_group" successfully extended
```

#### 9.2. 将现有的 `server_volume` LV 扩展到 700 MIB

```
[root@server ~]# lvxtend server_volume 700 MIB
Size of logical volume server_group/server_volume changed from 400.00 MIB (100 extents)
Logical volume server_group/server_volume resized.
```

#### 9.3. 使用 LV 上的空闲空间扩展 XFS 文件系统

```
[root@server ~]# xfs_growfs /data
...
data changed from 10240 to 17920
```

### 10. 验证 LV 已扩展且内容存在

#### 10.1. 使用 `ldisplay` 命令验证 LV 的大小

```
[root@server ~]# ldisplay /dev/server_group/server_volume
-- logical volume --
LV Path | /dev/server_group/server_volume
LV Name | server_volume
VG Name | server_group
LV UUID | 939Fuit-eg7-B5HM-r1p5-DVZH-n5cn-j5e2tw
LV Write Access | read/write
LV creation time | server.example.com, 2022-04-11 03:25:12 -0400
LV Status | available
LV Size | 700.00 MIB
Current LE | 175
Segments | 3
Allocation | inherit
Read ahead | 8192
- currently set to 253:0
Block device | /dev/mapper/
```

#### 10.2. 验证新的文件系统大小。验证之前复制的文件仍然存在

```
[root@servera ~]# df -h
Filesystem Size Used Avail Mounted on
/dev/mapper/server_group-server_volume 695M 26M 670M 4% /data
[root@servera ~]# ls /data | wc -l
32
```

### 11. 返回工作站

```
[root@servera ~]# exit
Connection to servera closed.
```

## 完成

在工作站上切换到 `student` 目录并使用 `lab` 命令完成此实验。此步骤确保之前的实验资源不受影响。

```
[student@workstation ~]$ lab finish lvm-manage
```
