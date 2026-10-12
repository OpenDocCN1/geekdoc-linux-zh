
```bash
##### mount -t reiserfs -o notail /dev/hda1 /reiserfs
##### cd /reiserfs
##### tar zxvf dbench-1.2.tar.gz
##### cd dbench
##### make
##### date && ./dbench 15 && date
```

```
dbench 的输出

Sat Jun 28 10:28:42 PDT 2003
+..................................................+..
+15 clients started
Throughput 25.8765 MB/sec (NB=32.3456 MB/sec
258.765 MBit/sec)
Sat Jun 28 10:29:59 PDT 2003
```

```bash
##### cd /
##### umount /reiserfs
```

通过添加 `notail` 挂载选项，运行 `dbench` 程序且拥有 15 个客户端的 ReiserFS 文件系统的吞吐量从 21.7191 MBps 增加到 25.8765 MBps。运行程序的时间从 1 分 31 秒缩短到 1 分 17 秒。

### JFS 的调优选项：使用外部日志提速

外部日志可以提高文件系统性能，因为日志更新被保存到一个与对应文件系统不同的分区，从而减少了硬盘寻道的次数。

以下示例通过使用默认选项（即文件系统日志位于卷内部）来建立文件系统的基线。测试程序在日志位于外部设备 `/dev/hdb1` 上时再次执行。

```bash
##### mkfs.jfs /dev/hda1
##### mount -t jfs /dev/hda1 /jfs
```

创建大量元数据更改的 `stress.sh` 脚本展示了使用外部日志的好处。

```bash
#!/bin/sh

for count in $(seq 1 30); do
    echo Count: $count
    mkdir a
    for i in $(seq 1 10000); do
        echo 0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz\xyz > a/$i
    done

    mkdir b
    for j in $(seq 1 10000); do
        ln -s $(pwd)/a/$j b/$j
    done

    rm -fr b
    rm -fr a
done

##### cd /jfs
##### mkdir test
```

如果你想在自己的机器上尝试这个示例，请将 `stress.sh` 脚本放入 `/jfs/test` 子目录中。

```bash
##### date && ./stress.sh && date
```

stress.sh 脚本的输出

```
Sat Jun 28 10:47:27 PDT 2003

Count: 1
Count: 2
...
Count: 30

Sat Jun 28 12:48:35 PDT 2003
##### umount /jfs
```

### 使用 jfs_tune 调优 JFS

`jfs_tune` 可以更改日志的位置。提高文件系统性能的一种方法是将日志移动到外部设备。

第一步是使用 `mkfs.jfs` 在外部设备 `/dev/hdb1` 上创建一个日志。

```bash
##### mkfs.jfs -J journal_dev /dev/hdb1
```

下一步是将该外部日志附加到位于 `/dev/hda1` 上的文件系统。

```bash
##### jfs_tune -J device=/dev/hdb1 /dev/hda1
##### mount -t jfs /dev/hda1 /jfs
##### date && ./stress.sh && date
```

stress.sh 脚本的输出

```
Mon Jun 30 02:42:08 PDT 2003
Count: 1
Count: 2
...
Count: 30
Mon Jun 30 04:39:08 PDT 2003
```

使用外部日志后，测试程序的执行时间减少了 4 分 8 秒。

### XFS 的调优选项

本节的示例展示了为运行 `dbench` 工具而调优 XFS 文件系统的三种方式。第一个示例使用默认设置格式化 XFS 分区，日志位于分区内部。第二个示例使用挂载选项 `logbufsize` 和 `logbsize`。第三个示例使用外部日志以及这两个挂载选项。

#### 使用默认设置

在下面的示例中，XFS 分区被格式化，日志位于分区内部。

```bash
##### mkfs.xfs -f /dev/hda1
##### mount -t xfs /dev/hda1 /xfs
##### cd /xfs
##### tar zxvf dbench-1.2.tar.gz
##### cd dbench
##### make
##### date && ./dbench 30 && date
```

dbench 的输出如下：

```
Fri Jun 27 15:40:52 PDT 2003
.++++30 clients started
Throughput 1.45512 MB/sec (NB=1.8189 MB/sec 14.5512 MBit/sec)
Fri Jun 27 16:34:13 PDT 2003
```

#### 使用 logbufsize 和 logbsize

本节的示例展示了如何使用挂载选项 `logbufsize` 和 `logbsize` 来调优 XFS 文件系统。

`logbufsize` 选项设置内存中保留的日志缓冲区数量。`logbufsize` 的值可以是 2 到 8。对于使用 64KB 块大小创建的文件系统，默认值为 8；对于使用 32KB 块大小创建的文件系统，默认值为 4；对于使用 16KB 块大小创建的文件系统，默认值为 3；对于其他块大小，默认值为 2。当 `logbufsize` 设置为最大值时，可以同时发生更多的事务，并且即使日志正在同步到磁盘，元数据更改仍然可以进行。然而，如果发生崩溃，相对于将 `logbufsize` 设置为较小值，可能会丢失更多的元数据更改。`logsize` 选项设置内存中保留的日志缓冲区大小。

```bash
##### mkfs.xfs -f /dev/hda1
##### mount -t xfs -o logbufsize=8,logbsize=32768 /dev/hda1 /xfs
##### cd dbench
##### date && ./dbench 30 && date
```

dbench 的输出

```
Sat Jun 28 02:01:36 PDT 2003
"....+..........*+..........*+...+*..++++++++...++++++++++30 clients
started ******........................*******
Throughput 1.97025 MB/sec (NB=2.46281 MB/sec
19.7025 MBit/sec)
Sat Jun 28 02:35:05 PDT 2003
```

#### 将日志放置在外部设备上

外部日志可以提高文件系统性能，因为日志更新被保存到一个与对应文件系统不同的分区，从而减少了硬盘寻道的次数。

本节的示例运行 `dbench`，参数与前几个示例相同，但日志被放置在外部设备 `/dev/hdb1` 上。

```bash
##### mkfs.xfs -l logdev=/dev/hdb1,size=32768b -f /dev/hda1
##### mount -t xfs -o logbufsize=8,logbsize=32768,logdev=/dev/hdb1 /dev/hda1 /xfs
```

`mount` 命令可用于检查每个文件系统的挂载选项，如下面的示例所示。

```bash
##### mount

/dev/hdb6 on / type reiserfs (rw)
proc on /proc type proc (rw)
devpts on /dev/pts type devpts (rw,mode=0620,gid=5)
shmfs on /dev/shm type shm (rw)
usbdevfs on /proc/bus/usb type usbdevfs (rw)
/dev/hda1 on /xfs type xfs (rw,logbufs=8,logsize=32768,logdev=/dev/hdb1)
##### cd dbench
##### date && ./dbench 30 && date
```

dbench 的输出
