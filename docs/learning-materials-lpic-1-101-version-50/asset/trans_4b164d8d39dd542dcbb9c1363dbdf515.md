
进程的标准输出会被管道捕获。假设你需要在屏幕上经历一个漫长的编译过程，同时希望将标准输出和标准错误都保存到一个文件中以便后续检查。假设当前目录中没有 *Makefile*，以下命令将输出错误：

```
$ make | tee log.txt
make: *** No targets specified and no makefile found.  Stop.
```

虽然错误消息显示在了屏幕上，但 *make* 生成的错误消息并未被 *tee* 捕获，文件 *log.txt* 被创建为空。在管道捕获 stderr 之前，需要进行重定向：

```
$ make 2>&1 | tee log.txt
make: *** No targets specified and no makefile found.  Stop.
$ cat log.txt
make: *** No targets specified and no makefile found.  Stop.
```

在这个例子中，*make* 的 stderr 被重定向到了 stdout，因此 *tee* 能够捕获它，在屏幕上显示并将其保存到文件 *log.txt* 中。在这种情况下，保存错误消息以便后续检查可能很有用。

## 命令替换

捕获命令输出的另一种方法是*命令替换*。通过将命令放在反引号内，Bash 会将其替换为其标准输出。以下示例展示了如何将一个程序的 stdout 用作另一个程序的参数：

```
$ mkdir `date +%Y-%m-%d`
$ ls
2019-09-05
```

程序 *date* 的输出，即格式化为 *年-月-日* 的当前日期，被用作 *mkdir* 创建目录的参数。使用 *$( )* 代替反引号也可以获得相同的结果：

```
$ rmdir 2019-09-05
$ mkdir $(date +%Y-%m-%d)
$ ls
2019-09-05
```

同样的方法也可以用于将命令的输出存储为变量：

```
$ OS=`uname -o`
$ echo $OS
GNU/Linux
```

命令 `uname -o` 输出当前操作系统的通用名称，该名称被存储在会话变量 `OS` 中。将命令的输出赋值给变量在脚本中非常有用，这使得可以以多种不同的方式存储和评估数据。

根据被替换命令生成的输出，内建命令替换可能并不合适。一种更高级的方法是使用程序输出作为另一个程序参数，采用名为 `xargs` 的中间工具。程序 `xargs` 使用通过 stdin 接收的内容，将这些内容作为参数运行给定的命令。以下示例展示了 `xargs` 运行程序 `identify`，其参数由程序 `find` 提供：

```
$ find /usr/share/icons -name 'debian*' | xargs identify -format "f: %wx%h\n"
debian-swirl.svg: 48x48
debian-swirl.png: 22x22
debian-swirl.png: 32x32
debian-swirl.png: 256x256
debian-swirl.png: 48x48
debian-swirl.png: 16x16
debian-swirl.png: 24x24
debian-swirl.svg: 48x48
```

程序 `identify` 是 *ImageMagick* 的一部分，*ImageMagick* 是一组用于检查、转换和编辑大多数图像文件类型的命令行工具。在示例中，`xargs` 获取了 `find` 列出的所有路径，并将它们作为参数传递给 `identify`，`identify` 随后按照选项 `-format` 的要求格式显示每个文件的信息。示例中 `find` 找到的文件是包含 Debian 文件系统中发行版标志的图像。`-format` 是 `identify` 的参数，而不是 `xargs` 的参数。

选项 `-n 1` 要求 `xargs` 每次只使用一个参数运行给定的命令。在示例中，而不是将 `find` 找到的所有路径作为参数列表传递给 `identify`，使用 `xargs -n 1` 将为每个路径单独执行命令 `identify`。使用 `-n 2` 将以两个路径作为参数执行 `identify`，`-n 3` 以三个路径作为参数，等等。类似地，当 `xargs` 处理多行内容时（如 `find` 提供的输入），可以使用选项 `-L` 来限制每次命令执行时使用的行数。

> **注意**
> 使用 `xargs` 配合选项 `-n 1` 或 `-L 1` 来处理由 `find` 生成的输出可能是不必要的。命令 `find` 具有选项 `-exec`，可以为每个搜索结果项运行给定的命令。

