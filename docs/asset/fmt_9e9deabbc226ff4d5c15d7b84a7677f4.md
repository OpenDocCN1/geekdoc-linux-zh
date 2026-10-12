
```
$student@localhost sys]$ ls
aio-max-nr dir-notify-enable inode-nr leases-enable overflow
aio-nr epoll inode-state mqueue quota
binfmt_misc file-max notify nr_open suid_dumpable
dentry-state file-nr lease-break-time overflowgid
[$student@localhost]$ file-max
```

你可能知道这个 `file-max` 意味着什么。这个问题的答案可以在 `/usr/share/doc/kernel-doc-2.6.32/Documentation/sysctl/fs.txt` 文件找到：

> “`file-max` 中的值表示 Linux 内核将分配的文件句柄（file-handles）的最大数量。当你收到大量关于文件句柄不足的错误信息时，你可能想要增加此限制。”

# 第 3 章：内核组件与编译

文件句柄（file-handle）是分配给打开文件的标识符，例如，当进程打开一个文件用于读取或写入时。因此，在以前的例子中，任何时候可以打开的文件限制是 49,305，这是存储在 `file-max` 文件中的值。你可以通过更改 `file-max` 文件中的值来临时更改此值：

```
[student@localhost fs]$ echo 60000 > file-max
[student@localhost fs]$ cat file-max
60000
```

在第 4 章中，你将看到如何进行永久更改。

如果你开始在内核文档中找寻，你会发现一些令人沮丧的信息：

1. 并不是所有内容都有记录。
2. 一些文档已经过时了。记得如果你读过 `zorro.txt` 文件，你会发现“Zorro 总线用于 Amiga 系列计算机。然而，是的，是 Amiga。（Amiga 已于 1996 年停产）。”

尽管有这些缺点，内核文档仍然是有用的。如果你对内核进行了许多更改，你将经常查阅这些文档。

## 内核镜像

到此时，你应该意识到内核实际上是合并在一起的软件组件集合。内核的核心是一个相对较小的软件程序，并没有很多功能。为了执行高级任务，内核需要内核模块（kernel modules）的增强。

内核模块与核心内核软件合并有两种主要方法。第一种方法称为 LKM（可加载内核模块）。这是内核模块位于与内核分离的文件中并在需要时加载到内存。LKM 可以在启动过程的内核阶段加载到内存，也可以根据需要加载。LKM 将在第 4 章中进行更详细的探讨。

第二种方法是创建一个包含核心内核软件以及必要的内核模块的内核。将内核与模块合并的结果是一个名为内核镜像（kernel image）的文件。Linux 中正在使用几种不同类型的内核镜像，但 LPIC-2 考试大纲中仅列出了两种：

1. `zImage` —— 在基于 Intel 的硬件架构上，前 640KB 的 RAM 被称为低内存（low memory）。旧系统要求内核必须存储在低内存中，因此 `zImage` 是一个限制在 512KB 以内的压缩内核镜像（这是压缩后的镜像大小），以便内核能够固定在低内存中。
2. `bzImage` —— 由于现代系统允许内核存储在高内存中（约 1MB 的内存），低内存限制不再是一个因素。这是幸运的，因为大多数内核镜像的大小远大于 512KB。`bzImage` 类型设计用于大于 512KB 的内核镜像。

**注意：** 有人会告诉你 `bzImage` 中的“bz”代表 `bzip2` 压缩。这是错误的。在内核 `2.6.30` 之前，镜像通常使用 `gzip` 工具压缩，从 `2.6.30` 开始，它们使用 `bzip2` 工具压缩。`bzImage` 术语实际上代表 `big image`（大镜像）。

内核镜像通常以以下格式命名：`vmlinuz-version.arch`。

`vmlinuz` 只是告诉你它是内核镜像。它可能是 `zImage` 也可能是 `bzImage`。你可以通过执行 `file` 命令查看：

```
[root@localhost]$ file /boot/vmlinuz-2.6.32-72.el6.x86_64
/boot/vmlinuz-2.6.32-72.el6.x86_64: PE32+ executable file (x86-64) for Intel 80386, Linux Kernel 2.6.32-72.el6.x86_64, compressed by bzip2, size 2097152, decompressed size 8453408, data
```

> **注意：** `clean`、`mrproper` 和 `distclean` 被称为 make `targets`（目标）。目标是 `make` 工具的一个参数，它用于告诉 `make` 工具要执行哪些操作。

`Makefile` 包含了当执行 `make` 命令时将执行的所有规则/命令。例如，如果你执行了 `make clean` 命令，`make` 工具将搜索 `Makefile` 以确定具体要执行哪些操作（以下命令在正确执行的情况下不会产生任何输出）：

```
root@localhost linux-2.6.32.68]# make clean
```

在大多数情况下，`make clean` 命令会执行必要的步骤，并给出建议和继续执行。如果过程稍后又发生了额外的错误，你可能需要执行 `make mrproper` 或 `make distclean` 命令。

## 创建配置文件

在这一步中，你将创建一个配置文件，告诉 `make` 命令如何编译内核。请记住，有数百个不同的内核参数。在过程的这一阶段，你需要指定你希望为参数设置的值。

创建此配置文件的方法之一是执行 `make config` 命令。相信我，你绝对不想用这种方法。你会被问数百个问题，每个可能的内核参数对应一个问题。有一个更好的方法！

相反，尝试使用 `make menuconfig` 命令。这种技术将你带入一个基于文本的菜单驱动程序，你可以在其中挑选并选择想要设置的参数。确保你在包含 `Makefile` 的目录中执行此命令。示例请见图 3-1。

![](img/a76ac3bb017d749781a228f025853f37_83_0.png)

![](img/a76ac3bb017d749781a228f025853f37_84_0.png)

**图 3-1** `make menuconfig` 命令

> **注意：** 考试中不会出现关于特定内核参数的问题。你只会被问关于生成内核配置文件的不同技术的问题。将本节的后续部分视为现实世界所需的知识，而不是考试内容。此 FYI 部分从这里开始继续对 `make xconfig` 和 `make gconfig` 的讨论。

你使用向上和向下方向键来高亮菜单选项。例如，图 3-2 显示了使用方向键高亮 `Device Drivers`（设备驱动）菜单选项的结果。

![](img/a76ac3bb017d749781a228f025853f37_85_0.png)

**图 3-2** 高亮 `Device Drivers` 菜单选项

按下回车键可以选择菜单选项并显示子菜单。参见图 3-3 的 `Drivers` 菜单选项的子菜单。

![](img/a76ac3bb017d749781a228f025853f37_86_0.png)

**图 3-3** `Drivers` 子菜单选择

在下一步，我选择了 `Block Devices`（块设备），图 3-4 中显示的菜单出现了。
