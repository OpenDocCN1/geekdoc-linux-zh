
还有一种在某些 Unix 版本中常见的压缩程序：pack。pack 命令使用 Huffman 编码压缩算法，可在 Solaris 8 上使用，但在 Linux 或 Darwin 上不可用。然而，由于 compress 和 gzip 的广泛可用性，我认为没人会使用它。

## 任务 7.2：使用 gzip

有替代的压缩工具，但 gzip 值得特别关注，因为它已成为 Unix 社区事实上的首选压缩工具。

- 1. 首先，让我们看看使用 --help 标志是否会产生一些有用的信息：

```
$ gzip --help
gzip 1.3
(1999-12-21)
usage: gzip [-cdfhlnNrtVv19] [-S suffix] [file ...]
 -c -stdout write to standard output, keep original files unchanged
 -d -decompress decompress
 -f -force force overwrite of output file and compress links
 -h -help give this help
 -l -list list compressed file contents
 -L -license display software license
 -n -no-name do not save or restore the original name and time stamp
 -N -name save or restore the original name and time stamp
 -q -quiet suppress all warnings
 -r -recursive operate recursively on directories
 -S .suf -suffix .suf use suffix .suf on compressed files
 -t -test test compressed file integrity
 -v -verbose verbose mode
 -V -version display version number
 -1 -fast compress faster
 -9 -best compress better
 file... files to (de)compress. If none given, use standard input.
Report bugs to <bug-gzip@gnu.org>.
```

注意每个命令标志都有两种形式：单字母的传统 Unix 标志（例如，-f、-v）和双破折号的全词标志（例如，--force、--verbose）。只有 GNU 版本的 Unix 命令才提供全词标志选项，因此虽然使用它们可能很诱人，但我建议你学习单字母标志。输入更少，而且当你使用非 GNU 命令时不会感到沮丧，该命令会把 --help 当作对五个标志 -、-h、-e、-l 和 -p 的请求。

- 2. 有了这个摘要，下面是 gzip 使用的第一个演示：

```
$ gzip -v Nice* maillog* prop* rowing*
Nice Work.mp3: 2.4% -- replaced with Nice Work.mp3.gz
```

```
maillog.txt: 92.3% -- replaced with maillog.txt.gz
proposal.doc: 79.9% -- replaced with proposal.doc.gz
rowing-w-jasmine2.jpg: 0.2% -- replaced with rowing-w-jasmine2.jpg.gz
```

它对 maillog.txt 文件的压缩效果非常出色：与 compress 平均 3.6MB 相比，gzip 已将其缩小到 2.9MB。然而，gzip 的一个令人讨厌的特性是它几乎压缩所有东西，即使节省空间毫无意义（JPEG 图像被压缩了 0.2%，原始文件为 522Kb，被替换为 521Kb 的 gzip 版本。）

以下是使用常规 gzip 调用压缩的四个文件的情况：

```
-rw-r--r-- 1 taylor coders 2992332 Jan 21 16:08 maillog.txt.gz
-rw-r--r-- 1 taylor coders 4197440 Jan 21 12:41 Nice Work.mp3.gz
-rw-r--r-- 1 taylor coders 26159 Jan 21 12:42 proposal.doc.gz
-rw-r--r-- 1 taylor coders 521565 Jan 21 12:43 rowing-w-jasmine2.jpg.gz
```

要解压缩它们，只需调用 gunzip 即可

```
$ gunzip *.gz
```

并使用更高的请求压缩比（-9 标志）进行压缩：

```
$ gzip -v9 Nice* maillog* prop* rowing*
```

```
Nice Work.mp3: 2.4% -- replaced with Nice Work.mp3.gz
maillog.txt: 93.3% -- replaced with maillog.txt.gz
proposal.doc: 80.1% -- replaced with proposal.doc.gz
rowing-w-jasmine2.jpg: 0.2% -- replaced with rowing-w-jasmine2.jpg.gz
```

结果文件只是小了一点点：

```
-rw-r--r-- 1 taylor coders 2604313 Jan 21 16:08 maillog.txt.gz
-rw-r--r-- 1 taylor coders 4197118 Jan 21 12:41 Nice Work.mp3.gz
-rw-r--r-- 1 taylor coders 25850 Jan 21 12:42 proposal.doc.gz
-rw-r--r-- 1 taylor coders 521565 Jan 21 12:43 rowing-w-jasmine2.jpg.gz
```

更好，但可能不足以让你担心是否记得使用 -9 标志！

- 3. gzip 的一个强大功能是它能够从给定点开始递归压缩当前目录以及任何子目录中的每个文件：
$ cd -testdud e
$ gzip -rv9 *
adduser.sh: 46.3% -- replaced with adduser.sh.gz
browse.sh: 57.1% -- replaced with browse.sh.gz
checkhomes.sh: 50.4% -- replaced with checkhomes.sh.gz
checkpwp.sh: 38.8% -- replaced with checkpwp.sh.gz
delete.sh: 43.7% -- replaced with delete.sh.gz

