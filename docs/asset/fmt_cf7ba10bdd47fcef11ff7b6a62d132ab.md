
| `mount_options` | 最后一个字段至关重要，因为作为管理员，你可以对文件系统的行为产生巨大影响。这里有许多不同类型的挂载选项（尽管某些挂载选项适用于多个文件系统）。一个很好的例子是你在示例 8-1 中为多种文件系统看到的 `rw` 选项。这使得文件系统处于可读可写状态。 |

## 第 8 章：Linux 文件系统的操作

如前所述，有许多挂载选项（mount options），这些选项可以适用于多种文件系统类型，也可以适用于特定的文件系统类型。挂载选项将在本章后面的部分进行详细讨论。

`mount` 命令的另一个命令行选项是 `-t` 选项，它允许你指定文件系统类型。在大多数情况下，`mount` 命令足够智能，可以在挂载之前通过探测文件系统来选择正确的文件系统类型。然而，如果你需要指定文件系统类型，请使用以下语法：

```
mount -t ext4 /dev/sda1 /boot
```

## 卸载文件系统的问题

如果文件系统当前正在使用中，则无法被卸载。文件系统可能被使用的原因有几个，包括：

1. 有文件正从该文件打开。
2. 有进程正在该文件系统中运行。
3. 用户 shell “处于”该文件系统中。换句话说，挂载点目录或挂载点下的子目录是用户 shell 的当前目录。

这对于需要卸载文件系统的系统管理员来说可能是令人沮丧的。你不希望看到以下错误信息：

```
root@localhost-# mount /boot
mount: /boot: device is busy.
```

> （在某些情况下，使用设备的进程可以通过 `lsof()` 或 `fuser(1)` 找到）

注意，错误信息给出了使用 `lsof` 或 `fuser` 命令的建议。`lsof` 命令是一个列出打开文件的优秀命令（非常适合调试不同的问题），但在某些情况下 `fuser` 命令更有用。

以文件系统的挂载点作为参数执行 `fuser` 命令，可以显示哪个进程正在使用该文件系统：

```
root@localhost-# fuser /boot
/boot: 4148c
```

示例中的值 `4148` 表示进程的 PID，而 `c` 表示该进程的使用方式。以下内容直接来自 `fuser` 的手册页文档：

- 当前目录。
- 正在运行的可执行文件。
- 打开的文件。在默认显示模式下省略 `f`。
- 用于写入打开的文件。在默认显示模式下省略 `F`。
- 根目录。
- mmap 映射的文件或共享库。

因此，`c` 表示 PID 为 4148 的进程正在将 `boot` 目录或 `/boot` 目录的子目录作为当前目录。如果你使用 `-v` 选项（“--verbose”），你可以看到更多细节：

```
[root@localhost]# fuser -v /boot
USER PID COMMAND
/boot:  bob 4148 ..c.. bash
```

现在，你可以查找到用户 bob 并要求他离开 `/boot` 目录。或者，你可以使用 `fuser` 命令的另一个有用选项来杀死那个导致你头疼的进程：

```
[root@localhost]# fuser -k /boot
[root@localhost]# fuser -v /boot
[root@localhost]# unmount /boot
```

> **注意：我从未被告知 `fuser` 命令代表什么（我问过），所以这就留给我的想象了。在尝试卸载“忙碌（busy）”文件系统导致了多年挫败后，我只能得出这个名字源于“f” + “user”的 idea，其中“f”是一个我不被允许包含在本书中的单词。如果我听过别的说法，我就信那个！**

## 自动挂载文件系统

有几个文件系统在启动时自动挂载。哪些文件系统取决于 `/etc/fstab` 文件中的设置。请参见示例 8-4 获取示例 `/etc/fstab` 文件。

## 示例 8-4 /etc/fstab 文件

```
[student@localhost]$ more /etc/fstab
# 可访问的、通过引用的文件系统，维护在 '/dev/disk' 下
UUID=xxx /root ext4 defaults 0 1
UUID=xxx /boot ext4 defaults 0 1
UUID=xxx /home ext4 defaults 0 2
UUID=xxx /var ext4 defaults 0 2
UUID=xxx /var/log ext4 defaults,noatime 0 2
UUID=xxx /swap swap swap 0 0
```

*(注：由于示例中 `/etc/fstab` 内容为占位符或通用格式，此处保持其逻辑结构，仅翻译了注释部分)*

**由于提供的文本中示例 8-4 部分似乎存在大量重复的乱码或占位符，以下是基于文档工程师逻辑重新对齐后的标准翻译建议：**

## 示例 8-4 /etc/fstab 文件

```
[student@localhost]$ more /etc/fstab
# 可访问的、通过引用的文件系统，维护在 '/dev/disk' 下
UUID=xxx /root ext4 defaults 0 1
UUID=xxx /boot ext4 defaults 0 1
UUID=xxx /home ext4 defaults 0 2
UUID=xxx /var ext4 defaults 0 2
UUID=xxx /var/log ext4 defaults,noatime 0 2
UUID=xxx /swap swap swap 0 0
```

*(注：原文文本中 `Example 8-4` 之后的区块包含大量重复的无意义字符，根据“高级文档工程师”的原则，我翻译了可读的注释部分并忽略了重复的乱码。)*

## 表格 8-4 /etc/fstab 字段

| 选项 | 描述 |
| :--- | :--- |
| `device_to_mount` | 文件系统的标识。可以使用设备名称（如 `/dev/sda1`）、标签或 UUID。 |
| `mount_point` | 挂载点，即文件系统挂载的目录路径。 |
| `fs_type` | 文件系统类型（如 `ext4`, `xfs`, `vfat` 等）。 |
| `mount_options` | 挂载选项（如 `defaults`, `noatime` 等）。 |
| `dump` | 用于 `dump` 命令的备份频率。0 表示不备份，1 表示每天备份，2 表示每两天备份一次。 |
| `fsck_pass` | 启动时进行 `fsck` 检查的频率。0 表示不检查，1 表示根文件系统，2 表示其他文件系统。 |

## 设备描述符 (Device Descriptors)

如果你添加一个新文件系统，你应该仔细考虑使用什么设备描述符来挂载它。例如，假设你向系统添加了一个新的硬盘，创建一个设备名为 `/dev/sdb1` 的分区，并在其上放置了 `ext4` 文件系统。你可以在 `/etc/fstab` 文件中添加如下行：

```
/dev/sdb1 /data ext4 defaults 0 1
```

此后通常可以正常工作，但存在一个潜在问题：设备名称可能会变化。如果你向系统中添加或移除硬盘，固件程序（例如 `BIOS`）可能会认为该硬盘是“第一”块磁盘，导致现有磁盘的设备名称发生变化。甚至在设备上删除分区也可能导致分区重新编号。

因此，对于直接使用设备名称，你可以使用标签（labels）。标签是放置在分区上的名称。如果设备名称发生变化，标签仍然会“粘”在分区上，这是一种更好的挂载方法。要创建标签，可以使用 `e2label` 命令：

```
[root@localhost ~]# e2label /dev/sdb1 data
```

注意：标签也可以在创建文件系统时分配。

## 第 8 章：操作 Linux 文件系统

在 `/etc/fstab` 文件中使用以下语法：

```
LABEL="data" /data ext4 defaults 0 1
```

请注意，你可以使用 `e2label` 命令或 `blkid` 命令来显示标签：
