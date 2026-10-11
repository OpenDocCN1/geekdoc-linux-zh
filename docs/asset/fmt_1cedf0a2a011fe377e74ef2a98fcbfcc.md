
$1 = 4.4 exp = 81 log = 1.5 sqrt = 2.1 int = 4 substr (beat, 2, 2) = ea

## 4.9 硬链接与软链接: ln

该工具允许你在文件之间创建硬链接和符号链接（软链接），如图 4–21 所示。

| 工具 |
| :--- |
| `ln -s original [newLink]` |
| `ln -s { original }+ directory` |

`ln` 是一个允许你对现有文件创建硬链接或符号链接的工具。

要在两个普通文件之间创建硬链接，请将现有文件标签指定为原始文件名（`original`），并将新文件标签指定为新链接（`newLink`）。此时这两个标签将指向同一个文件，这种安排将体现在 `ls` 工具显示的硬链接计数中。可以通过任何一个标签访问该文件，并且当所有关联的标签都被删除时，该文件将从文件系统中移除。如果省略了 `newLink`，则假设为 `original` 的最后部分。如果最后一个参数是目录名称，则会为所有指定的 `original` 文件名创建硬链接。硬链接可能跨越文件系统。

`-s` 选项允许 `ln` 创建符号链接。符号链接是一个包含指向另一个文件的指针（通过名称）的新文件。符号链接可以跨越文件系统，因为除了名称之外，没有到目标文件的显式连接。注意，如果符号链接指向的文件被删除，符号链接仍然存在，但在访问时将导致错误。

`-F` 选项允许超级用户创建目录的硬链接。

有关硬链接在文件系统中如何表示的更多信息，请参阅第 13 章“Linux 内部”中对 Linux 文件系统的讨论。

在以下示例中，我为现有标签 "`hold.3`" 指向的文件添加了一个新标签 "`hold`"。注意，当添加硬链接时，硬链接计数字段从一增加到二，当删除硬链接时又变回一：

```bash
$ ls -LG ... 查看当前目录内容。
total 3
-rw-r-r-- 1 glass 124 Jan 12 17:32 hold.1
-rw-r-r-- 1 glass 89 Jan 12 17:34 hold.2
-rw-r-r-- 1 glass 91 Jan 12 17:34 hold.3
$ ln hold.3 hold ... 创建一个新的硬链接。
$ ls -LG ... 查看新的目录内容。
total 4
-rw-r-r-- 2 glass 91 Jan 12 17:32 hold
-rw-r-r-- 1 glass 124 Jan 12 17:32 hold.1
-rw-r-r-- 1 glass 89 Jan 12 17:34 hold.2
-rw-r-r-- 1 glass 91 Jan 12 17:34 hold.3
$ rm hold ... 删除其中一个硬链接。
$ ls -LG ... 查看更新后的目录内容。
total 3
```

如果目录名称指定为最后一个参数，则向现有目录添加匹配模式 "`hold.*`" 的系列硬链接。在以下示例中：

```bash
$ mkdir tmp ... 创建一个新目录。
$ ln hold.* tmp ... 在 "tmp" 中创建链接。
$ ls -LG tmp ... 查看 "tmp" 的内容。
total 3
-rw-r-r-- 2 glass 124 Jan 12 17:32 hold.1
-rw-r-r-- 2 glass 89 Jan 12 17:34 hold.2
-rw-r-r-- 2 glass 91 Jan 12 17:34 hold.3
```

硬链接可能从一个文件系统的文件创建到另一个文件系统的文件。要创建符号链接（或软链接）——符号链接可以跨越文件系统。使用 `-s` 选项创建符号链接。在以下示例中，我尝试从家目录创建到 "`/usr/include/stdio.h`" 的硬链接。失败了，因为该文件在另一个系统上。使用 `-s` 选项则成功了。符号链接后面跟有 `@` 符号。

## 4.11 切换用户: su

默认情况下，`ls` 显示符号链接的内容；要获取链接指向的文件信息，请使用 `-L` 选项。

```bash
$ ln /usr/include/stdio.h stdio.h ... 硬链接。
ln: stdio.h: Cross-device link
$ ln -s /usr/include/stdio.h stdio.h ... 符号链接。
$ ls -Tlg ... 查看文件。
lrwrxwrfx 1 glass 20 Jan 12 17:58 stdio.h -> /usr/include/stdio.h
$ ls -F ...@ 表示符号链接。
stdio.h@
$ ls -LGL stdio.h ... 查看链接本身。
-rw-r-r-- 1 root 27839 May 11 07:40 stdio.h
$ cat stdio.h ... 查看文件。
/* Define ISO C stdio on top of C++ iostreams.

Copyright (C) 1991-1992,2003 Free Software Foundation
This file is part of the GNU C Library.

## 4.10 识别 shell: whoami

假设你遇到一个空 shell 提示符的系统。显然有人在 Linux 系统上工作但忘记注销了。你好奇是谁。要解决这个谜，可以使用 `whoami` 工具，它可以显示 shell 的所有者（图 4–22）。

| 工具 | 说明 |
| :--- | :--- |
| `whoami` | 显示 shell 的所有者。 |

图 4–22 `whoami` 命令说明。

例如，当我在系统中执行 `whoami` 时，我看到这个：

```bash

$ whoami

glass

```

## 4.11 切换用户: su

很多人认为 `su` 代表“超级用户”（super-user），但并不是。相反，它代表“替换用户”（substitute user），允许你创建一个属于另一个用户的 shell。

## 4.12 转换文件

有几个转换文件的工具，包括以下：

### 4.12.1 压缩文件: gzip 和 gunzip

GNU 文件压缩工具称为 `gzip`。正如你猜的 la，解压文件的工具是 `gunzip`。图 4–24 解析了这些。

| 工具 |
| :--- |
| `gzip -cv { fileName }` |
| `gunzip { fileName }` |
| `zcat { fileName }` |

`gzip` 将文件替换为压缩版本，并添加 “.gz” 后缀。`-c` 选项将结果发送到标准输出而不是覆盖原始文件。`-v` 显示了发生的压缩量。`gzip` 命令解压由 `gzip` 创建的文件。`zcat` 等同于 `gzip -c`。

图 4–23 `su` 的说明。

以下是使用 `gzip` 方法：

```bash

$ ls -lg palindrome.c reverse.c

-rw-r-r-- 1 glass 224 Jan 12 17:32 palindrome.c

-rw-r-r-- 1 glass 266 Jan 12 17:32 reverse.c

$ gzip -v palindrome.c reverse.c

palindrome.c: 34.3% -- replaced with palindrome.c.gz

reverse.c: 39.4% -- replaced with reverse.c.gz

$ ls -Tg palindrome.c.gz reverse.c.gz

-rw-r-r-- 1 glass 178 Jan 12 17:32 palindrome.c.gz

-rw-r-r-- 1 glass 189 Jan 12 17:32 reverse.c.gz

$ gunzip -v *.gz

palindrome.c.gz: 34.3% -- replaced with palindrome.c

reverse.c.gz: 39.4% -- replaced with reverse.c
```
