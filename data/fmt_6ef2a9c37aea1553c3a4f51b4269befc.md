
我们同时包含了`-a`选项（用于归档——导致递归并保留文件属性）和`-v`选项（详细输出），以在`foo`中制作`playground`目录的镜像。在命令运行时，我们会看到正在复制的文件和目录列表。最后，我们会看到如下的摘要消息：

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

请注意，没有文件列表。这是因为`rsync`检测到`~/playground`和`~/foo/playground`之间没有差异，因此它不需要复制任何内容。如果我们修改`playground`中的一个文件并再次运行`rsync`：

```
[me@linuxbox ~]$ touch playground/dir-099/file-Z
[me@linuxbox ~]$ rsync -av playground foo
building file list ... done
playground/dir-099/file-Z
sent 22685 bytes  received 42 bytes  45454.00 bytes/sec
total size is 3230  speedup is 0.14
```

我们看到`rsync`检测到了更改并仅复制了更新的文件。

作为一个实际示例，让我们考虑一下我们之前使用`tar`时所使用的那个想象中的外部硬盘。如果我们将该驱动器连接到系统，并且再次将其挂载在`/media/BigDisk`下，我们可以通过先在外部驱动器上创建一个名为`/backup`的目录，然后使用`rsync`将系统中最重要的内容复制到外部驱动器，从而执行有用的系统备份：

```
[me@linuxbox ~]$ mkdir /media/BigDisk/backup
[me@linuxbox ~]$ sudo rsync -av --delete /etc /home /usr/local /media/BigDisk/backup
```

在这个示例中，我们将`/etc`、`/home`和`/usr/local`目录从系统复制到了我们想象中的存储设备。我们包含了`--delete`选项，以删除备份设备上可能存在但在源设备上已不存在的文件（这在第一次备份时无关紧要，但在后续复制中会很有用）。重复连接外部驱动器并运行此`rsync`命令的流程将是一种有用（尽管不理想）的方式来保持小型系统备份。当然，这里使用别名也会有所帮助。我们可以创建一个别名并将其添加到`.bashrc`文件中以提供此功能：

```
alias backup='sudo rsync -av --delete /etc /home /usr/local /media/BigDisk/backup'
```

现在我们只需连接外部驱动器并运行`backup`命令即可完成任务。

## 使用 `rsync` 在网络上

`rsync`的真正优点之一是它可以用于在网络上复制文件。毕竟，`rsync`中的“r”代表“remote”，即远程。远程复制可以通过两种方式完成。第一种方式是使用安装了`rsync`以及远程 shell 程序（如`ssh`）的另一台系统。假设我们在本地网络上有一台硬盘空间充足的另一台系统，并且我们想使用远程系统而不是外部驱动器来执行备份操作。假设它已经有一个名为`/backup`的目录，我们可以在其中存放文件，我们可以这样做：

```
[me@linuxbox ~]$ sudo rsync -av --delete --rsh=ssh /etc /home /usr/local remote-sys:/backup
```

我们对命令做了两处修改以便于网络复制。首先，我们添加了`--rsh=ssh`选项，这指示`rsync`使用`ssh`程序作为其远程 shell。这样，我们就能使用`ssh`加密隧道安全地将数据从本地系统传输到远程主机。其次，我们通过在其名称前加上远程主机名（在本例中远程主机名为`remote-sys`）来指定远程主机。

`rsync`在网络上同步文件的第二种方式是使用`rsync`服务器。`rsync`可以配置为作为守护进程运行并监听传入的同步请求。这通常用于允许远程系统的镜像。例如，Red Hat Software 在其 Fedora 发行版的开发软件包下维护了一个庞大的软件包存储库。在发行版发布周期的测试阶段，让软件测试人员镜像此集合是很有用的。由于存储库中的文件经常更改（通常每天多次），因此通过定期同步而不是批量复制存储库来维护本地镜像是可取的。其中一个存储库保存在佐治亚理工学院；我们可以使用本地的`rsync`副本和他们的`rsync`服务器像这样镜像它：

