
root@server1 # `ls -l`

total 2

drwx-xr-x 3 root 4096 Jul 21 08:15 Desktop

-rw-r--r-- 1 root 20239 Jul 21 08:15 samplefile

-rw-r--r-- 1 root 574 Jul 21 08:18 sample2

root@server1]# `compress -v samplefile sample2`

samplefile: replaced with samplefile.Z, 48.06%

sample2: replaced with sample2.Z, 26.13%

root@server1]# `ls -1`

```
`compress` 工具保留了它压缩的每个文件的所有者、修改时间和访问时间。

默认情况下，`compress` 工具不压缩符号链接或极小文件；要强制 `compress` 工具压缩这些文件，必须使用 `-f` 选项。你可以通过使用 `-r` 选项并将目录名作为 `compress` 命令的参数来压缩目录下的所有文件。

压缩后，可以使用 `zcat` 命令显示压缩文件的内容，如下所示：

```
root@server1]# `zcat samplefile.Z`

Hi there, I hope this day finds you well.

Unfortunately we were not able to make it to your dining room this year while vacationing in Algonquin Park - I especially wished to see the model of.

I have一直在阅读阿尔松冈国家公园的历史，但哪里都没有找到高地酒店在凯什湖上的原始位置描述。

如果不麻烦的话，能否告诉我，这样我就不必等到明年光临你们的旅馆了？

此致，

Mackenzie Elizabeth
```

还存在 `zmore` 命令和 `zless` 命令，可以逐页查看压缩文件的内容。

要解压缩用 `compress` 工具压缩的文件，只需使用 `uncompress` 命令后跟要解压缩的文件名。

# 524 第12章 压缩、系统备份与软件安装

恢复原始文件名。以下输出解压并显示了之前创建的 samplefile.Z 和 samplefile2.Z 文件名：

```
[root@server1] # `uncompress -v samplefile.Z samplefile2.Z`

samplefile.Z: -- replaced with samplefile

samplefile2.Z: -- replaced with samplefile2

[root@server1]# `ls -l`
```

```
total 28

drwx-r-x-- 3 root root 4096 Jul 21 08:15 Desktop

-rw-r--r-- 1 root root 2023 Jul 21 08:15 samplefile

-rw-r--r-- 1 root root 574 Jul 21 08:18 samplefile2

[root@server1]#
```

![](img/9ee5f91f3446575a1e6ce62c54cae5d2_545_0.png)

在使用 `uncompress` 命令时，可以省略 `.Z` 扩展；执行 `uncompress -v samplefilesample2` 命令的效果与前面输出中显示的命令相同。

此外，`compress` 实用是一个过滤命令，可以从标准输入（Standard Input）获取信息并发送到标准输出（Standard Output）。例如，要将 `who` 命令的输出发送给 `compress` 实用并将压缩后的信息保存到文件中，可以执行以下命令：

```
[root@server1] root# `who | compress -v >file.Z`

Compression: 21.35%

[root@server1]#
```

之后，你可以使用 `zcat` 命令显示 `file.Z` 的内容，或使用 `uncompress` 将其解压，如下所示：

```
[root@server1]# `zcat file.Z`

root pts/1 Jul 20 19:22 (3.0.0.2)

root tty5 Jul 15 19:03

root pts/1 Jul 17 17:58

[root@server1]# `uncompress -v file.Z`

file.Z: -- replaced with file

[root@server1]#
```

表 12-1 汇总了常用于 `compress` 实用工具的选项。

表 12-1 `compress` 实用工具常用的选项

| 选项 | 描述 |
| - | - |
| `-c` | 与 `uncompress` 命令配合使用时，将压缩文件的内容显示到标准输出（与 `zcat` 命令相同）。 |
| `-f` | 与 `compress` 命令配合使用时，用于压缩符号链接。与 `compress` 命令配合使用时，会在不提示用户的情况下覆盖任何现有文件。 |
| `-r` | 指定递归地压缩或解压指定目录下的所有文件。 |
| `-v` | 在压缩和解过程中显示详细输出（压缩率和文件名）。 |

## zip 实用工具

GNU `zip` (`zip`) 实用工具使用 Lempel-Ziv 压缩算法 (`LZ77`)，该算法与 `compress` 实用工具使用的略不同。通常，该算法产生的压缩效果比 `compress` 使用的更好；`zip` 的平均压缩率为 60–70%。

与 `compress` 实用工具类似，除非给出 `-f` 选项，否则 `zip` 实用工具不会压缩符号链接，可以使用 `-r` 选项压缩目录中的所有文件。此外，压缩文件的所有者、修改时间和访问时间默认会被保留，`zip` 命令的 `-v` 选项可显示压缩率和文件名。然而，`zip` 默认使用 `.gz` 扩展名。

要压缩先前的 `samplefile` 和 `sample2` 文件并查看压缩率，可以使用以下命令：

```
@root@server1 # `zip -v samplefile samplefile`

samplefile: 56.8% -- replaced with samplefile

samplefile2: 40.7% -- replaced with samplefile2

@root@server1 #
```

你也可以使用 `zcat` 和 `zmore` 将压缩文件的内容发送到标准输出。同样，`zip` 命令可以通过标准输入接受信息。因此，要将 `date` 命令的输出压缩到名为 `file.gz` 的文件中并查看其内容，可以使用以下命令：

```
@root@server1 # `date | zip -v >file.gz`

- 6.8%

@root@server1 # `zcat file.gz`

Mon Jul 25 19:24 2005

@root@server1 #
```

要解压输出中的 `file.gz`，可以对 `gzip` 命令使用 `-d` 选项，如下所示：

```
[root@server1]# `gunzip -v file.gz`

file.gz: -6.8% -- replaced with file

[root@server1]#
```

与 `uncompress` 命令一样，除非指定 `-f` 选项，否则 `gunzip` 命令会提示覆盖现有文件。此外，解压文件时可以省略 `.gz` 扩展名，如下：

```
[root@server1]# `ls -l`

total 20

drwx-r-x-- 3 root root 4096 Jul 21 08:15 Desktop

-rw-r--r-- 1 root root 370 Jul 21 08:18 sample2.gz

-rw-r--r-- 1 root root 876 Jul 21 08:15 samplefile.gz

[root@server1]# `gunzip -v samplefile`

samplefile.gz: 56.8% -- replaced with samplefile

samplefile.gz: 40.7% -- replaced with samplefile

[root@server1]# `ls -l`

total 28

drwx-r-x-- 3 root root 4096 Jul 21 08:15 Desktop

-rw-r--r-- 1 root root 2023 Jul 21 08:15 samplefile

-rw-r--r-- 1 root root 574 Jul 21 08:18 sample2

[root@server1]#
```

`gzip` 优于 `compress` 实用工具的最大优势之一是可以通过数字选项控制压缩级别。`-9` 选项被称为“最佳压缩”，以时间为代价获得最高的压缩率。如果未指定压缩级别，`gzip` 命令假设级别为 6。

以下命令使用快速压缩压缩之前的 `samplefile` 并显示压缩率：
