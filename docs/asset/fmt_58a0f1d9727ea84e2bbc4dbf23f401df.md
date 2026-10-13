
你可以通过执行 `sudo xfs_admin -l /dev/sda`、`sudo blkid /dev/sda` 或 `sudo lsblk -f /dev/sda` 来确认新标签。

对于扩展文件文件系统，你可以使用 `e2label` 命令来应用标签，并使用 `tune2fs`、`blkid` 和 `lsblk` 命令进行验证。

现在，你可以将 `fstab` 文件中 `/boot` 的 `UUID="c1ff315e-4320-442c-a3c5-36db40b353f2"` 替换为 `LABEL=bootfs`，并按照上述示例卸载并重新挂载 `/boot` 以进行确认。

也可以为在 VDO 或 LVM 卷中创建的文件系统应用标签；但是，不建议在 `fstab` 文件中使用，因为这些逻辑卷的设备文件始终是唯一的，并且在系统重启后保持不变。

# 在启动时自动挂载文件系统

在 `/etc/fstab` 文件中定义的文件系统会在系统启动时自动挂载。该文件必须为每个列出的文件系统包含正确且完整的信息。不完整或不准确的条目可能会导致系统处于意外或无法启动的状态。向此文件添加条目的另一个用处是，你只需要指定要通过 `mount` 命令手动挂载的文件系统的四个属性中的其中一个——块设备名称、UUID、标签或挂载点。`mount` 命令会从该文件中获取其余信息。同样地，你只需要使用 `umount` 命令指定这些属性之一，即可将其从目录层次结构中分离出来。

默认的 `fstab` 文件包含了在安装时创建的文件系统条目。例如，在 `server2` 上，此文件目前有三个条目：

| `/dev/mapper/rhel-root` | xfs defaults | 0 0 |

| `UUID=1c3ff15e-4320-442c-a3c5-36db403b53f2` | `/boot` | xfs defaults | 0 0 |

| `/dev/mapper/rhel-swap` | swap defaults | 0 0 |

> 考试提示：此文件中的任何缺失或无效条目都可能导致系统无法启动。你必须以紧急模式启动系统来修复此问题。确保你理解文件中针对文件系统和交换分区条目的每个字段。

该文件的格式是每行被划分为六列，以识别每个文件系统成功挂载所需的属性。以下是各列包含的内容：

- **第 1 列**：定义文件系统所在的物理或虚拟设备路径，或其关联 UUID 或标签。这里也可以包含网络文件系统的条目。
- **第 2 列**：标识文件系统的挂载点。对于交换分区，使用 "none" 或 "swap"。
- **第 3 列**：指定文件系统类型，如 Ext3、Ext4、XFS、VFAT 或 ISO9660。对于交换分区，使用类型 "swap"。使用 "auto" 代替留给 `mount` 命令确定文件系统的类型。
- **第 4 列**：识别挂载文件系统时使用的一个或多个逗号分隔的选项。参见[表 15-3]() 获取某些选项的描述，咨询 `mount` 命令的手册页或 `fstab` 文件以获取更多选项和细节。
- **第 5 列**：用于 `dump` 工具确定需要转储的文件系统。值为 0（或省略此列）表示禁用此检查。此字段仅适用于扩展文件系统；XFS 不使用它。
- **第 6 列**：表示在启动时在文件系统上运行 `e2fsck`（扩展文件系统类型的文件系统检查和修复工具）的顺序号。默认情况下，内存型、远程和可移动文件系统使用 0，`//` 使用 1，`/boot` 和其他物理文件系统使用 2。0 也可以用于 `/`、`/boot` 以及你不想检查或修复的物理文件系统。此字段仅适用于扩展文件系统；XFS 不使用它。

> 对于 XFS、虚拟、远程和可移动文件系统类型，第 5 列和第 6 列中的 0 没有意义。你不需要为这些文件系统类型添加它们。

该文件是手动编辑的，因此必须小心以避免语法和拼写错误。

# 监控文件系统使用情况

在运行系统中，你经常需要检查文件系统使用情况，以确定挂载的文件系统是否需要扩展空间或清理以产生可用空间。这涉及检查文件系统的已用和可用空间。`df` 命令被用于此目的。它报告已挂载文件系统的使用详情。默认情况下，该命令以 KB 为单位报告数字，除非指定 `-m` 或 `-h` 选项以 MB 或人类可读格式查看大小。

