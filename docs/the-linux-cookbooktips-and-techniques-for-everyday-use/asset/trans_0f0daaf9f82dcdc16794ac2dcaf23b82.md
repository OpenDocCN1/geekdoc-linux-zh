

# Linux 实用手册：日常使用的技巧与方法：

```
$ ls -l /usr/doc/bash RET
total 72
-rw-r--r--  1 root    root     13744 Oct 19 22:57 CHANGES.gz
-rw-r--r--  1 root    root      1816 Oct 19 22:57 COMPAT.gz
-rw-r--r--  1 root    root     16398 Oct 19 22:57 FAQ.gz
-rw-r--r--  1 root    root      2928 Oct 19 22:57 INTRO.gz
-rw-r--r--  1 root    root      4751 Oct 19 22:57 NEWS.gz
-rw-r--r--  1 root    root      1588 Oct 19 22:57 POSIX.NOTES.gz
-rw-r--r--  1 root    root      2718 Oct 19 22:57 README.Debian.gz
-rw-r--r--  1 root    root     19596 Oct 19 22:57 changelog.gz
-rw-r--r--  1 root    root      1446 Oct 19 22:57 copyright
 drwxr-xr-x  9 root    root      1024 Jul 25  1997 examples
$
```

该命令输出 `/usr/doc/bash` 中文件的详细列表。输出的第一行给出文件占用的磁盘空间总量，以 1024 字节块为单位（在此示例中为 72）。每一后续行显示一个文件的信息，包含多列。

第一列显示文件类型和权限。该列的第一个字符指定文件类型；连字符 (`-`) 为默认值，表示该文件是普通文件。目录用 `d` 表示，符号链接（参见章节 [为文件提供多个名称](#)）用 `l` 表示。第一列的其余九个字符显示文件权限（参见章节 [控制文件访问](#)）。第二列列出指向该文件的硬链接数。第三列和第四列给出文件所属的用户和组名称。第五列给出文件的大小（字节），第六列给出最后修改的日期和时间，最后一个列给出文件名。

[<] [>]   [<<] [Up] [>>]   [Top] [Contents] [Index] [?]

## 6.3.2 递归列出目录

使用 `-R` 选项递归列出目录，该选项会输出该目录及其所有子目录的列表。

- 要输出当前目录的递归目录列表，输入：

```
$ ls -R RET
play    work

play:
notes

work:
notes
$
```

在此示例中，当前工作目录包含两个子目录 `work` 和 `play`，且没有其他文件。每个子目录都包含一个名为 `notes` 的文件。

- 要列出系统上的所有文件，输入：

```
$ ls -R / RET
```

该命令递归列出根目录 `/` 及其所有子目录的内容。通常会将此选项与属性选项 `-l` 结合使用，以输出系统上所有文件的详细列表：

```
$ ls -lR / RET
```

*NOTE:* 如果你没有权限，则无法列出系统上某些目录的内容（参见章节 Controlling Access to Files）。

## 6.3.3 按最新文件优先列出

使用 `-t` 选项与 ls 结合，可对目录列表进行排序，使最新文件优先列出。

- 要按最新优先列出 `/usr/tmp` 目录中的所有文件，输入：

```
$ ls -t /usr/tmp RET
```

## 6.3.4 列出隐藏文件

默认情况下，ls 不会输出以句点字符 (`.`) 开头的文件。为了减少杂乱，许多应用程序通过给文件名以句点开头的方式在你的主目录中“隐藏”配置文件；这些被称为点文件，或有时称为“隐藏”文件。如前所述，每个目录都有两个特殊的点文件：`..`，父目录，和 `.`，目录本身。

要列出目录的所有内容，包括这些点文件，请使用 `-a` 选项。

- 要列出当前目录中的所有文件，输入：

```
$ ls -a RET
```

使用 `-A` 选项可列出目录中几乎所有文件：它会列出所有文件，包括点文件，但除外 `.` 和 `..`。

- 要列出当前目录中除 `.` 和 `..` 之外的所有文件，输入：

```
$ ls -A RET
```

## 6.3.5 以颜色列出目录

使用 ls 配合 `--color` 选项可以颜色列出目录内容；文件会根据其内容以不同颜色显示。部分默认颜色设置包括用蓝色显示目录名、用白色显示文本文件、用绿色显示可执行文件、用青色显示链接。

- 要以颜色列出根目录中的文件，输入：

```
$ ls --color /
System.map  etc        man        usr
System.old  floppy     mnt        var
bin         home       proc       vmlinuz
boot        initrd     root       vmlinuz.old
cdrom       lib        sbin
dev         lost+found tmp
$
```

NOTE: 通常的做法是创建一个命令别名，将 `ls --color` 替换为 `ls`，这样仅输入 ls 即可输出彩色列表。要了解有关创建别名的更多信息，请参阅 Making a Command Alias。

## 6.3.6 列出目录树图

```
@sf(Debian): `tree`
@sf(WWW): http://mama.indstate.edu/linux/tree/
```

使用 tree 可输出给定目录树的 ASCII 树形图。

