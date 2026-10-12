
现在查看单独的段落。Hardy Heron 版本引入了通用标识符 (`UUID`)，它与为特定目录配置的分区、RAID 设备或逻辑卷相关。（有关 `UUID` 的更多信息请参阅第 5 章。）

`title` 指定了 GRUB 主菜单中显示的内容：

```
title kernel 2.6.24-16-server
```

`root (hd0,0)` 指令指定包含 `/boot` 目录文件的分区：

```
root (hd0,0)
```

在这种情况下，它是硬盘的第一个分区。（如果是 `root (hd1,2)`，则是第二个硬盘的第三个分区。）`root (hd0,0)` 指令与 `root (hd1,2)` 不同（此处原文表述可能有误，意指路径不同）。

第三行 `root` 指令 `root (hd0,0)`。

`kernel` 指令指向 Linux 内核文件名，相对于 `root (hd0,0)`。`root` 指令指定了挂载顶层根目录 (`/`) 的 `UUID`、分区、标签或逻辑卷。这些选项在第 5 章中有详细介绍。`ro` 意味着该顶层根目录 (`/`) 以只读方式挂载，直到系统读取 `/etc/stab` 配置文件。`quiet` 和 `splash` 选项通过 Ubuntu 屏幕隐藏消息。如果你想在 Ubuntu 系统启动时查看消息，可以删除这两个选项。

```
kernel /vmlinuz-2.6.24-16-server root=UUID=4090 ro
splash
```

最后，加载内存磁盘（简称为 `inittrd`），从上述 `root (hd0,0)` 指令关联的分区加载关联镜像。换句话说，初始内存磁盘文件 `inittrd.img-2.6.24-16-server` 位于 `/boot` 目录。

```
inittrd inittrd.img-2.6.24-16-server
```

Ubuntu 系统的恢复模式 GRUB 菜单选项包含类似的指令段。唯一的区别在于内核命令行。如此处所示，它用 `single` 替换了 `quiet splash`。`single` 选项让 Linux 进入单用户模式，也称为运行级别 1。你可以使用本节之前描述的技术对恢复模式进行密码保护。只需确保带密码的密码指令包含在恢复模式段落中。

```
root (hd0,0)

kernel /vmlinuz-2.6.24-16-server root=UUID=4090 ro single

inittrd inittrd.img-2.6.24-16-server
```

`quiet` 指令在初始内存磁盘加载后抑制消息：

```
quiet
```

### Linux 中 root 的含义

`root` 一词在 Linux 中有多种含义。在 GRUB 中，如 `root (hd0,1)` 这种关联分区指定了 `/boot` 目录。同样在 GRUB 中，内核命令行中的 `root=/dev/vda5` 指令指定了挂载顶层根目录 (`/`) 的分区或设备。`root` 管理用户的家目录是 `/root`，即使 `root` 用户没有密码（这是 Ubuntu 的默认设置），该目录也存在。`root` 提示符（在默认 `bash` 中通常为井号 `#`）表示你正以 `root` 用户身份登录。

## 第 4 章：启动过程与救援模式

作为对比，下一个段落（`stanza`）正如标题所示，与 Novell 的 SUSE Linux 发行版有关。`boot` 目录是第一块硬盘的第八个分区，正如其标题所示。内核命令行引用了 `/boot/mlinuz` 中的内核，这证实了 `/boot` 目录并不位于独立分区上。

```
title SUSE Linux Enterprise Server 10 (/dev/sda8)

root (hd0,7)

kernel /boot/mlinuz root=/dev/sda8 vga=0x314 splash=silent showtopts

initrd /boot/initrd

savedefault

boot
```

SUSE 和 Ubuntu 风格段落之间的差异非常细微：在 SUSE 段落中，根目录 (`/`) 和 `/boot` 目录都在第一块硬盘同一个分区上。由于它没有直接挂载在分区上，内核和初始内存磁盘文件是从 `/boot/mlinuz` 和 `/boot/initrd` 文件中提取的。`vga=0x314` 选项是一种帧缓冲区模式（`framebuffer mode`），在启动过程中使用。关于帧缓冲区模式的更多信息，请参考 http://org/HOWTO/Framebuffer-HOWTO.html；正如 `splash=silent` 所示，启动过程中不会出现 SUSE 启动屏幕。`showopts` 选项是间接的；在指令之前列出的选项在今天通常会被忽略；默认的 `boot` 选项使用该段落中的设置启动启动过程。

欲了解更多信息，请参阅 Red Hat 如何配置 GRUB 段落。以下内容用于启动了我安装的 Red Hat Enterprise Linux 5：

```
title Red Hat Enterprise Linux Server (2.6.18-8.1.8.e15)

root (hd0,2)

kernel /mlinuz-2.6.18-8.1.8.e15 root=LABEL=/ rhgb quiet

initrd /initrd-2.6.18-8.1.8.e15.img
```

`/boot` 目录的显示格式与基于 Ubuntu 的段落相同；在这种情况下，它位于第一块硬盘的第三个分区。由于该分区专门用于 `boot` 目录，内核指令固定了本地目录中指定的内核文件。与 Ubuntu 段落一样，`ro` 表示根目录 (`/`) 在系统启动之前是只读的。该根目录 (`/`) 与 `LABEL=` 标签相关，类似于 Ubuntu 使用 `UUID` 的方式。`rhgb` 选项与 Red Hat 图形启动相关；`quiet` 指令意味着在启动过程中隐藏的消息。

最后，查看 Windows 系统是如何从 GRUB 启动的：

```
title Windows XP Media Center Edition

root (hd0,1)

chainloader +1

boot
```
