
`1963_Live_At_Birdland`

`1964_A_Love_Supreme`

```
如果你想找到 `A Love Supreme` 之后的是什么，请使用 `-A`（或 `--after-context=#`）选项。

$ ls -l | grep -A 3 'A_Love_Supreme'

1964_A_Love_Supreme

1964_Coltrane's_Sound

1964_Crescent

1965_Ascension
```

要获取 `A Love Supreme` 的完整历史背景，尝试 `-C`（或 `--context=#`）选项，它将前后行结合在一起。

```
$ ls -l | grep -C 2 'A_Love_Supreme'

1963_John_Coltrane&_Johnny_Hartman

1963_Live_At_Birdland

1964_A_Love_Supreme

1964_Coltrane's_Sound

1964_Crescent
```

## 第三部分：查找内容

```bash
$ ls -1 | grep -c Live

1963_John_Coltrane&_Johnny_Hartman

1963_Live_At_Birdland

1964_A_Love_Supreme

----

1965_Last_Trane

1965_Live_in_Seattle

1965_Major_Works_of_John_Coltrane

----

1965_Transition

1966_Live_at_the_Village_Vanguard_Again!

1966_Live_in_Japan

1967_Expression

1967_Olatunji_Concert_Last_Live_Recording

1967_Stellar_Regions
```

`---` 用于分隔每个匹配组。前两组结果显然是标题中包含 `Live`，而紧随其后和几乎最后的组则稍微复杂一些。几行包含单词 `Live` 的专辑挨在一起，因此结果聚集在了一起。这看起来可能有点奇怪，但如果你观察每一行，你会发现匹配行前后的专辑也在列表中。

如果加入 `-n` 选项，结果会更加详细，它会列出行号（因为你使用了 `-1`，这是 `ls` 列表的行号）。

```bash
$ ls -1 | grep -n c Live

37-1963_John_Coltrane&_Johnny_Hartman

38-1963_Live_At_Birdland

39-1964_A_Love_Supreme

----

48-1965_Last_Trane

49-1965_Live_in_Seattle

50-1965_Major_Works_of_John_Coltrane

----

52-1965_Transition

53-1966_Live_at_the_Village_Vanguard_Again!

54-1966_Live_in_Japan

55-1967_Expression

56-1967_Olatunji_Concert_Last_Live_Recording

57-1967_Stellar_Regions
```

现在 `-C` 为你提供了关于每行的更多信息，如行号前的字符 `-` 所示。`:` 表示该行匹配成功，`-` 表示它是匹配项之前或之后的行。第 54 行 `1966_Live_in_Japan` 承担了双重职责。它位于 `1966_Live_at_the_Village_Vanguard_Again!` 之后，这意味着它本应该有一个 `-`，但它本身也是一个匹配项，因此需要一个 `:`。由于匹配项更重要，所以它胜出，最终使用的是 `:`。

## 显示文件中不包含某些单词的行

在爵士乐界，约翰·科特兰（John Coltrane）在去世近40年后仍占据着统治地位；同样，齐飞乐队（Led Zeppelin）也被认为是历史上最伟大的摇滚乐队之一。在活跃期间，齐飞乐队发行了九张专辑；然而，其中许多专辑的标题中包含了乐队名称（第四张没有标题，但大多数评论家将其识别为《齐飞乐队 IV》，所以也是如此）。如果你想查看包含齐飞乐队专辑的 MP3 文件夹列表，但排除那些实际上确实包含“Led Zeppelin”单词的文件夹怎么办？使用 `-v` 或 `--invert-match` 选项，你可以只显示不包含这些内容的结果：

```bash
$ ls -l

1969_Led_Zeppelin

1969_Led_Zeppelin_II

1970_Led_Zeppelin_III

1971_Led_Zeppelin_IV

1973_Houses_Of_The_Holy

1975_Physical_Graffiti

1976_Presence

1979_In_Through_The_Out_Door

1982_Coda

$ ls -l | grep -v Led_Zeppelin

1973_Houses_Of_The_Holy

1975_Physical_Graffiti

1976_Presence

1979_In_Through_The_Out_Door

1982_Coda
```

通过 `-v`，你可以开始筛选结果，只显示你需要的精确项目。你不会一直使用 `-v`，但当你需要时，它就会派上场。

## 列出包含搜索单词的文件

`grep` 命令列出包含你所搜索术语的行，但有时你可能不知道文件的名称；相反，你想知道包含这些行的文件名称。在之前的“忽略大小写在文件中搜索文本”中，你查找了 H.P. 洛克拉夫（H.P. Lovecraft）故事中包含隐藏单词的行。现在，你可以使用 `-l`（或 `--files-with-matches`）选项来生成这些文件的列表（记住，`-l` 是用于不区分大小写的搜索）。

```bash
$ grep -il hideous h_p_lovecraft/*

h_p_lovecraft/Call of Cthulhu.txt

h_p_lovecraft/From Beyond.txt

h_p_lovecraft/The Case of Charles Dexter Ward.txt
```

这种结果在与其他命令结合使用时特别有用。例如，如果你想打印包含隐藏单词的洛克拉夫故事列表，可以将 `grep` 与 `lpr` 命令结合如下：

```bash
$ grep -il hideous h_p_lovecraft/* | lpr
```

`find` 的另一个重要方面是，结果的格式取决于你搜索的路径。之前，我们使用的是相对路径，因此结果是以相对路径的形式给出的。如果我们改用以 `/` 开头的绝对路径会发生什么呢？

```
$ find -name "Shags**"

/music/Outs/Shags

/music/Outs/Shags/Gimme_Dat_Ting_(Live).mp3

/music/Outs/Shags/My_Pal_Foot_Foot.ogg

/music/Outs/Shags/f_Love.mp3

/music/Outs/Shags/Things_I_Wonder
```

如果你使用相对路径搜索，你的结果将使用相对路径；如果你使用绝对路径搜索，你的结果将使用绝对路径。我们将在本章后面的部分部分介绍这一原则的其他用法。现在，只需记住这个重要的观点。

> **注意**
>
> 要了解更多关于 The Shags 的信息，请访问 `www.allmusic.com/cg/am.dll?p=am&sql=11:qyk9kett7q7q`，或者在 `www.allmusic.com` 上搜索 “Shags”。在你下一次派对上播放“My Pal Foot Foot”之前，你算没生活过！

# 按所有权查找文件

```
find -user
```

除了按名称搜索文件，你还可以按所有者搜索文件。你想找到音乐驱动器上由 `scott` 拥有的文件吗？使用 `find` 配合 `-user`，后跟用户名（或用户 ID，你可以在 `/etc/passwd` 中找到它）：

```
$ find -user scott
```

哇！结果太多了！寻找不属于 `scott` 拥有的文件会简单得多。要这样做，在你想要反转的选项前面加一个 `!`：

> **注意**
>
> 为了节省空间，你通常通过 `ls -1` 能够看到的某些数据已被删除。

```
$ find ! -user scott

./Outsider/Wing/01-_Dancing_Queen.mp3

$ ls -1 ./.Outsider/Wing/01-_Dancing_Queen.mp3
```
