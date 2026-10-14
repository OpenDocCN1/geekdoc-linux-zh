

"bin/zip":

```
/usr/bin/zip
/usr/bin/zipcloak
/usr/bin/zipgrep
/usr/bin/zipinfo
/usr/bin/zipnote
/usr/bin/zipsplit
```

如果搜索需求不是那么简单，可以将 locate 与 grep 等其他工具结合起来设计更有趣的搜索：

```
[me@linuxbox ~]$ locate zip | grep bin
/bin/bunzip2
/bin/bzip2
/bin/bzip2recover
/bin/gunzip
/bin/gzip
/usr/bin/funzip
/usr/bin/gpg-zip
/usr/bin/preunzip
/usr/bin/prezip
/usr/bin/prezip-bin
/usr/bin/unzip
/usr/bin/unzipsfx
/usr/bin/zip
/usr/bin/zipcloak
/usr/bin/zipgrep
/usr/bin/zipinfo
/usr/bin/zipnote
/usr/bin/zipsplit
```

locate 程序已经存在多年，常见的使用变体有几种。在现代 Linux 发行版中最常见的两个是 slocate 和 mlocate，不过它们通常通过名为 locate 的符号链接来访问。locate 的不同版本具有重叠的选项集。某些版本包含正则表达式匹配（我们将在即将到来的章节中介绍）和通配符支持。查看 locate 的手册页以确定安装的是哪个版本的 locate。

## locate 数据库从何而来？

你可能会注意到，在某些发行版中，系统刚安装后 locate 无法工作，但如果第二天再试，就能正常工作。怎么回事？locate 数据库是由另一个名为 updatedb 的程序创建的。通常，它会作为 cron 作业定期运行；即由 cron 守护进程在固定间隔执行的任务。大多数配备 locate 的系统每天运行一次 updatedb。由于数据库不会持续更新，你会发现使用 locate 时非常新的文件不会显示出来。为了解决这个问题，可以通过成为超级用户并在提示符下手动运行 updatedb 来手动运行 updatedb 程序。

## find – 费力地查找文件

虽然 locate 程序可以根据文件名单独查找文件，但 find 程序会根据多种属性在给定目录（及其子目录）中搜索文件。我们将花大量时间学习 find，因为它具有许多有趣的功能，我们在后续章节开始介绍编程概念时将一再看到。

在最简单的使用中，find 会给出一个或多个要搜索的目录名称。例如，要列出我们的主目录：

```
[me@linuxbox ~]$ find ~
```

在大多数活跃的用户账户上，这会产生一个很长的列表。由于列表发送到标准输出，我们可以将列表通过管道传输到其他程序。让我们使用 wc 来计数文件数：

```
[me@linuxbox ~]$ find ~ | wc -l
47068
```

哇，我们很忙！find 的美妙之处在于它可以用来识别符合特定条件的 文件。它通过（略显奇怪的）选项、测试和操作的组合来实现这一点。我们先来看测试。

## Tests

假设我们想要从搜索结果中获取目录列表。为此，我们可以添加以下测试：

```
[me@linuxbox ~]$ find ~ -type d | wc -l
1695
```

添加测试 -type d 将搜索限制为目录。相反，我们也可以用此测试将搜索限制为普通文件：

```
[me@linuxbox ~]$ find ~ -type f | wc -l
38737
```

以下是 find 支持的常见文件类型测试：

表 17-1: find 文件类型

| 文件类型 | 描述 |
|---|---|
| b | 块特殊设备文件 |
| c | 字符特殊设备文件 |
| d | 目录 |
| f | 普通文件 |
| l | 符号链接 |

我们还可以通过添加一些额外的测试按文件大小和文件名进行搜索：让我们查找所有匹配通配符模式 "*.JPG" 且大于一兆字节的普通文件：

```
[me@linuxbox ~]$ find ~ -type f -name "*.JPG" -size +1M | wc -l
840
```

在这个例子中，我们添加 -name 测试，后跟通配符模式。注意我们用引号将其括起来以防止 shell 进行路径名展开。接下来，我们添加 -size 测试，后跟字符串 "+1M"。前导加号表示我们正在查找大于指定数字的文件。前导减号会改变其含义

