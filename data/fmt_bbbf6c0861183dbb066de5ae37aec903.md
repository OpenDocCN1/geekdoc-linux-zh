
应该很清楚，Unix 是操作系统的瑞士军刀。即使是最简单的命令也有数十种不同的选项。例如在 Mac OS X 上，`ls` 就有超过 33 个不同的标志。像 Unix 中几乎任何其他命令一样，它是一个用途无穷的工具——其中大部分来自你自己的创造力和个人喜好，其真正的威力来自于它与其他工具和命令结合使用的方式，正如你稍后会看到的那样。

## Task 4.5: Changing the Sort Order in ls

如果想要查看文件，但希望它们以不同于默认的目录排序顺序显示，例如按列优先顺序，该怎么办？如何更改 `ls` 中的排序顺序？

1. `-x` 标志按行排序，将输出以列的形式列出，或 [行优先顺序](#)（其中条目先横向排序，然后纵向排序）：

[Click here to view code image](#)

```
% ls -a
.		.elm		.plan		Global.Software
..		.forward		.pnewsexpert	Interactive.Unix
.Pnews.header	.ircmod		.rnlast		Mail
.accinfo		.login		.rnlock		News
.article		.logout		.rnsoft		Src
.cshrc		.newsrc		.sig		bin
.delgroups		.oldnewsrc	.tin		history.usenet.Z

% ls -x -a
.		..		.Pnews.header	.accinfo
.article		.cshrc		.delgroups	.elm
.forward		.ircmod		.login		.logout
.newsrc		.oldnewsrc	.plan		.pnewsexpert
.rnlast		.rnlock		.rnsoft		.sig
.tin		Global.Software	Interactive.Unix	Mail
News		Src		bin		history.usenet.Z
```

2. `ls` 中还有更多排序文件的方式。如果你想按最近访问到最少访问的顺序排序文件，则使用 `-t` 标志：

[Click here to view code image](#)

```
% ls -a -t
./		../		.rnlock		.cshrc
.newsrc		News/		.rnlast		.sig
.oldnewsrc	.tin/		.rnsoft		.plan
.article		.ircmod		Interactive.Unix	Mail/
.elm/		.delgroups	.accinfo*	.Pnews.header*
.forward	.login		Src/		.pnewsexpert
history.usenet.Z	bin/		Global.Software	.logout
```

从此输出中，你可以看到最近访问的文件是 `.newsrc` 和 `.oldnewsrc`，而 `.logout` 已很长时间未被触及。尝试在你的系统上使用 `-t` 标志，看看哪些文件你访问过，哪些没有。

3. 到目前为止，你已了解在 `ls` 命令中对文件进行排序的三种不同方法：列优先顺序、行优先顺序以及最近访问优先顺序。但 `ls` 中存在的选项远不止这三种。例如，`-r` 标志会反转任何排序顺序：

```
% ls
Global.Software	Mail/		Src/		history.usenet.Z
Interactive.Unix	News/		bin/
% ls -r
history.usenet.Z	Src/		Mail/		Global.Software
bin/			News/		Interactive.Unix
```

4. 当你组合使用这些标志时，事情可能会变得令人困惑。尝试列出比当前目录高一级的目录的内容，并按最近访问的文件排在最后的顺序排序。同时，你还想知道哪些项目是目录以及每个文件的大小。使用以下命令：

如果你尝试列出一个目录的内容而没有权限访问其信息，`ls` 会用错误信息警告你：

```
% ls ../marv
../marv unreadable
```

现在请求对目录 `/etc` 进行递归列出，并标明文件类型和大小，看看里面有什么。该列出将包含许多文件和子目录，但由于 `ls` 使用的所有表示法来指示文件和目录，因此应该很容易浏览。

## Task 4.7: Long Listing Format in ls

你已经看到如何通过使用 `-s` 标志来估计文件占用的块数来估算文件大小。要查找文件的确切大小（以字节为单位），请使用 `-l` 标志。 （使用小写字母 `l`。数字 `1` 会产生单列输出，正如你已经学到的那样。）

### 1. 第一个长列出显示了 `LISTS` 文件的信息：

Click here to view code image

```
% ls -l LISTS
-rw--- 1 taylor 106020 Oct 8 15:17 LISTS
```

输出在图 4.1 中进行了说明。

![](img/036fe100817eada43c999b050270081b_77_0.png)

FIGURE 4.1 The meaning of the -l output for a file.

对于 Unix 文件系统中的每个文件和目录，都会记录所有者、大小、名称、指向它的其他文件数（链接）以及访问权限。每个文件的创建、修改和访问时间及日期也会被记录。修改时间是 `-t` 排序选项的默认时间，也是 `ls` 长格式所列出时间。

### Permissions Strings

```
% ls -l -d Example
drwxr-x-  2 taylor      1024 Sep 30 10:50 Example/
```

记住，你必须同时具有目录的读和执行权限。如果你只有读或执行权限之一而没有两者，目录将无法使用（就像你没有任何权限一样）。当然，写权限使用户能够更改目录的内容或向目录添加新文件。

2. `Example` 目录可以如图所示进行解释 Figure 4.4。

![](img/036fe100817eada43c999b050270081b_79_0.png)

# FIGURE 4.4 Elements of directory permissions.

### Note

I’ve never understood the nuances of a directory with read but not execute permission, or vice versa, and explanations from other people have never proven to be correct. It’s okay, though, because I’ve never seen a directory on a Unix system that was anything other than ---, r-x, rw-, or rwx.

3. 现在试着自己使用 `-l` 标志。移动到你的主目录并输入 `ls -l`，如下所示：

Click here to view code image

```
% ls -l
total 403
drwx--  2 taylor      512 Sep 30 10:38 Archives/
drwx--  3 taylor      512 Oct  1 08:23 InfoWorld/
-rw---  1 taylor    46901 Oct  8 15:17 LISTS
```

`drwx--  2 taylor      1024 Sep 30 10:50 Mail/`

`drwx--  2 taylor       512 Oct  6 09:36 News/`

`drwx--  2 taylor       512 Sep 30 10:51 OWL/`

`-rw---  1 taylor      4643 Sep 20 10:49 RUMORS.18Sept`

`drwx--  2 taylor       512 Oct  1 09:53 bin/`

`-rw---  1 taylor      3843 Oct  6 18:02 iecc.list`

`-rw-rw-- 1 taylor    280232 Oct  6 09:57 mailing.lists`

`-rw-rw-- 1 taylor      1031 Oct  7 15:44 newlists`

`drwx--  2 taylor       512 Sep 14 22:14 src/`

目录的大小通常以 512 字节为增量，尽管某些 Unix 系统会显示目录中文件名的确切大小。 （Unix 不会显示目录中文件的大小，只会显示所有文件名的总大小。）第二个字段，即“链接”，是在列出目录时一个有趣且鲜为人知的数值。它并不是统计指向该文件的其他文件的数量（即有多少文件链接到当前文件），而是指示该特定目录中包含的目录数量。请记住，所有目录都有点号和点点号，因此最小值始终为 2。

## 4. 请考虑以下目录列表示例：

Click here to view code image