如果路径包含空格字符，重要的是使用选项 `-print0` 运行 `find`。此选项指示 `find` 在每个条目之间使用空字符，以便列表可以被 `xargs` 正确解析（输出被抑制）：

```
$ find . -name '*.avi' -print0 -o -name '*.mp4' -print0 -o -name '*.mkv' -print0 | xargs -0 du | sort -n
```

选项 `-0` 告诉 `xargs` 应使用空字符作为分隔符。这样，即使 `find` 给出的文件路径包含空格或其他特殊字符，也能被正确解析。上一个示例展示了如何使用命令 `du` 找出每个找到的文件的磁盘使用情况，然后按大小对结果进行排序。为了简洁，输出被抑制。请注意，对于每个搜索标准，都需要为 `find` 放置 `-print0` 选项。

默认情况下，`xargs` 将执行命令的参数放在最后。要改变这种行为，应使用选项 `-I`：

```
$ find . -mindepth 2 -name '*.avi' -print0 -o -name '*.mp4' -print0 -o -name '*.mkv' -print0 | xargs -0 -I PATH mv PATH ./
```

在最后一个示例中，`find` 找到的每个文件都被移动到当前目录。由于源路径必须在目标路径之前告知 `mv`，因此为 `xargs` 的选项 `-I` 提供了一个替换术语，然后该术语被适当放置在 `mv` 旁边。通过使用空字符作为分隔符，没有必要用引号括起替换术语。

## 引导练习

- 保存自动化脚本执行操作的日期是方便的。命令 `date +%Y-%m-%d` 以 *年-月-日* 格式显示当前日期。如何使用命令替换将此类命令的输出存储在名为 `TODAY` 的 shell 变量中？
- 使用命令 `echo`，如何将变量 `TODAY` 的内容发送到命令 `sed s/-/./g` 的标准输入？
- 如何将命令 `date +%Y-%m-%d` 的输出用作命令 `sed s/-/./g` 的 Here 字符串？
- 命令 `convert image.jpeg -resize 25% small/image.jpeg` 创建 `image.jpeg` 的较小版本，并将结果图像放置在子目录 `small` 中同名文件中。使用 `xargs`，如何对文件 `filelist.txt` 中列出的每个图像执行相同的命令？

# 探索性练习

- 一个简单的备份例程定期使用 `dd < /dev/sda1 > sda1.img` 创建分区 /dev/sda1 的镜像。为了执行未来的数据完整性检查，该例程还使用 `sha1sum < sda1.img > sda1.sha1` 生成文件的 SHA1 哈希。通过添加管道和命令 `tee`，如何将这两个命令合并为一个？
- 命令 `tar` 用于将许多文件归档到单个文件中，同时保留目录结构。选项 `-T` 允许指定包含要归档的路径的文件。例如，`find /etc -type f | tar -cJ -f /srv/backup/etc.tar.xz -T -` 根据命令 `find` 提供的列表（选项 `-T -` 指示标准输入作为路径列表）创建压缩 tar 文件 `etc.tar.xz`。为了避免因路径包含空格而可能导致的解析错误，`find` 和 `tar` 应该存在哪些命令选项？
- 除了打开一个新的远程 shell 会话，命令 `ssh` 还可以执行作为其参数指示的命令：`ssh user@storage "remote command"`。鉴于 `ssh` 也允许将本地程序的标准输出重定向到远程程序的标准输入，如何通过 `ssh` 将 `cat` 命令将名为 `etc.tar.gz` 的本地文件管道传输到 `user@storage` 上的 `/srv/backup/etc.tar.gz`？

## 总结

本课程涵盖了 Linux 使用的传统进程间通信技术。命令管道在两个进程之间创建单向通信通道，而命令替换允许将进程的输出存储在 shell 变量中。课程经过以下步骤：

- 如何使用 `管道` 将进程的输出流式传输到另一个进程的输入。
- 命令 `tee` 和 `xargs` 的用途。
- 如何捕获进程的输出，将其存储在变量中，或将其直接用作另一个命令的参数。

涉及到的命令和程序包括：

- 使用 `|` 进行命令管道。
- 使用反引号和 `$()` 进行命令替换。
- 命令 `tee`、`xargs` 和 `find`。

