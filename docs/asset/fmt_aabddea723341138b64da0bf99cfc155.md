
```
$ ln -s /dev symtobin
$ ls -l 2 drwxr-xr-x 19 root 4480 Feb 25 11:58 /dev
16518424 lwxrxr-x 1 sarawar faculty 4 Mar 4 14:19 symtobin -> /dev
$
```

在后面的章节中，我们展示了一个创建链接示例，使得该文件及其符号链接位于不同的文件系统。

```
$ ln -s /dev/home/Chapter3 temp.soft
$ ls -ld /dev/home/Chapter3 temp.soft
-4-rw-r-- 1 sarawar faculty 39573 Mar 6 07:26 /dev/home/Chapter3
16518443 lwxrxr-x 1 sarawar faculty 17 Mar 6 08:09 temp.soft -> /dev/home/Chapter3
$
```

# 当前目录的结构

# 当前目录的内容

| 章1 | 章2 | 章3 | 章3.soft |
| --- | --- | --- | --- |
| | | 16517779 | |
| | | 16517772 | |
| | | 16518415 | Chapter1 |
| | | 16518416 | Chapter2 |
| | | 16518417 | Chapter3 |
| | | 16518423 | Chapter3.soft |

![](img/2a18e06cd9c6395e451f26126ecba1fd_229_0.png)

# Inode 表

| 16518417 | Chapter3 |
| --- | --- |
| 16518423 | Chapter3.hard 的目录项 (Chapter3.soft) |

`Inode 16518417`

| `Inode 16518423` |
| --- |
| . |
| 链接计数 大小 更新时间 所有者 |
| --- |
| . |
| 文件在磁盘上的位置 |

`Inode 16518417`

| 链接计数 大小 更新时间 所有者 |
| --- |
| . |
| 文件在磁盘上的位置 |

![](img/2a18e06cd9c6395e451f26126ecba1fd_229_1.png)

**图 8.5** 建立软链接：(a) 当前目录的逻辑结构；(b) 当前目录的内容；(c) 通过在现有文件的链接文件（路径）中建立指针来实现的软链接。

以下内容显示了如何为目录中的所有文件创建符号链接，包括目录文件。`ln -sf ~/linux2e/examples/dir1/* ~/linux2e/examples/dir2` 命令为名为 `~/linux2e/dir1` 的目录中的所有文件创建链接，并将它们放入 `~/linux2e/examples/dir2` 目录中。你必须对路径中的所有目录具有执行和写入权限。`-f` 选项用于在 `~/linux2e/examples/dir2` 中已存在文件 `f1`, `f2` 或 `f3` 的任何情况下强制创建软链接。在某些系统上，`-f` 和 `-s` 选项可能无法一起工作，在这种情况下你将使用 `-s` 选项。

```
$ cd ~/linux2e/examples
$ more dir1/f1
```

# Linux

Hello, World!

这是一个测试文件。

```
$ ls -l dir1
-rw-r--r-- 1 sarwar faculty 35 Jun 22 22:21 f1
-rw-r--r-- 1 sarwar faculty 168 Jun 22 22:33 f2
-rwxr-xr-x 1 sarwar faculty 783 Jun 22 22:35 f3
$ ln -sf /linux2e/examples/dir1/ -> /linux2e/examples/dir2
-rwxr-xr-x 1 sarwar faculty 38 Jun 22 22:54 f1 -> /home/sarwar/linux2e/examples/dir1/f1
-rwxr-xr-x 1 sarwar faculty 38 Jun 22 22:54 f2 -> /home/sarwar/linux2e/examples/dir1/f2
-rwxr-xr-x 1 sarwar faculty 38 Jun 22 22:54 f3 -> /home/sarwar/linux2e/examples/dir1/f3
$ more dir2/f1
```

Hello, World!

这是一个测试文件。

