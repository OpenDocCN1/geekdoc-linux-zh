
```
[root@server1 root]# cat prologue
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny.
Where civil blood makes civil hands unclean.
From forth the fatal loins of these two foes
A pair of star-cross'd lovers take their life;
Whole misadventured piteous overthrows
Do with their death bury their parents' strife.
The fearful passage of their death-mark'd love,
And the continuance of their parents' rage,
Which, but their children's end, no might could remove,
Is now the two hours' traffick of our stage;
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1 root]# _
```

如果你想要将前一个文件中的所有小写`a`字符替换为大写`A`字符，按每行第一个字符对内容排序，将输出设为双倍行距，并逐页查看结果，可以使用以下管道：

```
[root@server1 root]# cat prologue | tr a A | sort | pr -d | less
2002-05-30 09:32 Page 1

And the continuance of their parents' rage,
A pair of star-cross'd lovers take their life;
Do with their deAth bury their pARENTs' strife.

From Ancient grudge break to new mutiny.

From forth the fAtAl loins of these two foes

In fAir VeronA, where we lAy our scene,

Is now the two hours' trAffic of our stAge;

The feArfuL pAssAge of their deAth-mark'd love.

The which if you with pAtient eArs Attend,

Two household, both alike in dignity,
:
```

前一个例子中使用的命令通过`less`命令将最终的标准输出显示到终端屏幕。在许多情况下，你可能希望显示管道结果，同时也希望保留硬盘上文件中的副本。因此，存在`tee`命令，它是一个过滤器命令，从标准输入接收信息，并将该信息发送到文件，同时也发送到标准输出。

要在显示到终端屏幕之前保存操纵后的序言副本（使用`less`命令显示），可以使用以下命令：

```
[root@server1 root]# cat prologue | tr a A | sort | pr -d | tee newfile | less
2002-05-30 09:32 Page 1

And the continuAnce of their pARENTs' rAge.

A pAir of stAr-cross'd lovers tAke their life;

Do with their deAth bury their pARENTs' strife.

From Ancient grudge break to new mutiny.

From forth the fAtAl loins of these two foes

In fAir VeronA, where we lAy our scene,

Is now the two hours' trAffic of our stAge;

The feArfuL pAssAge of their deAth-mark'd love.
```

## 2.1 命令输入和输出

此外，您可以将重定向和管道组合使用；但是，输入重定向必须出现在管道的开头，而输出重定向必须出现在管道的末尾。以下输出展示了一个示例，该示例将前一个示例中使用的`prologue`文件中所有小写字母`A`替换为大写字母`A`，然后对文件进行排序，为每一行编号，并将输出保存到名为`newprologue`的文件中，而不是将输出发送到终端屏幕。

```
[root@server1 root]# tr a A <prologue | sort | nl >newprologue
[root@server1 root]# cat newprologue
   1 And the continuance of their parents' rage.
   2 A pair of star-cross'd lovers take their life.
   3 Do with their death bury their parents' strife.
   4 From ancient grudge break to new mutiny.
   5 From forth the fatal loins of these two foes
   6 In fair Verona, where we lay our scene,
   7 Is now the two hours' traffic of our stage;
   8 The fearful passage of their death-mark'd love,
   9 The which if you with patient ears attend,
  10 Two households, both alike in dignity,
  11 What here shall miss, our toil shall strive to mend.
  12 Where civil blood makes civil hands unclean.
  13 Which, but their children's end, nought could remove,
  14 Whole misadventured piteous overthrows
[root@server1 root]# _
```

许多Linux命令可用于提供大量有用的文本信息。因此，Linux管理员经常使用`sed`和`awk`过滤命令与管道配合，以操作从这些命令获取的文本信息。

`sed`命令通常用于搜索特定的字符串，并使用语法`s/search/replace/`将该文本字符串替换为另一个文本字符串。例如，以下输出演示了如何使用`sed`在之前使用的`prologue`文件中搜索字符串 "the" 并将其替换为字符串 "THE"：

```
[root@server1 root]# cat prologue | sed s/the/THE/
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
From forth the fatal loins of these two foes
A pair of star-cross'd lovers take their life;
Whole misadventured piteous overthrows
Do with THEIR death bury their parents' strife.
The fearful passage of THEIR death-mark'd love,
And THE continuance of their parents' rage,
Which, but THEIR children's end, nought could remove,
Is now THE two hours' traffic of our stage;
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1 root]# _
```
