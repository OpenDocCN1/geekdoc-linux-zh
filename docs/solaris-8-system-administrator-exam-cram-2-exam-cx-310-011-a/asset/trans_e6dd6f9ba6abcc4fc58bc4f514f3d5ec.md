

## 文件类型

文件系统上分配的空间以目录或文件的形式存在。目录只有一种类型。然而，文件有几种类型。用于存储数据或可执行文件的文件被称为*普通*或*常规*文件。其他文件则用于特殊用途。表9.5列出了所有支持的文件类型。你可以通过`ls -l`命令产生的单字符标识来识别文件的类型。

![](img/b957f979417d9f16274c2eb52c8f2c9f_229_0.png)

请熟悉Solaris环境中支持的文件类型以及`ls`命令用于识别文件类型的字符标识。

**表9.5 文件类型**

| 类型 | `ls -l`标识 | 描述 |
| --- | --- | --- |
| 普通文件 | `-` | 普通或常规文件。用于存储数据和可执行文件。 |
| 目录 | `d` | 目录。用于组织文件和其他目录。 |
| 链接 | `l` | 符号链接。用于提供文件或目录的替代路径（参见下一节“链接类型”）。 |
| 块特殊文件 | `b` | 提供面向块的外设接口的文件。这些文件通常位于`/dev`或`/device`目录下。也称作*设备文件*。 |
| 字符特殊文件 | `c` | 提供面向字符的外设接口的文件。这些文件通常位于`/dev`或`/device`目录下。也称作*设备文件*。 |
| 门（Door） | `D` | 提供程序之间以及内核与用户空间进程之间远程过程调用（RPC）机制接口的文件。 |
| FIFO | `p` | 先进先出或命名管道数据结构，为两个协作程序提供通信机制。 |
| 套接字 | `s` | 用于通过网络接口通信的网络（AF_UNIX）套接字数据结构。 |

## 链接类型

如前所述，文件和目录通过*链接*连接到目录中。该链接作为目录中的一条条目存储，为定位和访问文件或目录提供引用。

目录条目实际上是指向文件系统内文件或目录位置的指针，被称为*硬链接*。由于链接基于文件或目录在文件系统中的位置来指向它们，因此链接不能用于指向不同文件系统中的文件或目录。因此，硬链接意味着文件或目录位于当前文件系统中。

*软链接*或*符号链接*提供了一种引用另一文件系统上文件或目录的机制。目录条目不是指向文件系统中的位置，而是包含另一个文件或目录的完整路径名。使用符号链接，你可以创建不同文件系统上的多个路径名和文件名，这些路径名和文件名都指向同一个文件或目录。

你可以使用**link**(1M)和**ln**(1)命令创建硬链接。然而，只有**ln**命令可用于创建符号链接（通过使用**-s**命令行参数）。**unlink**(1M)命令用于删除硬链接或软链接。当指向文件或目录的所有硬链接都被删除时，该文件或目录即被移除。你也可以使用**rm**(1)和**rmdir**(1)命令删除硬链接或软链接。

## 文件和目录压缩

目录和文件可以被压缩，以使用更少的磁盘驱动器空间，更重要的是，减少备份设备（如磁带和光盘介质）上的空间。Solaris支持三种用于压缩和解压缩（即展开）数据的实用程序：

- **compress**(1)和**uncompress**(1)
- **gzip**(1)和**gunzip**(1)
- **zip**(1)和**unzip**(1)

### compress和uncompress命令

**compress**命令使用自适应Lempel-Ziv编码算法来压缩一个或多个通过命令行参数（以空格分隔）指定的文件。使用**compress**命令压缩的文件会被赋予.Z扩展名。你可以使用**uncompress**命令解压缩文件，将文件名作为命令行参数（以空格分隔）指定。请注意，**compress**命令只能用于普通文件，并且每个文件被单独压缩。以下示例展示了这些命令的使用：

```text
# ls -l
total 3
-rw-r--r--  1 root     other    103306 Apr  6 02:27 file4

# compress file4

# ls -l
total 3
-rw-r--r--  1 root     other     41280 Apr  6 02:27 file4.Z

# uncompress file4

# ls -l
total 3
-rw-r--r--  1 root     other    103306 Apr  6 02:27 file4
#
```

你可以使用**zcat(1)**命令查看使用**compress**命令压缩的文件内容。然而，**zcat**命令不像**uncompress**命令那样生成未压缩的文件或删除压缩文件。

### gzip和gunzip命令

