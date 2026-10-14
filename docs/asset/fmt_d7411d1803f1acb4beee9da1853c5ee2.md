
```
earth:  # dd if=/dev/yyyy of=New-File bs=512 count=1
earth:  # dd if=Backup-Date of=/dev/yyyy
```

- 如果 `LILO` 位于 `zzz` 的 `MBR` 中（例如 `hda`、`sda`）：

```
earth:  # dd if=/dev/zzz of=New-File bs=512 count=1
earth:  # dd if=Backup-Date of=/dev/zzz bs=446 count=1
```

最后一条命令是“谨慎”的，不会覆盖分区表。再次强调，*不要忘记*：使用 `fdisk` 将所需的启动分区标记为*可引导*。引导扇区备份做起来又快又简单。我们建议经常这样做。

## 创建 Linux 启动盘

Linux 启动盘（有些简化地说）由一个或多个 Linux 内核组成，可能由 `LILO` 管理。即使无法直接从硬盘启动（可能原因：`MBR` 被覆盖、引导管理器配置错误、安装时出错），它也能用来启动你的系统。

这样的启动盘*只*加载内核。其余一切，包括可正常工作的系统程序和 `init` 启动脚本，都必须由硬盘上的安装来提供。启动盘与硬盘上系统之间的联系，是通过在内核中将相关根分区设置为根设备来建立的。

不要将此与用于安装和紧急情况的 SuSE 启动盘混淆。要创建新的 SuSE 启动盘，请将 SuSE CD-ROM 的 `disks` 目录中的相应映像复制到软盘上（参见第 285 页的*SuSE 救援系统*一节）。

## 不带 LILO 的启动盘

通常，如果硬盘控制器的支持已经集成到内核中，那么你的内核*不*需要任何额外的、带有硬件信息的命令行。创建启动盘最简单的方法，就是将实际内核写入原始磁盘并调整根设备（如果之前还没有这样做的话）。

```
earth:  # /sbin/badblocks -v /dev/fd0 1440
earth:  # dd if=my_kernel of=/dev/fd0 bs=18k
earth:  # rdev /dev/fd0 my_root_partition
earth:  # rdev -R /dev/fd0 1
```

最后一条命令确保内核最初以只读方式挂载根目录（启动脚本期望如此）。

## 带 LILO 的启动盘

通过将完整的 `LILO` 引导启动机制传输到软盘上，可以创建一个功能更强大的启动盘，带有欢迎提示符和内核参数（参见第 93 页的*LILO 的组成*一节）。为此，软盘需要一个文件系统。`Minix` 文件系统最适合这一用途。

为此，请按以下步骤操作：

- 在一张全新且空白的软盘上创建 `Minix` 文件系统，然后使用以下命令将软盘挂载到 `/mnt`：

```
earth:  # /sbin/mkfs.minix -c /dev/fd0 1440
earth:  # /bin/mount /dev/fd0 /mnt
```

如果软盘驱动器支持更高容量，可以尝试其他值，例如 `/dev/fd0u1722` 或 `1722`。

- 现在，将你的内核文件和 `LILO` 文件 `/boot/boot.b` 复制到 `/mnt`（即软盘）上。

- 可选：创建消息文件 `/mnt/message`。

- 在 `/mnt` 上创建 `lilo.conf`。— 用实际的根分区替换 `Your_Root_Device`。示例见文件 6。

```
# LILO Configuration file bootdisk
# Start LILO global Section
boot=/dev/fd0                 # Installation: Floppy
install=/mnt/boot.b           # Of course LILO and
map=/mnt/map                  # map fit onto floppy!
message=/mnt/message          # optional
prompt
timeout=100      # Wait at prompt: 10 s
vga = normal     #
# End LILO global section

# Linux bootable partition config begins
image = /mnt/vmlinuz           # default
      root = /dev/Your_Root_Device  # Here is your root partition!
      label = linux
# Linux bootable partition config ends
```

*文件 6：用于启动盘的 lilo.conf*

- 如果使用 `initrd`，请按照第 278 页*引导加载程序*一节中的说明将其添加到 `lilo.conf`。

- 使用这个 `lilo.conf` 安装 `LILO`：

```
earth:  # /sbin/lilo -C /mnt/lilo.conf
```

- 卸载软盘

```
earth:  # /bin/umount /mnt
```

- 在下次系统启动时检查你的启动盘，以验证其是否正常工作。

## 示例配置

如果 Linux 是你机器上唯一的操作系统，那么就无需再做任何事了。所有必需的步骤都已被 YaST 完成。以下各节给出了一些面向多系统计算机的示例配置。更多信息可以在 `/usr/share/doc/howto/en/mini/Linux+*.gz` 下找到。

## DOS/Windows 95/98 与 Linux

*要求：* `DOS`/`Windows 95`/`98` 和 `Linux` 各自至少需要一个主分区位于 1024 柱面限制以下（第 94 页的*LILO 位置*一节）。

对于这种情况，我们已经讨论过一种配置（第 97 页的文件 3）——只需调整 `root`、`image` 和其他设置。`LILO` 安装在 `MBR` 中。

保存好你的 `/etc/lilo.conf`，并确保你有一张 Linux 启动盘。`Windows 95`/`98` 尤其倾向于清除“外来”的 `MBR`。如果你仍然可以用启动盘引导 Linux，那么这个问题很快就能用以下命令解决：

```
earth:  # /sbin/lilo
```

这样就完成了你的 `LILO` 安装。

## 同一块硬盘上的 Windows NT 与 Linux

1. 如果 `Windows NT` 和 `Linux` 需要共存于同一块硬盘上，请使用 `NT` 引导管理器进行引导。它既可以启动内核映像，也可以启动引导扇区本身。执行以下步骤可为 `Linux` 与 `Windows NT` 的和平共处做好一切准备：

- 安装 `NT`。

- 分区 `NT` 磁盘（使用 `FAT` 以便 `Linux` 可以写入）。

- 按常规安装 `Linux`（在本示例中，根分区位于 `/dev/sda3`）。挂载 `DOS` 分区或无错误的 `DOS` 软盘（例如，挂载到 `/dos`）。

- 安装 `LILO`，但将其安装在 `Linux` 的根分区（`/dev/sda3`）中，而不是 `MBR`（`/dev/sda`）中。你仍然可以为 `LILO` 配置一组 `Linux` 内核。以下文件展示了 `lilo.conf` 的示例。

```
# LILO Configuration file
# Start LILO global Section
boot=/dev/sda3        # Target of installation
backup=/boot/boot.sda3.970428    # Backup previous boot sector;
                                # 28. Apr 1997

prompt
timeout=100           # Wait at prompt: 10 s
vga = normal          # force sane video state
# End LILO global section
# Linux bootable partition config begins
image = /vmlinuz      # default image to boot
    root = /dev/sda3 # Here the root partition!
    label = Linux
# Linux bootable partition config ends
```

编辑 `lilo.conf` 后，使用 `/sbin/lilo` 按常规安装 `LILO`。

- 将 `LILO` 启动扇区复制到 `NT` 可以找到的位置。例如，

```
earth: # /bin/dd if=/dev/sda3 bs=512 count=1 of=/dos/bootsect.lin
```

此步骤以及以下步骤必须在每次内核更新后执行。
