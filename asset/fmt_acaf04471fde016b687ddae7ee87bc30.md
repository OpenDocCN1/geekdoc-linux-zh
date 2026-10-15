
有损。另一方面，有损压缩在压缩过程中删除数据以允许应用更多压缩。当有损文件被恢复时，它与原始版本不匹配；相反，它是一个接近的近似。`JPEG`（用于图像）和 `MP3`（用于音乐）是有损压缩的例子。

在我们的讨论中，我们将只关注无损压缩，因为计算机上的大多数数据都不能容忍任何数据丢失。

## gzip

`gzip` 程序用于压缩一个或多个文件。执行时，它会用原始文件的压缩版本替换原始文件。相应的 `gunzip` 程序用于将压缩文件恢复为原始的未压缩形式。下面是一个示例：

```
[me@linuxbox ~]$ ls -l /etc > foo.txt
[me@linuxbox ~]$ ls -l foo.*
-rw-r--r-- 1 me me 15738 2018-10-14 07:15 foo.txt
[me@linuxbox ~]$ gzip foo.txt
[me@linuxbox ~]$ ls -l foo.*
-rw-r--r-- 1 me me 3230 2018-10-14 07:15 foo.txt.gz
[me@linuxbox ~]$ gunzip foo.txt
[me@linuxbox ~]$ ls -l foo.*
-rw-r--r-- 1 me me 15738 2018-10-14 07:15 foo.txt
```

在这个示例中，我们从目录列表创建了一个名为 `foo.txt` 的文本文件。接下来，我们运行 `gzip`，它用名为 `foo.txt.gz` 的压缩版本替换了原始文件。在 `foo.*` 的目录列表中，我们可以看到原始文件已被压缩版本替换，并且压缩版本的大小约为原始文件的五分之一。我们还可以看到压缩文件具有与原始文件相同的权限和时间戳。

接下来，我们运行 `gunzip` 程序来解压缩文件。之后，我们可以看到文件的压缩版本已被原始文件替换，权限和时间戳同样得以保留。

`gzip` 有许多选项，如表 18-1 所描述。

表 18-1：`gzip` 选项

| Option | Long option | Description |

|---|---|---|

| -c | --stdout --to-stdout | Write output to standard output and keep the original files. |

| -d | --decompress --uncompress | Decompress. This causes gzip to act like gunzip. |

| -f | --force | Force compression even if a compressed version of the original file already exists. |

| -h | --help | Display usage information. |

| -l | --list | List compression statistics for each file compressed. |

| -r | --recursive | If one or more arguments on the command line is a directory, recursively compress files contained within them. |

| -t | --test | Test the integrity of a compressed file. |

| -v | --verbose | Display verbose messages while compressing. |

| -number |  | Set amount of compression. number is an integer in the range of 1 (fastest, least compression) to 9 (slowest, most compression). The values 1 and 9 may also be expressed as --fast and --best, respectively. The default value is 6. |

让我们回到之前的示例。

```
[me@linuxbox ~]$ gzip foo.txt
[me@linuxbox ~]$ gzip -tv foo.txt.gz
foo.txt.gz: OK
[me@linuxbox ~]$ gzip -d foo.txt.gz
```

在这里，我们用名为 `foo.txt.gz` 的压缩版本替换了 `foo.txt`。接下来，我们使用 `-t` 和 `-v` 选项测试了压缩版本的完整性。最后，我们将文件解压缩为原始形式。

`gzip` 还可以通过标准输入和输出以有趣的方式使用。

```
[me@linuxbox ~]$ ls -l /etc | gzip > foo.txt.gz
```

此命令创建了目录列表的压缩版本。

`gunzip` 程序用于解压缩 `gzip` 文件，它假定文件名以扩展名 `.gz` 结尾，因此无需指定它，只要指定的名称不与现有未压缩文件冲突即可。

```
[me@linuxbox ~]$ gunzip foo.txt
```

如果我们的目标只是查看压缩文本文件的内容，我们可以这样做：

```
[me@linuxbox ~]$ gunzip -c foo.txt | less
```

另外，`gzip` 随附有一个名为 `zcat` 的程序，它等同于带 `-c` 选项的 `gunzip`。它可以像 `cat` 命令一样用于 `gzip` 压缩文件。

```
[me@linuxbox ~]$ zcat foo.txt.gz | less
```

## TIP

*There is a zless program, too. It performs the same function as the previous pipeline.*

## bzip2

`bzip2` 程序由 Julian Seward 编写，与 `gzip` 类似，但使用不同的压缩算法，在压缩速度的代价下实现了更高的压缩率。在大多数方面，它的工作方式与 `gzip` 相同的方式。 用 `bzip2` 压缩的文件使用 `.bz2` 作为扩展名。

```
[me@linuxbox ~]$ ls -l /etc > foo.txt
[me@linuxbox ~]$ ls -l foo.txt
-rw-r--r-- 1 me me 15738 2018-10-17 13:51 foo.txt
[me@linuxbox ~]$ bzip2 foo.txt
[me@linuxbox ~]$ ls -l foo.txt.bz2
-rw-r--r-- 1 me me 2792 2018-10-17 13:51 foo.txt.bz2
[me@linuxbox ~]$ bunzip2 foo.txt.bz2
```

正如我们所见，`bzip2` 可以像 `gzip` 一样使用。 我们为 `gzip` 讨论过的所有选项（`-r` 除外）也在 `bzip2` 中受支持。 需要注意的是，压缩级别选项（`-number`）对 `bzip2` 来说含义略有不同。 `bzip2` 带有 `bunzip2` 和 `bzip2` 用于解压缩文件。

`bzip2` 还附带 `bzip2recover` 程序，它会尝试恢复损坏的 `.bz2` 文件。

## 不要成为压缩强迫症

我偶尔会看到有人尝试对已经使用有效压缩算法压缩过的文件进行压缩，比如这样做：

```
$ gzip picture.jpg
```

不要这样做。 你很可能只是在浪费时间和空间！ 如果你对已经压缩的文件应用压缩，通常会得到一个更大的文件。 这是因为所有压缩技术都会在文件中添加一些开销来描述压缩。 如果你尝试压缩一个已经不包含冗余信息的文件，压缩通常不会产生任何节省来抵消额外的开销。

## 归档文件

与压缩经常一起使用的常见文件管理任务是归档。 归档是将许多文件收集起来捆绑到单个大文件中的过程。 归档通常作为系统备份的一部分进行。 它也用于将旧数据从系统移动到某种长期存储。

## tar

在类 Unix 的软件世界中，`tar` 程序是归档文件的经典工具。 它的名字，缩写自 tape archive，揭示了它作为制作备份磁带的工具的根源。 虽然它仍然用于该传统任务，但在其他存储设备上同样擅长。 我们经常看到以 `.tar` 或 `.tgz` 结尾的文件名，分别表示“普通”`tar` 归档和 `gzipped` 归档。 `tar` 归档可以由一组单独的文件、一个或多个目录层次结构，或两者的混合组成。 命令语法如下：

```
tar mode[options] pathname...
```

这里，`mode` 是表 18-2 中列出的操作模式之一（此处仅显示部分列表；请参阅 `tar` 手册页以获取完整列表）。

Table 18-2: `tar` Modes

| Mode | Description |

|------|-------------|

| c | Create an archive from a list of files and/or directories. |

| x | Extract an archive. |
