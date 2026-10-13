
```
-rw-rw---- 1 taylor coders 81491 Dec 5 05:12 /etc/passwd
drwxr-x--- 2 taylor coders 4096 Dec 5 05:12 Exchange/
drwxrwxr-- 5 taylor coders 4096 Dec 5 05:16 Gator/
-rw-rw---- 1 taylor coders 605 Dec 5 05:21 getmodemdriver.sh
-rw-rw---- 1 taylor coders 569 Dec 5 05:21 getsocks.sh
-rw-rw---- 1 taylor coders 593 Dec 5 05:21 getterssheet.sh
-rw-rw---- 1 taylor coders 0 Dec 5 05:21 gif.gif
drwxrwxr-- 4 taylor coders 4096 Dec 5 05:28 IBM/
drwxrwxr-x 12 10185 root 4096 Dec 18 07:07 Lynx/
-rw-r--r-- 1 taylor coders 4303501 Jan 21 12:41 Nice Work.mp3
-rw-r--r-- 1 taylor coders 130048 Jan 21 12:42 proposal.doc
-rw-r--r-- 1 taylor coders 522970 Jan 21 12:43 rowing-w-jasmine2.jpg
-rw-r--r-- 1 root coders 12290 Jan 14 04:15 suspend.sh
```

存在一些大文件，包括超过四兆字节的 MP3 音频文件 Nice Work.mp3 和 522KB 的 JPEG 图像 rowing-w-jasmine2.jpg。这些似乎还不算失控，但如果用户不是只有这一个文件，而是整个 Ella Fitzgerald 的唱片目录都在线上呢？如果每首歌大约为 4MB，那将是许多、许多千兆字节的空间，而这些空间其他用户就无法使用了。

解决方案是对文件进行压缩，以最小化使用的磁盘空间并最大化驱动器本身的利用率。

2. 用于压缩文件的标准 Unix 命令是 compress，它有多种不同的起始参数：

```
$ compress --help
Unknown flag: '--'; Usage: compress [-dfvcVr] [-b maxbits] [file ...]
 -d If given, decompression is done instead.
 -c Write output on stdout, don't remove original.
 -b Parameter limits the max number of bits/code.
 -f Forces output file to be generated, even if one already exists, and even if no space is saved by compressing.
 If -f is not used, the user will be prompted if stdin is a tty, otherwise, the output file will not be overwritten.
 -v Write compression statistics.
 -V Output version and compile options.
 -r Recursive. If a filename is a directory, descend into it and compress everything in it.
```

![](img/5ced0c78d748bd190e9027e5549a3622_151_0.png)

> 你可以看到懒惰的系统管理员记住如何使用特定 Unix 命令的捷径：使用 --help 标志。命令要么理解该标志并输出一些帮助信息，要么解析该标志发现它不被识别并输出包含帮助信息的 Usage 错误。无论哪种方式，都很简单，并且 99% 的时间都有效。

最有趣的标志是 -v，它显示压缩活动的結果。让我们试试！

```
$ compress -v *mp3
Nice Work.mp3: No compression -- Nice Work.mp3 unchanged
```

一个有趣的首次测试：由于此文件中信息排列的方式，compress 尝试压缩它，但发现压缩后的文件与原始文件相比并没有显著变小，因此拒绝完成压缩任务。

让我们改试其他一些文件：

```
$ compress -v *jpg *doc
rowing-w-jasmine2.jpg: No compression -- rowing-w-jasmine2.jpg unchanged
proposal.doc: -- replaced with proposal.doc.Z Compression: 62.31%
```

这里可以看到结果：proposal.doc 文件压缩了超过 60%——它原本为 130K，但现在只有 49K，如下所示：

```
$ ls -l p*
-rw-r--r-- 1 taylor coders 49010 Jan 21 12:42 proposal.doc.Z
```

然而，文件本身在未先解压缩之前就无法使用，这正是 uncompress 命令的目的。

3. 一个非常实用的工具是 zcat，它可以让你无需麻烦地处理压缩文件，它的作用与 cat 命令完全相同，但可以在运行时解压缩压缩文件。举例来说，许多 Unix 上的 man 系统就是这样工作的：所有 man 页面都以压缩形式存储，其内容在运行时解压缩，zcat 将其输出馈送到 nroff 格式化程序。

就我们的目的而言，让我们使用 zcat 在不解压缩的情况下偷看压缩的邮件日志文件的开头几行：

```
$ zcat maillog.txt.Z | head -2
Dec 24 04:02:09 staging sendmail[16202]: fB0C29k16202: from=root, size=186,
class=0, nrcpts=1, msgid=<200112241202.fB0C29k16202@staging.intuitive.com>,
relay=root@localhost
Dec 26 04:02:09 staging sendmail[19880]: fB0C29D19880: from=root,
size=1315, class=0, nrcpts=1,
msgid=<200112261202.fB0C29D19880@staging.intuitive.com>,
relay=root@localhost
```

