
本小时探讨了账户管理的许多方面，重点是如何处理顽固用户并在需要时将其关闭。它还强调了不同 Unix 版本之间可能存在多大的差异。仅仅因为它们都有相同的操作系统名称并不意味着它们是相同的！

### Q&A

Q 如果你要禁用某人的账户，为什么确保他们没有登录如此重要？

A 通常你会发现需要暂停账户是因为用户有不当行为，或者用户暂时被休假。在这些情况下，最好的做法是通过简单地将用户踢出系统来避免任何潜在的机密文件复制、破坏系统的企图或其他行为。

Q 文件锁定的整个概念似乎对多用户操作系统的设计至关重要。是这样吗？

A 绝对是的，即使有文件锁定，多个管理员覆盖彼此的更改（我称之为“互相踩踏”）的情况也不少见。最好的策略是让一个人有权更改关键文件，然后让其他人向他们提交更改请求。

### Workshop

#### Quiz

- 1. 暂停用户账户的超快不到一分钟的技术是什么？
- 2. 大多数 Unix 系统上的 `passwd` 命令有启发式（规则的 fancy 词）定义什么是可接受的密码。找出你主系统上的规则是什么。
- 3. 用于锁定账户的内置 `usermod -L` 机制仅需在加密的密码字符串前加上一个 `!`。这对任何系统都有效吗？试试看。
- 4. 你可能在 Linux 或 Solaris 系统上使用 `passwd -d` 的原因是什么？

#### Answers

- 1. 暂停用户账户可以通过 `root` 更改密码来非常快速地完成。
- 2. 了解 `passwd` 命令使用什么规则的最简单方法是查看 `passwd` 手册页。以下是 Solaris 手册页中的相关摘录：

密码必须满足以下要求：

- 每个密码必须有 `PASSLENGTH` 个字符，其中 `PASSLENGTH` 在 `/etc/default/passwd` 中定义并设置为 6。只有前八个字符有意义。
- 每个密码必须包含至少两个字母字符和至少一个数字或特殊字符。在此情况下，“字母”指的是所有大写或小写字母。
- 每个密码必须与用户的登录名以及该登录名的任何反向或循环移位不同。为比较目的，大写字母与其对应的小写字母等价。
- 新密码必须与旧密码至少有三个字符不同。为比较目的，大写字母与其对应的小写字母等价。

- 3. 在加密的密码字符串前加上一个新字符肯定会使密码无法匹配，从而有效地关闭账户。如果没有锁定机制可用，这是你可以使用的另一个技巧。
- 4. 如果你设置了一个 shell 为 `lpq` 或类似的账户，你可以通过告知用户他们可以从任何登录提示符登录到 `lpq` 账户来查看打印机队列的状态，从而使其成为通用访问。

在下一小时，我们将仔细研究 Unix 的备份和归档工具，特别关注 `gzip` 和 `tar`，这两个工具每个 Unix 系统管理员都应该像俗话说的那样倒背如流。我们还将比较压缩包，看看哪一个在节省磁盘空间和使传输更快速方面做得最好。

![](img/5ced0c78d748bd190e9027e5549a3622_149_0.png)

## Hour 7

## Large File Management and Backups

过去几个小时集中在管理 Unix 系统用户账户的工具和技术上。然而，用户对你作为系统管理员的期望与你对他们的期望一样。首要的期望是文件系统具有高度的完整性。换句话说，你最好进行备份！

本小时将集中讨论管理大文件和归档，然后讨论将数据备份到归档设备上的常见方法。

在本小时你将学习关于

- 使用 `compress` 管理大文件
- `gzip` 替代方案
- `zip` 的快速导览
- 使用 `tar` 复制目录树
- `Dump` 和系统备份

### Shrinking Big Files with compress

如果你在过去几年里拿起过报纸或走进过电脑商店，你就知道硬盘的价格以相当惊人的速度下降。今天我可以走进当地的电子商店，花不到 100 美元买一个 40 GB 的硬盘。当我想起我第一块 20 MB 硬盘多年前花了多少钱……好吧，我答应过不会用回忆来让你厌烦，所以我到此为止。

重点是，很难想象磁盘会被填满，或 Unix 系统上的文件会大到需要担心想出一种技术来缩小它们。

直到你的用户开始探索多媒体文件时。四个多分钟的 MP3 编码音乐文件很容易超过 50MB 或更多，数码相机的 JPEG 图像可能占用 1MB 或更多，甚至 Word 文档在编辑和审阅开始后也以惊人的速度增长。

这就是为什么系统管理的基础主题之一是管理大文件。无论你喜欢与否，你的计算机上有些大文件，随着更多用户被添加（或你自己使用得更多），你注定会有更多。

#### Task 7.1: Working with compress

管理大文件的首要跨平台工具是一个名为 `compress` 的程序，它使用自适应 Lempel-Ziv 编码，平均可将文件缩小 20% 到 30%。

1. 开始时，我一直在探索我的用户如何使用他们的磁盘空间，发现那个讨厌的 `taylor` 小伙子在他的目录中有各种大文件。以下是代表性样本：

```
$ ls -l
total 5036
-rw-r--r-- 1 taylor coders 1113 Jan 10 08:12 adduser.sh
-rw-r--r-- 1 taylor coders 56 Dec 5 05:10 badjoke
-rw-r--r-- 1 taylor coders 56 Dec 5 05:10 badjoke.rot13
drwxrwxr-- 2 taylor coders 4096 Dec 5 05:48 bin/
-rw-r--r-- 1 taylor coders 739 Dec 5 05:11 browse.sh
-rw-r--r-- 1 taylor coders 276 Dec 5 05:11 buckaroo
drwxrwxr-x 2 taylor coders 4096 Dec 18 21:26 CBO_MAIL/
-rw-r--r-- 1 root coders 537 Jan 9 22:39 checkhomes.sh
-rw-r--r-- 1 root coders 756 Jan 14 21:31 checkpw.sh
drwxrwxr-- 2 taylor coders 4096 Dec 5 05:12 CraigsList/
-rw-r--r-- 1 root coders 693 Jan 14 06:40 delete.sh
drwxrwxr-- 4 taylor coders 4096 Jan 7 21:47 DEMO/
-rw-r--r-- 1 taylor coders 373 Jan 7 20:22 diskhogs.sh
drwxrwxr-- 2 taylor coders 4096 Dec 5 05:12 elance/
```

![](img/5ced0c78d748bd190e9027e5549a3622_150_0.png)

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

存在一些大文件，包括超过四兆字节的 MP3 音频文件 `Nice Work.mp3` 和 522KB 的 JPEG 图像 `rowing-w-jasmine2.jpg`。这些似乎还不算失控，但如果用户不是只有这一个文件，而是整个 Ella Fitzgerald 的唱片目录都在线上呢？如果每首歌大约为 4MB，那将是许多、许多千兆字节的空间，而这些空间其他用户就无法使用了。

解决方案是对文件进行压缩，以最小化使用的磁盘空间并最大化驱动器本身的利用率。

2. 用于压缩文件的标准 Unix 命令是 `compress`，它有多种不同的起始参数：
