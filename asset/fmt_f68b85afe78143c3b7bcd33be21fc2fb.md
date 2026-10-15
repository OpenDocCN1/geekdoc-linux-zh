
`8 hour a day.txt:78:nice paint job too`

`ghost pain.txt:32:Subject: ghost pain`

```
fiery inferno in space.txt:56:watch the paint peel,
three_no_more_forever.txt:19:all alone and in pain
speed of morning.txt:66:of a Chinese painting.
8 hour a day.txt:78:nice paint job too
ghost pain.txt:32:Subject: ghost pain
```

现在你已经知道了字符串 `pain` 的每个实例的行号，那么在几乎任何文本编辑器中直接跳转到那些行就是件简单的事情。太棒了！

## 在其他命令的输出中搜索特定单词

```
$ ls -1 | grep 1960
```

`grep` 命令在单独使用时非常强大，但当你将其作为其他程序输出的过滤器时，它就变得真正活跃了。例如，假设你所有的 John Coltrane MP3 都按每个专辑组织在单独的子文件夹中（共 66 个……是的，Coltr 确实那么出色），并以年份开头。部分列表可能如下（在 `ls` 中使用了 `-1` 选项，以便每行一个结果）：

```
$ ls -1
1956_Coltrane_For_Lovers
1957_Blue_Train
1957_Coltrane_[Prestige]
1957_Lush_Life
1957_Thelonious_Monk_With_John_Coltrane
```

现在，如果你只想看到你拥有的 Coltrane 在 1960 年发布的专辑列表？将 `ls -1` 的结果管道给 `grep`，几秒钟就能得到答案。

```
$ ls -1 | grep 1960
1960_Coltrane_Plays_The_Blues
1960_Coltrane's_Sound
1960_Giant_Steps
1960_My_Favorite_Things
```

在你开始思考它后，你会发现 `grep` 以这种方式真的有几百种用法。这里有另一个强大的用法。`ps` 命令列出运行中的进程，而 `-f` 选项告诉 `ps` 提供完整列表，包含关于每个进程的大量信息，而 `-U` 选项后跟用户名会将输出限制为该用户拥有的进程。通常情况下，`ps -fU scott` 会导致一个长列表，如果你正在寻找关于特定进程的信息，列表就太长了。然而，通过 `grep`，你可以轻松地限制输出。

注意：为了节省空间，你通常通过 `ps` 看到的一些信息已被剔除。

```
$ ps -fU scott | grep firefox
scott 17623 /bin/sh /opt/firefox/firefox
scott 17634 /opt/firefox/firefox-bin
scott 1601 grep firefox
```

# 查看文件中出现单词的上下文

`ps` 命令列出了 `scott` 用户拥有的所有命令（实际上有 64 个），但它将该输出管道给 `grep`，后者只列出包含 `firefox` 单词的行。遗憾的是，输出的最后一行是错误的：你只关心真正的 Firefox 程序，而不是使用 `grep` 对 `firefox` 进行搜索。为了在 `grep` 结果中隐藏对 `firefox` 的搜索，请尝试这种方法：

```bash
$ ps -fU scott | grep [f]firefox
scott 17623 /bin/sh /opt/firefox/firefox
scott 17634 /opt/firefox/firefox-bin
```

你的 `grep` 搜索使用了一个正则范围，从 `f` 到 `t`，它在 `ps` 运行 Firefox 的那些行中找到了 `firefox`；然而，它没有匹配到 `grep` 所在的行，因为该行实际上是 `[f]firefox`，这是不会被匹配的。这里的 `grep` 命令无法匹配原始字符串 `ps -ef | grep [f]firefox`，因为它包含了 `[ ]`，而对 `[f]firefox` 的 `grep` 搜索解析为搜索精确单词。这有点困惑，但如果你自己尝试并思考一下，它就会变得通顺。无论如何，它是有效的。试试吧！

## 查看文件中出现单词的上下文 -A, -B, -C

