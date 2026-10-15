

drwx--  2 taylor      1024 Sep 30 10:50 Mail/
drwx--  2 taylor       512 Oct  6 09:36 News/
drwx--  2 taylor       512 Sep 30 10:51 OWL/
-rw---  1 taylor      4643 Sep 20 10:49 RUMORS.18Sept
drwx--  2 taylor       512 Oct  1 09:53 bin/
-rw---  1 taylor      3843 Oct  6 18:02 iecc.list
-rw-rw-- 1 taylor    280232 Oct  6 09:57 mailing.lists
-rw-rw-- 1 taylor      1031 Oct  7 15:44 newlists
drwx--  2 taylor       512 Sep 14 22:14 src/

目录的大小通常以 512 字节为增量，尽管某些 Unix 系统会显示目录中文件名的确切大小。 （Unix 不会显示目录中文件的大小，只会显示所有文件名的总大小。）第二个字段，即“链接”，是在列出目录时一个有趣且鲜为人知的数值。它并不是统计指向该文件的其他文件的数量（即有多少文件链接到当前文件），而是指示该特定目录中包含的目录数量。请记住，所有目录都有点号和点点号，因此最小值始终为 2。

## 4. 请考虑以下目录列表示例：

Click here to view code image

```
$ ls -Fa
./          .gopher rc   .oldnews rc   .sig        OWL/
../         .history*   .plan        Archives/   RUMORS.18Sept
.A genda    .info        .pnewsexpert Cancelled.mail bin/
.autoconfigrc .letter    .report      InfoWorld/  iecc.list
.article    .login       .rm-timestamp LISTS       mailing.lists
.cshrc      .mailrc      .rnlast      Mail/       newlists
.elm/       .news rc     .rns oft     News/       src/
$ ls -ld .
drwx-- 10 taylor      1024 Oct 10 16:00 ./
```

## 5. 尝试输入 ls -ld . 并查看它是否能正确识别你主目录中的目录数量。移动到其他目录并查看列表是否与你自己统计的目录数量一致。

`ls -l` 命令的输出无疑是复杂且信息密集的。解释权限字符串是理解和使用 Unix 的重要部分，后续章节会提供更多解释。

表 4.3 总结了本小时你所学到的 `ls` 的许多不同命令标志。

| Flag | Meaning |
|---|---|
| `-1` | Force single-column output on listings. |
| `-a` | List all files, including any dot files. |
| `-C` | Force multiple-column output on listings. |
| `-d` | List directories rather than their contents. |
| `-F` | Indicate file types: `/` = directory and `*` = executable. |
| `-l` | Generate a long listing of files and directories. |
| `-m` | Show files as a comma-separated list. |
| `-r` | Reverse the order of any file sorting. |
| `-R` | Recursively show directories and their contents. |
| `-s` | Show size of files, in blocks (typically 1 block = 1,024 bytes). |
| `-t` | Sort output in most-recently modified order. |
| `-x` | Sort output in row-first order. |

## TABLE 4.3 Summary of Command Flags for ls

毫无疑问，`ls` 是 Unix 中最强大、因此也最令人困惑的命令之一。了解所有标志如何协同工作的最佳方法是尝试不同的组合。

## Task 4.9: Creating Files with the touch Command

到目前为止，你已经了解了各种有助于你在文件系统中移动并了解特定文件的 Unix 工具。现在是使用 `touch` 命令的时候了，该命令可帮助你在系统上创建新文件，而无需任何程序以外的 shell 本身。这对于组织新的文件集合等非常有帮助。

在 Unix 中使用 `touch` 的主要原因是强制更新文件的最后修改时间，如以下示例所示：

[Click here to view code image](#)

```
 % ls -l iecc.list
-rw---- 1 taylor    3843 Oct  6 18:02 iecc.list
 % touch iecc.list
 % ls -l iecc.list
-rw---- 1 taylor    3843 Oct 10 16:22 iecc.list
```

由于 `touch` 命令会更改文件的修改时间，任何基于修改时间对文件进行排序的操作，当然都会在文件被 `touch` 修改时改变该文件的位置。

- 1. 请考虑以下输出：

[Click here to view code image](#)

```
 % ls -t
mailing.lists   LISTS          News/          OWL/          src/
Canceled.mail    newlists       bin/           Mail/
RUMORs.18Sept    iecc.list      InfoWorld/     Archives/
```

