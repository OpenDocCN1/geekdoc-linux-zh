
以下是 `cpio` 在备份和恢复文件中的一些使用示例：

- 将当前目录中的文件复制到名为 `newfile` 的 `cpio` 归档文件：

```
$ cpio -oVo newfile
```

- 打印归档文件的目录表：

```
cpio -tvF newfile
```

或者

```
cpio -itvI newfile
```

- 将归档文件中的所有文件提取到当前目录，覆盖任何现有文件：

```
cpio -ivul newfile
```

- 使用复制传递模式（`-p` 开关），复制或链接（`-l` 选项）`/home/carol` 中的所有文件和目录到当前路径中的 `newdir` 目录：

```
find /home/carol -depth -print | cpio -pdlmv newdir 2>cpio.log
```

`-d` 开关告诉 `cpio` 根据需要创建目录，`-m` 表示保留修改时间，`-v` 打开详细模式。`cpio` 的所有日志消息都被重定向到当前目录中的 `cpio.log` 文件。请注意，将 `stderr` 重定向为 `stdout` 是一个有效的输出路径，因此 `cpio` 将消息记录到 `stderr` 而不是。`Newdir` 必须存在；否则，`cpio` 命令将失败。

在备份中使用 `cpio` 还是 `tar` largely 取决于个人喜好。然而，由于命令语法更简单并且在其他操作系统上广泛可用，`tar` 似乎是更受欢迎的选择。

### 使用 dd 转换和复制数据

`dd` 程序是另一个老而弥新的工具，用于数据转换和传输。它最初设计用于将大型机数据导入 Unix 系统。在大型机上，数据使用 EBCDIC 字符编码方案传输到磁带上。为了在大多数 Unix 机器上使用此类数据，`dd` 用于读取磁带并将编码更改为 ASCII。然而，随着大型机上 TCP/IP 的可用性，`dd` 不再需要，因为 FTP 和其他基于 IP 的协议可以通过网络完成相同的工作（并消除对磁带的需求）。

`dd` 可以剥离文件头、提取二进制文件的一部分并写入软盘中间；它甚至被 Linux 内核 `makefile` 用于创建启动映像。它可用于复制和转换磁带格式、在 ASCII 和 EBCDIC 之间转换、交换字节以及强制大小写转换。

> **警告**
>
> 因为 `dd` 处理卷头、引导记录和类似的系统数据区域，其误用可能会破坏你的硬盘和文件系统。因此，有些人将 `dd` 称为“Destroy Disk”或“Delete Data”，因为如果误用，无论是意外还是其他原因，磁盘分区或输出文件都可能被迅速破坏。

今天 `dd` 的一个常见用途是创建文件系统的磁盘映像，或将 CD 或 DVD 内容复制到 ISO 映像，然后你可以通过挂载映像在以后访问（无需再次使用 CD 或 DVD）。

与大多数使用命令行开关的 Linux/Unix 命令不同，`dd` 使用 `keyword=value` 格式作为其参数。据称这是以 IBM System/360 JCL（作业控制语言）为模型，后者对 I/O 设备有复杂的 DD（数据集定义）规范。

大多数情况下，你只需要使用两个关键字：`if=infile` 和 `of=outfile`。如果未指定这两个关键字，输入默认为 `stdin`，输出默认为 `stdout`。例如，要将一个文件复制到另一个文件，请使用以下命令：

```
Athena:/home/admin # dd if=/etc/passwd of=passwd.backup
4+1 records in
4+1 records out
```

默认情况下，`dd` 以 512 字节记录复制文件。前面输出的 (4+1 records) 表示读取并写入了四个完整的 512 字节记录加一个部分的 512 字节记录。（在这种情况下，`/etc/passwd` 的大小为 2,185 字节。）你可以在此示例中修改使用的缓冲区大小：

```
Athena:/home/admin # dd if=/etc/passwd of=passwd.backup bs=3000
0+1 records in
0+1 records out
```

以下是 `dd` 命令的一些额外示例用法：

- 创建 1.44MB 软盘的磁盘映像（`bs=` 指定 1.44MB 格式软盘的标准几何结构：18 个 512 字节扇区、2 个磁头和 80 个磁柱，总计 1,474,560 字节；这导致对 `/dev/fd0` 的单次 1,474,560 字节读取请求和对 `/tmp/floppy.image` 的单次 1,474,560 字节写入请求）：

