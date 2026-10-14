
注意：SFTP 协议受 Linux 发行版中发现的许多图形文件管理器支持。使用 `Nautilus`（GNOME）或 `Konqueror`（KDE），我们可以将以 `sftp://` 开头的 URI 输入到位置栏中，并在运行 SSH 服务器的远程系统上操作文件。

## WINDOWS 的 SSH 客户端？

假设你坐在 Windows 机器前，但需要登录你的 Linux 服务器并完成一些实际工作。你该怎么办？当然是为你的 Windows 电脑获取一个 SSH 客户端程序！有许多此类程序。其中最流行的是 Simon Tatham 及其团队的 `PuTTY`。`PuTTY` 程序显示一个终端窗口，允许 Windows 用户在远程主机上打开 SSH（或 telnet）会话。该程序还提供了 `scp` 和 `sftp` 程序的类似物。

`PuTTY` 可在 `http://www.chiark.greenend.org.uk/~sgtatham/putty/` 获取。

## 17 搜索文件

随着我们漫游在 Linux 系统中，有一件事变得非常清楚：典型的 Linux 系统有很多文件！这就引出了一个问题：“我们如何找到东西？”我们已经知道 Linux 文件系统是按照约定井然有序的，这些约定从一代 Unix-like 系统传到下一代，但 sheer 的文件数量可能会带来一个令人望而生畏的问题。

在本章中，我们将介绍两种用于在系统上查找文件的工具：

- `locate`—按名称查找文件。
- `find`—在目录层次结构中搜索文件。

我们还将介绍一个通常与文件搜索命令一起使用的命令来处理 resulting 的文件列表：

- `xargs`—从标准输入构建并执行命令行。

此外，我们还将介绍几个帮助我们探索的命令：

- `touch`—更改文件时间。
- `stat`—显示文件或文件系统状态。

### locate—轻松查找文件

`locate` 程序会对路径名执行快速数据库搜索，然后输出与给定子字符串匹配的每个名称。举例来说，我们想要找到所有名称以 `zip` 开头的程序。由于我们正在寻找程序，可以假设包含程序的目录名会以 `bin/` 结尾。因此，我们可以尝试这样使用 `locate` 来找到文件：

```
[me@linuxbox ~]$ locate bin/zip
```

`locate` 将搜索其路径名数据库并输出包含字符串 `bin/zip` 的内容：

```
/usr/bin/zip
/usr/bin/zipcloak
/usr/bin/zipgrep
/usr/bin/zipinfo
/usr/bin/zipnote
/usr/bin/zipsplit
```

如果搜索要求不是那么简单，`locate` 可以与其他工具（如 `grep`）结合使用，以设计更有趣的搜索：

```
[me@linuxbox ~]$ locate zip | grep bin
```

```
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
/usr/bin/unzipSfx
/usr/bin/zip
/usr/bin/zipcloak
/usr/bin/zipgrep
/usr/bin/zipinfo
/usr/bin/zipnote
/usr/bin/zipsplit
```

`locate` 程序已经存在多年，市面上存在几种不同的变体。现代 Linux 发行版中最常见的两个是 `slocate` 和 `mlocate`，尽管它们通常通过名为 `locate` 的符号链接访问。`locate` 的不同版本具有重叠的选项集。某些版本包含正则表达式匹配（我们将在第 19 章中介绍）和通配符支持。检查 `locate` 的 man 手册以确定安装了哪个版本的 `locate`。

### LOCATE 数据库从何而来？

你可能会注意到，在某些发行版中，系统刚安装后 `locate` 无法工作，但如果第二天再试，它就能正常工作。怎么回事？`locate` 数据库是由另一个名为 `updatedb` 的程序创建的。通常，它会作为 cron 作业定期运行，即由 `cron` 守护进程在固定间隔执行的任务。大多数配备 `locate` 的系统每天运行一次 `updatedb`。由于数据库不会持续更新，你会注意到使用 `locate` 时非常新的文件不会显示出来。为克服此问题，可以通过成为超级用户并在提示符下手动运行 `updatedb` 来手动运行 `updatedb` 程序。

### find—艰难地查找文件

虽然 `locate` 程序可以根据文件名称查找文件，但 `find` 程序会根据多种属性在给定目录（及其子目录）中搜索文件。我们将花费大量时间使用 `find`，因为它具有许多有趣的功能，我们在后续章节开始介绍编程概念时将一再看到。

在最简单的使用中，`find` 会给出一个或多个要搜索的目录名称。例如，它可以生成我们主目录的列表：

```
[me@linuxbox ~]$ find ~
```

在大多数活跃的用户账户中，这会产生一个很长的列表。由于列表发送到标准输出，我们可以将列表通过管道传输到其他程序。让我们使用 `wc` 来计数文件数量：

```
[me@linuxbox ~]$ find ~ | wc -l
47068
```

哇，我们很忙！`find` 的美妙之处在于它可以用来识别符合特定条件的 files。它通过测试、操作和选项的（略显奇怪）应用来实现这一点。我们先来看测试。

## 测试

假设我们想要从搜索结果中获取目录列表。为此，我们可以添加以下测试：

```
[me@linuxbox ~]$ find ~ -type d | wc -l
1695
```

添加测试 `-type d` 将搜索限制为目录。相反，我们也可以使用此测试将搜索限制为常规文件：

```sh
[me@linuxbox ~]$ find ~ -type f | wc -l
38737
```

表 17-1 列出了 `find` 支持的常见文件类型测试。

### Table 17-1: find File Types

| File Type | Description |
|---|---|
| b | 块特殊设备文件 |
| c | 字符特殊设备文件 |
| d | 目录 |
| f | 常规文件 |
| l | 符号链接 |

我们还可以通过添加一些额外的测试来按文件大小和文件名进行搜索。让我们查找所有匹配通配符模式 `*.JPG` 且大于 1 兆字节的常规文件：

```sh
[me@linuxbox ~]$ find ~ -type f -name "*.JPG" -size +1M | wc -l
840
```
