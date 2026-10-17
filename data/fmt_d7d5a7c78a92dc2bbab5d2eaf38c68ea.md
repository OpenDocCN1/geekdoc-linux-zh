
# 第3章 目录与文件属性：通过 `ls` 观察

`ls c *.c` 列出匹配 `*.c` 的文件名。

如果参数是目录，`ls` 会列出其内容。如果参数是文件，`ls` 会列出其名称或属性。命令行选项会影响 `ls` 的行为和显示内容。

## 3.2.3 常用命令行选项

`ls` 手页列出了许多命令行选项。常用的选项如下表所示：

| 命令 | 操作 |
| --- | --- |
| `ls -a` | 显示隐藏文件 |
| `ls -lu` | 显示最后读取时间 |
| `ls -s` | 显示块大小 |
| `ls -t` | 按时间排序 |
| `ls -F` | 显示文件类型 |

## 关于点的说明

如果你是 Unix 新手，`-a` 选项需要解释。Unix 使用一种简单的约定来实现隐藏文件的概念。该约定是：如果文件名的第一个字符是点，`ls` 不列出该文件。操作系统（即内核）并不关心这一点；这纯粹是一种约定。有些程序使用用户目录中的点文件名来存储易编辑的文件，但你并不总是看到它们。

## 3.2.4 答案

通过实验 `ls` 并阅读手册页，我们发现它执行两件事：

- 列出目录内容

- 显示文件信息

注意 `ls` 对目录执行一种操作，对文件执行另一种操作。如果我们要写一个 `ls` 版本，我们需要掌握三种技能：

- 如何列出目录内容

- 如何获取并显示文件属性

- 如何确定名称是指文件还是目录

## 3.3 系统树简要回顾

在我们关注那三个项目之前，让我们看看 Unix 如何组织磁盘上的文件。磁盘被组织为一个目录树，每个目录都包含文件或目录。图 3 使用矩形表示目录内部的文件，并使用线条显示目录与上下目录的连接：

![](img/99837708330d437de319a559cfa6cda7_94_0.png)

图3 目录树

在 Unix 中，系统的每个文件都位于单个目录树的某处。并没有独立的驱动器或卷。事实上，物理独立的磁盘和分区被并入这棵树中。即使是软磁盘、CD-ROM 和其他移动驱动器作为树中某处的子目录出现。这种简单意味着我们只需要考虑目录和文件。

## 3.4 问题 2：`ls` 如何工作？

`ls` 生成文件名列表。它可以有多复杂？初步猜测：

```
open directory
++-> read entry -end of dir?
| display file info
| close directory <-----------
```

这个轮纲与 `who` 的逻辑相似。主要区别在于 `who` 程序从文件打开并读取，而 `ls` 从目录打开并读取数据。从文件中读取目录有多大区别？目录到底是什么？

### 3.4.1 目录到底是什么？

答案：目录是一种包含文件和目录列表的文件。在某些方面，目录类似于 `tmp` 文件（第2章）；它由一系列记录组成，每条记录都有定义清晰且完整的结构。目录中的每条记录代表一个项目——单个文件或单个目录。

与普通文件不同，目录永远为空。每个目录都包含两个特定项目——分别称为 `.` 和 `..`。`.` 是当前目录的名称，`..` 是上级目录的名称。

### 3.4.2 `open`, `read` 和 `close` 适用于目录吗？

答案：在过去没有其他方法。在你的系统上尝试这些命令：

```
$ cat /
as'a'asa..a'bw.tagsb'c'
quota.userc(
  quota.groupbescet'sbtmp'sbdev sbmnt ' wcsbin '2
  sbopt2
  8
  sbus8
  sbvar9
（省略大量难以阅读的数据）
$ more /tmp
/tmp is a directory
$ cd -c /dev
0000000 360 001 \0 0 024 \0 0 001 \0 \0 \0 \0 360 001 \0
0000020 001 200 \0 0 002 \0 0 024 \0 002 \0 \0 \0 \0 \a \0
0000040 002 010 \0 0 201 \0 0 361 \0 0 030 \0 \a \0
0000060 M A K E D E V \0 \0 k 1 \0 g \0 0 001
```

