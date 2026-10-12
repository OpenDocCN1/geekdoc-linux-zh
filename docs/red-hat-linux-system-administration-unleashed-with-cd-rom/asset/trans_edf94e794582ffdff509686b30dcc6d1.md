
如果自安装以来你没有更改 X 服务器，那么链接 /etc/X11/X（它指向你使用的特定 X 服务器，例如 XF86_Mach64 或 XF86_FBDev）是安装过程中创建的最后几个符号链接之一。指向 xwrapper 的链接 /usr/X11R6/bin/X 会早几分钟，因为它是在安装早期创建的。文件 /boot/map 上的时间戳也是一个不错的候选，除非当然你重新编译过内核。

使用 tar 命令是备份文件最快也最简单的方法之一。它存在于你能找到的每一次 Linux 安装中（以防你需要在另一台机器上恢复文件），以及我见过的太阳底下所有的 UNIX（包括，他一本正经地说，Sun 的）。GNU tar 以外的变体通常不支持 gzip 压缩，因此请注意不要在想要导出到这些变体的文件上使用 -z 选项。

以下命令将备份最近两天内更改过的所有文件，除 /dev、/var/lock、/var/spool、/tmp 和 /proc 子目录中的文件外，并将其保存到名为 changed.tar 的文件中：

```
find / -path '/dev' -prune -o -path '/var/lock' -prune -o
  -path '/var/spool' -prune -o -path '/tmp' -prune -o
  -path '/proc' -prune -o -type f -mtime 2
  -print0 | tar --null -cvf changed.tar --files-from -
```

另外，如果你先执行命令

```
touch -t 07120000 sentinel
```

来创建一个名为 sentinel 的文件，其时间戳为 7 月 12 日 00:00 小时（我的测试系统于 7 月 11 日傍晚安装），你可以使用：

```
find / -path '/var/log' -prune -o -path '/proc' -prune -o
  -path '/tmp' -prune -o -path '/dev' -prune -o
  -type f -newer sentinel -print0
| tar --null -cvf changed.tar --files-from -
```

添加 -g SNAPSHOT-FILE-NAME 选项会创建一个文件，使增量备份（-G 选项）能够知道哪些文件在哪个级别被备份。该文件包含上次备份的日期，以及每个被备份文件的信息，每行一个。它可能会变得相当大。

## 使用 dump 和 restore 实现完整备份和恢复

如果整个文件系统（即整个磁盘驱动器）或整个目录需要备份，dump 和 restore 程序也是可用的。dump 程序内置支持“dump-levels”。这个“dump-level”与 tar 程序使用的相同：任何 dump-level 都会备份自相同或更高编号的级别执行以来已更改或添加的文件。Level-0 为最高，level-9 为最低，因此 level-1 包含 1 到 9 级，但不包括 level-0。

此命令创建一个子目录的 level-0 备份：

/sbin/dump -0u -f /dev/nst0 /usr/src

所有文件都会被备份，在本例中备份到连接到软盘驱动器控制器的磁带单元。增量备份可以任意指定 1 到 9 的 dump-level；如果你始终使用相同的值，你将获得自上次相同级别或更高编号的增量备份以来修改过的文件。

命令

/sbin/dump -3u -f /dev/nst0 /usr/src

仅会在自上次 level-3 或更高编号的备份运行以来被修改的情况下，才备份 /usr/src 树中的更改文件。

要恢复使用 dump 命令备份的文件、目录或文件系统，请使用 restore 命令。当使用 -i 选项时（如 restore -if /dev/nst0），可以恢复特定的文件或子目录。例如，恢复我已修改的文件 /etc/cron.daily/logrotate，输出如下：

```
[root@clarence /root]# /sbin/restore -if /dev/nst0
restore > ls
.:
dev/ etc/ root/ tmp/ usr/ var/

restore > cd etc
restore > ls
./etc:
cron.daily/ dumpdates

restore > add cron.daily
restore > ls cron.daily
./etc/cron.daily:
*logrotate

restore > extract
You have not read any tapes yet.
Unless you know which volume your file(s) are on you should start
with the last volume and work towards the first.
Specify next volume #: 1
set owner/mode for '.'? [yn] n
restore > quit
[root@clarence /root]# ls ./etc
cron.daily
[root@clarence /root]# ls ./etc/cron.daily/
logrotate
```

