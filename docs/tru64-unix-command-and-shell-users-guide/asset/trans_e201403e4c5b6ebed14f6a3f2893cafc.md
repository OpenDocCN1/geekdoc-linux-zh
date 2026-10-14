

- 硬链接只能让你链接同一文件系统中的文件。当你创建硬链接时，实际上是为同一个文件提供了另一个名称。一个文件的所有硬链接名称（包括原始名称）都是平等的。认为某个文件名是真实名称、另一个只是链接，是不正确的。

- 软链接或符号链接可以让你链接文件和目录。此外，你还可以在不同文件系统之间链接文件和目录。符号链接实际上是一个独立的文件，其中包含指向另一个文件或目录的指针。这个指针就是目标文件或目录的路径名。只有原始文件名才是该文件或目录的真实名称。与硬链接不同，软链接实际上只是一个链接。

无论使用硬链接还是软链接，通过一个名称对文件所做的更改，都会在通过另一个名称查看该文件时体现出来。

硬链接与软链接的一个主要区别体现在删除操作上。具有硬链接名称的文件会一直存在，直到其所有名称都被删除。具有软链接名称的文件在其原始名称被删除后就会消失；任何剩余的软链接随后会指向一个不存在的文件。参见第 3.4.5 节。

## 3.4.2 链接与文件系统

在本讨论中使用的术语“文件系统”与本书先前的用法有所不同。此前，文件系统被定义为将文件组织到目录结构中的一种有效安排。在这里，这个术语获得了更精确的含义：单个磁盘分区中所包含的文件和目录。磁盘分区是物理磁盘或其一部分，已被准备好用于容纳文件目录。

你可以使用 df 命令来查找操作系统中包含某个特定目录的磁盘分区名称。下面是一个示例，其中 df 显示目录 /u1/info 和 /etc 位于不同的文件系统中，而 /etc 和 /tmp 位于同一文件系统中：

```
$ df /u1/info
Filesystem 512-blks  used avail capacity Mounted on
/dev/rz2c   196990  163124  14166    92%   /u1
$ df /etc
Filesystem 512-blks  used avail capacity Mounted on
/dev/rz3a   30686   19252   8364    70%   /
$ df /tmp
Filesystem 512-blks  used avail capacity Mounted on
/dev/rz3a   30686   19252   8364    70%   /
$
```

有关 df 命令的更多信息，请参阅 df(1) 参考页。

## 3.4.3 使用链接

要在同一文件系统中链接文件，请使用以下命令格式：

```
ln /dirname1/filename1 /dirname2/filename2
```

/dirname1/filename1 条目是现有文件的路径名。/dirname2/filename2 条目是同一文件系统中要链接到现有 /dirname1/filename1 的新文件名的路径名。如果你在同一目录中链接文件，dirname1 和 dirname2 参数是可选的。

如果要在不同文件系统之间链接文件和目录，可以创建符号链接。要创建符号链接，请在 ln 命令序列中添加 -s 标志，并指定两个文件的完整路径名。用于符号链接的 ln 命令采用以下形式：

```
ln -s /dirname1/filename1 /dirname2/filename2
```

/dirname1/filename1 条目是现有文件的路径名。/dirname2/filename2 条目是不同文件系统或同一文件系统中新文件名的路径名。

在示例 3-5 中，你使用 ln 命令将新文件名 checkfile 链接到名为 file3 的现有文件。然后使用 more 命令验证 file3 和 checkfile 是同一文件的两个名称。

### 示例 3-5：链接文件

```
$ ln file3 checkfile 1
$ more file3 2
You will find that vi is a useful 3
editor that has many features. 3
$ more checkfile 4
You will find that vi is a useful 3
editor that has many features. 3
$
```

以下列表项与示例中的编号相对应：

- 1 在两个文件之间创建硬链接。
- 2 显示 file3 的文本。
- 3 现在显示 checkfile 的文本。
- 4 注意，file3 和 checkfile 包含相同的信息。当你通过另一个名称访问该文件时，通过一个名称对其所做的任何更改都会显示出来。例如，更新 file3 也会更新 checkfile。

如果你的两个文件位于两个不同文件系统中的目录中，则需要在它们之间创建符号链接。例如，要将 /reports 目录中名为 newfile 的文件链接到

