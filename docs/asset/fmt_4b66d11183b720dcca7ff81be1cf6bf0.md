
如果尚未下载，可以在 https://digitalcorpora.s3.amazonaws.com/corpora/rives/nps-2010-emails/nps-2010-emails.E01 下载。

## 2. 下载完成后，打开一个新的终端并切换到 Downloads 文件夹，就像我们之前做过的那样。你可以通过输入以下命令来查看选项和用法：

```
bulk_extractor -h
```

以下截图显示了之前使用的命令的输出。

```
[(kali@kali)]~~/Downloads]
$ bulk_extractor -h
bulk_extractor version 2.0.0: A high-performance flexible digital forensics program.
Usage:
bulk_extractor [OPTION...] image_name
-A, --offset_arg         Offset (in bytes) to feature locations (default:0)
-B, --banner_file arg     Path to file whose contents are prepended to top of all feature files
-C, --context_window arg Size of context window reported in bytes (default:10)
-d, --debug_arg           enable debugging (default:1)
-D, --debug_help          help on debugging
-E, --enable_exclusive arg disable scanners except the one specified. Same as -x -E scanner.
-e, --enable_arg          enable a scanner (can be repeated)
-x, --disable_arg         disable a scanner (can be repeated)
-f, --find arg            search for a pattern (can be repeated)
```

*图 9.23 – bulk_extractor 使用选项*

## 3. 像 Foremost 和 Scalpel 一样，使用 `bulk_extractor` 的语法非常简单，只需指定输出文件夹 `-o` 和取证镜像。现在让我们输入以下命令，使用 `bulk_extractor` 刻取证据文件并将所有发现的文件和信息保存到 Downloads 文件夹中名为 `bulk_carved` 的文件夹中：

```
bulk_extractor -o bulk_carved nps-2010-emails.E01
```

```
(kali@kali):~/Downloads
$ bulk_extractor -o bulk_curved nps-2010-emails.E01
opening nps-2010-emails.E01

bulk_extractor version: 2.0.0
Input file: "nps-2010-emails.E01"
Output directory: "bulk_curved"
Disk Size: 8MD570
Scanners: aes base64 elvx facebook gib httptps json klml_curved msxml nnet et tfndsf nftlogfile mftnfsun pdf rar sqlite utcmp vard_curved windirs winln
Threads: 2
goming multi-threaded... ( 2 )
bulk_extractor      Fri Oct 28 14:22:21 2022

available_memory: 6097850368
bytes_queued: 0
depth_queued: 0
depth_bufs_queued: 0
elapsed_time: 00:00:00
estimated_date_completion: 2022-10-28 14:22:20
estimated_time_remaining: n/a
fraction_read: 0.000000 %
max_offset: 0
```

图 9.24 - `bulk_extractor` 命令输出

## 4. 一旦 `bulk_extractor` 指出所有线程已完成，就会提供过程摘要甚至一些发现。以下截图中的最后一行列出了 67 个发现的电子邮件特征：

```
Phase 2. Shutting down scanners
Computing final histograms and shutting down ...
Phase 3. Generating stats and printing final usage information
All threads finished.
Elapsed time: 2.006 sec.
Total MB processed: 10
Overall performance: 5928 MB/sec 2.614 (MB/sec/thread)
bufs created: 62785
bufs uncreated: 0
Time producer spent waiting for scanners to process data: 00:00:00 (0.00 second)
s)
Time consumers spent waiting for data from producer: 00:00:00 (0.04 second)
s)
Average time spent waiting for data from producer: 00:00:00 (0.00 second)
s)
More time spent waiting for reader. You need faster I/O for improved performance.
Total email features found: 67
```

图 9.25 - `bulk_extractor` 输出片段

## 5. 要查看 `bulk_extractor` 的输出和发现，我们可以切换到 Downloads 中的 `bulk_carved` 文件夹并使用 `ls -l` 命令。在下面的截图中，我们可以看到如 `domain_histogram.txt`、`domain.txt`、`email_domain_histogram.txt` 和 `email.txt` 等文本文件包含数据，因为它们的大小大于零：

![](img/7489105e357b7dff3e56cd1cbb0de4fa_229_0.png)

图 9.22 - scalpelOutput 文件夹内的刻取内容

## 6. 要查看 `bulk_extractor` 的输出和发现，我们可以切换到 Downloads 中的 `bulk_carved` 文件夹并使用 `ls -l` 命令。在下面的截图中，我们可以看到如 `domain_histogram.txt`、`domain.txt`、`email_domain_histogram.txt` 和 `email.txt` 等文本文件包含数据，因为它们的大小大于零：

# NTFS 恢复 scrounge-ntfs

`scrounge-ntfs` 是一种用于恢复 NTFS（New Technology File System 的缩写）驱动器的命令行工具，通常由 Windows 设备使用。大多数存储介质（包括闪盘）也可以使用 Windows 系统中的默认工具格式化为 NTFS。

硬盘出现损坏的 MFT（Master File Table，主文件表）是非常常见的。该表存储了 NTFS 驱动器中所有文件的信息，包括大小、权限、内容和时间戳。如果该表损坏，驱动器的内容可能无法访问，或者驱动器可能无法启动操作系统。

无论 NTFS 驱动器损坏的原因是什么，`scrounge-ntfs` 都是为了恢复 NTFS 分区内的文件而设计的。在实验中，我将使用一个格式化为 NTFS 的外部驱动器，其内容如下：

1. 运行以下命令查看我们的驱动器在 Kali 中被显示为：

```
sudo fdisk -l
```

以下显示了之前输入的命令的输出：

[此处为图像/表格内容]

图 9-2 - `fdisk` 输出

可见，我连接的驱动器也被显示为 `sdb`。

2. 在开始恢复过程之前，我想在桌面上创建一个名为 `Scrounge_recovery` 的文件夹，所有 `scrounge-ntfs` 恢复的文件将保存在其中。

为此，我将通过以下命令切换到 Desktop 目录：

```
cd Desktop
```

然后，我将通过以下命令创建一个新目录：

```
mkdir Scrounge_recovery
```
