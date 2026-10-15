
在你创建好要放入 CD-ROM 的镜像后，你需要将镜像发送到 CD 写入器。你必须知道 CD 写入器的精确位置，`cdrecord` 程序可以确定这一点（此处使用 `-scanbus` 所示）：

```bash
# cdrecord -scanbus
cdrecord 1.8 (i586-linux-gnu) Copyright (C) 1995-2000 Jörg Schilling
Using libscg version '0.1'
Total extents actually written = 126318
Total translation table size: 0
Total rockridge attributes bytes: 0
Total directory bytes: 0
Path table size(bytes): 10
Max brk space used 9024
126318 extents written (246 Mb)
```

在 `mkisof` 从数据文件创建镜像后，你会看到文件创建的统计信息。最终，它会告诉你文件的大小。这是底线。确保输出的长度（下例中的粗体部分）小于 650MB，因为那是 CD-ROM 能容纳的所有容量。

```
Total extents actually written = 126318
Total translation table size: 0
Total rockridge attributes bytes: 0
Total directory bytes: 0
Path table size(bytes): 10
Max brk space used 9024
126318 extents written (246 Mb)
```

# 从崩溃的系统中恢复

如果你的系统由于硬件故障、文件损坏或任何原因而崩溃，你需要知道如何恢复你的系统。通常，让系统重新运行的唯一助力是获得对该系统的访问。现在就是使用你为系统保存的启动盘的时候了。

要使用你的内核创建启动盘（如果你对内核进行了修改），请向软驱器中插入一张空白且已格式化的磁盘。在 root 用户下执行以下三条命令：

```
dd if=/vmlinuz of=/dev/fd0
rdev /dev/fd0
rdev -R /dev/fd0 1
```

这与你首次在计算机上安装 Debian 并被要求创建启动盘时发生是一样的。

将启动盘插入软驱器并开启电脑。（确保 BIOS 已设为优先从软驱启动。）此磁盘会绕过硬盘上的 LILO 启动信息，但它仍然会引导到你的系统。然后你可以修复任何影响 LILO、内核或任何初始启动参数的问题。

## 救援盘启动选项

当你使用书中附带的安装光盘或从 Debian 软盘镜像创建的救援盘启动计算机时，在启动提示符处会有一些选项。

按下 F1 列出帮助键。按下 F3 显示启动 linux、ramdisk、软驱或 rescue 的不同方式。按下 loading 启动该过程。如果你已经加载了系统，请将其作为最后的手段。首先尝试使用 rescue 并将其指向根分区，如下所示：

```
boot: rescue=/dev/root own
```

这会启动文件系统并建立 shell，你可以在其中开始修复任何错误。如果这不起作用，请尝试使用软驱重启。这应该加载一个小型环境，你在该环境中拥有有限的控制权。

你还可以使用救援盘启动系统并进入 single。这会将你带单用户模式。你拥有系统的 root 权限来检查硬件、进行测试，并确定让你的系统正常运行需要哪些更改。

## 修复磁盘问题

如果磁盘出现问题，你可以检查文件系统是否存在任何错误。`e2fsck` 程序会在磁盘上执行此检查。它会扫描磁盘的物理错误、错位数据以及任何其他问题。DOS 的对应程序是 `chkdsk`；对于 Windows，使用 `scandisk`。以下是该命令的语法：

```
e2fsck [options] filesystem
```
