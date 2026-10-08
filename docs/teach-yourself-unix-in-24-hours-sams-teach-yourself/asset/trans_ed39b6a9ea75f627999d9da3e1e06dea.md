
UNIX 多年来一直提供一种类似的功能，在 UNIX 术语中它被称为“符号链接”（symbolic link）。符号链接（例如表 4.1 中的 `bin`）包含另一个文件或目录的名称，而不是其本身的内容。如果你查看其内部，它看起来可能像 `bin = @usr/bin`。每当有人尝试查看 `bin` 时，系统会显示 `/usr/bin` 的内容。

你将在书的稍后部分学习更多关于符号链接以及它们如何帮助你组织文件的知识。现在，请记住，如果你看到 `@` 文件名，它是指向文件系统中另一个位置的链接。

- `ls` 的一个标志（在你的 UNIX 版本中可能不可用）是 `-m` 标志，它将文件以逗号分隔的列表形式输出。如果文件很多，`-m` 可以是一种快速且方便的查看可用文件方法。

```
% ls -m
Archives, Infolist, LISTS, Mail, News, OWL, RUMORS.18Sept., bin, ie.list, mailing.lists, src
```

有时你可能想将每个文件单独列在一行，也许为了打印你想要注释的输出。你已经看到过 `-c` 标志可以强制顽固的 `ls` 版本输出多列。遗憾的是，使用小写的 `c` 无法获得相反的行为。（UNIX 应该如此一致！）相反，请使用 `-1` 标志表示你有一列输出。尝试一下吧。

# 任务 4.3：组合标志

你到为止学到的不同标志总结在表 4.2 中。

表 4.2. `ls` 的一些常用标志
| 标志 | 含义 |
| :--- | :--- |
| -a | 列出所有文件，包括隐藏文件（点文件） |
| -F | 指定文件类型；/= = 目录，* = 可执行。 |
| -m | 以逗号分隔的列表显示文件。 |
| -s | 以块显示文件大小（通常，1 块 = 1,024 字节）。 |
| -C | 强制列表进行多列输出。 |
| -1 | 强制列表进行单列输出。 |

你想列出的一个使用 `-F` 惯例生成、同时显示所有文件并标明其类型的列表是什么？

# 列出文件和管理磁盘空间

## 操作

1. 在 UNIX 中组合标志非常简单。你所做的就是将它们以字符序列的形式一起运行，并在整个序列前加一个连字符：

```
% ls -aF
-/ .gopherc .oldnewsrc -sig
-/ RUMORS.18Sept .plan Archives/
-/ .history*
-/ /bin/ .info .newsexpert InfoWorld/
-/ lecc.list .letter report LISTS
-/ aconfogric -mailing.lists
-/ article .login -rm-timestamp Mail/
-/ news
-/ cshrc -rlast News/
-/ src/
-/ .elm/ .rnsoft OWL/
```

2. 有时，将所有标志分开保持更方便。只要每个标志前面都带有一个连字符，这样做就是可以的：

```
% ls -F
total 403
1 Archives/ 1 Mail/ 5 RUMORS.18Sept 280 mailing.lists
1 InfoWorld/ 1 News/ 2 bin/ 2 news
108 LISTS 1 OWL/ 4 lecc.list 1 src/
```

3. 在你自己的电脑上尝试这些组合。也尝试多次列出同一个标志（例如，`ls -ss -s`），或以不同的顺序列出标志。

## 总结

极少数 UNIX 命令在乎标志列出的顺序。因为标志的存在与否才是重要的，所以多次列出同一个标志没有任何区别。

# 任务 4.4：在不改变位置的情况下列出目录

## 描述

每当我尝试在图书馆进行任何研究时，我发现自己在那里花费了几个小时，但我觉得我的研究比预想的要少。这是因为我大部分时间都花在了寻找书的位置以及书本身上。如果你被限制只能列出你所在的目录，就会让你陷入困境。仅使用 `ls` 会大大减慢你的速度并强迫你每次都使用 `cd`。相反，你可以通过 `ls` 指定你感兴趣的文件。

![](img/f32f6f53c129de2ebafcd2b4ff01b19_0_png)

## 操作

1. 在你的系统上尝试这个。列出 `/usr`：

