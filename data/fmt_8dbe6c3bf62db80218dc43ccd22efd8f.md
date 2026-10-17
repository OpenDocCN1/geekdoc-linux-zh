
VFAT 文件系统支持——此选项提供了从 Linux 访问 VFAT 风格长文件名的功能。除了文件名支持发生变化外，VFAT 和 MSDOS 的工作方式相同。

如果你将所有这些选项编译进内核，你可以使用三种文件系统类型之一（`mdos`、`umsdos` 和 `vfat`）来挂载包含 FAT 文件系统的分区，分别对应 MSDOS、FAT 处理和 FAT。这些选项中的第一个和最后一个使用了一系列附加选项（在下一节中描述），来确定文件接收的所有权和权限。`UMDOS` 选项默认采用 MSDOS 行为——8.3 文件名、无权限等。你可以通过使用 `umsync` 命令在目录中使用 UNIX 风格的权限和长文件名，该命令会为目录创建 `..LINUX....UMDOS`。

### 使用挂载点
Linux 提供了大量的挂载选项，可以修改 Linux 处理分区的方式。你可以通过在命令行提示符输入 `man` 并搜索有关各种 FAT 文件系统的信息来学习这些选项。（许多选项列在 `mount` 帮助的 MSDOS 部分。）

一些更有实用的选项包括：

- `-r` 或 `ro`——将文件系统设为只读。Linux 的 FAT 支持相当稳定，此选项的主要用途是保护你免受用户错误或应用程序 bug 的影响。
- `-o uidxxx` 为分区上的所有文件设置用户 ID（UID）。例如，`-uid=502` 将所有文件的 ID 设置为 502。你可以检查 `/etc/passwd` 文件的内容来确定合适的的用户 ID。在文件中找到你想要拥有文件的用户。该 ID 是第三个由冒号分隔的字段。
- `-o gidxxx` 为分区上的所有文件设置组 ID（GID）。此选项的作用与 `-o uid` 选项类似。你可以在 `/etc/group` 文件中找到组及其 ID 编号；组 ID 在每行中第三个被分隔的字段中。
- `-umaskxxx` 为默认权限设置掩码（一种针对不存在的值的位图掩码）。例如，如果你想让用户对分区具有完全访问权限，umask 为 000，即不拒绝任何权限。要拒绝除所有者以外的所有人的访问，请使用 umask 077。
- `-o [conv=b[binary] | conv=t[ext] | conv=auto]` 设置行尾字符的转换选项。微软风格的操作系统在文本文件行尾使用的字符与 UNIX 风格的操作系统（包括 Linux）不同。此选项可以在复制文件时尝试通过在 UNIX 风格和微软风格的行尾编码之间进行转换来解决问题。使用 `t` 将文件转换为 Linux 风格的行尾字符，而 `a` 则将没有已知二进制扩展名的文件转换为行尾字符。这两个选项都具有潜在危险，因为它们可能会损坏二进制文件。因此，`b` 选项是默认选项；它执行转换。

你可以将这些选项应用于三种实际文件系统的任何一种，并可以通过逗号分隔多个选项。例如，你可以使用以下挂载命令：

```
mount -t mdos -o uid=502,gid=100,conv=a /dev/hda2 /dosstuff
```

该命令使用 MSDOS 文件系统将 `/dev/hda2` 挂载到 `/dosstuff`，并将所有权赋予用户 ID 502 和组 ID 100。你也可以将 `-o` 选项包含在 `/etc/fstab` 的分区条目中，以便在启动挂载分区时自动应用。

### UNIX 的 FAT 可能性
并不是只有 Linux 支持 FAT。其他 UNIX 类系统也有访问 FAT 分区的方法。Linux 不是唯一支持 FAT 的系统，但它是最灵活的系统之一。

## 外部 NTFS 和 NTFS 5.0 支持
多种操作系统和多种形式都支持 NTFS，但 NTFS 的支持不如 FAT 那样广泛。然而，Windows 2000 包含了 NTFS 的更改（称为 NTFS 5.0），这需要对磁盘格式进行修改。旧版本的 Windows 在没有更新驱动程序的情况下无法使用 NTFS。

## DOS NTFS 驱动
你可以从 `http://www.sysinternals.com/ntfs30.htm` 获取适用于 DOS 的只读 NTFS 驱动。NTFS for DOS 软件包非常容易使用——只需输入 `FSDOS` 或在你的 `AUTOEXEC.BAT` 文件创建条目，驱动程序就会加载到内存中，找到所有 NTFS 分区并为其分配驱动器号。

