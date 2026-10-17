
上例使用的命令通过 `less` 命令将最终的 `stdout` 显示在终端屏幕上。在许多情况下，你可能希望显示管道结果的同时，使用 `tee` 命令在硬盘上的文件中保存一份副本，`tee` 命令接收 `stdin` 的信息并将该信息发送到文件以及 `stdout`。

在用 `less` 命令将处理过的序言显示到终端之前，为了保存一份副本，可以使用以下命令：

```bash
[root@server1 ~]# cat prologue|tr a A|sort|pr -d tee inputFile|less
```

输出将如下所示（转换后的文本示例）：

```text
In fAir Verona, where we lAy our scene,
Is now the two hours’ trAffic of our stAge;
The feArful pAssAge of their deATh-Ark’d love,
The which if you with pAtient eArs Attend,
Two households, both Alike in dignity,
What here shAll miss, our toil shAll strive to mend.
Where civil blood mAkes civil hAnds uncleAn.
Which, but their children’s end, nought could remove,
Whole misAdventured piteous overthrows
Do with their deATh bury their pArents’ strife.
From Ancient grudge breAk to new mutiny,
From forth the fAtAl loins of these two foes
And the continuanceA of their pArents’ rAge,
A pAir of stAr-cross'd lovers take their life;
```

你也可以结合重定向和管道，只要输入重定向发生在管道开头且输出重定向发生在末尾。以下输出显示了示例，它将上例中使用的 `prologue` 文件中的所有小写字母替换为大写，然后对文件排序，为每行编号，并将输出保存到名为 `newlog` 的文件中，而不是发送到终端。

```bash
[root@server1 ~]# tr a A < prologue | sort | nl > newlog
[root@server1 ~]# cat newlog
1 And the continuanceA of their pA’ rAge,
2 A pAir of stAr-cross'd lovers take their life;
3 Do with their deAth bury their prents’ strife.
4 From Ancient grudge breAk to new mutiny,
5 From forth the fAtAl loins of these two foes
6 In fAir Verona, where we lAy our scene,
7 Is now the two hours’ trAffic of our stAge;
8 The feArful pAssAge of their deAth-Ark’d love,
9 The which if you with pAtient Attend,
10 Two households, both Alike in dignity,
11 What here shAll miss, our toil shAll strive to mend.
12 Where civil blood mAkes civil hAnds unclean.
13 Which, but their children’s end, nought could remove,
14 Whole misAdventured overthrows
```

许多 Linux 命令可以提供大量的有用信息。因此，Linux 管理员经常配合 `sed` 和 `awk` 过滤器来处理这些命令产生的文本。

`sed` 命令通常用于搜索特定的文本字符串，并使用 `s/search/replace/` 语法替换该文本。例如，以下输出演示了如何对之前的 `prologue` 文件中的 `the` 字符串使用 `sed` 并将其替换为 `THE`：

```bash

[root@server1 ~]# cat prologue | sed s/the/THE

Two households, both in dignity,

in fair Verona, where we lay our scene,

From ancient grudge break to new mutiny,

Where blood makes hands unclean.

From forth THE fatal loins of these two foes pair of star-cross'd lovers take THEIR life;

Whole misadvent piteous overthrows

Do with THEIR bury parents' strife.

The fearful passage of THEIR death-mark'd love,

And THE continuance of THEIR parents' rage,

Which, but THEIR children' end, could remove,

Is now THE two hours' traffic of our stage;

The which if you with patient ears attend,

What here shall miss, our tail strive to mend.

```

注意上述输出 `sed` 只搜索并替换了每行中字符串“the”的首次出现处。让搜索替换表达式全局追加一个 `g`：

```bash

[root@server1 ~]# cat prologue | sed s/the/THE/g

Two households, both in dignity,

in fair Verona, where we lay our scene,

From ancient grudge break to new mutiny,

Where blood makes hands unclean.

From forth THE fatal loins of these two foes pair of star-cross'd lovers take THEIR life;

Whole misadvent piteous overthrows

Do with THEIR bury parents' strife.

The fearful passage of THEIR death-mark'd love,

And THE continuance of THEIR parents' rage,

Which, but THEIR children' end, could remove,

Is now THE two hours' traffic of our stage;

The which if you with patient ears attend,

What here shall miss, our tail strive to mend.

```

## 第 7 章 使用 BASH Shell

你也可以通过在搜索和替换表达式前面加上前缀来告诉 sed 要搜索的特定行。例如，为了强制 sed 在包含字符串 "love" 的行中全局将字符串 "the" 替换为 "THE"，你可以使用以下命令：

```
[root@server1 #]# cat prologue | sed /love/s/the/THE/g
```

- 两个世家，尊严对等
在美丽的维罗纳，我们故事的背景就在这里，
从古老的仇恨演变为新的叛乱，
平民的鲜血弄脏了双手。
从这两个仇敌致命的狮子中，
一对命途多舛的恋人结束了他们的生命；
整个不幸而悲惨的覆灭，
用他们的死亡埋葬了父母的争端。
他们死亡之标记的爱的恐怖经过，
以及他们父母愤怒的持续，
除非他们子女的终结否则无法消除，
现在成了我们舞台上两个小时的戏份；
若你耐心地倾听，
此处遗漏的内容，我们将在结尾力求弥补。
[root@server1]#_

```

你也可以强制 sed 在某些行上执行搜索和替换。要在第 5 到 8 行中全局将字符串 "the" 替换为 "THE"，你可以使用以下命令：

```
[root@server1 #]# cat prologue | sed 5,8/s/the/THE/g
```

- 两个世家，尊严对等，

在美丽的维罗纳，我们故事的背景就在这里，

从古老的仇恨演变为新的叛乱，

平民的鲜血弄脏了双手。
