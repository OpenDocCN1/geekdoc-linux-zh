
# 19.2 增加系统交换空间 (Swap Space)

要增加交换空间，首先使用以下命令创建一个交换文件：

```bash
mkswap -n [size] [swapfile]
```

创建交换文件后，通过 `swapon` 激活它：

```bash
swapon [swapfile]
```

要禁用交换空间，使用 `swapoff` 命令：

```bash
swapoff [swapfile]
```

# 19.3 控制 root 权限

`root` 用户是 UNIX 系统上权限最大的用户，拥有所有文件和命令的访问权限。将 `root` 权限限制在必要的用户有助于防止意外或恶意破坏。控制 `root` 权限的一种方法是使用 `sudo` 命令，它允许授权的用户以 `root` 权限执行命令。

`sudo` 命令在 `/etc/sudoers` 文件中配置。该文件定义了哪些用户或组可以使用 `sudo` 以及可以使用哪些命令。例如：

```
username ALL=(ALL:ALL) ALL
```

此条目允许用户 `username` 运行任何命令。使用 `sudo`，用户只需在命令前加上：

```bash
sudo [command]
```

# 19.4 显示系统配置信息

有很多命令可以显示 UNIX 系统的配置信息。其中最有用的是 `uname`，它提供了有关内核和硬件的信息。

```bash
uname -a
```

`-a` 参数显示所有可用信息，包括内核名称、发布版本、构建日期和处理器架构。

另一个常用的命令是 `df`，它显示所有文件系统的磁盘使用情况：

```bash
df -h
```

`-h` 参数以人类可读的格式（例如 GB、MB）显示输出。

`du` 命令用于显示特定文件或目录的磁盘使用情况：

```bash
du -sh [directory]
```

`-s` 参数提供目录的总和，而 `-h` 参数以人类可读的格式显示大小。

# 模块 19：重要的系统管理任务/信息 559

这显示了系统当前使用的交换空间（swap space）总量——在本例中为 52,008K（或 52008000 字节）。系统上配置的交换空间总量为 1,062,656K。当使用的交换空间接近系统可用空间的总量时，是时候增加交换空间的大小了。此外，即使当前使用的空间略小于总空间，增加交换空间也并不不少见——也许系统管理员想要获得额外的性能提升，或者配置了一个或多个额外的驱动器来支持交换。通过这种方式，交换活动被分散到额外的物理驱动器上，从而提高了系统性能。

使用 `swapon -s` 命令可以显示可用和已空间的大小：

| 文件名 | 类型 | 大小 | 已用 | 优先级 |
|---|---|---|---|---|
| /dev/hda5 | 分区 | 740840 | 14048 | -1 |

# 添加更多交换空间

要向系统添加更多空间，取决于具体的系统，使用 `swapon` 或 `swap` 命令。增加交换空间可以通过增大当前交换区域的大小或添加额外的交换文件或磁盘分区来实现。通常，大多数 UNIX 系统的安装程序描述了如何使用单独的分区来实现交换空间。例如，在 Linux 系统的 `/etc/fstab` 片段中，我们看到：

```
none /proc proc defaults 0 0
one /dev/shm tmpfs defaults 0 0
none /dev/pts devpts gid=5,mode=620 0 0
/dev/hda5 swap defaults 0 0
bedrock:/docs /mnt/bedrock/docs nfs,hard 0 0
bedrock:/usr /mnt/bedrock/usr nfs,bg,soft 0 0
```

交换分区由 `/dev/hda5` 定义，可以使用 `fdisk` 等工具（对于 Linux，用于增加分区大小，前提是磁盘上有可用空闲空间）。

增加交换空间的另一种方法是定义另一个用于交换的分区，并简单地将该分区添加到挂载文件表中。

### 提示

在尝试调整交换分区的大小时，应将系统置单用户模式（single-user mode）；这种预防措施应作为对系统进行关键类型更改的标准程序。

