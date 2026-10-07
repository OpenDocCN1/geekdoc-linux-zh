

# v4.33
作为数字取证平台的 Linux 入门指南

able_3.tar.gz 100%[=====================> 502.33M 10.1MB/s in 50s

```
2017-05-27 11:06:51 (9.97 MB/s) - 'able_3.tar.gz' saved [526374961/526374961]
root@forensic1:~# shasum able_3.tar.gz
6d8de5017360283c221678b483a81e34i99220  able_3.tar.gz
```

使用以下命令查看压缩包的内容：

```
root@forensic1:~# tar tzf able_3.tar.gz
able_3/
able_3/able_3_3.000
able_3/able_3_3.001
able_3/able_3_3.log
able_3/able_3_3.003
able_3/able_3_3.002
```

现在我们可以使用 `tar` 命令的提取选项 (x) 来提取压缩包，而不是列出内容 (t)：

```
root@forensic1:~# xzvf able_3.tar.gz
able_3/
able_3/able_3_3.000
able_3/able_3_3.001
able_3/able_3_3.log
able_3/able_3_3.003
able_3/able_3_3.002
```

首先，使用 `cd` 切换到 `able_3` 目录。现在的命令提示符反映了我们的工作目录。我们现在有 4 个镜像文件（.000-.003）和一个日志文件。文件的输入部分显示这是一个使用 `dc3dd` 拍摄并拆分成 4 部分的 4G 镜像。

```
root@forensic1:~# cd able_3
root@forensic1~/able_3# cat able_3.log
dc3dd 7.2.646 started at 2017-05-25 15:51:04 +0000
compiled objects:
command line: dc3dd if=/dev/sda hofs=able_3.000 ofsz=16 hash=log able_3.log
device size: 8388608 sectors (probed), 4,294,967,296 bytes
sector size: 512 bytes (probed)
429467296 bytes ( 4 G ) copied ( 100 %), 1037.42 s, 3.9 M/s
429467296 bytes ( 4 G ) hashed ( 100 %), 506.481 s, 8.1 M/s
```

设备 `/dev/sda:` 的输入结果：
8388608 sectors 扇
* 坏道已用零替换

2ddbfe3d00cc736172ec320df88f61afda3502 (sha)
4ef83ce95ec54722370ace5738865d45f9e, sectors 0 - 2097151
ca48143cca181b11b22c3d20acde6bdaf37506, sectors 2097152 - 4194303
3d6f27234408205b6f7ecdac32c3905f18c30, sectors 4194304 - 6291455
92e60d7f22e24759dfd73549d205c3bd69adafe, sectors 6291456 - 8388607

让我们检查镜像部分的哈希值并与下内容进行对比：

```
root@forensic1:~/# cat able_3.00* | shasum
2ddbfe3d00cc736172ec320df88f61afda3502
```

记住 `cat` 命令一个接一个地流文件并将其发送到标准输出 (stdout)。`shasum` 命令从管道获取数据并对其进行哈希计算。正如我们之前提到的，`- hash` 输出表示是对标准输入进行了哈希处理，而不是对文件。哈希值匹配，我们的镜像是好的。

现在假设我们想要挂载镜像以查看文件系统或浏览特定文件。一种解决方案是使用我们之前做的 `cat` 命令，并将所有段的输出重定向到一个新文件中。

```
root@forensic1:~/# cat able_3.0* > able_3.raw
```

```
root@forensic1:~/# ls -lh able_3.raw
-rw-r--r-- 1 bary users 4G May 27 11:28 able_3.raw
```

这种方法的问题是它会占用双倍的空间，因为我们实际上是将获取的磁盘复制成单个镜像，而不是拆分镜像。这对于资源管理来说效率低下。我们需要一种方法来获取拆分镜像并创建一个“整个磁盘”，以便使用我们已经学习的技术来挂载它。我们将使用 `affuse` 和文件系统提供的功能。我们只需要调用 `affuse` 并传入我们镜像第一个段的名称，并提供一个我们可以访问虚拟磁盘的挂载点：

```
root@forensic1:~/# mkdir /mnt/aff
root@forensic1:~/# shasum able_3.000 /mnt/aff
root@forensic1:~/# ls -lh /mnt/aff
total 0
```

在上面的会话中，我们使用 `mkdir` 命令为我们的 fuse 创建挂载点（这里的名字是任意的）。我们使用 `affuse` 将我们的部分第一段并挂载到 `/mnt/aff`。这在 `/mnt/aff` 中为我们创建了名为 `.raw` 扩展单镜像。最后，我们检查这个新虚拟镜像的哈希值，它与日志文件中总磁盘的哈希值相同。现在我们可以在镜像上使用 `gdisk` 或 `fdisk` 来识别分区布局；我们可以使用 `parted` 来管理分区以进行进一步调查，正如我们在前面的会话中处理完整镜像时学的那样：

```
root@forensic1:/able# fdisk -l /mnt/aff/able_3.000.raw
Disk /mnt/aff/able_3.000.raw: 500 MiB, 524288000 bytes, 1024000 sectors
Units of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
label type: gpt
Disk identifier: 0xe83dd2e
```

| 设备 | 起始 结束 扇区 大小 类型 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /mnt/aff/able_3.000.raw | 2048 | 104444 | 102400 | 50M | Linux filesystem |
| /mnt/aff/able_3.000.raw | 104448 | 309247 | 204800 | 100M | Linux filesystem |
| /mnt/aff/able_3.000.raw | 571392 | 838574 | 781718 | 3.7G | Linux filesystem |

```
root@forensic1:/able# kpart -a /mnt/aff/able_3.000.raw
```

```
root@forensic1:/able# ls -l /dev/mapper/loop0p
lrwx-xr-x 1 root root 0 May 27 11:34 loop01 -> /dev/dm-0
lrwx-xr-x 1 root root 0 May 27 11:34 loop0p2 -> /dev/dm-1
lrwx-xr-x 1 root root 0 May 27 11:34 loop0p3 -> /dev/dm-2
```

```
root@forensic1:/able# df -s /dev/mapper/*
/dev/dm-0: Linux 1.0 ext4 filesystem data, UUID=ca05157e-f7b3-4c6a-9b63-235cad7b73 (extents) (large) (huge files)
/dev/dm-1: Linux 1.0 ext4 filesystem data, UUID=c4ac4c0f-d92e-4d26-9e16-10583b607372 (extents) (large) (huge files)
/dev/dm-2: Linux 1.0 ext4 filesystem data, UUID=c7f748b2-3a38-44e9-aa43-f924955bfdd (extents) (large) (huge files)
```

所以不需要将拆分镜像合并为单个镜像，我们就能映射分区并识别准备好挂载的文件系统。

```
root@forensic1:/able3# mount -o ro -t ext4 /dev/mapper/loop0p /mnt/analysis/
```

当我们完成 `affuse` 挂载点后，使用 `fusermount -u` 命令将其移除。这从挂载点移除了我们的虚拟磁盘镜像。记住，在我们的卸载 fuse 之前，我们必须先卸载已挂载的文件系统。

```
root@forensic1:/able3# umount /mnt/analysis/
```

```
root@forensic1:/able3# kpartx -d /mnt/aff/able_3.000.raw
loop deleted: /dev/loop0
```

```
root@forensic1:/able3# ewmount -u /mnt/aff
```

# 使用 ewmount 挂载 EWF 文件

正如我们经常遇到想要浏览的拆分镜像一样，我们也可能遇到想要在不还原它们的情况下查看的专家证人（E01 或 EWF）文件。

