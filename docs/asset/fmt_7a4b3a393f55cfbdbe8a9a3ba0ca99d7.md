
# 4

这要容易得多，而且可能就是你需要的全部。不要让 `locate` 向你倾泻如洪水般的结果；相反，要控制 `locate` 命令的输出并利用它为自己服务。

## 更新 locate 使用的数据库

`updateddb`

在本章介绍 `locate` 的第一部分“搜索文件名数据库”中提到，该命令之所以如此快速，是因为它实际上是在搜索一个包含你机器文件和目录名称的数据库。当安装 `locate` 时，它会自动设为扫描你的硬盘并在白天更新该数据库。这样做是为了方便，但如果你需要找到你刚刚放在电脑上的文件，这可就不太妙了。

例如，如果你安装了 Rootkit Hunter（一个用于寻找 rootkit——即坏人用来控制你 Linux 的后门程序的程序），然后你想查看该程序安装的文件？`locate` 命令将无法为你提供帮助，因为它并不知道这些文件，并且在数据库被 `updateddb` 更新之前，它不会知道这些文件。由于该命令会索引你电脑上的每个文件和文件夹，因此你需要运行它（或者在 Linux/Ubuntu 等不鼓励使用 root 用户的发行版上使用 `sudo`）。

```
# apt-get install rkhunter

# exit

$ locate rkhunter

$ su

$ updateddb

# exit

$ locate rkhunter

/usr/local/rkhunter

/usr/local/rkhunter/bin

/usr/local/rkhunter/etc
```

在前面的命令中，你首先安装了 `rkhunter`（Rootkit Hunter 的包名），然后退出 root。搜索 `rkhunter`，但找不到它。你再次变为 root，运行 `updateddb` 扫描硬盘并让 `locate` 知道任何变化，然后退出 root。最后，再次用 `locate` 查找 `rkhunter`，这次你成功了。

你需要注意的一点是：`updateddb` 的运行速度与硬盘上的内容以及电脑的速度成正比。快速处理器、快速硬盘和少量文件？那么 `updateddb` 会运行得很快。如果你有一个慢速的 CPU、5400RPM 的硬盘和百万个文件？请预计 `updateddb` 将花费相当长。如果你想知道运行需要多久，可以在 `updateddb` 前加上 `time` 命令，如下所示：

```
# time updateddb
```

当 `updateddb` 完成时，`time` 会告诉你整理好 `locate` 数据库花了多久。这些信息记在心里很有用，以防你以后需要使用 `updateddb` 且时间紧迫。

### 注意

`updateddb` 命令与运行 `slocate -u` 完全相同，而且 `updateddb` 实际上是 `slocate` 的一个链接，你可以很容易地看到这一点。

```
$ ls -l /usr/bin/updateddb -> slocate
```

## 在文本文件中内部搜索模式

`grep`

`locate` 命令搜索文件和目录的名称，但它不能搜索这些文件的内部。要做到这一点，你需要使用 `grep`。基本上，你给 `grep` 提供一个你想要搜索的模式，将其指向你想要搜索的文件或一组文件（甚至是整个硬盘），然后 `grep` 会输出匹配你模式的行列表。

```
$ grep pain three_no_more_forever.txt

all and in pain
```

在这种情况下，你使用 `grep` 来查看 `pain` 这个词是否出现在一个包含 Peter Mhlen 创作的名为《永不再三个》（Three More Forever）诗歌的文件中。果其然，`pain` 这个词在文件中，所以 `grep` 打印出包含你搜索词的行。但如果你想同时查看 Peter 的几首诗呢？通配符来救场了！

```
$ grep pain *

fiery inferno in space.txt:which the

three_no_more_forever.txt:all and in

the speed of morning.txt:of a

hour a day.txt:nice job

ghost pain.txt:Subject: ghost pain
```

注意 `grep` 找到的是整个字符串，包括 `painting`。还要注意 `grep` 如何显示包含该术语的文件名以及包含该术语的行。到目前为止，用 `grep` 搜索文件内部是相当简单的，正如你将在后续章节中发现的那样。

## 在文本文件中内部搜索模式的基础

在上一节中，你学习了 `grep` 是通过在一组文件中搜索模式来工作的。你第一次使用 `grep` 非常基础，但现在你需要变得更复杂一点了，为了做到这一点，你需要理解 Linux 工具箱中最强大的工具之一：正则表达式，或 `regex`。为了充分利用 `grep` 的作用，你真的需要了解正则表达式；然而，正则表达式本身就是一本书，所以我们在这里只涵盖基础知识。

### 提示

想了解更多关于正则表达式的知识吗？[正则表达式入门 (Learn GNU Regular Expressions)](https://en.wikipedia.org/wiki/Regular_expression) 是一本很好的书。如果你想了解更多，可以查看 [正则表达式百科](https://en.wikipedia.org/wiki/Regular_expression)。

### 9.1 grep 的不同版本

| 模式 | 命令 | 说明 |
|---|---|---|
| 基础正则表达式 | `grep` | `grep` (Basic) |
| 扩展正则表达式 | `grep -E` | `egrep` |
| 固定字符串 | `grep -F` | `fgrep` |
| Perl 兼容的正则表达式 | `grep -P` | `pgrep` |

*(注：原文中重复出现的表格和段落已根据指令去重。)*

### 9.1 grep 的不同版本

*(注：此处保留原结构标题，但内容已在上文去重展示。)*

## 管理搜索文件名数据库时收到的结果

`-n`

如果你经常使用 `locate`，最终你会遇到这样的情况：

```
$ locate pdf

/etc/cups/pdftops.conf

/etc/xpdf

/etc/xpdf/xpdfrc-latin2
```

*(注：以下内容为原文中位于不同位置但逻辑上相关的片段整理)*

# 第三部分：寻找内容

```
/txt/rider_haggard/Queen_of_the_Dawn.txt
/txt/rider_haggard/Allan_and_the_Ice-Gods.txt
/txt/rider_haggard/Heu-Heu_or_The_Monster.txt
/txt/rider_Haggard
/txt/Rider_Haggard/King_Solomons_Mines.txt
/txt/Rider_Haggard/Quaternaim.txt
```

事实证明，艾伦·哈加德（Allan Haggard）可用的小说比他最初看起来要多。记住，当你想要最大化定位结果时要使用 `-i` 参数，否则你可能会错过你想要查找的重要文件和文件夹。

### 注意

关于 H. 莱德·哈加德（H. Rider Haggard），请参见 `http://en.wikipedia.org/wiki/Rider_Haggard`。他是一位很有趣（尽管有些过时）作家。

## 管理搜索文件名数据库时收到的结果

`-n`

如果你经常使用 `locate`，最终你会遇到这样的情况：

```
$ locate pdf

/etc/cups/pdftops.conf

/etc/xpdf

/etc/xpdf/xpdfrc-latin2
```
