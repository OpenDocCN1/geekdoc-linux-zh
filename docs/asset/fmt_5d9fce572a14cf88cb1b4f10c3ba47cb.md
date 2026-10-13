
2. 否则，尝试使用 `:w newfile` 写入文件：当你按下回车键时，你会看到这个：

--

"newfile" [新文件] 9 行，276 个字符

3. 现在注意光标在文件中的位置。`:r` (readfile) 命令总是包含当前行以下的内容。在我按下回车键之前，我的屏幕是这样的：

> 我发现自己正偷看自己的手表，无意中听到猫将军的助手向他传了最新消息。

“他甚至不在这儿，”对话中说道。

# 使用 vi 进行编辑

“谁？”

“万岁。”

“他到底在哪儿？”

“在埃尔帕索的医院里。”

“什么？为什么我们没被通知？他到底怎么了？”

-

-

-

-

:r newfile

按下回车键得到如下结果：

-

-

# 第 11 小时：高级技巧、工具和技巧

这是一种可以将文件包含在另一个文件中，或者构建一个包含许多其他文件的有用方法。

4. 现在既然我弄乱了文件，我想把它保存到一个新文件 `buckaroo` 中：

```
:w buckaroo.confused
```

当我按下回车键时，我看到这个：

```
"buckaroo.confused" [新文件] 17 行，546 个字符
```

5. 现在是时候移动到启动时提供的文件列表中的第二个文件了。要这样做，我使用 `:n` (nextfile) 命令：

```
:n
```

按下回车键会将下一个文件引入编辑器以替换第一个：

| | | | |

|---|---|---|---|

| leungct | ttyRV | Dec | 18:27 (magenta) |

| tuynhwa | ttyRX | Dec | 22:38 (expert) |

| hollenst | ttyRZ | Dec | 22:14 (dov) |

| brandt | ttyRB | Nov | 28:03 (age) |

| holmes | ttyJ | Dec | 21:59 (age) |

| yuxi | ttyN | Dec | 14:19 (pc) |

| frodo | ttyO | Dec | 22:01 (mentor) |

| labeck | ttyT | Dec | 22:02 (dov) |

| chen1x2 | ttyR | Dec | 21:53 (mentor) |

| leungct | ttyS | Nov | 28 | 15:11 (gold) |

| chinese | ttyS | Dec | 22:53 (excalibur) |

| cdmmert | ttyS | Dec | 23:00 (mentor) |

| yuenca | ttyS | Dec | 23:00 (mentor) |

| janitor | ttyS | Dec | 18:18 (age) |

| mathisb | tysS | Dec | 23:17 (age) |

| cs541 | ttyC | Dec | 2 | 15:16 (solaria) |

# 使用 vi 进行编辑

```
yansong | ttysL | Dec | 14:44 (math)
mdps | ttysO | Nov | 30 | 19:39 (localhost)
md | ttysU | Dec | 2 | 08:45 (muller)
jac | ttysa | Dec | 18:18 (localhost)
eichted | ttyysb | Dec | 23:21 (pc1)
sweetet | ttysc | Dec | 3 | 22:40 (dov)
*big.output* 40 行，1659 个字符
```

在处理这个过程中，我突然意识到我需要对最近保存的 `buckaroo.confused` 进行微调。这时 `:e` 命令大派用场了。使用它，我可以编辑任何其他文件：

```
:e buckaroo.confused
```

我按下回车键看到这个：

> 我发现自己正偷看自己的手表，无意中听到

猫将军的

我发现正偷看自己的手表，无意中听到

猫将军的

助手向他传了最新消息。

“他甚至不在这儿，”对话中说道。

“谁？”

“万岁。”

“他到底在哪儿？”

“在埃尔帕索的医院里。”

“什么？为什么我们没被通知？他到底怎么了？”

助手向他传了最新消息。

“他甚至不在这儿，”对话中说道。

“谁？”

“万岁。”

“他到底在哪儿？”

“在埃尔帕索的医院里。”