```
DEMO/testfile:               0.0% .. replaced with DEMO/testfile.gz
DEMO/Src/cribbage.c:         69.0% .. replaced with DEMO/Src/cribbage.c.gz
DEMO/snapshot.sh:            28.8% -- replaced with DEMO/snapshot.sh.gz
DEMO/sourcefiles.cpio:       72.8% -- replaced with DEMO/sourcefiles.cpio.gz
diskhogs.sh:                 37.2% -- replaced with diskhogs.sh.gz
getmodemdriver.sh:           37.0% -- replaced with getmodemdriver.sh.gz
getstocks.sh:                39.1% -- replaced with getstocks.sh.gz
gettersheet.sh:              37.0% -- replaced with gettersheet.sh.gz
rowing-w-jasmine2.jpg:        0.2% .. replaced with rowing-w-jasmine2.jpg.gz
suspend.sh:                  47.3% -- replaced with suspend.sh.gz
```

![](img/5ced0c78d748bd190e9027e5549a3622_157_0.png)

> 如果你之前没见过，~acct 记法是用户 acct 主目录的便捷快捷方式。如果未指定任何账户，~ 本身在几乎所有有价值的 shell 中都会扩展为你的主目录。

gzip 程序已自动将目录（及其下方的子目录）中的每个文件替换为压缩版本，并且如常，每个文件都加上了 .gz 后缀。

这种行为对系统管理员来说非常棒。特别是，当账户被挂起时，这可以是一个很好的额外步骤——自动压缩用户主目录中的所有文件，以最大化活跃用户的可用磁盘空间。

- 4. gunzip 命令是通过硬链接的 gzip 程序的另一个名称。符号链接与硬链接的细微差别有点超出本书范围（请查看 Sams Teach Yourself Unix in 24 Hours 以获得良好解释），但当你看到类似 gzip（带命令列表）的 man 手册页开头时，这意味着文件系统以某种方式设置。

因为确保命令正确安装是重要的系统管理员任务，让我们快速插一段来学习这是如何完成的！而且，我喜欢这些插曲，你呢？

```
$ man gzip | head
GZIP(1)                                                                 GZIP(1)

NAME
gzip, gunzip, zcat - compress or expand files

SYNOPSIS
gzip [ -acfhlLnNrtvV19 ] [ -S suffix ] [ name ... ]
gunzip [ -acfhlNrtvV ] [ -S suffix ] [ name ... ]
zcat [ -f hLV ] [ name ... ]
```

![](img/5ced0c78d748bd190e9027e5549a3622_157_1.png)

任何时候你在 man 手册页的 SYNOPSIS 中看到一组不同的命令名称，这意味着同一个可执行二进制文件在文件系统中有多个名称。
这应该可以用 ls 来揭示：

```
$ which gzip
/bin/gzip
$ cd /bin
$ ls -l gzip gunzip zcat
-rwxr-xr-x 3 root root 51228 Aug 23 20:02 gunzip*
-rwxr-xr-x 3 root root 51228 Aug 23 20:02 gzip*
-rwxr-xr-x 3 root root 51228 Aug 23 20:02 zcat*
```

完美。它们大小都相同，并且三个的链接计数也相同（-l 长输出格式的第二列）。
在上一个输出中注意到什么令人惊讶的地方吗？翻回几页找找线索....
zcat 命令本应与 compress 实用程序相关联，但你可以看到它显然是 gzip 压缩命令家族的一部分。
这里发生了什么？
这个谜题的解决方案是 gzip 的一个鲜为人知的特性是，它不仅可以解压缩自己的压缩文件格式，还可以解压缩来自 compress、zip 和 pack 的文件！

- 6. 如果你不断遇到磁盘空间问题而买不起更大的磁盘，你可以将 gzip 与 find 结合使用，自动遍历用户文件并自动压缩任何异常大的文件：

```
$ find /home -type f -size +1000k -print
/home/taylor/Gator/Snapshots/MAILOUT.tar.Z
/home/taylor/IBM/fop.jar
/home/taylor/IBM/j2sdk_1_3_0_02-solx86.tar
/home/taylor/Lynx/src/lynx
/home/taylor/Lynx/lynx
/home/taylor/maillog.txt.gz
/home/taylor/Nice Work.mp3.gz
```

这个特定命令列出所有大于 1000Kb 的文件（-type f）。
将此转换为完全可用的 shell 脚本需要若干步骤，但这次我们直接跳到最终产品：

```
# cat autocompress.sh
#!/bin/sh

# AUTOCOMPRESS : automatically find and compress excessively large files
# in the /home directory tree, sending email to the user so they know
# what’s happened.

homedir="/home"
threshold="+1000k"  # files must be bigger than this to compress
```
