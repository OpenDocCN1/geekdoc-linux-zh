
```
compressed=0

# clean up our temp files before we start
/bin/rm -f /tmp/autocompress.*

for fname in `find $homedir -type f -size $threshold -print | \
egrep -v '(\.Z$|\.gz$|\.tgz$)'`
do
owner=`ls -l $fname | awk '{print $3}'`
if [ $owner = 'root' ]; then
echo "... skipping file $fname (owned by root)"
else
echo 'autocompressing file $fname (owned by $owner)'
gzip $fname
echo "$fname" >> /tmp/autocompress.$owner
compressed=`expr $compressed + 1`
fi
done

# now send out email reports to any users who has had files compressed

if [ $compressed -gt 0 ]; then
for report in `ls /tmp/autocompress.*`
do
recipient=`echo $report | sed 's|/tmp/autocompress.||'`
echo ""
echo "Sending autocompress report to ${recipient}:"
cat $report
(
echo 'In an effort to save disk space, files larger than $threshold'
echo 'are automatically compressed on this system. On a regular sweep'
echo 'through the disk, the following file or files of yours have been'
echo 'identified and auto-compressed:'
cat $report
echo 'To learn how to work with compressed files, please see the '
echo 'gzip man page. You can do this with the command '
echo 'man gzip'
) | mail -s 'Notice: Compressed your big files' $recipient

/bin/rm -f $report
done
echo ""
echo "$compressed file(s) compressed."
else
echo ""
echo "autocompress: no files compressed, no report generated"
fi

exit 0
```

这是一个比之前章节中介绍的脚本更为复杂的 shell 脚本，因此我建议你花一些时间逐行阅读它。特别注意 $compressed 变量是如何统计匹配项数量的，以及括号如何生成一个独立的子 shell，并让你能够使用各种 Unix 命令为用户组合出一封非常友好的电子邮件。 使用临时文件存储中间信息的做法也值得研究。

## 7. 运行脚本看看会发生什么：

```
# autocompress.sh
autocompressing file /home/taylor/IBM/fop.jar (owned by taylor)
autocompressing file /home/taylor/IBM/j2sdk-1_3_0_02-solx86.tar (owned by taylor)
... skipping file /home/taylor/Lynx/src/lynx (owned by root)
... skipping file /home/taylor/Lynx/lynx (owned by root)

Sending autocompress report to taylor:
/home/taylor/IBM/fop.jar
/home/taylor/IBM/j2sdk-1_3_0_02-solx86.tar

2 file(s) compressed.
```

两个文件已被压缩，另外两个潜在的大文件因归 root 所有而被跳过（这表明它们可能更为重要）。脚本的后半部分确保这些更改不会静默发生。相反，用户将收到一封电子邮件通知，告知其自动压缩情况：

```
From: root
Subject: Notice: Compressed your big files

In an effort to save disk space, files larger than >1000k
are automatically compressed on this system. On a regular sweep
through the disk, the following file or files of yours have been
identified and auto-compressed:
/home/taylor/IBM/fop.jar
/home/taylor/IBM/j2sdk-1_3_0_02-solx86.tar
To learn how to work with compressed files, please see the
gzip man page. You can do this with the command
man gzip
```

在 Unix 系统上，compress 和 gzip 两个命令执行相同的功能——它们用一个包含相同信息但使用性稍差的较小文件替换大文件。压缩质量的差异很重要，但并非关键，因此如果你早已将 compress 牢记为缩小文件的方式，那么你可能无需学习任何新技巧。

然而，如果你第一次接触这个主题，gzip 才是首选。如果你想要一个强有力的动机，可以查看 /usr/share/man 目录，注意所有的 man 手册页
都以 .gz 后缀存储——它们默认都以 gzip 压缩格式存储。在下一小时我们将探索各种 Unix 包机制，你会再次看到 gzip 是软件开发社区的首选压缩系统。

## zip 的简要介绍

虽然 zip 听起来像是 gzip 的直系亲属，但实际上它是一个完全不同的程序。是的，它确实进行文件压缩（不过 zip 称之为放气和充气，而不是压缩和解压缩），但 zip 工具的主要目的是创建包含多个文件和文件夹的归档文件。