```
[me@linuxbox ~]$ mkdir fedora-devel
[me@linuxbox ~]$ rsync -av --delete rsync://rsync.gtlib.gatech.edu/fedora-linux-core/development/i386/os fedora-devel
```

在这个示例中，我们使用远程`rsync`服务器的 URI，它由协议（`rsync://`）、远程主机名（`rsync.gtlib.gatech.edu`）以及存储库的路径名组成。

## 小结

我们查看了 Linux 及其他类 Unix 操作系统上常用的压缩和归档程序。对于归档文件，`tar`/`gzip`组合是类 Unix 系统上的首选方法，而`zip`/`unzip`则用于与 Windows 系统的互操作。最后，我们查看了`rsync`程序（个人最爱），它非常适合高效地在系统之间同步文件和目录。

## 进一步阅读

- 这里讨论的所有命令的手册页都写得很清楚，并且包含有用的示例。此外，GNU 项目为其版本的`tar`提供了一个很好的在线手册。它可以在这里找到：

# 19 – 正则表达式

在接下来的几章中，我们将学习用于处理文本的工具。正如我们所看到的，文本数据在所有类 Unix 系统（如 Linux）中都扮演着重要角色。但在我们充分领略这些工具提供的所有功能之前，必须先了解一项通常与这些工具最复杂用法相关的技术——正则表达式。

在探索命令行提供的众多功能和设施时，我们遇到了一些真正晦涩难懂的 shell 特性和命令，例如 shell 展开和引用、键盘快捷键、命令历史，更不用说`vi`编辑器了。正则表达式延续了这一“传统”，并且可以说（有人会认为）是其中最为晦涩难懂的特性。这并不是说花时间去学习它们不值得。恰恰相反，深入理解正则表达式将使我们能够完成令人惊叹的任务，尽管它们的全部价值可能不会立刻显现出来。

## 什么是正则表达式？

简而言之，正则表达式是用于识别文本模式的符号表示法。在某些方面，它们类似于 shell 中匹配文件和路径名的通配符方式，但规模要大得多。许多命令行工具和大多数编程语言都支持正则表达式，以便解决文本处理问题。然而，更让人困惑的是，并非所有正则表达式都是相同的；它们在不同的工具和编程语言之间略有差异。在讨论中，我们将仅限于 POSIX 标准中描述的正则表达式（这涵盖了大多数命令行工具），而不是许多编程语言（尤其是 Perl）所使用的规模更大、更丰富的符号集。

## `grep`

我们将用来处理正则表达式的主要程序是我们的老朋友`grep`。`grep`这个名字实际上源自短语“全局正则表达式打印”（global regular expression print），因此我们可以看出`grep`与正则表达式有关。本质上，`grep`在文本文件中搜索指定正则表达式的出现，并将包含匹配项的任何一行输出到标准输出。

到目前为止，我们一直使用固定字符串来使用`grep`，如下所示：

```
[me@linuxbox ~]$ ls /usr/bin | grep zip
```

这将列出`/usr/bin`目录中文件名包含子字符串“zip”的所有文件。

`grep`程序以这种方式接受选项和参数：

```
grep [options] regex [file...]
```

其中`regex`是一个正则表达式。

以下是常用的`grep`选项列表：

### 表20-1：`grep`选项

| 选项 | 描述 |
|---|---|
| `-i` | 忽略大小写。不区分大小写字符。也可以用`--ignore-case`指定。 |
| `-v` | 反向匹配。通常，`grep`会打印包含匹配项的行。此选项使`grep`打印每一行不包含匹配项。也可以用`--invert-match`指定。 |
| `-c` | 打印匹配次数（如果同时指定了`-v`选项，则为不匹配次数），而不是打印行本身。也可以用`--count`指定。 |