“什么？为什么我们没被通知？他到底怎么了？”

-

-

-

-

-

"buckaroo.confused" 17 行，546 个字符

# 第 11 小时：高级技巧、工具和技巧

就是这些！你现在对 Unix 中最重要且最常用的命令之一有了相当的了解。还有更多东西要学（哪不是呢？），但你现在可以从容地编辑文件了！

# 任务 11.3: 如何正确启动 vi

如果 `vi` 命令没有一些可用的启动选项，它就不会是 Unix 的一部分，但只有两个选项值得提。`-R` 标志会让 `vi` 以只读模式显示指定的文件，以确保你不修改它们。第二个选项不是以连字符开头，而是以加号开头：加号后面的任何命令都将作为程序的初始命令。这比听起来要有用得多。例如，`vi +sample` 命令会在 `sample` 底部启动编辑器，而 `vi +17 sample` 则会在 `sample` 的第 17 行启动编辑器。

- 首先是只读格式：

```
vi -R buckaroo
```

> 我发现正偷看自己的手表，无意中听到

猫将军的

助手向他传了最新消息。

“他甚至不在这儿，”对话中说道。

“谁？”

“万岁。”

“他到底在哪儿？”

“在埃尔帕索的医院里。”

“什么？为什么我们没被通知？他到底怎么了？”

状态行上增加了 [Read only] 消息。你可以编辑文件，但如果你尝试使用 `:w` 保存编辑，你会看到这个：

# 使用 vi 进行高级编辑

![](img/9187b56a3187b3f4de32441e7ff5d7a5_236_0.png)

"buckaroo" 文件只读

使用 :q! 退出 vi。

2. 接下来，回想 `janitor` 出现在 `big.output` 文件的许多地方。我将从文件中包含 `janitor` 的那行开始启动 vi：

% vi +janitor big.output

```
brandt ttyrb  Nov 28 23:03 (age)
holmes ttyr]  Dec  3 21:59 (age)
yuxi;   ttyrn  Dec  3 14:19 (pc)
frodo  ttyr0  Dec  3 22:01 (mentor)
laback ttyrt  Dec  3 22:02 (dov)
chenlx2 ttyru  Dec  3 21:53 (mentor)
leungtc ttys0  Nov 28 15:11 (gold)
chinese ttys2  Dec  3 22:53 (excalibur)
cmdemert ttysc  Dec  3 23:00 (mentor)
uuenca ttynr  Dec  3 23:00 (mentor)
janitor ttyt7  Dec  3 16:18 (age)
mathisp ttys8  Dec  3 23:17 (dov)
janitor ttys9  Dec  3 18:18 (age)
cs541 ttysc  Dec  2 15:16 (solaria)
yansong ttysl  Dec  1 14:44 (math)
mdps   tty00  Nov 08 19:39 (localhost)
jd     ttyU  Dec  2 08:45 (muller)
jac    ttysa  Dec  3 18:18 (localhost)
eichdsted ttysb  Dec  3 23:21 (pc1)
sweett ttysc  Dec  3 22:40 (dov)
wellman ttysd  Dec  3 23:00 (dov)
tuttleeno ttysc  Dec  3 23:03 (indyax)
wu      ttyr  Dec  3 23:10 (term0)
"big.output" 40 lines, 1659 characters
```

这次，注意光标停留在该位置。再次使用 :q 退出。

3. 最后，启动 vi 并让光标停在 `buckaroo` 文件的第三行：

% vi +3 buckaroo

我发现自己正在偷看自己的手表，并无意中听到猫鸟将军的

助手在向他转述最新线消息。

“他甚至不在儿，”对话是这样。

“谁？”

“Banzai。”

![](img/9187b56a3187b3f4de32441e7ff5d7a5_236_1.png)

# 第 11 小时：高级 vi 技巧、工具和技术

> “他到底在哪儿？”

“在埃尔帕索的医院。”

“什么？为什么不通知我们？他怎么了？”

"buckaroo" 9 行, 276 个字符

再次，注意光标停留在哪里。
