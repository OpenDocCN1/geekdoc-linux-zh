
## 第12章：压缩、系统备份与软件安装

完成本章学习后，您将能够：

- 概述常用压缩工具的功能
- 使用常用压缩工具压缩和解压缩文件
- 使用 `tar`、`cpio` 和 `dump` 命令执行系统备份
- 使用 `tar`、`cpio` 和 `restore` 命令查看和提取归档
- 使用光盘刻录软件将文件备份到 CD-RW 和 DVD-RW
- 描述常见的 Linux 软件类型
- 从源代码编译和安装软件包
- 使用 Red Hat 包管理器安装、管理和卸载软件包

在上一章中，您研究了定期执行的常见管理任务。在本章中，您将学习经常执行的任务，但重点在于与文件和软件相关的管理。您将从学习文件系统上常用于压缩文件的工具开始，随后讨论系统备份和归档工具。最后，您将了解适用于 Linux 系统的不同形式的软件，如何编译源代码以生成可用的程序，以及 Red Hat 包管理器的特性和使用方法。

### 压缩

有时，由于磁盘空间有限，您可能希望减小文件或一组文件的大小。您可能还希望压缩通过计算机网络（如互联网）发送的文件，以缩短传输时间。在这两种情况下，都有若干工具可以对文件执行一组标准指令以减小其大小，方法是剥离字符。此过程称为**压缩**，用于压缩文件的标准指令集被称为**压缩算法**。要解压缩文件，您只需反向运行压缩算法即可。

由于压缩工具使用不同的压缩算法，它们对类似类型的文件实现了不同的压缩率。压缩率被称为**压缩比**；如果一个压缩工具将文件压缩到其原始大小的 52%，则其压缩比为 48%。

Linux 用户有许多可用的压缩工具；本节考察了其中最常见的三个：

- `compress`
- `gzip`
- `bzip2`

#### compress 工具

`compress` 工具是大多数 UNIX 和 Linux 系统中常见的最古老的压缩工具之一。它使用的压缩算法称为自适应 Lempel-Ziv 编码（LZW），其平均压缩比为 40–50%。

要使用 `compress` 工具压缩文件，您可以将要压缩的文件作为**compress 命令**的参数指定。每个文件都会被重命名并加上 `.Z` 文件扩展名，以指示其已被压缩。此外，您可以使用 `compress` 命令的 `-v`（详细）选项在压缩期间显示压缩比。以下输出显示了 `samplefile` 和 `samplefile2` 文件在压缩前后的文件名和大小：

```text
[root@server1 root]# ls -1
total 28
drwx-- --- - 3 root root 4096 Jul 21 08:15 Desktop
-rw-r--r-- 1 root root 20239 Jul 21 08:15 samplefile
-rw-rw-r-- 1 root root 574 Jul 21 08:15 samplefile2
[root@server1 root]# compress -v samplefile samplefile2
samplefile: -- replaced with samplefile.Z Compression: 48.06%
samplefile2: -- replaced with samplefile2.Z Compression: 26.13%
[root@server1 root]# ls -1
total 20
drwx-- --- - 3 root root 4096 Jul 21 08:15 Desktop
-rw-rw-r-- 1 root root 424 Jul 21 08:18 samplefile2.Z
-rw-r--r-- 1 root root 10512 Jul 21 08:15 samplefile.Z
[root@server1 root]#
```

![](img/09bf13b782f71165e17bb3839040c96a_466_0.png)

`compress` 工具保留其压缩的每个文件的原始所有权、修改时间和访问时间。

默认情况下，`compress` 工具不压缩符号链接或非常小的文件；若要强制 `compress` 工具压缩这些文件，您必须使用 `-f` 选项。您可以使用 `-r` 选项并指定目录名作为 `compress` 命令的参数，来压缩某个目录中的所有文件。

压缩后，可以使用**zcat 命令**来显示压缩文件的内容，如下面的输出所示：