# Windows 9x 的 NTFS 驱动程序
生产 NTFSOS 的公司 Winternals 也为 Windows 98 生产了 NTFS，它为 Windows 9x 系统提供了 NTFS 访问功能。与 NTFSOS 类似，只读版本是免费的，而读写版本需要付费（本文写作时价格为 49 美元）。两个版本的工作原理与 NTFSOS Professional 相同——它们使用 Windows 自身的驱动程序和工具在 Windows 9xr 内部访问 NTFS 分区。因此，如果你使用支持 NTFS 5.0 的驱动程序，该产品支持 NTFS 5.0 分区。你可以在 `http://www.sysinternals.com/ntfs98.htm` 找到有关该产品的更多信息。

由于 Windows 98 版 NTFS 使用了 NTFS 文件，你必须在 FAT 分区上安装 Windows，或者将关键文件从 NTFS 启动分区复制到 FAT 分区以使用该程序。你必须复制以下文件：

```
<WININT>SYSTEM32\DRIVERS\NTFS.SYS
<WININT>SYSTEM32\NTOSKERNEL.EXE
<WININT>SYSTEM32\AUTOCH.EXE
<WININT>SYSTEM32\INTL.DLL
<WININT>SYSTEM32\C_437.NLS
<WININT>SYSTEM32\C_1252.NLS
<WININT>SYSTEM32\L_INTL.NLS
```

在每个情况下，`<WININT>` 表示 Windows NT 系统目录——`c:\WINNT`。如果你在安装 Windows 98 版 NTFS 之前复制这些文件，将会节省时间。

安装完成后，你可以通过运行软件包随带的 NTFS Configure 程序来配置 Windows 98 版 NTFS，如图 13.4 所示。此配置中最重要的方面之一是驱动器号分配。如果你留空驱动器号字段，那么你的 NTFS 分区将按照它们在硬盘上的位置强制顺序出现，就像 FAT 分区一样。如果这迫使其他驱动程序的分区发生变化，可能会导致问题。

- 要了解更多关于驱动器号分配的信息，请参见“驱动器号更改”，第 183 页。

![](img/a1fdd83cd6e78ae8289e5a9f74e5d320_363_0.png)

# 外 NTFS 和 NTFS 5.0 支持
与 DOS 版 NTFS 不同，Windows 98 版 NTFS 将 HPFS 分区误识别为 NTFS 分区，因为这两种文件系统共享相同的分区代码。除非你尝试格式化 HPFS 分区，否则这种误识别不会引起任何问题。

# OS/2 NTFS 驱动程序
在本章前面的部分，我提到了 OS/2 VFAT 驱动程序，它基于 Linux 的 VFAT 代码，可以在 `http://www.dsteiner.com/products/software/os2/ifs.htm` 获取。事实上，这不仅仅是一个 VFAT 驱动程序；它还支持 NTFS 和 ext2fs。该驱动程序的 NTFS 支持目前是只读的，并且与其 VFAT 和 ext2fs 支持一样，它是基于源自 Linux 的长期驱动。

要使用 NTFS 支持，你必须在 OS/2 的 `CONFIG.SYS` 文件的 VFAT 行中添加 `-NTFS` 参数，并可能需要修改 `-VFAT` 参数以包含 NTFS 驱动程序。它不支持 NTFS 5.0 分区。

这种 NTFS 驱动程序支持非常初步，且更新频率较低。它在你的计算机上可能有效，也可能完全无效。程序的作者还将 NTFS 驱动程序与 NTFS 驱动程序分开提供。

# BeOS NTFS 驱动程序
你可以从 `http://www.cs.tamu.edu/people/tkg143/index.html` 获取 BeOS 的 NTFS 驱动程序。该驱动程序仅支持读取访问，在写作时仍然非常新（版本 0.05）。尽管很新，但它确实支持读取 NTFS 5.0 分区。安装后，它允许像挂载 BFS 或 FAT 分区一样，通过右键点击桌面并在挂载菜单中选择分区来挂载 NTFS 分区。

> 注意
> 在写作期间，BeOS NTFS 驱动程序被认为是 Alpha 级软件，这意味着它们可能不稳定，可能会导致你的 BeOS 系统崩溃。请自担风险使用。

# Linux 的 NTFS 驱动程序
Linux 内核带有只读 NTFS 支持，该支持对 NTFS 5.0 分区有效。从 2.2.0 版本开始，内核带有读写 NTFS 支持，但该支持被认为是实验性的，并被广泛认为极具危险。在 2.4.0 内核发布时，这种情况可能会有所改善，但没人对此做出任何保证。

# 第 13 章 访问外部文件系统的工具

### 注意
