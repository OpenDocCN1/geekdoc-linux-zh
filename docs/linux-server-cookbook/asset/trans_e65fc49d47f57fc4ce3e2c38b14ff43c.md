
## 命令 free

| 选项 | 描述 |
| :--- | :--- |
| used | 已用内存（used = total -- free -- buffers - cache） |
| free | 未用内存 |
| shared | 被 tmpfs（一种虚拟内存文件系统）使用的内存 |
| buffers | 被内核缓冲区使用的内存 |
| cache | 被页面缓存使用的内存 |
| buff/cache | buffers 和 cache 的总和 |
| available | 估算可用于新申请的内存量。 |

表 3.3：命令 free 的列

操作系统（不仅限于 Linux）中的内存是一个复杂的话题，需要高级知识来了解内存如何在不同的进程之间预留和共享。列 `free` 和 `available` 提供了系统内存是否耗尽的良好概览。下图展示了一台物理服务器的示例输出：

```bash
root@ubuntu:~# free -h
              total        used        free      shared  buff/cache   available
Mem:           31Gi        11Gi       5,8Gi       2,7Gi        13Gi        16Gi
Swap:          31Gi          0B        31Gi
```

图 3.14：命令 free 以人类可读格式输出的示例

## 命令 df

命令 `df`（disk free）报告文件系统的磁盘空间使用情况。如果没有参数，该命令将显示所有文件系统及其挂载点的信息，并且指定一个参数将限制输出到该文件系统或挂载点。用于过滤结果的常用选项如下：

| 选项 | 选项描述 |
| :--- | :--- |
| -h / --human-readable | 以人类可读格式显示信息，而不是以 KB 显示。 |
| -i / --inodes | 显示分区中的文件数量和可用数量。 |
| -l / --local | 排除已挂载的远程分区。 |
| -t / --type=TYPE | 过滤文件系统列表以匹配指定的 TYPE。 |
| -T / --print-type | 显示文件系统类型。 |
| -x / --exclude-type=TYPE | 过滤文件系统列表以排除指定的 TYPE。 |

表 3.4：命令 df 的常用选项

下图展示了以人类可读格式和文件系统类型信息的示例输出。以下图是虚拟机的示例输出：

```bash
root@ubuntu:~# df -hT
Filesystem            Type   Size  Used Avail Use% Mounted on
tmpfs                 tmpfs  393M  1.2M  392M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv
                     ext4     12G  5.0G  5.7G  47% /
tmpfs                 tmpfs  2.0G     0  2.0G   0% /dev/shm
tmpfs                 tmpfs  5.0M     0  5.0M   0% /run/lock
/dev/vda2             ext4   2.0G  126M  1.7G   7% /boot
tmpfs                 tmpfs  393M  4.0K  393M   1% /run/user/1000
```

图 3.15：命令 df 的输出示例

## 命令 lspci、lsusb 和 lsblk

这三个常用命令用于显示以下信息：

- **lspci**：是显示系统中 PCI 总线信息以及连接到它们的设备的实用工具。通过使用选项 -v、-vv 或 -vvv 可以获取更多信息（更多的 v 表示更详细的输出）。
- **lsusb**：是显示系统中 USB 总线信息以及连接到它们的设备的实用工具。此命令接受选项 -v 以显示更高级的信息。
- **lsblk**：是列出所有可用或指定块设备信息、显示设备的分区、标签和分区 ID 的实用工具。可以指定参数将输出过滤到指定的设备（例如，/dev/sda）。

## 用于列出元素的 CLI 命令

有两个常用命令用于列出和查找系统中的文件、目录、链接或块设备等元素：`ls` 和 `find`。

### 命令 ls

命令 `ls` 列出文件和目录的信息，如果没有指定参数，则列出当前目录。此命令有很多选项；一些最有用选项在下面的表格中描述：

