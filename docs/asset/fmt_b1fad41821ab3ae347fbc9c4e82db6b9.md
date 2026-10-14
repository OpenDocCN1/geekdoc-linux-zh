
## 回到游乐场

现在是时候将 `find` 用于一些（几乎）实际的用途了。我们将创建一个游乐场，并尝试使用我们学到的一些知识。

首先，让我们创建一个包含许多子目录和文件的游乐场：

```
[me@linuxbox ~]$ mkdir -p playground/dir-{00{1..9},0{10..99},100}
[me@linuxbox ~]$ touch playground/dir-{00{1..9},0{10..99},100}/file-{A..Z}
```

惊叹于命令行的威力吧！凭借这两行命令，我们创建了一个游乐场目录，其中包含一百个子目录，每个子目录包含二十六个空文件。试试用图形界面完成这件事！

我们完成这一神奇操作的方法涉及一个熟悉的命令 `mkdir`、一种奇特的 shell 展开（花括号展开）和一个新命令 `touch`。通过将 `mkdir` 的 `-p` 选项（该选项使 `mkdir` 创建指定路径的父目录）与花括号展开相结合，我们能够创建一百个目录。

`touch` 命令通常用于设置或更新文件的访问时间、状态改变时间和修改时间。然而，如果文件名参数对应一个不存在的文件，则会创建一个空文件。

在我们的游乐场中，我们创建了一百个名为 `file-A` 的文件实例。让我们找出它们：

```
[me@linuxbox ~]$ find playground -type f -name 'file-A'
```

注意，与 `ls` 不同，`find` 不会按排序顺序输出结果。其顺序由存储设备的布局决定。为了确认我们确实有一百个该文件的实例，我们可以用下面的方式验证：

```
[me@linuxbox ~]$ find playground -type f -name 'file-A' | wc -l
100
```

接下来，让我们看看如何根据修改时间查找文件。这在创建备份或按时间顺序整理文件时会很有帮助。为此，我们首先创建一个参考文件，以便与之比较修改时间：

```
[me@linuxbox ~]$ touch playground/timestamp
```

这将创建一个名为 `timestamp` 的空文件，并将其修改时间设置为当前时间。我们可以通过另一个方便的命令 `stat` 来验证这一点，`stat` 是 `ls` 的一种增强版。`stat` 命令会显示系统所了解的关于文件及其属性的所有信息：

```
[me@linuxbox ~]$ stat playground/timestamp
  File: `playground/timestamp'
  Size: 0          Blocks: 0          IO Block: 4096 regular empty file
Device: 803h/2051d Inode: 14265061 Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1001/ me)   Gid: ( 1001/ me)
Access: 2008-10-08 15:15:39.000000000 -0400
Modify: 2008-10-08 15:15:39.000000000 -0400
Change: 2008-10-08 15:15:39.000000000 -0400
```

如果我们再次 `touch` 该文件，然后用 `stat` 检查它，我们会看到文件的时间已经更新：

```
[me@linuxbox ~]$ touch playground/timestamp
[me@linuxbox ~]$ stat playground/timestamp
  File: `playground/timestamp'
  Size: 0          Blocks: 0          IO Block: 4096 regular empty file
Device: 803h/2051d Inode: 14265061 Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1001/ me)   Gid: ( 1001/ me)
Access: 2008-10-08 15:23:33.000000000 -0400
Modify: 2008-10-08 15:23:33.000000000 -0400
Change: 2008-10-08 15:23:33.000000000 -0400
```

接下来，让我们使用 `find` 更新一些游乐场文件：

```
[me@linuxbox ~]$ find playground -type f -name 'file-B' -exec touch '{}' ';'
```

这会更新游乐场中所有名为 `file-B` 的文件。接下来，我们将使用 `find`，通过将所有文件与参考文件 `timestamp` 进行比较来识别已更新的文件：

```
[me@linuxbox ~]$ find playground -type f -newer playground/timestamp
```

结果包含所有一百个 `file-B` 实例。由于我们在更新 `timestamp` 之后对游乐场中所有名为 `file-B` 的文件执行了 `touch`，它们现在比 `timestamp` “更新”，因此可以通过 `-newer` 测试识别出来。

最后，让我们回到之前执行的不良权限测试，并将其应用于游乐场：

```
[me@linuxbox ~]$ find playground \( -type f -not -perm 0600 \) -or \( -type d -not -perm 0700 \)
```

这条命令列出了游乐场中的所有一百个目录和两千六百个文件（以及 `timestamp` 和游乐场本身，总共 2702 个），因为它们都不符合我们对“良好权限”的定义。凭借我们对操作符和动作的了解，我们可以在该命令中添加动作，为游乐场中的文件和目录应用新的权限：

```
[me@linuxbox ~]$ find playground \( -type f -not -perm 0600 -exec chmod 0600 '{}' ';' \) -or \( -type d -not -perm 0711 -exec chmod 0700 '{}' ';' \)
```

在日常使用中，我们可能会发现发出两条命令（一条用于目录，一条用于文件）比这一条大型复合命令更容易，但知道我们可以这样做也很好。这里的重要之处在于理解操作符和动作如何结合使用以执行有用的任务。

### 选项

最后，我们来说说选项。选项用于控制 `find` 搜索的范围。在构建 `find` 表达式时，它们可以与其他测试和动作一起使用。以下是最常用选项的列表：

表 18-7：`find` 选项

| 选项 | 描述 |
|---|---|
| `-depth` | 指示 `find` 先处理目录中的文件，再处理目录本身。当指定 `-delete` 动作时，此选项会自动应用。 |
| `-maxdepth levels` | 设置 `find` 在执行测试和操作时，在目录树中下降的最大层级数。 |
|  | actions. |
|---|---|
| `-mindepth levels` | 设置 `find` 在对目录树应用测试和操作之前将下降的最小层数。 |
| `-mount` | 指示 `find` 不要遍历安装在其他文件系统上的目录。 |
| `-noleaf` | 指示 `find` 不要基于其正在搜索类 Unix 文件系统的假设来优化其搜索。在扫描 DOS/Windows 文件系统和 CD-ROM 时需要此选项。 |

### Further Reading

- `locate`、`updatedb`、`find` 和 `xargs` 程序都是 GNU 项目的 *findutils* 包的一部分。GNU 项目提供了一个网站，其中包含广泛的在线文档，质量相当不错，如果你在高安全环境中使用这些程序，应该阅读：

- http://www.gnu.org/software/findutils/

## 19 – Archiving And Backup

计算机系统管理员的主要任务之一是保持系统数据安全。一种方法是及时备份系统文件。即使你不是系统管理员，复制东西以及在不同位置和不同设备之间移动大量文件集合也经常很有用。

在本章中，我们将介绍用于管理文件集合的几个常用程序。有文件压缩程序：

- `gzip` – 压缩或扩展文件

- `bzip2` – 一种块排序文件压缩器

归档程序：

- `tar` – 磁带归档实用程序

- `zip` – 打包并压缩文件

以及文件同步程序：

- `rsync` – 远程文件和目录同步

### Compressing Files

在计算历史上，一直在努力将尽可能多的数据放入最小的可用空间中，无论该空间是内存、存储设备还是网络带宽。我们今天习以为常的许多数据服务，例如便携式音乐播放器、高清电视或宽带互联网，都得益于有效的 *数据压缩* 技术。
