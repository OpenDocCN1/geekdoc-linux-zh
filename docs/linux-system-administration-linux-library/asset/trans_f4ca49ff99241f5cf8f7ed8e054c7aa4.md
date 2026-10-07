
要从软盘中提取文件，请将第一卷磁盘放入驱动器并使用以下命令：

```
# tar -xvMF /dev/fd0
```

系统会提示你插入后续的软盘，就像你写入归包时一样。遗憾的是，`tar` 命令不允许对多卷备份进行压缩。如果你尝试这样做，将得到以下错误：

```
tar: Cannot use multi-volume compressed archives
```

```
tar: Error is not recoverable: exiting now
```

尽管 `tar` 使用 `-0` 参数可以将内容写入标准输出，但与许多归档工具不同，它不会从标准输入读取文件列表。许多人认为这是一个主要的缺点。另外两个归档工具 `cpio` 和 `afio` 具有这种能力。

## cpio

`cpio` 工具以 `cp` 命令和输入/输出（I/O）命名，其设计旨在兼具 `dump` 和 `tar` 的优点，包括备份和恢复特殊文件的能力，以及从 cpio 归档中提取单个文件或目录的功能。它的主要用途是将文件从一台计算机传输到另一台计算机，而不是用于归档。然而，由于 `cpio` 从标准输入读取并写入标准输出，它是脚本化备份的绝佳候选。由于输出可以重定向到文件或原始设备，该命令非常通用，经常被用来替代 `tar` 使用。随着 `afio` 的出现，`cpio` 的使用率有所下降。

## 归档到本地目录

由于 `cpio` 期望归档文件列表来自标准输入，因此输入和输出遵循 `cpio` 使用的标准重定向；它使用 `o` 参数创建归档。与 `tar` 类似，`i` 参数用于解包归档，`t` 参数用于列出归档的内容。

让我们从一个简单的示例开始。将当前目录下的文件归档到名为 `archive.cpio` 的文件中，请使用以下命令：

```
# find . | cpio -o > archive.cpio
```

输出看起来类似于所示：

```
cpio: : truncating inode number
```

```
cpio: usr/local/bin: truncating inode number
```

```
cpio: usr/local/bin/gpg-check: truncating inode number
```

```
cpio: usr/local/bin/gpg-encrypt: truncating inode number
```

![](img/4fb617eb648f87def380ef5d92052d01_402_0.png)

## 第11章 备份与恢复

cpio: usr/local/bin/gpg-sign: truncating inode number
cpio: usr/local/bin/gpg-sign+encrypt: truncating inode number

要将归档转储到当前目录，请使用 `i` 参数：

```
# cpio -i < archive.cpio
```

该命令的输出将是写入的块计数。
要获取归档中包含的文件列表，请如下使用 `t` 选项：

```
# cpio -t < archive.cpio
```

此命令将输出从转储的归档中写出的文件列表。输出如下：

```
cpio:
cpio: usr/local/bin
cpio: usr/local/bin/gpg-check
cpio: usr/local/bin/gpg-encrypt
cpio: usr/local/bin/gpg-sign
cpio: usr/local/bin/gpg-sign+encrypt
```

## 归档到磁带

使用 `tar` 时，这是用于常规备份的归档操作。要归档到磁带而不是同一磁盘驱动器或网络，请将归档名称替换为磁带机的设备名称。如果磁带设备是 SCSI 链上的第一个设备，则设备名称为 `/dev/st0`。向该磁带写入、检索和列出当前工作目录中文件的命令将是：

```
# find . > /dev/st0
# cpio -i < /dev/st0
# cpio -t < /dev/st0
```

输出看起来与之前的示例基本相同。

## 远程归档到另一台计算机

要让 `cpio` 写入另一台计算机，你可以使用 `-F` 参数指定远程服务器名称在该服务器上的文件名。此过程使用备份服务器上的 `rsh` 或 `in.sh` 守护进程。你可以在备份服务器上指定磁带设备文件名将数据发送到该设备。因此，命令类似于：

```
# find . | cpio -o -F buserver:/dev/st0
```

## 归档到软磁盘

由于存储容量极其有限，将归档到软磁盘仅对于拷贝几个文件有意义，而不适用于备份系统。要写入软盘，只需将磁带设备名称替换为软盘设备，通常为 `/dev/fd0`。结果命令如下：

```
# find | cpio -o /dev/fd0
```

要从软盘中提取文件，请使用以下命令：

```
# cpio -i </dev/fd0
```

要列出软磁盘上的文件，请使用 `-t` 代替 `-i`。

## afio

`afio` 工具随某些但并非所有 Linux 发行版提供。它没有包含在 Red Hat 7.0 中，但是 Red Hat Tools 包的一部分，可以从 Linux 存档网站获取，包括 RPM Find (http://www.rpm-find.com/linux)。一些管理员认为 `afio` 最有用，因为它使用了压缩算法。`afio` 的另一个让你欣赏的功能是它的双缓冲；`afio` 使用内存缓冲区存储数据，直到磁带机几乎满。这允许 `afio` 在磁带停止时继续运行。

输出可以重定向到文件或原始设备，该命令非常通用，经常被用来替代 `tar` 使用。随着 `afio` 的出现，`cpio` 的使用率有所下降。