你可以运行以下命令在你的主目录中创建一个指向文件 `/home/sarwar/linux2e/examples/demol` 的符号链接。该软链接也称为 `demol`（主目录）。如果 `demol` 已经存在于你的主目录中，你可以使用 `-f` 选项覆盖它。如果 `demol` 存在于主目录中而你没有使用 `-f` 选项，屏幕上将显示一条错误信息，告知你 `demol` 已存在。你必须对 `/home/sarwar/linux2e/examples/demol` 路径中的目录具有执行权限，并且 `demol` 必须是一个文件。

```
$ ln -sf /home/sarwar/linux2e/examples/demol ~
$
```

用户 `sarwar` 可以运行以下命令，在 `bob` 的主目录下的目录 `dir1` 中创建一个名为 `demol` 的软链接，它指向 `/home/sarwar/linux2e/examples/demol` 文件。图 8.6 显示了软链接是如何扩展的。

```
$ ln -sf /home/sarwar/linux2e/examples/demol /home/bob/dir1
```

用户 `sarwar` 必须对 `bob` 的主目录具有执行权限，并对 `dir1`（创建软链接的目录）具有执行和写入权限。用户 `bob` 必须对 `sarwar` 目录结构中的 `demol` 具有访问权限才能访问该文件。因此，如果 `sarwar` 和 `bob` 在同一个用户组中且 `bob` 拥有 `demol` 的编辑权限，那么 `sarwar` 必须设置文件的组权限以读取它。用户 `bob` 就可以使用例如 `vi` 命令来编辑 `demol`。以下命令完成了相同的任务。记住，`sarwar` 运行了此命令。

![](img/2a18e06cd9c6395e451f26126ecba1fd_230.png)

图 8.6 在 (a) `/home/sarwar/linux2e/examples/demol` 和 (b) `/home/bob/dir1` 之间的软链接。

# 文件共享

```
$ ln -sf /linux2e/examples/demol /home/bob/dir1
$
```

你可以运行以下命令为主主目录中的所有文件（包括目录文件）创建软链接。这些软链接位于主目录中的 `linux2e/examples` 目录，并具有原始文件的名称。`john` 必须在主目录中创建 `linux2e/examples` 目录。为了成功运行该命令，`john` 必须对 `examples` 目录具有执行权限。

```
$ ln -sf ~/linux2e/examples/* /home/john/examples
```

## 8.6.4 符号链接的优点

如前所述，符号链接没有硬链接的问题和限制。符号链接可以跨文件系统建立到目录和文件。此外，符号链接指向的文件可以由任何编辑器编辑，只要路径不发生变化。符号链接存在一个与硬链接不同的问题：如果符号链接从一个目录指向另一个目录，则无法再通过链接访问。原因是链接文件包含了原始位置的路径。当文件位置更改时，链接会悬空；即它指向一个不存在的文件。以下会说明了这一点。

```
$ mv temp.soft /Chapter3
cat temp.soft: No such file or directory
```

假设 `temp.soft` 是指向 `/linux2e/examples/Chapter3` 的符号链接。使用 `mv` 命令将 `temp.soft` 移动到当前目录。`cat` 命令失败是因为链接仍然指向路径。这种结果是逻辑上的，但在硬链接中，只要移动的文件留在文件系统中，`cat` 命令就不会失败。

符号链接的其他缺点是 Linux 必须支持额外的文件类型（链接），并且为每个链接都要创建一个新文件。链接的创建填充了额外的 inode、存储文件所需的磁盘空间以及内核数据结构。符号链接还导致文件操作变慢，因为对文件的每次引用都必须打开并读取以到达实际文件。如果通过符号链接引用文件，则需要执行额外的磁盘访问。

在接后的练习中，你将使用 `ln -s` 和 `ls` 创建并识别软链接，并验证可以跨文件系统创建软链接。

## 练习 3

为练习 8.1 中创建的文件 `CH8Ex1` 建立一个软链接。将链接命名为 `CH8Ex1.soft`。验证链接已建立。你使用了什么命令来建立链接并验证创建？

## 练习 8.4

在你的 Linux 系统上执行 `ln -s ~/tmp` 命令。该命令的目的是？执行时发生了什么？结果合理吗？为什么或为什么不？

## 总结
