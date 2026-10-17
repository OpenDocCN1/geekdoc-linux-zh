
在 Linux 中挂载 FreeBSD 分区的一个重要前提是支持 BSD 分区方案。通常，Linux 使用 x86 样式的主分区、扩展分区和逻辑分区；它不使用 BSD 样式的分区。因此，要访问 BSD 分区，你必须启用名为 BSD Disklabel (BSD Partition Tables) Support 的 Linux 内核选项，该选项位于内核配置菜单中文件系统的 Partition Types 子菜单中。你的 Linux 发行版可能已经启用该选项，也可能没有。如果未激活，你必须重新编译 Linux 内核。有关如何做到这一点的更多信息，请参阅 Linux 系统管理书籍，如 Richard Petersen 的 *Linux: The Complete Reference, 4th Edition* (McGraw-Hill/Osborne, 2000) 或 Vicki Stanfield 和我的 *Linux System Administration, 2nd Edition* (Sybase, 2002)。添加此功能后，Linux 将 FreeBSD 切片视为扩展分区。切片内的 FreeBSD 分区将使用 5 及以后的分区号可用，或者从最后一个逻辑分区编号之后的数字开始。

> **注意**
>
> 如果 BSD 切片使用的分区号小于扩展分区，向 Linux 添加或移除 BSD 分区支持会改变逻辑分区的编号，因为 Linux 根据逻辑分区或 FreeBSD 分区所在的扩展分区或 FreeBSD 切片的顺序对逻辑分区或 FreeBSD 分区进行编号。这种分区编号的变化又可能导致 Linux 无法启动，直到你修改 Linux `/etc/fstab` 文件以反映此变化。如果你的扩展分区具有比 FreeBSD 切片更小的编号，这些问题就不会发生。

Linux 对 FFS 的支持并不完美。特别是，读写支持是独立于只读支持进行编译的，而且只读支持被视为实验性功能。因此，即使你已经在 Linux 内核中编译了基本的 FFS 支持，你也可能无法向 FreeBSD 分区写入数据。如果你需要向 FFS 分区写入数据，我建议你谨慎行事，因为 Linux 可能会损坏该分区。

### 关于外部访问的注意事项

从非 BSD 操作系统访问 FreeBSD 文件系统时，会遇到与从 FreeBSD 访问非 BSD 文件系统时类似的注意事项。特别是，由于多年来 FFS 的演变和差异，你可能无法从非 BSD 的类 UNIX 操作系统访问 FreeBSD 的文件系统，即使这些操作系统名义上支持 FFS。即使你可以挂载文件系统，如果你的 UID 和 GID 在安装之间不一致，你也可能会注意到文件的表观所有者和组存在差异。在创建用户和组时具备一定的前瞻性，可以极大程度地减少这些问题。

更令人担忧的是文件损坏的可能性，尤其是在使用 Linux 的读写 FFS 支持时。在你从 Linux 向 FFS 分区写入之前，应该备份你的 FreeBSD 文件。不过，Linux 的只读 FFS 支持危险程度低得多，因此如果你只是想读取一些 FreeBSD 文件，应该不会有什么大问题。

## 在 FreeBSD 中运行非 BSD 程序

FreeBSD 提供了广泛的软件，但偶尔你可能会发现需要运行一个 FreeBSD 上不可用的程序。与其使用第二台电脑或双启动进入另一个操作系统，你也许可以使用几种能够让 FreeBSD 运行旨在其他操作系统上使用的程序的工具之一。其中最为可靠的是 FreeBSD 的 Linux 仿真功能，它让 FreeBSD 可以运行 Linux 程序。其他工具可以让你运行 Windows 程序，或者在一个完整仿真的计算机中运行任何 x86 操作系统。

### 运行 Linux 程序

尽管谱系不同，但 FreeBSD 和 Linux 是非常相似的操作系统。事实上，在许多情况下，相同的源代码可以在两者上编译和运行。因此，绝大多数在其中一个操作系统上运行的开源程序也可以在另一个操作系统上原生运行。然而，并非所有程序都是开源的，而且一些商业程序仅在 Linux 上可用，而在 FreeBSD 上不可用。为此，FreeBSD 提供了运行 Linux 程序的能力。这种支持涉及一系列库和支持包。安装这些之后，你可以几乎像在 FreeBSD 上运行程序那样运行 Linux 程序。由于 FreeBSD 和 Linux 使用几乎相同的系统调用，在运行 Linux 程序时无需使用大量的仿真例程。因此，Linux 程序在 FreeBSD 下的运行速度与在 Linux 下大致相同。不过，内存会受到影响，因为 Linux 程序需要 Linux 兼容的系统库，其中许多库的功能与 FreeBSD 标准库中的功能重复。