```text
[root@server1 root]# zcat samplefile2.Z
Hi there, I hope this day finds you well.

Unfortunately we were not able to make it to your dining
room this year while vacationing in Algonquin Park - I
especially wished to see the model of the Highland Inn
and the train station in the dining room.

I have been reading on the history of Algonquin Park but
no where could I find a description of where the Highland
Inn was originally located on Cache lake.

If it is no trouble, could you kindly let me know such that
I need not wait until next year when I visit your lodge?

Regards,
Mackenzie Elizabeth
[root@server1 root]#
```

![](img/09bf13b782f71165e17bb3839040c96a_467_0.png)

要解压缩使用 `compress` 工具压缩的文件，只需使用**uncompress 命令**后跟要解压缩的文件名。这将恢复原始文件名。以下输出解压缩并显示前面创建的 `samplefile.Z` 和 `samplefile2.Z` 文件的文件名：

```text
[root@server1 root]# uncompress -v samplefile.Z samplefile2.Z
samplefile.Z: -- replaced with samplefile
samplefile2.Z: -- replaced with samplefile2
[root@server1 root]# ls -l
total 28
drwx------     3 root  root    4096 Jul 21 08:15 Desktop
-rw-r--r--     1 root  root    20239 Jul 21 08:15 samplefile
-rw-rw-p--     1 root  root      574 Jul 21 08:18 samplefile2
[root@server1 root]#
```

![](img/09bf13b782f71165e17bb3839040c96a_467_1.png)

使用 `uncompress` 命令时，您可以省略 `.Z` 扩展名；命令 `uncompress -v samplefile samplefile2` 将取得与前面输出中所示命令相同的结果。

此外，`compress` 工具是一个过滤器命令，它可以从标准输入获取信息并将其发送到标准输出。例如，要将 `who` 命令的输出发送到 `compress` 工具并将压缩后的信息保存为名为 `file.Z` 的文件，您可以执行以下命令：

```text
[root@server1 root]# who | compress -v > file.Z
Compression: 21.35%
[root@server1 root]#
```

随后，您可以使用 `zcat` 命令显示 `file.Z` 的内容，或使用 `uncompress` 命令对其进行解压缩，如下面的输出所示：

```text
[root@server1 root]# zcat file.Z
root pts/1 Jul 20 19:22 (3.0.0.2)
root tty5 Jul 15 19:03
root pts/1 Jul 17 19:58
[root@server1 root]# uncompress -v file.Z
file.Z: -- replaced with file
[root@server1 root]#
```

表 12-1 总结了 `compress` 工具常用选项。

**表 12-1 compress 工具常用选项**

| 选项 | 描述 |
| :--- | :--- |
| `-c` | 与 `uncompress` 命令一起使用时，它将压缩文件的内容显示到标准输出（功能与 `zcat` 命令相同）。 |
| `-f` | 与 `compress` 命令一起使用时，可用于压缩符号链接。与 `uncompress` 命令一起使用时，它会在不提示用户的情况下覆盖现有文件。 |
| `-r` | 指定递归地压缩或解压缩指定目录内的所有文件。 |
| `-v` | 在压缩和解压缩期间显示详细输出（压缩比和文件名）。 |

#### gzip 工具

GNU zip（`gzip`）工具使用 Lempel-Ziv 压缩算法（LZ77），该算法与 `compress` 工具使用的算法略有不同。通常，该算法比 `compress` 使用的算法提供更高的压缩率；`gzip` 的平均压缩比为 60–70%。

与 `compress` 工具类似，除非提供 `-f` 选项，否则 `gzip` 工具不会压缩符号链接，并且可以使用 `-r` 选项压缩某个目录中的所有文件。此外，压缩文件的所有权、修改时间和访问时间默认都会保留，并且可以使用 `gzip` 命令的 `-v` 选项来显示压缩比和文件名。然而，`gzip` 默认使用 `.gz` 文件扩展名。