```
dd bs=2x80x18b if=/dev/fd0 of=/tmp/floppy.image
1+0 records in
1+0 records out
```

- 将相同的磁盘映像写回软盘：

```
dd bs=2x80x18b if=/tmp/floppy.image of=/dev/fd0
1+0 records in
1+0 records out
```

- 制作分区的完整副本：

```
dd if=/dev/sda1 of=/backup/boot.partition.image
```

- 制作主引导记录（MBR）的备份副本，MBR 是磁盘上的第一个块：

```
dd if=/dev/sda of=/backup/mbr_backup count=1
```

- 制作 DVD 磁盘的 ISO 映像（假设 DVD 驱动器为 `/dev/hdc`）：

```
dd if=/dev/hdc of=/backup/dvd.image
```

要挂载使用 `dd` 创建的 ISO 映像以供访问，请使用 `mount -o loop /path/image.name /mountpoint`，例如，

```
mount -o loop /backup/dvd.image /mnt
```

请参阅 `man mount` 获取更多信息。

#### 提示

根据所涉及的文件大小，使用更大的缓冲区大小可能是有利的，因为这样可以减少系统调用次数，性能提升可能显著。如果输入和输出设备不同（例如从文件到磁带），你可以使用 `ibs=` 和 `obs=` 分别为读取和写入设置不同的缓冲区大小；`bs=` 为读取和写入设置相同的大小。

你可以通过使用 `dump --help` 命令获得所有可用关键字的完整列表。

### 使用 dump 和 restore

`dump` 程序执行增量文件系统保存操作。它可以备份所有指定的文件（通常是整个文件系统，或文件系统内在特定日期之后或自上次 `dump` 操作以来发生变化的文件）。输出（称为 `dump` 映像或归档）可以是磁带、软盘或磁盘文件。输出设备可以是本地或远程的。`restore` 程序检查 `dump` 以恢复单个文件或整个文件系统。

#### 注

在某些版本的 Unix 中，`dump` 被称为 `fsdump`，而 `restore` 可能被称为 `restore` 或 `fsrestore`。在 HP/UX 上，`fbackup` 执行与 `dump` 类似的功能。

#### 警告

`dump` 仅适用于 `ext2/ext3` 类型的文件系统。

### dump：好的一面、坏的一面和丑陋的一面

一种简单而原始的工具，`dump` 设计为在 `inode` 级别工作，但它确实具有增量归档的出色功能。它会识别上次备份后新建或修改的文件，并非常高效地将其快速存储到 `dump` 映像中。

#### 注

每个 Linux/Unix 文件都有一个 `inode`。`Inode` 是保存有关文件描述性信息的数据结构，例如文件类型、权限、所有者、时间戳、大小以及指向磁盘上数据块的指针。（它们的作用类似于 NetWare 中找到的目录项表（DET）条目，或 Windows 中找到的文件分配表（FAT）条目。）

例如，假设一个名为 `foobar` 的文件在上次归档期间被备份，随后被删除。在下一次增量归档时，`dump` 会将记录放入归档中，内容为“Hey, there used to be a file foobar at inode xxx, but it was removed.”在完整文件系统恢复过程中，已删除的文件不会被复活。如果你例如使用 `tar` 进行常规增量备份任务，并在某天尝试完整恢复，你可能会因为尝试恢复大量先前已删除的文件而耗尽磁盘空间。使用 `dump` 时，你永远不会遇到此类问题，因为它处理增量备份的方式。

`dump` 的增量备份是通过为特定备份分配 `dump` 级别来控制的。有 10 个 `dump` 级别，范围从 0 到 9。当执行某个级别 N 的 `dump` 时，所有自上次级别 N−1 或更低级别的 `dump` 以来发生变化的文件都会被备份。例如，如果周一进行了级别 2 的 `dump`，周二随后进行了级别 4 的 `dump`，那么周三进行的后续级别 3 的 `dump` 将包含自级别 2（周一）备份以来修改或添加的所有文件。

#### 注

级别 0 的 `dump` 会备份整个文件系统。
