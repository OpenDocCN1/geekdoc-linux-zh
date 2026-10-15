
# 第 7 章 使用 BASH Shell

## 7.1 使用 BASH Shell

例如，取莎士比亚的《罗密欧与朱丽叶》中的序言：

```
[root@server1 ~# cat prologue
Two households, both like dignity,
In Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
From the fatal loins of these two foes
A pair of star-cross'd lovers take their life;
Whose misadventured piteous overthrows
Do with their death bury their parents' strife.
The fearful passage of their death-mark'd love,
And the continuance of their parents' rage,
Which, but their children's end, nought could remove,
Is now the twos' traffic of our stage,
If which with patient ears attend,
What shall miss, our toil shall strive to mend.
```

现在，假设你将上述文件中所有的小写字母 `"a"` 替换为大字母 `"A"`，按每行的第一个字符对内容进行排序，输出双倍行间距，并分页查看结果。为了完成这些操作，你可以使用以下管道：

```
[root@server1 ~# cat prologue | tr a A | sort | pr -d | less
```

```
2010-08-20 08:00 Page 1
And the continuance of their parents' rAge,
A pair of star-crossAn'd lovers take their strife.
Do with their deathA bury their parents' strife.
From Ancient grudge breakA to new mutiny,
From forth the fatal lAins of these two foes
In fair Verona, where we lAY our scene,
Is now the twos' trAffic of our stAge,
The feAful pAssage of their deAth-mArk'd love,
The which you with patient ears Attend,
Two households, both alike in dignity,
```

上例中的命令通过 `less` 命令将最终的标准输出（`stdout`）显示在终端屏幕上。很多情况下，你可能希望在显示管道结果的同时，在硬盘上的文件中保存一份副本。这项工作的过滤命令是 `tee` 命令，它从标准输入（`stdin`）接收信息并将该信息发送到文件以及标准输出。

在用 `less` 命令将处理后的序言显示到终端屏幕之前，保存其副本，请使用以下命令：

```
[root@server1 ~# cat prologue | tr A Sort|pr -d|tee less
2010-08-20 08:06 Page 1
And the continuanceA of their parents' rAge,
```

## 命令输入与输出

A Pair of stAr-cross'd lovers tA their life;

Do with their deAth bury their pArents' strife.

From Ancient grudge breAk to new mutiny,

From forth the fatalAl loins of these two foes

In fair VeronA, where we lAy our scene,

Is now the two hours trAfficic of our stAGe;

The Fearful pAssage of their deAth-mArk'd love,

The which you if with pAtient ears Attend,

Two households, both Alike in dignity,

```
[root@server1]#

[root@server1]# cat newfile
```

```
2010-08-20 08:06
And the continuance of their parents' rAge,
A Pair of stAr-cross'd lovers tAke their life;
Do with their deAth bury their pArents' strife.
From Ancient grudge breAk to new mutiny,
From forth the fatal loins of these two foes
In fair VeronA, where we lAy our scene,
Is now the two hours trAfficic of our stAGe;
The Fearful pAssage of their deAth-mArk'd love,
The which you if with pAtient ears Attend,
Two households, both Alike in dignity,

Page 1
```

![image](img/bafa5678973f896b93838a140b8f7840_330_0.png)

What her shall miss, our toil shAll strive to mend.
Where civil blood mAkes civil hands uncle,
Which, their children's night could remove,
Whose misadvented piteous overflows

```
[root@server1]-#
```

你还可以将减少（reduction）和管道结合，就像在页面开头进行输入减少而在页面末尾进行输出减少一样。以下输出显示了这种示例，它将上例中使用的序言文件中所有的 `"a"` 字符替换为大写 `"A"`，对文件进行排序、标记行号并将输出保存到名为 `newprologue` 的文件中；将输出发送到终端：

```
[root@server1]-# tr A -prologue | sort | nl newprologue

[root@server1]# cat newprologue
```
