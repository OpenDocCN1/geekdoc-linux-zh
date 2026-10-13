
## 4. 让我们看看哪些文件系统需要备份，哪些不需要备份：

```
# /sbin/dump -W
Last dump(s) done (Dump '>' file systems):
```

| 设备 | 文件系统 | 最后一次备份 |
|---|---|---|
| /dev/sda5 | / | 从未 |
| /dev/sda1 | /boot | 级别 0，日期 Wed Jan 23 12:58:11 2002 |
| /dev/sda3 | /home | 从未 |
| /dev/sdb1 | /usr | 从未 |
| /dev/sdb2 | /var | 从未 |

令人惊讶的是，/home 分区仍然显示为从未备份。这是因为 -T 标志与更新增量备份数据文件 /etc/dumpdates 所必需的 -u 标志互斥。

## 5. dump 的配套命令是 restore，它可以从 dump 归档中提取一个或多个文件。要列出 dump 归档中的内容，-t 标志应该很熟悉：

```
# /sbin/restore -tf /tmp/homedump
Dump date: Wed Jan 23 13:10:09 2002
Dumped from: Mon Jan 21 00:00:00 2002
Level 0 dump of /home on staging.intuitive.com:/dev/sda3
Label: /home
2
.
326401      ./taylor
328408      ./taylor/.bash_history
1256641     ./taylor/bin
1256671     ./taylor/bin/autocompress.sh
326425      ./taylor/mail.log
326427      ./taylor/sentinel.file
326428      ./taylor/proposal.doc.gz
326423      ./taylor/rowing-w-jasmine2.jpg.gz
1644161     ./testdud e
1893121     ./testdud e/DEMO
1909441     ./testdud e/DEMO/Src
1909473     ./testdud e/DEMO/Src/cribbage.c.gz
1903763     ./testdud e/DEMO/testdir
1893123     ./testdud e/DEMO/testfile.gz
1893124     ./testdud e/DEMO/snapshot.sh.gz
1893125     ./testdud e/DEMO/sourcefiles.cpio.gz
1844169     ./testdud e/adduser.sh.gz
1844179     ./testdud e/browse.sh.gz
1844171     ./testdud e/delete.sh.gz
1844173     ./testdud e/getmodemdriver.sh.gz
1844174     ./testdud e/getstocks.sh.gz
1844175     ./testdud e/gettermsheet.sh.gz
1844176     ./testdud e/rowing-w-jasmine2.jpg.gz
1844177     ./testdud e/suspend.sh.gz
1844180     ./testdud e/checkhomes.sh.gz
1844170     ./testdud e/checkpw.sh.gz
1844172     ./testdud e/diskhogs.sh.gz
```

虽然你可以直接从命令行指定要恢复的文件，但 restore 具有一个很方便的交互模式，使用起来要容易得多。你可以通过 -i 标志进入该模式：

这与 tar 的处理方式有点不同，因为 restore 实际上是它自己的交互式程序，如本示例所示：

```
# /sbin/restore -if /tmp/homedump
/sbin/restore > what
Dump date: Wed Jan 23 13:10:09 2002
Dumped from: Mon Jan 21 00:00:00 2002
Level 0 dump of /home on staging.intuitive.com:/dev/sda3
Label: /home
/sbin/restore > ls
./
taylor/
testdud e/

/sbin/restore > cd testdud e
/sbin/restore > ls
./testdud e:
DEMO/
adduser.sh.gz          checkpw.sh.gz          getstocks.sh.gz
browse.sh.gz           delete.sh.gz           gettermsheet.sh.gz
jasmine2.jpg.gz        diskhogs.sh.gz         rowing-w-jasmine2.jpg.gz
checkhomes.sh.gz       getmodemdriver.sh.gz   suspend.sh.gz

/sbin/restore > cd DEMO
/sbin/restore > ls
./testdud e/DEMO:
Src/                   sourcefiles.cpio.gz    testfile.gz
snapshot.sh.gz         testdir/

/sbin/restore > add testfile.gz
/sbin/restore > add snapshot.sh.gz
/sbin/restore > ls
./testdud e/DEMO:
Src/                   sourcefiles.cpio.gz    *testfile.gz
*snapshot.sh.gz        testdir/

/sbin/restore > extract
You have not read any tapes yet.
Unless you know which volume your file(s) are on you should start
with the last volume and work towards the first.
Specify next volume #: 1
set owner/mode for '.'? [yn] y
/sbin/restore > quit
```

这里的概念是，你正在交互式地浏览归档，并标记每个希望添加到恢复列表（提取）中的文件。完成后，extract 开始实际工作。如果你的备份在多个卷中，你需要指定卷号，或者对于单卷 dump 指定 1。

在 Unix 系统上安全可靠地实现备份是困难的，因为命令和实用程序相对原始。尽管如此，忽视备份是一种危险的做法，系统随时可能崩溃并可能烧毁。那时你的用户会怎么说你呢？

在线探索有关不同备份设备及其权衡的信息——一个不错的起点是 http://www.backupcentral.com/——然后在购买和安装之前，确保该设备得到你所使用的 Unix 版本的支持。一旦一切运行顺畅，立即建立磁带轮换制度并将 dump 命令添加到你的 crontab 文件中。（我们将在第 15 小时“在未来运行作业”中详细介绍 cron。）