历史上，zip 由 PKWare（PKZIP 的制造商）的 Phil Katz 于 1989 年开发，此后已被各种厂商和大多数主要计算平台采用为归档格式。Linux 上的 zip 命令经过多年开发，并非 GNU 项目的一部分，因此它不支持那些奇特的 - -word 命令参数。

## 任务 7.3：使用 zip

别再多说了，让我们看看 zip 都能做什么！

- 1. 就在他离开前，我们的朋友 testdude 询问我们是否可以为他构建一个 Windows 友好的归档文件，包含他主目录中的文件和文件夹并通过电子邮件发送给他。这正是 zip 的完美工作！

![](img/5ced0c78d748bd190e9027e5549a3622_161_0.png)

> 值得指出的是，你在未经确认是否合适的情况下可能不想发送用户主目录中的所有文件。我建议你在让用户获取其电子邮件归档、项目目录或任何有疑问的文件之前，先以书面形式获得人力资源或法律部门的批准。

如果你查看 zip 手册页，你无疑会感到有点不知所措，但幸运的是，不带任何参数输入 zip 会给出一个（非常）简洁的使用摘要：

```
$ zip
Copyright (C) 1990-1999 Info-ZIP
Type 'zip -L' for software license.
Zip 2.3 (November 29th 1999). Usage:
zip [-options] [-b path] [-t mmddyyyy] [-n suffixes] [zipfile list] [-xi list]
The default action is to add or replace zipfile entries from list, which
can include the special name - to compress standard input.
If zipfile and list are omitted, zip compresses stdin to stdout.

-f freshen: only changed files    -u update: only changed or new files
-d delete entries in zipfile      -m move into zipfile (delete files)
-r recurse into directories       -j junk (don't record) directory names
-0 store only                     -1 convert LF to CR LF (-11 CR LF to LF)
-1 compress faster                -9 compress better
-q quiet operation                -v verbose operation/print version info
-c add one-line comments          -z add zipfile comment
-o read names from stdin          -o make zipfile as old as latest entry
-x exclude the following names    -i include only the following names
-F fix zipfile (-FF try harder)   -D do not add directory entries
-A adjust self-extracting exe     -J junk zipfile prefix (unzipspx)
-T test zipfile integrity         -X eXclude extra file attributes
-y store symbolic links as the link instead of the referenced file
-R PKZIP recursion (see manual)   -n don't compress these suffixes
-e encrypt
```

要构建一个 PKZIP 兼容的归档文件，你需要确保使用以下标志：-r 会导致程序递归进入子目录并包含其中的内容，-9 请求最佳可能的压缩，-v 提供详细输出：

```
$ zip -r -9 -v testdude.zip *
  adding: adduser.sh (in=1113) (out=597) (deflated 46%)
  adding: browse.sh (in=739) (out=317) (deflated 57%)
  adding: checkhomes.sh (in=537) (out=266) (deflated 50%)
  adding: checkpw.sh (in=756) (out=462) (deflated 39%)
  adding: delete.sh (in=693) (out=390) (deflated 44%)
  adding: DEMO/ (in=0) (out=0) (stored 0%)
  adding: DEMO/testfile (in=0) (out=0) (stored 0%)
  adding: DEMO/Src/ (in=0) (out=0) (stored 0%)
  adding: DEMO/Src/cribbage.c (in=26150) (out=8081) (deflated 69%)
  adding: DEMO/snapshot.sh (in=263) (out=187) (deflated 29%)
  adding: DEMO/sourcefiles.cpio... (in=153600) (out=41688) (deflated 73%)
  adding: DEMO/testdir/ (in=0) (out=0) (stored 0%)
  adding: diskhogs.sh (in=373) (out=234) (deflated 37%)
  adding: getmodemdriver.sh (in=605) (out=381) (deflated 37%)
  adding: getstocks.sh (in=569) (out=346) (deflated 39%)
  adding: gettermssheet.sh (in=593) (out=373) (deflated 37%)
  adding: rowing-w-jasmine2.jpg...... (in=522970) (out=521525) (deflated 0%)
  adding: suspend.sh (in=1290) (out=679) (deflated 47%)
  total bytes:710251, compressed=575526 -> 19% savings
```

做得漂亮，文件 testdude.zip 现在已准备好通过电子邮件发送给用户。请注意，最后几行显示的 compressed 值实际上是生成的归档文件的大小：575,526 字节。
