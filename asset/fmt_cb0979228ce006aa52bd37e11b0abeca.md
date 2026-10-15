
在你自己的文件中尝试一个出现多次的模式。完成后，使用 `:q` 退出 `vi`。

`vi` 的命令不是几十个而是数百个。与其用所有命令淹没你，我选择向你展示最重要的命令。事实上，这本书就是这样组织的；毕竟，如果你想要一个庞大的命令参考，你会去读 `man` 手册，对吧？等你完成这一小时后，你对 `vi` 命令的了解将是实质性的，并且你将能够轻松使用该编辑器。

此任务专注于搜索模式，这是一个常见需求，也是任何编辑器的有帮助功能。此外，你还学会了如何移动到文件顶部 (`1G`) 和文件底部 (`G`)，以及两者之间的任意位置。

# Task 11.2: vi 中的冒号命令

不用太多解释，你已经学习了几个冒号命令——也就是说，以冒号为第一个字符的命令。冒号会立即将光标移动到屏幕底部以供进一步输入。这些命令实际上是相当大的一组命令的子集，所有这些命令都是 `vi` 所基于的 `ex` 编辑器的一部分。

还记得我在上一小时开头告诉你的关于 `vi` 是 `ex` 编辑器的可视化外壳的事情吗？事实证明 `ex` 在系统上仍然是一个部分。

## 注意

关于冒号命令，有一点需要注意：与你在 `vi` 命令模式下输入的命令不同，在冒号提示符下输入的命令必须按回车键，编辑器才会处理。这是 `vi` 中一个常见的混淆点，但只要你试过就会习惯。

表 11.1 列出了最有用的冒号命令。

| 命令 | 功能 |
|---|---|
| `:e filename` | 停止编辑当前文件并编辑指定文件。 |
| `:n` | 停止编辑当前文件并编辑命令行中指定的下一个文件。请记住，你始终可以用 `vi *txt` 或类似方式启动 `vi`。 |
| `:N` | 转到上一个指定文件。 |
| `:q` | 退出编辑器。 |
| `:q!` | 无论是否做过修改都退出，忽略所有警告。 |
| `:r filename` | 将指定文件的内容包含在当前正在编辑文件的此位置处。 |
| `:w` | 将文件写入磁盘。 |
| `:w filename` | 以指定文件名将文件写入磁盘。 |

## 表 11.1 最实用的冒号命令

1. 再次启动 `vi`，这次指定要编辑的文件列表；`vi` 会提示你指定的文件不止一个：

```
$ vi buckaroo big.output

2 files to edit.
```

接着它会清屏并显示第一个文件：

点击此处查看代码图片

```
I found myself stealing a peek at my own watch and overheard

General Catbird's

aide give him the latest.

"He's not even here," went the conversation.

"Who?"

"Banzai."

"Where the hell is he?"

"At the hospital in El Paso."

"What? Why weren't we informed? What's wrong with him?"

~

~

~

~

~

~

~
```

```
buckaroo" 9 lines, 276 characters
```

键入命令序列 `:w` 并按下回车键，文件就会以当前名称写入磁盘。这种情况下没什么可看的。

2. 相反，试着用 `:w newfile` 写入另一个文件：

```
:w newfile
```

按下回车键后，你会看到：

> 我发现自己偷偷看了一眼手表，无意中听到
> 卡特伯德将军的
> 副官向他报告最新情况。
> “他甚至不在这里，”对话这样进行着。
> “谁？”
> “班赛。”
> “他到底在哪儿？”
> “在埃尔帕索的医院里。”
> “什么？为什么没人通知我们？他怎么了？”

```
:r newfile
```

按下回车键会产生如下结果：

点击此处查看代码图片

```
I found myself stealing a peek at my own watch and overheard

General Catbird’s

I found myself stealing a peek at my own watch and overheard

General Catbird’s

aide give him the latest.

“He’s not even here,” went the conversation.

“Who?”

“Banzai.”

“Where the hell is he?”

“At the hospital in El Paso.”

“What? Why weren’t we informed? What’s wrong with him?”

aide give him the latest.

“He’s not even here,” went the conversation.

“Who?”

“Banzai.”

“Where the hell is he?”

“At the hospital in El Paso.”

“What? Why weren’t we informed? What’s wrong with him?”

~

~

~

~

~

~

~
```

这是一种很有用的方式，可以让你将文件相互包含，或构建一个包含许多其他文件的文件。

4. 现在我已经把文件弄乱了，想把它保存到一个新文件 `buckaroo.confused`：

```
~ 
:w buckaroo.confused_
```

按下回车键后，我会看到：

点击此处查看代码图片

```
~ 
"buckaroo.confused" [New file] 17 lines, 546 characters
```

5. 现在该切换到启动 `vi` 时给定的文件列表中的第二个文件了。为此，我使用 `:n`（即 `next-file`，下一个文件）命令：

```
~ 
:n_
```

按下回车键后，下一个文件会被调入编辑器，替换第一个文件：

点击此处查看代码图片

```
leungtc ttyrV Dec 1 18:27 (magenta)

tuyinhwa ttyX Dec 3 22:38 (expert)

hollenst ttyrZ Dec 3 22:14 (dov)

brandt ttyrb Nov 28 23:03 (age)

holmes ttyrj Dec 3 21:59 (age)
```

```
yuxi      ttyrn  Dec  1 14:19  (pc)

frodo     ttyro  Dec  3 22:01  (mentor)

labeck    ttyrt  Dec  3 22:02  (dov)

chenlx2   ttyru  Dec  3 21:53  (mentor)

leungtc   ttys0  Nov 28 15:11  (gold)

chinese   ttys2  Dec  3 22:53  (excalibur)

cdemmert  ttys5  Dec  3 23:00  (mentor)

yuenca    ttys6  Dec  3 23:00  (mentor)

janitor   ttys7  Dec  3 18:18  (age)

mathisbp  ttys8  Dec  3 23:17  (dov)

janitor   ttys9  Dec  3 18:18  (age)

cs541     ttysC  Dec  2 15:16  (solaria)

yansong   ttysL  Dec  1 14:44  (math)

mdps      ttysO  Nov 30 19:39  (localhost)

md        ttysU  Dec  2 08:45  (muller)

jac       ttySa  Dec  3 18:18  (localhost)

eichsted  ttysb  Dec  3 23:21  (pcl)

sweett    ttysc  Dec  3 22:40  (dov)

"big_output" 40 lines, 1659 characters
```

6. 工作到一半，我突然意识到需要小幅修改刚才保存的 `buckaroo.confused` 文件。这时 `:e` 命令就派上用场了。使用它，我可以编辑任何其他文件：

```
~
~
:e buckaroo.confused_
```

我按下回车键，看到：

点击此处查看代码图片

```
I found myself stealing a peek at my own watch and overheard

General Catbird's

I found myself stealing a peek at my own watch and overheard

General Catbird's

aide give him the latest.

"He's not even here," went the conversation.

"Who?"

"Banzai."
```