| 选项 | 选项描述 |
| :--- | :--- |
| -a / --all | 显示隐藏文件和目录（以点开头） |
| -c / --color=WHEN | 指示何时给输出上色，可以是 *always*、*auto* 或 *never*。 |
| -d / --directory | 列出目录本身而不是其内容。 |
| -h / --human-readable | 以*人类可读*格式显示大小，使用更可读的单位。 |
| -l | 使用长列表格式，包括所有者、大小和权限。 |
| -r / --reverse | 排序时反转顺序 |
| -R / --recursive | 递归列出子目录。 |
| -S | 按文件大小排序，最大的文件将首先显示。 |
| -t | 按时间排序，最新的文件/目录将首先显示。 |
| -1 | 每行列出一个文件，而不是按列显示（当选项 *-l* 未使用时） |

表 3.5：命令 ls 的常用选项

图 3.16 展示了命令 `ls` 按大小排序（-S）并以反转模式（-r）、使用长格式（-l）和人类可读格式（-h）的输出。

```bash
root@ubuntu:~/examples# ls -lhSr
total 12K
drwxr-xr-x 2 root root 4.0K Jul  3 20:01 example3
drwxr-xr-x 2 root root 4.0K Jul  3 20:27 example2
drwxr-xr-x 2 root root 4.0K Jul  3 20:00 example1
-rw-r--r-- 1 root root 1.0M Jul  3 20:27 file1M.bin
-rw-r--r-- 1 root root 2.0M Jul  3 20:58 file2M.bin
-rw-r--r-- 1 root root   10M Jul  3 20:29 file10M.bin
```

图 3.16：命令 ls 的输出示例

### 命令 find

命令 `find` 在系统中搜索文件、目录或其他对象。如果没有选项和参数，此命令将递归列出当前目录下的所有元素。它强制先指定路径，然后指定过滤表达式。存在多个选项和组合，下表显示了一些最常用的选项：

| 选项 | 选项描述 |
| :--- | :--- |
| -amin n | 文件在 n 分钟前被访问过，或访问次数多于或少于 n 次。 |
| -atime n | 文件在 n*24 小时前最后一次被访问，或访问次数多于或少于 n 次。 |
| -cmin n | 文件在 n 分钟前被修改过，或修改次数多于或少于 n 次。 |
| -ctime n | 文件在 n*24 小时前最后一次被修改，或修改次数多于或少于 n 次。 |
| -mmin n | 文件在 n 分钟前被修改过，或修改次数多于或少于 n 次。 |
| -mtime n | 文件在 n*24 小时前最后一次被修改，或修改次数多于或少于 n 次。 |
| -name pattern | 使用模式过滤文件或目录的名称 |
| -perm mode | 按权限过滤，可用于查找易受攻击的文件 |
| -size n[kMG] | 文件使用的空间少于、多于或恰好 n 个单位。 |
| -type c | 过滤文件类型，部分选项包括：<br>• b：块特殊<br>• c：字符特殊<br>• d：目录<br>• f：文件<br>• l：链接 |
| -user username/userid | 文件属于指定的用户或用户 ID。 |
| -xdev | 不降入其他文件系统上的目录。 |

表 3.6：命令 find 的常用选项

数字 n 可以与 +n（大于 n）、-n（小于 n）一起使用，仅使用 n 表示恰好该值。可以使用选项 -delete、-exec 命令（作为示例）对结果执行不同的操作，或者使用 -ls 或 -print0 等选项格式化输出。下图展示了如何过滤大于 1 MB 的文件：

![](img/863afa537de4eed7deb11978bfbfa90e_98_0.png)

图 3.17：命令 find 的输出示例

## 标准流解释

在 Linux 系统中，当执行命令时，存在三个相关的流：一个是用于数据输入，一个是用于数据输出，一个是用于诊断或错误输出。这些流与一个名称和一个相关的整数关联，如下表所示：

| 整数 | 名称 | 流描述 |
| :--- | :--- | :--- |
| 0 | stdin | 标准输入流，应用程序使用此流接收数据。 |
| 1 | stdout | 标准输出流，使用此流显示信息。 |
| 2 | stderr | 标准错误流，使用此流显示诊断信息或错误。 |

表 3.7：流的信息和相关的整数

当命令需要用户输入数据时，应用程序将使用 stdin 读取用户输入以引入请求的数据。当应用程序向用户返回信息时，它会将其发送到标准输出（stdout），如果有错误或诊断信息需要显示，则会使用标准错误（stderr）。以下插图显示了标准流的信息：