```
% ls -F /usr
bin/      diag/      share/    ucba@
include/  dict/      lib/      source/    ucblib@
lib/       etc/      local/    spool/    xpg2bin/
acc/       export/  last-found/ src       xpg2include/
acctlog   games/    man@      stand/    xpg2lib/
adm/       hosts/    mde0      sys/
bin/       include/  old/       system/
boot/      kvm/       sccs/      ucb/

你在 `/usr` 目录下可能列出了不同的文件和目录。记住，`@` 是符号链接。

2. 你可以指定多个目录：

```
% ls -F /usr/local/home/taylor /home/taylor:Global.Software Mail/ Srcusenet.Z Interactive.Unix News/bin/
/usr/local/:emacs/ ftp/ admin/emacs-18Sept gnubin/ bin/ include/ net/ cat/ policy/
```
在这个例子中，命令将目录排在了前面。我指定查看 `/usr/local` 和 `/home/taylor`，但它们以相反的顺序呈现。我从来没搞明白当你要求列出多个项时 `ls` 是如何排序的——它不是字母顺序。如果你必须按特定顺序输出，可以使用 `ls` 命令。

![](img/f32f6f53c129de2ebafcd2b4ff01b_82_png)

## 分钟

3. 点缩写在这里非常有用。自己尝试一下：

```
% ls -d bruce, cedric, christine, david, green, guest, higgins, james, laura, mark, rank, shalini, taylor, vicki
```
如果你在文件系统的某个分支并想查看另一个分支的文件，可以轻松地使用命令 `ls ../source`。

![](img/f32f6f53c129de2ebafcd2b4ff01b_1)

# 列出文件和磁盘使用

4. 这里有一个问题。你看到你可以指定文件名来查看这些文件，指定目录名来查看目录的内容，但如果你对目录本身感兴趣而不是它的内容呢？我想只列出两个目录——不是内容，只是文件，如下所示：

```
% ls -d Archives/ Mail/ RUMORS.18Sept mailing.lists Infoworld/ bin/ LISTS OWL/ iecc.list src/
```
```
% ls -s Mail/
total 705
8 cennamo 27 ean 4 kcs 21 mark 7 satin
28 den_sommer 2 gordon 34 lehman 5 raf shelf
14 decc 48 harris 64 mac 7 rock 20 steve
3 dummy 14 james 92 mailbox 18 tai
```

5. 问题在于 `ls` 不知道你想查看内部，除非使用 `-d` 标志，它强制 `ls` 列出目录而不是内容。同样的 `ls` 命令加上 `-d` 标志会有完全不同的输出：

```
% ls -ds Mail/
108 LIST 1
```

在你自己的系统上尝试这些标志，并观察它们是如何协同工作的。要列出文件或目录，你可以将其指定给 `ls`。然而，除非你包含 `-d` 标志，否则目录会显示它们的内容。

# 特殊命令标志

你应该很清楚 UNIX 是终极工具箱。即使是最简单的命令也有几十种不同的选项。在我使用的一个系统中，`ls` 有 20 个不同的标志。

# 任务 4.5：更改 ls 的排序顺序

如果你想查看文件，但想以不同于默认的顺序显示它们（即列优先顺序），你该如何更改 `ls` 的排序顺序？

1. `-x` 标志横向排序，以列的形式输出，或按第一行顺序（项横向排序，然后向下排序）：

![](img/f32f6f53c129de2ebafcd2b4ff01b_83_0_png)

# 4 小时

```
% ls -a .elm .plan Global.Software
.Pnews.header .forward .pnewsexpert Interactive.Unix
.ironmot .rmlast Mail
.accinfo .login .rlock
% ls -x historyusenet.Z
```

2. `ls` 有排序文件的方法。如果你想按最近访问到最少访问的顺序进行排序，请使用 `-t` 标志：

```
% ls -at ../crc
```

从这个输出中，你可以看到最近访问的文件是 `.newsrc` 和 `.oldsrc`，而 `.logout` 很久没动过了。对它们使用 `-t` 标志可以查看你访问了哪些哪些没有。

3. 所以，你知道了 `ls` 命令排序文件的三种不同方法：列优先顺序、行顺序和最近访问顺序。`ls` 的选项不仅是这三个；`-r` 标志可以反转任何顺序。

```
% ls -r Global.Software
```

4. 组合某些标志时事情可能会变得混乱。尝试列出当前上一级目录的内容，并使得最近访问的文件在最后。和上次一样，标明哪些是目录以及每个文件的大小。

```
% ls -r -t -F -s ..
total 150
2 bruce/ 2 rank/ 2 kane/ 14 hiccups/
```