# 560 UNIX 系统管理：初学者指南

系统表，形如 `/etc/fstab` (Solaris)。使用这种方法，系统在可以使用新的交换区域之前需要重启。另一方面，如果你想在不重启系统的情况下使用交换空间，请使用 `swap` 命令。例如，假设你想使用 `/dev/dsk/c0d0s0` 分区进行交换。可以使用此命令（在 Solaris 上）：

```
# swap -a /dev/dsk/c0d0s0
```

当运行 `swap -l` 命令时，它会显示分配的交换空间总量，我们看到系统已添加了额外的交换空间：

| | swaplo | 块数 | 空闲 | |
|---|---|---|---|---|
| /dev/dsk/c0d0s3 | 102,3 | 8204848 | 2042848 | 分配新交换 |
| /dev/dsk/c0d0s7 | 102,7 | 84194288 | 4194288 | |

增加交换空间的最后方法是使用 `mkfile` 命令（在 Solaris 上）创建一个简单的 UNIX 文件，该命令会创建一个所需交换空间大小的文件。完成后，使用 `swap` 命令并将文件作为参数而不是磁盘分区。

# 19.3 根控制

大多数 UNIX 版本都有一种机制来控制根权限。如果你想在不重启系统的情况下使用交换空间，请使用 `swap` 命令。例如，假设你想使用 `/dev/dsk/c0d0s0` 分区进行交换。可以使用此命令（在 Solaris 上）：

```
# swap -a /dev/dsk/c0d0s0
```
（注：此处原文似乎存在逻辑错乱或重复，翻译已根据上下文意图处理）

# 19.4 显示配置

显示的交换空间总量，我们看到系统已添加了额外的交换空间。当运行，，，，，显示以下。，该文件：

```
# 交换空间
# 
交换 
/dev/console
```

# 模块 19：重要的系统管理任务/信息 561

当尝试调整交换分区的大小时，系统应被置于单用户模式；这种预防措施应作为对系统进行关键类型更改的标准程序。

# 562 UNIX 系统管理：初学者指南

| 命令选项 | 描述 |
|---|---|
| -B | 显示设备信息。 |
| -F | 显示帧信息。 |
| -V | 启用详细模式。 |

# 模块 19：重要的系统管理任务/信息 563

另一个非常有用的 Solaris 命令是 `showrev`。这是该命令的输出：

```
Hostname: bedrock
Hostid: 1e05f4b
Release: 5.8
Kernel architecture: i86pc
Application architecture: i386
Domain: home.com
Kernel version: SunOS 5.8 Generic 18529-07 February 2001
```

从输出可以看出，该命令提供了系统的一些信息。此外，很好的命令行选项是 `-c`。它指示命令列指定命令的详细版本信息。例如，命令

```
showrev -c ls Determine UNIX 命令的信息
```

显示：

```
PATH is:
/usr/sbin:/usr/bin:/usr/dt:/bin:/usr/openwin/bin:/usr/ucb
Pid is:
/
LD_LIBRARY_PATH 未在当前环境中设置
File: /usr/bin/ls
=================
File type: ELF 32-bit LSB executable 0386 Version 1, dynamically linked, stripped
Command version: SunOS 5.8 Generic 2000
File mode: r-xr-xr-x
所有者: root
所属组: bin
库信息:
libc.so.1 => /usr/lib/libc.so.1
libld.so.1 => /usr/lib/libld.so.1
总和: 43151
File: /usr/bin/ls
=================
File type: ELF 32-bit LSB executable 0386 Version 1, dynamically linked, stripped
Command version: SunOS 5.8 Generic 2000
File mode: r-xr-xr-x
所有者: root
所属组: bin
库信息:
libc.so.1 => /usr/lib/libc.so.1
libld.so.1 => /usr/lib/libld.so.1
```

# 564 UNIX 系统管理：入门指南
```
