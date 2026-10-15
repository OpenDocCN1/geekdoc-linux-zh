

## 查找并操作文件：

+   find ~/ -name "*.backup" -ok rm {} \;

输入 find 加上通配表达式，后跟 -ok（用于执行以下命令，并进行确认），rm（要执行的命令），以及 {} \; 以将找到的每个文件作为参数填入命令。如果你想，例如，不经确认地压缩匹配的文件，你可以使用 find ~/ -name "*.backup" -exec compress {} \; 来为你完成工作。

## 提示

+   在某些 Unix 系统上，你可能不需要 -print 标志。尝试不带 -print 标志输入 find。如果你在屏幕上看到结果，那么你不需要添加 -print 标志。

+   避免从根目录开始 find 命令，如 find / -name the_missing_file -print。从根目录（用 / 表示）开始，你很可能会遇到每个你没有访问权限的目录的烦人错误信息，而这样的目录会有很多。当然，如果你以 root 身份登录，则不适用。

+   如果你只知道部分文件名，可以使用带引号的通配符与 find 一起使用，如 find . -name 'info*' -print。

+   find 提供了大量章节的选项。如果你正在寻找基于任何特征的特定文件或文件，你可以用 find 找到它们。例如，你可以使用 find /home/shared -mtime -3 来查找在过去三天内修改过的所有位于 shared 目录下的文件。参见附录 C，其中列出了大量（但不全面）的选项。

## 使用 locate 查找丢失的文件

如果你正在寻找系统文件——即 Unix 系统本身的一部分程序或文件，而不是你个人主目录中的个人文件——请尝试使用 locate 来查找。它会给出你无法处理的更多结果，但这是一种快速简便的定位系统文件的方法。

locate 命令并非在所有 Unix 系统上都可用，但无论如何都值得一试。参见代码清单 2.13，了解 locate 的实际使用情况。

## 定位文件：

+   - locate fortune

如果你尝试定位 fortune，你将获得所有包含 "fortune" 的系统文件的列表。该列表包括 fortune 程序、fortune 程序使用的 fortune 数据文件以及相关内容。在大多数情况下，这是一个巨大的列表（代码清单 2.13）。

## 提示

+   - 尽可能将 locate 与 grep 结合使用（参见第 6 章中的 使用正则表达式与 grep），以缩小你的列表。

+   - 许多人使用 locate 快速查看包含相关文件的目录（/usr/share/games/fortunes 包含大量与 fortune 程序相关的文件），然后使用其他工具进行更仔细的查看。

+   - 并非所有系统都包含 fortune——它无疑只是一个有趣的东西，绝非必不可少。如果你“定位”不到它，请尝试 bash 或 csh 来看看 locate 的工作原理。（参见第 8 章，了解有关不同 shell 及其优缺点的更多信息。）

```
[jdoe@fraz jdoe]$ locate fortune
/usr/share/man/man6/fortune.6.bz2
/usr/share/doc/fortune-mod-1.0
/usr/share/doc/fortune-mod-1.0/cs
/usr/share/doc/fortune-mod-1.0/cs/HISTORIE
/usr/share/doc/fortune-mod-1.0/cs/LICENSE
/usr/share/doc/fortune-mod-1.0/cs/README
/usr/share/doc/fortune-mod-1.0/fr
/usr/share/doc/fortune-mod-1.0/fr/
  COPYING.linuxfr
/usr/share/doc/fortune-mod-1.0/fr/
  COPYING.glp
/usr/share/doc/fortune-mod-1.0/fr/ffr
...
/usr/share/games/fortunes/songs-poems
/usr/share/games/fortunes/sports.dat
/usr/share/games/fortunes/sports
/usr/share/games/fortunes/startrek.dat
/usr/share/games/fortunes/startrek
/usr/share/games/fortunes/translator-me.dat
/usr/share/games/fortunes/translate-me
/usr/share/games/fortunes/wisdom.dat
/usr/share/games/fortunes/wisdom
/usr/share/games/fortunes/work.dat
/usr/share/games/fortunes/work
/usr/share/games/fortunes/zippy.dat
/usr/share/games/fortunes/zippy
/usr/share/sol-games/fortunes.scm
/usr/share/games/fortune
[jdoe@fraz jdoe]$
```

代码清单 2.13 使用 locate 查找与大多数系统文件相关的所有内容——所有内容。

## 使用 ln 进行链接（硬链接）

假设你的老板刚刚为你雇了一名助手（是时候了，对吧？）。你需要确保你的新助手可以访问你的文件，这样你就可以把工作推给他。而且，你需要访问修订后的文件，以便跟上助手的工作情况——也许在下一次员工会议上为他的工作邀功。

一种让助手轻松访问你的文件的好方法是，从你的主目录创建一个硬链接。在创建硬链接时，你所做的只是从现有文件开始并创建一个链接，该链接（有点）将现有文件放置在助手的 home 目录中。链接不会创建文件的副本；相反，你创建了指向磁盘上同一物理文件的第二个指针。与 Macintosh 或 Windows 计算机中的别名或快捷方式的附加指针不同，这里的两个指针都引用同一个实际文件，因此从 Unix 系统的角度来看，文件实际上位于两个位置（参见代码清单 2.14）。

由于使用硬链接通常需要你有权访问另一个用户的主目录，你可以查阅第 5 章，了解有关使用 chmod、chgrp 和 chown 访问另一个用户的目录和文件的详细信息。

```
代码清单 2.14 硬链接让两个用户可以轻松共享文件。

$ ls /home/deb/Projects/schedule/our* /home/helper/our*
$ ls -l /home/helper/our*
$ ln /home/Projects/schedule/our.projects.latest /home/helper/our_projects
$ ls -l /home/helper/our*
-rw-r--r--  3 e j r   3 users 1055 Jun 26 11:00 /home/helper/our.projects
```