**gzip**命令使用自适应Lempel-Ziv编码（LZ77）算法来压缩一个或多个通过命令行参数（以空格分隔）指定的文件。使用**gzip**命令压缩的文件会被赋予.gz扩展名。你可以使用**gunzip**命令解压缩文件，将文件名作为命令行参数（以空格分隔）指定。请注意，**gzip**命令只能用于普通文件，并且每个文件被单独压缩。以下示例展示了这些命令的使用：

```text
# ls -l
total 3
-rw-r--r--  1 root     other    103306 Apr  6 02:27 file4

# gzip file4

# ls -l
total 7
-rw-r--r--  1 root     other     32757 Apr  6 02:27 file4.gz

# gunzip file4

# ls -l
total 3
-rw-r--r--  1 root     other    103306 Apr  6 02:27 file4
#
```

你可以使用**gzcat(1)**命令查看由**gzip**命令压缩的文件内容。然而，**gzcat**命令不像**gunzip**命令那样生成未压缩的文件或删除压缩文件。

### zip和unzip命令

**zip**命令将命令行参数指定的一个或多个文件和/或目录压缩到单个归档文件中。由**zip**命令创建的归档文件会被赋予.zip扩展名。你可以使用**unzip**命令解压缩该归档文件，将归档文件作为命令行参数指定。以下示例展示了这些命令的使用：

```text
# ls -lR
total 2
drwxr-xr-x  2 root     other         512 Apr  6 03:15 dir1

./dir1:
total 296
-rw-r--r--  1 root     other          27 Apr  6 03:04 file1
-rw-r--r--  1 root     other         389 Apr  6 03:04 file2
-rw-r--r--  1 root     other       34341 Apr  6 03:04 file3
-rw-r--r--  1 root     other      103306 Apr  6 03:04 file4

# zip dir1.zip dir1/
  adding: dir1/file1 (deflated 33%)
  adding: dir1/file2 (deflated 59%)
  adding: dir1/file3 (deflated 68%)
  adding: dir1/file4 (deflated 68%)

# rm -r dir1

# ls -l
total 88
-rw-r--r--  1 root     other       44284 Apr  6 03:15 dir1.zip

# unzip dir1.zip
Archive:  dir1.zip
  inflating: dir1/file1
  inflating: dir1/file2
  inflating: dir1/file3
  inflating: dir1/file4

# ls -lR
total 90
drwxr-xr-x  2 root     other         512 Apr  6 03:16 dir1
-rw-r--r--  1 root     other       44284 Apr  6 03:15 dir1.zip

./dir1:
total 296
-rw-r--r--  1 root     other          27 Apr  6 03:04 file1
-rw-r--r--  1 root     other         389 Apr  6 03:04 file2
-rw-r--r--  1 root     other       34341 Apr  6 03:04 file3
-rw-r--r--  1 root     other      103306 Apr  6 03:04 file4
#
```

## 备份与恢复

Solaris 8提供了不仅能够备份和恢复整个文件系统，还能备份和恢复目录甚至所选文件的实用程序。通常使用磁带备份数据，但也可以使用其他介质，如硬盘、可写光盘，甚至软盘。

一盘磁带可以包含多组数据，或*数据集*。在某些情况下，数据集可能是一个单一文件。通常，数据集是作为单个单元写入磁带的文件集合。数据集之间由文件结束（EOF）标记分隔，并由任意数量的记录或块组成。用于在磁带上存储数据的命令决定了块大小。

### mt命令

`mt(1)`命令用于控制磁带操作，包括将磁带定位到数据集的开始、倒带，甚至擦除磁带。表9.6列出了可以作为命令行参数指定的mt操作。大多数操作期望另一个命令行参数提供一个值，指定操作应重复的次数（在表中显示为*计数*）。如果未指定*计数*，则操作执行一次。

| 命令 | 描述 |
| --- | --- |
| `asf count` | 将磁带定位到第*count*-1个EOF标记之后 |
| `bsf count` | 向后跳过*count*个EOF标记 |
| `bsr count` | 向后跳过*count*条记录 |
| `eof count` | 写入*count*个EOF标记 |
| `eom` | 向前跳转到最后一个数据集之后的位置 |
| `erase` | 擦除整盘磁带 |
| `fsf count` | 向前跳过*count*个EOF标记 |
| `fsr count` | 向前跳过*count*条记录 |
| `rewind` | 倒带 |
| `status` | 显示磁带驱动器的状态 |

如果在`-f`命令行参数后未指定原始磁带设备，则假定使用默认磁带设备`/dev/rmt/0n`。以下示例将磁带定位到第五个数据集（即跳过四个EOF标记）：

```sh
# mt -f /dev/rmt/0n fsf 4
#
```

