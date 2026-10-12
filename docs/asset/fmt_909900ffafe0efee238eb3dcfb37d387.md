
# 7. 文件系统

## 7.6. 练习：文件系统

- 1. 列出系统已识别的文件系统。
- 2. 在 `200MB` 分区上创建一个 `ext2` 文件系统。
- 3. 在一个 `300MB` 的逻辑驱动上创建一个 `ext3` 文件系统。
- 4. 在 `400MB` 分区上创建一个 `ext4` 文件系统。
- 5. 将 `ext3` 文件系统的根目录预留空间设置为 `0%`。
- 6. 使用 `fdisk` 和 `df` 验证你的工作。
- 7. 对所有新文件系统进行文件检查。

## 7.7. 答案：文件系统

### 1. 列出系统识别的文件系统

```bash
man fs
```

```bash
cat /proc/filesystems
```

```bash
cat /etc/filesystems # 所有 Linux 发行版均适用
```

### 2. 在 200MB 分区上创建一个 ext2 文件系统

```bash
mke2fs /dev/sdc1 # 替换 sdc1 为正确的分区
```

### 3. 在一个 300MB 的逻辑驱动上创建一个 ext3 文件系统

```bash
mke2fs /dev/sdb5 # 替换 sdb5 为正确的分区
```

### 4. 在 400MB 分区上创建一个 ext4 文件系统

```bash
mkfs.ext4 /dev/sdb1 # 替换 sdb1 为正确的分区
```

### 5. 将 ext3 文件系统的根目录预留空间设置为 0%

```bash
tune2fs -m 0 /dev/sdb5
```

### 6. 使用 fdisk 和 df 验证你的工作

`mke2fs` 对这些命令的输出没有影响

主要的变化在下一节：挂载

### 7. 对所有新文件系统进行文件检查

```bash
fsck /dev/sdb1
fsck /dev/sdc1
fsck /dev/sdb5
```

# 8. 挂载

一旦你在分区上放置了文件系统，就可以挂载它。挂载文件系统会使其可用，通常作为一个目录。在所有的 Unix 系统中，每个文件和目录都是大树的一部分。要访问一个文件，你需要从根目录开始的完整路径。当你将文件系统添加到计算机时，需要在树的某处使其可用。提供文件系统的目录被称为挂载点。

## 8.1. 挂载本地系统

### 8.1.1. mkdir

此示例显示了如何使用 `mkdir` 创建挂载点。

```bash
root@RHEL4 ~# mkdir /home/project42
```

### 8.1.2. mount

当挂载点创建且分区上存在文件系统时，`mount` 可以将文件系统挂载到挂载点。

```bash
root@RHEL4 ~# mount -t ext2 /dev/sdb1 /home/project42
```

挂载后，用户就可以访问新的文件系统。

### 8.1.3. /etc/filesystems

实际上不需要 `-t ext2` 参数。`mount` 命令能够自动检测许多文件系统。在不显式指定文件系统的情况下挂载文件系统，`mount` 会首先探测 `/etc/filesystems`。

```bash
root@RHEL4 ~# cat /etc/filesystems
ext3
ext2
nodev
devpts
iso960
```

### 8.1.4. /proc/filesystems

当 `/etc/filesystems` 不存在，或者最后只有一行时，`mount` 将读取 `/proc/filesystems`。

```bash
root@RHEL4 ~# cat /proc/filesystems | grep -v nodev
ext2
iso960
```

### 8.1.5. unmount

你可以使用 `umount` 命令卸载已挂载的文件系统。

```bash
root@pasha ~# ummount /home/project2
```

## 8.2. 显示挂载的文件系统

要显示所有挂载的文件系统，请执行 `mount` 命令。查看 `/proc/mounts` 和 `/etc/mtab`。

### 8.2.1. mount

查看所有挂载的最简单常用的方法是不带任何参数地执行 `mount` 命令。

```bash
root@RHEL4 ~# mount | grep /dev/sdb
/dev/sdb1 /home/project42 ext2 (rw)
```

### 8.2.2. /proc/mounts

内核以文件形式在 `/proc/mounts` 提供信息，但 `/proc/mounts` 在任何硬盘上都不作为文件存在。查看 `/proc/mounts` 是直接查看来自内核的信息。

```bash
root@RHEL4 ~# cat /proc/mounts | grep /dev/sdb
/dev/sdb1 /home/project42 ext2 0 0
```

### 8.2.3. /etc/mtab

`/etc/mtab` 文件不由内核更新，而是由 `mount` 命令维护。不要手动编辑 `/etc/mtab`。

```bash
root@RHEL4 ~# cat /etc/mtab | grep /dev/sdb
/dev/sdb1 /home/project42 ext2 0 0
```

### 8.2.4. df

查看挂载文件系统的用户友好的方法是 `df`。`df` (disk free) 命令增加了每个挂载磁盘可用空间的好处。像许多 Linux 命令一样，`df` 支持 `-h` 选项，使输出更易读。

```bash
root@RHEL4 ~# df
Filesystem             1K-blocks      Used Available Use% Mounted on
/dev/mapper/VolGroup00-LogVol100
  11071922     6366996 4746240  58 % /boot
/dev/sda              1019886     9300     86567  10 % /dev/shm
none                   127988        0     127988   0 %
/dev/sdb1             108865     1550    101694   2 % /home/project2

root@RHEL4 ~# df -h
Filesystem            Size Used Avail Use% Mounted on
/dev/mapper/VolGroup00-LogVol100
  120G     6.1G  4.6G   58 % /boot
/dev/sda               125M      0     125M   0 % /dev/shm
none
/dev/sdb1             107M     1.6M    100M   2 % /home/project2
```

### 8.2.5. df -h

在 `-h` 示例中，你可以看到特定挂载点的容量、可用空间、GB 和百分比。

```bash
root@Laika:-# df -h | egrep "(sdb2|File)"
Filesystem            Size Used Avail Use% Mounted on
/dev/sdb2               92G     83G    91 % /media/sdb2
```

### 8.2.6. du

`du` 命令可以显示文件和目录的磁盘占用。通过对挂载点运行 `du`，你可以有效地获取文件系统的磁盘空间。

虽然 `du` 可以递归显示每个子目录，但 `-s` 选项会提供目录摘要。该选项通常与 `-h` 配合使用。这意味着在挂载点上运行 `du -sh` 可以获得该分区文件系统使用的总量。

```bash
root@debian-6# du -sh /srv/wolf
  6.2M /boot
  1.1T /srv/wolf
```

## 8.3. 从开始到结束

下面的截图显示了从检测硬件 (`/dev/sdb`) 直到在 `/mnt` 上进行监控的总结路线图。

```bash
[root@centos65 ~]$ dmesg | grep '\[sdb\]'
sd 3:0:0: [sdb] 150994944 512-byte logical blocks: (77.3 GB/72.0 GiB)
sd 3:0:0: [sdb] Write Protect is off
sd 3:0:0: [sdb] Mode Sense: 00 3a 00 00
sd 3:0:0: [sdb] Write cache: enabled, read cache: enabled, doesn't support \
Qdepth 308
```
