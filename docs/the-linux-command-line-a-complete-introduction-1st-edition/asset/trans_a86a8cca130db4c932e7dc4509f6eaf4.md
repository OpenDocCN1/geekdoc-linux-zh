

tar 处理归档中路径名的另一种有趣行为。路径名的默认值为相对路径，而不是绝对路径。tar 在创建归档时只是简单地删除路径名开头的斜杠即可实现这一点。为了演示，我们将重新创建我们的归档，这次指定绝对路径名：

```
[me@linuxbox foo]$ cd
[me@linuxbox ~]$ tar cf playground2.tar ~/playground
```

请记住，~/playground 在我们按下回车键时会被展开为 /home/me/playground，因此我们将为演示获得一个绝对路径名。接下来，我们将像之前一样提取归档并观察会发生什么：

```
[me@linuxbox ~]$ cd foo
[me@linuxbox foo]$ tar xf ../playground2.tar
[me@linuxbox foo]$ ls
home playground
[me@linuxbox foo]$ ls home
me
[me@linuxbox foo]$ ls home/me
playground
```

在这里我们可以看出，当我们提取第二个归档时，它会相对于我们当前的工作目录 ~/foo 重新创建目录 home/me/playground，而不是相对于根目录，如使用绝对路径名时那样。这看起来可能是一种奇怪的工作方式，但实际上这样更有用，因为它允许我们将归档提取到任何位置，而不是被迫提取到其原始位置。重复该练习并加上详细选项 v 将更清晰地显示正在发生的情况。

让我们考虑一个假设的但实用的 tar 使用示例。想象我们想将 home 目录及其内容从一台系统复制到另一台系统，并且我们有一个可以用于传输的大型 USB 硬盘。在我们的现代 Linux 系统上，该驱动器会被“自动”挂载到 /media 目录。让我们再假设当我们连接它时磁盘的卷名为 BigDisk。要创建 tar 归档，我们可以执行以下操作：

```
[me@linuxbox ~]$ sudo tar cf /media/BigDisk/home.tar /home
```

归档文件写入后，我们卸载驱动器并将其连接到第二台计算机。同样，它被挂载在 /media/BigDisk。要提取归档，我们这样做：

```
[me@linuxbox2 ~]$ cd /
[me@linuxbox2 /]$ sudo tar xf /media/BigDisk/home.tar
```

这里重要的是要看到，我们必须先更改目录到 /，以便提取相对于根目录进行，因为归档中的所有路径名都是相对的。

在提取归档时，可以限制提取的内容。例如，如果我们想从归档中提取单个文件，可以这样做：

```
tar xf archive.tar pathname
```

通过在命令后添加尾部的路径名，我们确保 tar 只会恢复指定的文件。可以指定多个路径名。请注意，路径名必须是与存储在归档中完全相同的完整相对路径名。在指定路径名时，通常不支持通配符；然而，GNU 版本的 tar（这是 Linux 发行版中最常找到的版本）使用 --wildcards 选项支持它们。以下是使用我们之前的 playground.tar 文件的示例：

```
[me@linuxbox ~]$ cd foo
[me@linuxbox foo]$ tar xf ../playground2.tar --wildcards 'home/me/playground/dir-*/file-A'
```

此命令将仅提取与指定路径名匹配的文件，包括通配符 dir-*。

tar 通常与 find 结合使用来生成归档。在此示例中，我们将使用 find 来生成要包含在归档中的文件集：

```
[me@linuxbox ~]$ find playground -name 'file-A' -exec tar rf playground.tar {} \;
```

在这里我们使用 find 匹配 playground 中所有名为 file-A 的文件，然后使用 -exec 动作调用 tar 以追加模式 r 将匹配的文件添加到归档 playground.tar

使用 find 与 tar 结合是创建目录树或整个系统的增量备份的好方法。通过使用 find 匹配比时间戳文件更新的文件，我们可以创建仅包含比上次归档更新的文件的归档，前提是每次创建归档后立即更新时间戳文件。

tar 还可以同时使用标准输入和输出。以下是一个综合示例：

```
[me@linuxbox foo]$ cd
[me@linuxbox ~]$ find playground -name 'file-A' | tar cf - --files-from=- | gzip > playground.tgz
```

在此示例中，我们使用 find 程序生成匹配文件的列表并将其通过管道传输到 tar。如果指定文件名 -，则表示标准输入或输出，根据需要使用。顺便说一下，使用 - 表示标准输入/输出的约定也被许多其他程序使用。--files-from 选项（也可以指定为 -T）使 tar 从文件而不是命令行读取其路径名列表。最后，tar 生成的归档被通过管道传输到 gzip 以创建压缩归档 playground.tgz。.tgz 扩展名是 gzip 压缩 tar 文件的惯用扩展名。.tar.gz 扩展名有时也使用。