> 此命令可能无法为 VDO 和 Stratis 文件系统产生正确信息。请使用它们自己的工具查看使用情况。

让我们在 `server2` 上带 `-h` 选项运行此命令：

```bash
[user@server2 ~]$ df -h
Filesystem Size Used Avail % Mounted on
devtmpfs 900M 0 900M /
```

# 计算磁盘占用

与 `df` 命令返回整个文件系统的使用信息不同，`du` 命令报告文件或目录占的空间。默认情况下，它以 KB 显示输出；然而，你可以使用 `-m` 或 `-h` 选项以 MB 或人类可读格式查看。此外，你可以使用 `-s` 查看摘要，并使用 `-c` 查看总计。

让我们在 `server2` 上带 `-h` 选项运行此命令：

```bash
[user@server2 ~]$ du -sh /
4.0M  /
```

# 练习 15-1：创建 Ext4、VFAT、XFS 分区

练习中，你将创建三个分区：一个 Ext4、一个 VFAT 和一个 XFS。然后你对它们进行格式化并挂载。

## 1. 初始化第一个分区 (sdb1) 为 Ext4

```bash
[user@server2 ~]$ sudo parted /dev/sdb mkpart primary ext4 0MiB 500MiB
[user@server2 ~]$ sudo mkfs.ext4 /dev/sdb1
Creating filesystem on /dev/sdb1
...
```

## 2. 初始化第二个分区 (sdb2) 为 VFAT

```bash
[user@server2 ~]$ sudo parted /dev/sdb mkpart primary fat32 500MiB 1GB
[user@server2 ~]$ sudo mkfs.vfat /dev/sdb2
Creating a32 filesystem on /dev/sdb2
...
```

## 3. 初始化第三个分区 (sdb3) 为 XFS

```bash
[user@server2 ~]$ sudo parted /dev/sdb mkpart primary xfs 1GB 2GB
[user@server2 ~]$ sudo mkfs.xfs /dev/sdb3
Formatting XFS filesystem /dev/sdb3; done.
```

## 7. 打开 `/etc/fstab` 文件

到文件末尾，使用它们的 UUID 添加文件系统的条目以实现持久化：

```
UUID="681c0535-44e4-4043-8bef-17413c6897f9b" /ext4fs1 ext4 defaults 0 0
UUID="E4BB-B3A5E"               /vfatfs1 vfat defaults 0 0
UUID="eb6bc0e-d73d-4737-adeb-c140b2b8c5cf5" /xfsfs1 xfs defaults 0 0
```

## 8. 使用 `mkdir` 命令为三个文件系统创建挂载点 `/ext4fs1`、vfatfs1 和 `/xfsfs1`

```
[user1@server2 ~]$ sudo mkdir /vfatfs1 /xfsfs1
```

## 9. 使用 `mount` 命令挂载新文件系统

如果文件中存在任何无效或缺失的信息，此命令将失败。

```
[user1@server2 ~]$ sudo mount -a
```

## 10. 使用 `df` 命令查看三个文件系统的挂载状态、可用性以及类型

```
[user1@server2 ~]$ df -HT
```

| `/dev/sdb1` | ext4 | 88M | 1.6M | 80M | 2% | `/ext4fs1` |

| `/dev/sdb2` | vfat | 95M | 0 | 95M | 0% | `/vfatfs1` |

| `/dev/sdc` | xfs | 245M | 15M | 231M | 6% | `/xfsfs1` |

输出验证了三个文件系统的创建状态和可用性。它们已添加到到 `fstab` 文件中以实现持久化。此时重启系统将自动挂载它们。这些文件系统现在可以存储文件。

# 练习 15-2：在 VDO 卷中创建并挂载 XFS 文件系统

此练习应在 `server2` 上以 `user1` 身份执行，并在需要时使用 `sudo`。

在此练习中，你将在 `sdf` 磁盘上创建一个逻辑大小为 16GB 的 VDO 卷（该磁盘的实际大小为 4GB）。你将使用 XFS 文件系统类型初始化该卷，使用其设备文件定义持久化配置，创建挂载点 `/xfsdo1`，将其附加到目录结构中，并验证其可用性和使用情况。