![](img/5ced0c78d748bd190e9027e5549a3622_152_0.png)

> Linux 上的 zcat 命令实际上是 gzip 实用程序的一部分，我们将在本小时稍后探索它。

5. 事实证明，在 Red Hat Linux 的世界里，有许多实用程序可以直接处理压缩文件，如以下列表所述：

```
zcat [compress]      (1)  - compress and expand data (version 4.1)
zcat [gzip]          (1)  - compress or expand files
zcat [uncompress]    (1)  - compress and expand data (version 4.1)
zcmp [zdiff]         (1)  - compare compressed files
zdiff                (1)  - compare compressed files
zgrep                (1)  - search possibly compressed files for expression
zless                (1)  - file perusal filter for viewing compressed text
zlib                 (3)  - compression/decompression library
zmore                (1)  - file perusal filter for viewing compressed text
znew                 (1)  - recompress .Z files to .gz files
```

6. 观察同一命令压缩同一原始文件在不同的 Unix 平台上产生不同的结果，既有趣又能说明 Unix 各发行版之间细微的差异。

```
Red Hat Linux 7.2:
$ compress -v Nice* maillog* prop* rowing*
Nice Work.mp3: No compression ... Nice Work.mp3 unchanged
maillog.txt: ... replaced with maillog.txt.Z Compression: 90.66%
proposal.doc: ... replaced with proposal.doc.Z Compression: 62.31%
rowing-w-jasmine2.jpg: No compression ... rowing-w-jasmine2.jpg unchanged
```

```
Solaris 8:
$ compress -v Nice* maillog* prop* rowing*
Nice Work.mp3: Compression: -29.87% ... file unchanged
maillog.txt: Compression: 90.80% ... replaced with maillog.txt.Z
proposal.doc: Compression: 62.31% ... replaced with proposal.doc.Z
rowing-w-jasmine2.jpg: Compression: -30.28% ... file unchanged
```

```
Darwin/Mac OS X:
$ compress -v Nice* maillog* prop* rowing*
Nice Work.mp3: file would grow; left unmodified
maillog.txt.Z: 9% compression
proposal.doc.Z: 58% compression
rowing-w-jasmine2.jpg: file would grow; left unmodified
```

令人惊讶的是，maillog.txt 文件的最终大小在每个平台上都不同，如表 7.1 所述。

表 7.1 压缩文件大小的变化
| 文件名 | 原始大小 | Linux | Solaris | Darwin |
|---|---|---|---|---|
| maillog.txt | 39,350,440 | 3,677,629 | 3,696,761 | 3,696,039 |

随着你在 Unix 系统上花费更多时间探索，你不可避免地会发现很少访问的大文件。也许是一个以归档格式保存的老开发项目？为车库乐队存储在服务器上的 MP3 集合？不再属于网站的一部分的流媒体视频？为长期系统使用分析而保留的归档日志文件？

无论很少使用文件的原因是什么，compress 都是一个很棒的工具，可以帮助最大化你的磁盘空间可用性。不仅如此，它也是一个很好的命令，可以教给你的用户，以便他们也能更明智地管理自己的磁盘空间。

## gzip 替代方案

虽然 compress 有着悠久而值得尊敬的历史，但它并不是 Unix 系统上唯一懂得压缩文件的实用程序。还有两个值得注意的工具，zip 和 gzip。它们听起来像是同一个程序，但绝对不是。

zip 实用程序让你可以构建文件和目录的包，然后自动压缩它们。这个实用程序最有帮助的地方在于它与 Windows 上非常流行的 PKZIP 和 WinZip 实用程序完全兼容。更棒的是，Aladdin System 非常成功的 Mac OS StuffIt 系统也知道如何处理 ZIP 归档，因此它是一个完全跨平台的解决方案。

![](img/5ced0c78d748bd190e9027e5549a3622_154_0.png)

> 事实上，ZIP 归档在 Unix、VMS、MSDOS、OS/2、Windows、Macintosh、Amiga、Atari，甚至 Acorn 系统之间都是兼容的。

gzip 实用程序旨在成为 compress 的替代品，正如程序作者在文档中明确指出的：“我们开发这个程序是为了替代 compress，因为 UNISYS 和 IBM 对 compress 使用的 LZW 算法拥有专利。这些专利使我们无法使用 compress，我们需要一个替代品。gzip 更优的压缩比只是锦上添花。”

![](img/5ced0c78d748bd190e9027e5549a3622_154_1.png)

> 一点历史：'GNU' 项目（其缩写是，而且我没开玩笑，GNU's Not Unix）诞生于开发者社区对 AT&T 的不满，AT&T 是原始 Unix 系统的专利持有者和所有者，采用了强硬手段。GNU 的存在目的是提供一个摆脱所有专利和其他公司知识产权的 Unix 免费版本，并且它出人意料地取得了成功。这是一段引人入胜的阅读，可以在 http://www.gnu.org/ 在线找到。
