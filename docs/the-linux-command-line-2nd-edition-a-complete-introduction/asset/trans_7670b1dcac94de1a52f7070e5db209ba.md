

(再次，使用带破折号参数的 f 选项)。

## zip

zip 程序既是压缩工具也是归档工具。该程序使用的文件格式 Windows 用户很熟悉，因为它可以读取和写入 .zip 文件。然而在 Linux 中，gzip 是主要的压缩程序，bzip2 紧随其后。

在最基本的使用中，zip 的调用方式如下：

zip options zipfile file...

例如，要制作我们 playground 的 zip 归档，我们会这样做：

```
[me@linuxbox ~]$ zip -r playground.zip playground
```

除非我们包含用于递归的 -r 选项，否则只会存储 playground 目录（但不包含其内容）。虽然 .zip 扩展名的添加是自动的，但我们为了清晰起见仍会包含文件扩展名。

在创建 zip 归档期间，zip 通常会显示如下一系列消息：

```
adding: playground/dir-020/file-Z (stored 0%)
adding: playground/dir-020/file-Y (stored 0%)
adding: playground/dir-020/file-X (stored 0%)
adding: playground/dir-087/ (stored 0%)
adding: playground/dir-087/file-S (stored 0%)
```

这些消息显示添加到归档中的每个文件的状态。zip 会使用两种存储方法之一将文件添加到归档中：要么“存储”文件而不进行压缩，如此处所示，要么“deflate”文件以执行压缩。存储方法后显示的数值表示实现的压缩量。由于我们的 playground 只包含空文件，因此其内容不会被压缩。

使用 unzip 程序提取 zip 文件的内容非常简单：

```
[me@linuxbox ~]$ cd foo
[me@linuxbox foo]$ unzip ../playground.zip
```

```
[me@linuxbox ~]$ ls -l /etc/ | zip ls-etc.zip -
adding: - (deflated 80%)
```

在此示例中我们将 ls 的输出通过管道传递给 zip。与 tar 类似，zip 将尾随的破折号解释为“对输入文件使用标准输入”。

unzip 程序允许其输出在指定 -p（管道）选项时发送到标准输出：

```
[me@linuxbox ~]$ unzip -p ls-etc.zip | less
```

我们触及了 zip/unzip 可以执行的一些基本操作。它们都有很多选项增加了灵活性，尽管其中一些是针对其他系统的特定平台选项。zip 和 unzip 的 man 手册都写得很好，包含有用的示例。然而，这些程序的主要用途是与 Windows 系统交换文件，而不是在 Linux 上执行压缩和归档，在 Linux 上 tar 和 gzip 更受青睐。

## 同步文件和目录

维护系统备份副本的一种常见策略涉及将一个或多个目录与位于本地系统（通常是某种可移动存储设备）或远程系统上的另一个目录（或多个目录）保持同步。例如，我们可能在本地有一个正在开发的网站副本，并不时将其与远程 Web 服务器上的“实时”副本同步。

在类 Unix 世界中，完成此任务的首选工具是 rsync。该程序可以通过使用 rsync 远程更新协议来同步本地和远程目录，该协议允许 rsync 快速检测两个目录之间的差异并执行将它们同步所需的最少复制量。这使得 rsync 相比其他类型的复制程序非常快速且经济高效。

rsync 的调用方式如下：

```
rsync options source destination
```

其中 source 和 destination 是以下之一：

- 本地文件或目录
- 远程文件或目录，形式为 [user@]host:path
- 使用 URI rsync://[user@]host[:port]/path 指定的远程 rsync 服务器

请注意，源或目标必须是一个本地文件。不支持远程到远程复制。

让我们在一些本地文件上试用 rsync。首先，让我们清空我们的 foo 目录：

```
[me@linuxbox ~]$ rm -rf foo/*
```

接下来，我们将 playground 目录与 foo 中的对应副本同步：

```
[me@linuxbox ~]$ rsync -av playground foo
```

我们同时包含了 -a 选项（用于归档——导致递归并保留文件属性）和 -v 选项（详细输出），以在 foo 中制作 playground 目录的镜像。在命令运行时，我们会看到正在复制的文件和目录列表。最后，我们会看到如下的摘要消息：

```
sent 135759 bytes  received 57870 bytes  387258.00 bytes/sec
total size is 3230  speedup is 0.02
```

表示执行的复制量。如果我们再次运行该命令，我们会看到不同的结果：

```
[me@linuxbox ~]$ rsync -av playground foo
building file list ... done
sent 22635 bytes  received 20 bytes  45310.00 bytes/sec
total size is 3230  speedup is 0.14
```

请注意，没有文件列表。这是因为 rsync 检测到 ~/playground 和 ~/foo/playground 之间没有差异，因此它不需要复制任何内容。如果我们修改 playground 中的一个文件并再次运行 rsync：

```
[me@linuxbox ~]$ touch playground/dir-099/file-Z
[me@linuxbox ~]$ rsync -av playground foo
building file list ... done
playground/dir-099/file-Z
sent 22685 bytes  received 42 bytes  45454.00 bytes/sec
total size is 3230  speedup is 0.14
```

