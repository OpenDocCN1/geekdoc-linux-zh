
## 4.8. 文件系统

### 4.8.3 应该使用哪种文件系统？

通常使用许多不同的文件系统并没有意义。目前，`ext2fs` 是最流行的，它可能可能是最明智的选择。根据账本结构的开销、速度、（感知的）可靠性、兼容性以及其他原因，使用另一个文件系统可能是建议的。这需要根据具体情况决定。

### 4.8.4 创建文件系统

文件系统是通过 `mkfs` 命令创建（即初始化）的。实际上，每种文件系统类型都有一个独立的程序。`mkfs` 只是一个前端，根据所需的文件系统类型运行相应的程序。通过 `-t fs` 选项选择类型。

`mkfs` 调用的程序命令行界面略有不同。下面列出了常用且重要的选项：更多信息请参阅帮助手册页。

- `-t ftype` 选择文件系统的类型。
- `-c` 查找坏块并据此初始化坏块列表。
- `-l filename` 从文件 `filename` 读取初始块列表。

要在软盘上创建一个 `ext2` 文件系统，需要执行以下命令：

```bash
$ fdformat -n /fd0H1440
Double-sided, 80 tracks, 18 sec/track. Total capacity 1440 kB.
Formatting ... done
$ badblocks -dev/fd0H1440 > bad-blocks
$ mkfs -t ext2 -l bad-blocks /dev/fd0H1440
mke2fs 0.5a, 5-Apr-94 for EXT2 FS 0.5, 94/03/10
360 inodes, 1440 blocks
72 blocks (5.0%) reserved for the super user
First data block=1
Block size=1024 (log=0)
Fragment size=1024 (log=0)
1 block group
8192 blocks per group, 8192 fragments per group
360 inodes per group
Writing inode tables: done
Writing superblocks and filesystem accounting information: done
$
```

首先，格式化了软盘（`-n` 选项防止了验证，即坏块检查）。然后使用 `badblocks` 查找坏块，并将输出重定向到文件 `bad-blocks`。最后，创建文件系统，并用 `badblocks` 找到的任何结果初始化块列表。`mkfs` 可以使用 `-c` 选项代替使用 `badblocks` 和单独的文件。下面的示例就是这样做的。

```bash
$ mkfs -t ext2 -c /dev/fd0H1440
mke2fs 0.5a, 5-Apr-94 for EXT2 FS 0.5, 94/03/10
360 inodes, 1440 blocks
72 blocks (5.0%) reserved for the super user
First data block=1
Block size=1024 (log=0)
Fragment size=1024 (log=0)
1 block group
8192 blocks per group, 8192 fragments per group
360 inodes per group
Checking for bad blocks (read only): done
Writing inode tables: done
Writing superblocks and filesystem accounting information: done
$
```

`-c` 比单独使用 `badblocks` 更方便，但在文件系统创建后，`badblocks` 对于检查是必不可少的。在硬盘或分区上准备文件系统的过程与软盘相同，只是不需要格式化。

### 4.8.5 挂载与卸载

在挂载文件系统之前，必须先挂载。挂载操作是让文件系统看起来像一个目录。每当有人试图查看 `proc` 文件系统的任何部分时，内核都会让该部分看起来存在于某处，尽管它实际上。因此，尽管有一个数兆的 `/proc/kcore` 文件，它也没有占用任何磁盘空间。