此特定实现的 restore 如果我直接给出命令 add etc/cron.daily/logrotate 而不先添加 cron.daily 子目录，就会产生核心转储。我不太确定原因，但由于我有源代码，我可以查看并修复该特定错误。或者我可以给作者发送一份错误报告。或者我可以像这里这样做，绕过它。restore 对 etc/cron.daily 子目录的列表在 logrotate 名称前有一个星号，表示它已被添加到提取列表。你会注意到提取相对于我当前的工作目录恢复了中间的 etc/ 子目录。这使我能够恢复因升级而可能已损坏的系统文件，并只复制我想要的内容。关于“指定下一个卷”的提示在 dump 占用多盘磁带且你知道所需特定文件所在位置时非常有用。

## 使用 cpio 快速归档

另一个快速归档的候选是 cpio 程序，尤其是在你需要从一种机器移动到另一种机器时。cpio 默认不创建目录或覆盖现有文件这一事实，具体取决于当时的需求而是好是坏。

存在许多变体；请查阅 dump、find、tar 和 cpio 的 man 和 info 页面（info dump, info tar, info find, info cpio, man tar, man find, man cpio）以查看更多示例。

这些命令中的任何一个都可以放入脚本文件并通过 cron 执行。先从命令行运行脚本始终是一个非常好的主意，这样你就可以在让它运行之前查看输出中是否有任何错误。如果你的脚本在 STDOUT 上生成输出（这是系统管理员的说法，意思是“脚本中某个地方有 echo 行”），cron 作业的所有者将会收到邮件，内容为本应打印到屏幕的内容——也许最后一行类似：

```
echo The backup script completed on `date`.
```

这样你就会知道是时候更换磁带了。

## 可能的备份问题和替代方案

使用其中一种方法作为唯一的备份方法存在一个小问题：如何确定哪个 tar 文件包含你需要的特定文件？如何知道特定文件何时被备份？你需要跟踪备份了什么、何时发生的以及文件在哪里。这个文件，或可能这些文件，将构成所谓的索引。GNU tar 程序具有 -g filename 选项，它会将运行的日期放入名为 filename 的文件中。-G 选项会生成一个被备份到 tar 中的文件列表。添加一个或两个（或七个）自定义脚本，你就拥有了一个你完全了解细节的备份系统——如果你有时间和能力做所有这些。如果没有，请考虑替代方案。

## 专用备份软件

一种替代方案是获取专门用于备份的软件。专用备份软件来自多个来源。有些以 GNU 公共许可证发布并且免费；其他则是商业专有产品。你如何在 Linux 下找到可供使用的产品？当然要去通常的地方。快速查看 Linux Applications and Utilities Page at http://www.chariot.com/linapp2.html 显示了五个商业产品和六个免费产品。查看 LinuxBerg at http://www.linuxberg.com 显示了 18 个控制台备份应用程序和三个专门为 X 编写的应用程序。Linux Links 站点 at http://linuxlinks.com 提供了备份部分 34 个条目的列表，但其中也包括一个用作备份实用程序的刻录 CD-ROM 程序。到你阅读本文时，我怀疑会有更多程序来自更多地方。

如果你使用特定软件包来实现备份，作者通常会有自己的跟踪磁带内容的实现。他们甚至可能决定将信息存储在只有他们的程序才能理解的格式中。其他程序将使用基于文本的索引文件并将数据存储在标准格式之一中，例如 tar 或 cpio。你选择哪一个？如果你猜测答案是“视情况而定”，那么你就开始掌握这整个系统管理员的事情了。

在你承诺（以及你的整个组织）使用任何备份程序之前，你应该非常仔细地评估它，以查看它是否满足你的需求，而不是作者的需求或销售它的公司的需求。你的需求。如果它不做你需要的事情，你会在某个时间点非常后悔——通常是在人们依赖备份来拯救他们免受不愉快的事情时。
