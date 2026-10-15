
```
Group 0: (Blocks 1 -- 8192)
  Block bitmap at 4 (+3), Inode bitmap at 5 (+4)
  Inode table at 6 (+5)
  6682 free blocks, 2019 free inodes, 2 directories
Free blocks: 1511-8192
Free inodes: 14-2032
Group 1: (Blocks 8193 -- 16384)
Block bitmap at 8196 (+3), Inode bitmap at 8197 (+4)
Inode table at 8198 (+5)
7932 free blocks, 2031 free inodes, 1 directories
Free blocks: 8453-16384
Free inodes: 2034-4064
Group 2: (Blocks 16385 -- 24576)
Block bitmap at 16388 (+3), Inode bitmap at 16389 (+4)
Inode table at 16390 (+5)
7932 free blocks, 2031 free inodes, 1 directories
Free blocks: 16645-24576
Free inodes: 4066-6096
Group 3: (Blocks 24577 -- 32768)
Block bitmap at 24580 (+3), Inode bitmap at 24581 (+4)
Inode table at 24582 (+5)
7880 free blocks, 386 free inodes, 1 directories
Free blocks: 24889-32768
Free inodes: 7743-8128
Group 4: (Blocks 32769 -- 40960)
Block bitmap at 32772 (+3), Inode bitmap at 32773 (+4)
Inode table at 32774 (+5)
5206 free blocks, 1952 free inodes, 1 directories
Free blocks: 35165-35172, 35763-40960
Free inodes: 8209-10160
Group 5: (Blocks 40961 -- 49152)
Block bitmap at 40964 (+3), Inode bitmap at 40965 (+4)
Inode table at 40966 (+5)
7237 free blocks, 2027 free inodes, 0 directories
Free blocks: 41220, 41917-49152
Free inodes: 10161, 10167-12192
Group 6: (Blocks 49153 -- 57344)
Block bitmap at 49156 (+3), Inode bitmap at 49157 (+4)
Inode table at 49158 (+5)
7932 free blocks, 2031 free inodes, 1 directories
Free blocks: 49413-57344
Free inodes: 12194-14224
Group 7: (Blocks 57345 -- 65536)
Block bitmap at 57348 (+3), Inode bitmap at 57349 (+4)
Inode table at 57350 (+5)
6308 free blocks, 1928 free inodes, 1 directories
Free blocks: 59229-65536
Free inodes: 14329-16256
Group 8: (Blocks 65537 -- 73728)
Block bitmap at 65540 (+3), Inode bitmap at 65541 (+4)
Inode table at 65542 (+5)
7751 free blocks, 2024 free inodes, 1 directories
Free blocks: 65959-65974, 65984-73728
Free inodes: 16263, 16266-18288
Group 9: (Blocks 73729 -- 81920)
Block bitmap at 73732 (+3), Inode bitmap at 73733 (+4)
Inode table at 73734 (+5)
7908 free blocks, 2028 free inodes, 1 directories
Free blocks: 74013-81920
Free inodes: 18293-20320
Group 10: (Blocks 81921 -- 90112)
Block bitmap at 81924 (+3), Inode bitmap at 81925 (+4)
Inode table at 81926 (+5)
7927 free blocks, 2026 free inodes, 1 directories
Free blocks: 82186-90112
Free inodes: 20327-22352
Group 11: (Blocks 90113 -- 98304)
Block bitmap at 90116 (+3), Inode bitmap at 90117 (+4)
Inode table at 90118 (+5)
7932 free blocks, 2031 free inodes, 1 directories
Free blocks: 90373-98304
Free inodes: 22354-24384
Group 12: (Blocks 98305 -- 106496)
Block bitmap at 98308 (+3), Inode bitmap at 98309 (+4)
Inode table at 98310 (+5)
6294 free blocks, 1993 free inodes, 1 directories
Free blocks: 100203-106496
Free inodes: 24424-26416
Group 13: (Blocks 106497 -- 114688)
Block bitmap at 106500 (+3), Inode bitmap at 106501 (+4)
Inode table at 106502 (+5)
7932 free blocks, 2031 free inodes, 1 directories
Free blocks: 106757-114688
Free inodes: 26418-28448
```

要检查磁盘完整性，请使用命令 `e2fsck`。这将告诉你分区是干净的还是非连续的。

```bash
# e2fsck /dev/hda1
```

另一个有用的工具是 `tune2fs`。它允许你调整文件系统。你可以更改对错误的响应（继续、以只读方式挂载或内核恐慌），设置卷标签以及任何其他可以使用 `mke2fs` 创建的参数。但是，你正在处理的是一个活动文件系统。请注意，你可能会导致一些剧烈且可能不想要的结果。

![](img/8ad518fddafc7f5e73715a2604b61d50_96_0.png)

> 切勿在可读写挂载的分区上运行 `e2fsck` 或 `tune2fs`！在使用 `e2fsck` 或 `tune2fs` 之前，请确保备份磁盘上的数据并卸载分区。请记住，你正在更改磁盘本身的配置，并且可能会丢失你的数据。

## 链接

在你的 Linux 系统中，有两种类型的链接可用：`硬链接` 和 `符号链接`（也称为 `软链接` 或 `symlink`）。Inode 在这两种类型的功能中都起着重要作用。`链接` 是文件的“昵称”方式；你可以用多个名称引用同一个文件。以下列表展示了一个名为 `inodes` 的文件、一个 `符号链接` 和一个 `硬链接`。