这些示例显示了一些有趣现象。首先，`cat` 和 `od` 能够像读取普通文件一样读取目录。这两个程序使用了标准的文件访问调用：`open`、`read` 和 `close`。因此，目录可以作为普通文件被读取。

其次，`more` 拒绝显示目录。`more` 知道参数是指目录，它会显示目录的内容，但不会显示你想的内容。某些版本的 `cat` 会像这个版本的 `more` 一样，告诉你文件是一个目录且不显示内容。

最后，这些示例表明目录并不包含纯文本。目录由一组结构体组成。

答案 2 使用 `open`、`read` 和 `close` 来列出目录内容是不好的。Unix 支持多种类型的目录，并可以使用 Apple HFS 格式、ISO9660、VFAT 格式、NFS 目录以及各种类型的 Unix 目录读取磁盘。使用 `read` 处理每种类型需要知道每种目录记录的格式。

### 3.4.3 好的，好的，我该如何读取目录？

我们查看手册。使用关键字 `direct` 进行搜索：

```
$ man -k direct
```

在系统上找到了 81 条条目。对该输出进行关键字 `read` 的过滤后得到：

```
$ man -k direct | grep read
DXSystemDisplay (3X) - 在 Bookreader 中显示帮助文件的主题或目录。
opendir, readdir, readdir_r, teldir, seekdir, rewinddir, closedir (3)
对目录执行操作
$
```

这看起来非常完美。帮助页的第一页显示了：

```
$ man 3 readdir
opendir(3)
```

NAME

`opendir`, `readdir`, `readdir_r`, `teldir`, `seekdir`, `rewinddir`, `closedir`

对目录执行操作

LIBRARY

标准 C Library (`libc.a`)

SYNOPSIS

```
#include <sys/types.h>
#include <dirent.h>

DIR *opendir (
const char *dir_name );

struct dirent *readdir
DIR *dir_pointer);

int readdir_r (
DIR *dir_pointer,
struct dirent *entry,
struct dirent **result);

long telldir (
DIR *dir_pointer );

void seekdir (
  DIR *dir_pointer,
  long location );

void rewinddir (
  DIR *dir_pointer ;
);

int closedir (
  DIR *dir_pointer ;
);

[more] (11%)
```

阅读帮助页，我们发现从目录获取数据与从文件获取数据相似。`opendir` 打开与目录的连接，`readdir` 返回目录中下一个项的指针，`closedir` 关闭连接。`seekdir`、`telldir` 和 `rewinddir` 类似于 `lseek`。图 3.2 显示了过程。

![](img/99837708330d437de319a559cfa6cda7_97_0.png)

图 3.2

从目录读取条目。

### 读取目录内容

目录是一个文件列表，准确地说说是记录序列，每个记录都是目录条目。我们通过调用 `readdir` 读取条目。每次调用 `readdir` 返回指向下一个记录的指针，其类型为 `struct dirent` 变量。该结构的组件在某些帮助页和头文件 `/usr/include/dirent.h` 中有所描述。例如，一个关于 `dirent` 的 Sun OS 帮助页开头如下：

文件格式 `dirent` (4)

+   NAME

`dirent` - 与文件系统无关的目录条目

SYNOPSIS

```
#include <dirent.h>
```

不同的文件系统类型可能有不同的目录类型条目。`dirent` 结构定义了一个与文件系统无关的目录条目，它包含了不同文件系统类型的目录条目共有的信息。`getents(2)` 系统调用返回一组这样的结构。

`dirent` 结构定义如下：

```
struct dirent {
    ino_t           d_ino;
    off_t           d_off;
    unsigned short d_recl;
    char            d_name[1];
}
```