`ps` 命令列出了所有由 `scott` 用户拥有的命令（实际上有 64 个），但将该输出管道给 `grep`，后者只列出包含 `firefox` 单词的行。遗憾的是，输出的最后一行是错误的：你只关心真正的 Firefox 程序，而不是使用 `grep` 对 `firefox` 进行搜索。为了在 `grep` 结果中隐藏对 `firefox` 的搜索，请尝试这种方法：

```bash
$ ps -fU scott | grep [f]firefox
scott 17623 /bin/sh /opt/firefox/firefox
scott 17634 /opt/firefox/firefox-bin
```

你的 `grep` 搜索使用了一个正则范围，从 `f` 到 `t`，它在 `ps` 运行 Firefox 的那些行中找到了 `firefox`；然而，它没有匹配到 `grep` 所在的行，因为该行实际上是 `[f]firefox`，这是不会被匹配的。这里的 `grep` 命令无法匹配原始字符串 `ps -ef | grep [f]firefox`，因为它包含了 `[ ]`，而对 `[f]firefox` 的 `grep` 搜索解析为搜索精确单词。这有点困惑，但如果你自己尝试并思考一下，它就会变得通顺。无论如何，它是有效的。试试吧！

在处理数据时，上下文就是一切。正如你所学到的，`grep` 显示包含术语的行，但也可以让 `grep` 显示匹配项前后的几行。要找到匹配项之前的行，请使用 `-B`（或 `--before`）选项。

```bash
$ grep -B 3 "pain" *
fiery inferno in space.txt:56:watch the paint peel,
three_no_more_forever.txt:19:all alone and in pain
speed of morning.txt:66:of a Chinese painting.
8 hour a day.txt:78:nice paint job too
ghost pain.txt:32:Subject: ghost pain
```

现在你已经知道了字符串 `pain` 的每个实例的行号，那么在几乎任何文本编辑器中直接跳转到那些行就是件简单的事情。太棒了！

如果你想显示匹配项之后的行，请使用 `-A`（或 `--after`）选项。

```bash
$ grep -A 3 "pain" *
fiery inferno in space.txt:56:watch the paint peel,
three_no_more_forever.txt:19:all alone and in pain
speed of morning.txt:66:of a Chinese painting.
8 hour a day.txt:78:nice paint job too
ghost pain.txt:32:Subject: ghost pain
```

如果你想同时显示匹配项及其前后的几行，请使用 `-C`（或 `--context`）选项。

```bash
$ grep -C 3 "pain" *
fiery inferno in space.txt:56:watch the paint peel,
three_no_more_forever.txt:19:all alone and in pain
speed of morning.txt:66:of a Chinese painting.
8 hour a day.txt:78:nice paint job too
ghost pain.txt:32:Subject: ghost pain
```

## 显示文件中不包含单词的行

```
-v
```

## 列出包含搜索词的文件

你可以只显示不匹配给定模式的结果。

```
$ ls -1
1969_Led_Zeppelin
1969_Led_Zeppelin_II
1970_Led_Zeppelin_III
1971_Led_Zeppelin_IV
1973_Houses_Of_The_Holy
1975_Physical_Graffiti
1976_Presence
1979_In_Through_The_Out_Door
1982_Coda

$ ls -1 | grep -v Led_Zeppelin
1973_Houses_Of_The_Holy
1975_Physical_Graffiti
1976_Presence
1979_In_Through_The_Out_Door
1982_Coda
```

通过 `-v`，你真的可以开始筛选结果，只显示你需要的精确项目。你可能不会一直都使用 `-v`，但当你需要它时，你会庆幸它的存在。

## 列出包含搜索词的文件

```
-1
```

`grep` 命令列出包含你搜索术语的行，但有时你并不想知道那些行；相反，你想知道包含这些匹配行的文件名称。在之前的“在文件中搜索文本，忽略大小写”中，你曾在 H.P. 洛夫拉特的故事中寻找包含 `hideous` 单词的行。通过 `-1`（或 `--files-with-matches`）选项，你可以改为生成这些文件的列表（记得 `-i` 用于不区分大小写的搜索）。

```