#### 准备运行 Linux 程序

在基本安装中，FreeBSD 并未配置为运行 Linux 程序。若要执行此操作，请完成以下步骤：

- **安装 Linux 基础端口。** `linux_base` 软件包包含核心 Linux 库和支持工具。其中大部分位于 `/compat/linux` 目录树中。你可以按照第 11 章中描述的其他软件包安装方式安装此软件包。
- **配置主机名解析。** 一些 Linux 程序在使用默认配置运行时，在将主机名解析为 IP 地址时会出现问题。如果你遇到此问题，应编辑 `/compat/linux/etc/host.conf` 文件，使其包含以下内容：

```
order hosts,bind
multi on
```

- **启动 Linux 兼容模式。** 输入 `kldload linux` 以启动 Linux 兼容模式。此后，你应该能够运行 Linux 程序。如果你希望系统在启动后自动启用此模式，请确保在 `/etc/rc.conf` 文件中添加以下行（如果尚未存在）：

```
linux_enable="YES"
```

此时，FreeBSD 应支持 Linux 二进制文件。若要检查是否确实如此，你可以使用 `kldstat` 程序，它会返回有关系统上加载的内核模块的信息，包括 FreeBSD 的 Linux 兼容模块。正常工作的 Linux 支持层应产生类似于以下内容的输出：

```
$ kldstat
Id Refs Address     Size      Name
1   5   0xc0100000  3ef2dc    kernel
2   1   0xc1cb2000  16000     linux.ko
```

可能会有更多行显示额外的模块。关键在于应存在引用 `linux.ko` 内核模块的行，例如前面示例中 ID 为 2 的那一行。

#### 重新配置和运行 Linux 程序

FreeBSD 和 Linux 使用相同的基本格式来组织程序文件。这种格式被称为*可执行与链接格式*（ELF）。尽管基本格式相同，但一些细节存在差异，这有时会导致 FreeBSD 无法识别 Linux 二进制文件为有效文件。如果 FreeBSD 报告某个 Linux 二进制文件无效，你必须使用 `brandelf` 程序以 FreeBSD 能够识别的方式标记该程序文件。具体而言，你需要使用类似于以下命令：

```
# brandelf -t Linux linux-binary
```

在此示例中，`linux-binary` 是你想要运行的二进制程序文件的名称。在某些情况下，程序现在应该可以像 FreeBSD 程序一样正常工作：尝试输入其名称，看看它是否运行。文本模式程序应产生正常的输出，X 程序应打开窗口并运行。事实上，仅凭用户界面很难辨别出一个程序是 Linux 程序。

不幸的是，Linux 程序经常需要你的 FreeBSD 系统未安装的库。更准确地说，Linux 程序需要 Linux 版本的库。拥有本地 FreeBSD 版本的库是不够的；你必须安装该库的 Linux 版本。`linux_base` 软件包的大部分仅就是这些——许多 Linux 程序所依赖的库。然而，该软件包无法做到面面俱到，因此你可能需要追踪 Linux 版本的库。

追踪其中一种方法是使用 Linux 或 FreeBSD 中的 `ldd` 命令。应用于 FreeBSD 4.4 系统中 Caldera OpenLinux 3.1 的 `ls` 二进制文件的如下所示的结果应该类似于以下形式：

```
$ ldd ls
ls:
    /lib/libc.so.6: version `GLIBC_2.2' not found (required by ls)
    libc.so.6 => /lib/libc.so.6 (0x28068000)
    /lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x28053000)
```

> **注意**
>
> 此示例使用较新版本的 Linux 和较旧版本的 FreeBSD，因为它说明了旧库（在 FreeBSD 4.4 的 Linux 兼容软件包中）可能无法与新二进制文件（较新的 Caldera 3.1 中常见的 `ls` 二进制文件）配合使用的事实。