## Summary
## 摘要

本小时探讨了压缩和文件系统备份的细微差别。我们看到了不同的压缩工具在 Unix 系统上会产生惊人不同的结果，而且这些实用程序还有多种非磁带备份用途。最后一点评论：如果你要创建备份方案，请记住轮换你的磁带，这样除了用于最新备份的磁带外，你始终还会有几天前的安全备份。

## Q&A
## 问答

Q Why are the backup solutions so poor on Unix?
Q Unix 上的备份解决方案为什么这么差？
A That’s a good question with no good answer. With thousands of Unix servers powering the Internet, you’d think that there are better backup solutions than dump and expensive commercial solutions. The only other interesting backup applications I know of are Kbackup (X Window System-based), BURT (based on Tcl/Tk), and Amanda (Advanced Maryland Automatic Network Disk Archiver).
A 这是个好问题，但没有好答案。成千上万台驱动互联网的 Unix 服务器，你会认为除了 dump 和昂贵的商业解决方案之外应该有更好的备份解决方案。我所知道的唯一其他有趣的备份应用程序是 Kbackup（基于 X Window System）、BURT（基于 Tcl/Tk）和 Amanda（Advanced Maryland Automatic Network Disk Archiver）。

Q How do you do backups on your own server?
Q 你自己的服务器上如何做备份？
A Um, err, next question?
A 呃，嗯，下一个问题？

Q What’s your favorite compression program?
Q 你最喜欢的压缩程序是什么？
A I always use gzip -9 if it’s available, to get the maximum compression possible. On the other hand, the command compress is certainly more mnemonic, so perhaps an alias…?
A 如果有的话，我总是使用 gzip -9 以获得最大可能的压缩率。另一方面，命令 compress 确实更易记，所以也许可以设置一个别名…？

## Workshop
## 练习

### Quiz
### 测验

- 1. Why do you think that compress had different results on different platforms?
- 1. 你认为为什么 compress 在不同平台上会有不同的结果？
- 2. When compressing lots of different types of files, what's the main difference—other than compression efficiency—between compress and gzip?
- 2. 在压缩大量不同类型的文件时，除了压缩效率之外，compress 和 gzip 的主要区别是什么？
- 3. How do you view the contents of compressed files without uncompressing them?
- 3. 如何在不解压缩的情况下查看压缩文件的内容？
- 4. Where will cd ~ take you?
- 4. cd ~ 会带你到哪里？
- 5. What does tar -xzvPf /dev/st0 do?
- 5. tar -xzvPf /dev/st0 是做什么的？

### Answers
### 答案

- 1. Actually, that's a really good question. Logically, if they're using the same algorithm, they should all have the same results. I'd be interested in hearing your own theory on this puzzling variation.
- 1. 实际上，这真是个好问题。逻辑上，如果它们使用相同的算法，结果都应该相同。我很感兴趣听听你对这种令人困惑的差异的自己的理论。
- 2. The main difference is that gzip likes to compress everything, even if the resultant file is a tiny bit bigger than the original. This rarely occurs, because gzip does a great job of compression, but it's still peculiar.
- 2. 主要区别在于 gzip 喜欢压缩所有内容，即使 resulting 文件比原始文件稍大一些。这种情况很少发生，因为 gzip 的压缩效果非常好，但仍然很奇怪。
- 3. Use zcat, or if you have them, zmore, zgrep, or something similar.
- 3. 使用 zcat，或者如果有的话，使用 zmore、zgrep 或类似工具。
- 4. To your home directory, exactly as cd $HOME and cd would do.
- 4. 到你的主目录，就像 cd $HOME 和 cd 所做的那样。
- 5. Extract commands from the /dev/st0 device, uncompressing them with verbose output, and try to retain ownership and permission information from the archive.
- 5. 从 /dev/st0 设备提取命令，使用详细输出解压缩它们，并尝试保留归档中的所有权和权限信息。

下一小时将探讨精妙的软件包管理世界——管理员通过该机制可以在计算机上获取、安装和卸载新软件。本小时将提供软件包管理功能的基本概述，并使用 RPM 和 fink（Mac OS X 软件包管理系统）探索基本软件包功能。

![](img/5ced0c78d748bd190e9027e5549a3622_177_0.png)

## Hour 8
## 第 8 小时

### Unix Package Management
### Unix 软件包管理

在个人电脑的世界里，如果你想向系统添加软件包，你可以购买它（或下载它，也许）并运行一个安装程序，该程序在幕后进行大量操作，最终弹出“已安装！”消息。它做了什么，以及你系统上实际安装了什么，可能是一个谜。

源自更平等的根源，Unix 系统多年来一直被困于以源代码分发的软件包，以及关于如何在（好吧，如果？）它编译时构建和安装程序的非常复杂的说明。

然而，在过去的六年里，Unix 已经赶上并在许多方面超越了个人电脑世界的安装策略。然而，没有标准。例如，Red Hat Linux 使用 RPM，即 Red Hat Package Manager 系统。Darwin 使用仍在发展的 fink 系统，而 Solaris 有自己的解决方案——pkg。
