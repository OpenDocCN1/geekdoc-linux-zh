
# 第 9 章系统初始化与 X Windows

```
[root@server1 root]# lilo
Added linux *
[root@server1 root]# _
```

> 要从活动分区或 MBR 卸载 LILO，你可以使用 `lilo -U` 命令。

尽管 LILO 是一个健壮的引导程序，但它可能会遇到错误并无法正常加载；如果发生这种情况，你会收到一个指示问题性质的错误代码。表 9-2 列出了 LILO 错误消息和可能的解决方案。

| 错误消息 | 描述 |
| --- | --- |
| L | LILO 引导程序的第一部分加载失败，通常由于硬盘参数不正确。重启机器有时可以解决此问题；你可能还需要 `/etc/lilo.conf` 中添加 `"linear"`。 |
| LI | LILO 引导程序的第二部分加载失败或缺少 `/boot/boot.b` 文件。在 `/etc/lilo.conf` 中添加 `"linear"` 可能解决问题。 |
| LIL? | LILO 已正确加载但找不到运行所需的某些文件，例如 `/boot/map` 和 `/boot/boot.b`。在 `/etc/lilo.conf` 中添加 `"linear"` 可能解决问题。 |

> 对于使用扩展固件接口 (EFI) 的 Intel Pentium 和 Itanium 计算机提供了 ELILO 版本，可以在 http://sourceforge.org/projects/elilo/ 下载。

## GRUB

通用统一引导程序 (`GRUB`) 类似于引导程序，且比 LILO 引导程序更新。`GRUB` 引导程序的第一部分（称为 Stage1）位于主引导记录（MBR）；引导程序的其余部分（称为 Stage1.5 和 Stage2）位于 `/boot` 目录。`GRUB` Stage1 直接指向 Stage1.5，加载文件系统并加载 `GRUB` Stage2。`GRUB` Stage2 执行实际引导并显示如图 9-2 所示的图形引导界面。与 LILO 类似，`GRUB` 的配置是通过编辑文件实现的；但在编辑此文件后不需要重新安装 `GRUB`。

```
GNU GRUB version 0.94 (64K lower / 512K upper memory)
Fedora Core (2.6.5-38)
使用 f 和 j 键选择高亮项。
按回车启动选定的操作系统，按 'e' 在启动前编辑内核参数，或按 'c' 进入命令行。
高亮项将在 5 秒后自动启动。
```

图 9-2 GRUB 启动界面

```
[root@server1 root]# cat /boot/grub.conf
## grub.conf 由 anaconda 产生
# 注意：更改此文件后无需重新运行 grub
## 你有一个 /boot 分区。这意味着所有内核和 initrd 路径都是相对于 /
# root (hd0,0)
kernel vmlinuz-version root=/dev/hda1
initrd /initrd-version.img
boot=0
timeout=10
splashimage=...
title Fedora Core (2.6.5-358)
root (hd0,0)
kernel /boot/vmlinuz-2.6.5-358 root=/dev/sda1 quiet
initrd /boot/initrd-2.6.5-358.img
[root@server1 root]# _
```

![](img/9ee5f91f3446575a1e6ce62c54cae5d2_407_0.png)

或者，你可以查看并编辑 `/etc/grub.conf` 文件，它只是 `/boot/grub.conf` 的符号链接。

> 要理解 `/boot/grub.conf` 文件中的项目，你必须首先理解 `GRUB` 如何引用硬盘上的分区。硬盘通过以下格式的数字识别：`(hd<驱动器#>,<分区#>)`。因此，前面的 `/boot/grub.conf` 文件中的 `(hd0,0)` 分系统的第一个硬盘（无论它是 SCSI 还是 IDE）以及该硬盘上的第一个分区。同样，第一个硬盘上的第二个分区称为 `(hd0,1)`，第三个硬盘上的第四个分区称为 `(hd2,3)`。

此外，`GRUB` 将包含 `GRUB` 引导程序 Stage2 的分区称为根分区。通常，`GRUB` 根分区是包含 `/boot` 目录的文件系统，不应与 Linux 根文件系统混淆。如果你的系统有一个挂载到 `/boot` 的独立分区，`GRUB` 会引用文件 `/boot/grub/grub.conf`。如果系统没有独立的 `/boot` 文件系统，则简单称为 `/boot/grub.conf`。

因此，之前显示的 `/boot/grub.conf` 示例显示了图形启动 `splashimage=(hd0,0)/boot/grub/splash.xpm.gz`，并在第一个硬盘上启动默认操作系统内核（在 10 秒内 `(default=0)` `(timeout=10)`）。默认操作系统内核位于 `GRUB` 根文件系统 `(hd0,0)`，被称为 `/boot/mlinux-2.6.5-358.img`。

内核最初将 `/dev/hda1` 根文件系统挂载为只读，以避免 `fsck` 命令的问题，并使用 ramdisk 镜像加载启动时需要的模块 (`initrd /boot/initrd-2.6.5-358.img`)。

将适当的关键字传递给 `/boot/grub.conf` 中的内核行。或者，你可以添加一行使用 `append=` 关键字的内容，其语法与 `/etc/lilo.conf` 中的 `append=` 关键字相同。

![](img/9ee5f91f3446575a1e6ce62c54cae5d2_407_1.png)

如果启用了密码，如果你想操作启动过程，需要在类似于图 9-2 所示的第一个图形 `GRUB` 界面上按 `p` 键。接受密码后，你可以按 `e` 从 `/boot/grub/grub.conf` 编辑配置（如图 9-3 所示），或按 `c` 获取 `grub>` 提示符。

```
GNU GRUB version 0.94 (64K lower = 64512K upper memory)
root (hd0,0)
  kernel /boot/vmlinux-2.6.15-358 root=LABEL=\-
initrd /boot/initrd-2.6.15-358.img
```

使用 `i` 和 `j` 键选择高亮的条目；

按 `b` 启动，按 `e` 编辑启动序列中的选定命令，按 `c` 进入命令行，按 `o` 在选定行之后打开新行（`^` 表示在之前），按 `d` 删除选定行，或按 `escape` 返回主菜单。

![](img/9ee5f91f3446575a1e6ce62c54cae5d2_408_0.png)

# 图 9-3 配置 GRUB 引导加载界面

如果你选择打开 `grub>` 提示符，可以输入各种命令来查看系统硬件配置、查找并显示文件、修改 `GRUB` 配置或启动操作系统内核。要在 `grub>` 提示符下查看所有可用命令，只需在此界面输入 `help`，如图 9-4 所示。

`grub` 提示符也可以按照 `/boot/grub/grub.conf` 所示的方式启动系统；要启动之前示例中使用的 Linux 操作系统，你只需在 `grub>` 提示符处输入 `/boot/grub/grub.conf` 中的内核和 `initrd` 行（每行后按回车），然后输入“boot”单词并再次按回车继续启动过程。

请记住，在安装期间你要求选择 `GRUB` 引导加载程序。无论如何，在安装后你可以随时从 `GRUB` 切换到 LILO 反之亦然。要安装 LILO，你需要在命令行提示符处使用 `lilo`，LILO 引导加载程序将根据 `/etc/lilo.conf` 文件的配置进行安装，如前面的节。然而，要安装 `GRUB` 引导加载程序，必须使用 `grub-install` 命令。要在第一个 IDE 硬盘的主引导记录（MBR）中安装 `GRUB` Stage 1，你可以输入以下命令：

```
[root@server1]# grub-install /dev/hda
Installation finished. No error reported.
```
