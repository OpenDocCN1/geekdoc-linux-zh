
"Where the hell is he?"

"At the hospital in El Paso."

"What? Why weren't we informed? What's wrong with him?"

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

"buckaroo.confused" 17 lines, 546 characters

```

就是这样！你现在已经相当了解 Unix 中一个最重要、当然也是使用最频繁的命令。还有更多东西要学（不是总有吗？），但

你现在可以从容地编辑你的文件了！

## Task 11.3: 正确启动 vi

如果 `vi` 命令没有可用的启动选项，那它就不会是 Unix 的一部分了，但实际上只有两个值得提及。`-R` 标志将 `vi` 设置为以只读模式显示指定的文件，以确保你不会意外修改它们。第二个选项不是以连字符开头，而是以加号开头：在加号后面跟随的任何命令都将用作程序的初始命令。这比听起来更有用。例如，命令 `vi +$ sample` 会在文件 `sample` 的底部启动编辑器，而 `vi +17 sample` 则在 `sample` 的第 17 行启动编辑器。

- 1. 尝试只读格式：

Click here to view code image

```
$ vi -R buckaroo
```

```
I found myself stealing a peek at my own watch and overheard

General Catbird’s

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

~

~

~

"buckaroo" [Read only] 9 lines, 276 characters
```

注意屏幕底部状态行上添加的 `[Read only]` 消息。你可以编辑文件，但如果你尝试用 `:w` 保存编辑，就会看到：

```
~
"buckaroo" File is read only
```

使用 `:q!` 退出 `vi`。

- 2. 回想一下 `janitor` 在 `big.output` 文件中出现多次。在包含模式 `janitor` 的文件行上启动 `vi`：

Click here to view code image

```
% vi +/janitor big.output
```

```
brandt     ttyrb  Nov 28 23:03  (age)

holmes     ttyrj  Dec  3 21:59  (age)

yuxi       ttyrn  Dec  1 14:19  (pc)

frodo      ttyro  Dec  3 22:01  (mentor)

labeck     ttyrt  Dec  3 22:02  (dov)

chen1x2    ttyru  Dec  3 21:53  (mentor)

leungtc    ttys0  Nov 28 15:11  (gold)

chinese    ttys2  Dec  3 22:53  (excalibur)

cdemmert   ttys5  Dec  3 23:00  (mentor)

yuenca     ttys6  Dec  3 23:00  (mentor)

janitor    ttys7  Dec  3 18:18  (age)

mathisbp   ttys8  Dec  3 23:17  (dov)

janitor    ttys9  Dec  3 18:18  (age)

cs541      ttysC  Dec  2 15:16  (solaria)

yansong    ttysL  Dec  1 14:44  (math)

mdps       ttysO  Nov 30 19:39  (localhost)

md         ttysU  Dec  2 08:45  (muller)

jac        tty sa Dec  3 18:18  (localhost)

eichsted   ttysb  Dec  3 23:21  (pcl)

sweet t    ttysc  Dec  3 22:40  (dov)

wellman    ttysd  Dec  3 23:01  (dov)

tuttleno   ttyse  Dec  3 23:03  (indy vax)

wu         ttysf  Dec  3 23:10  (term01)

"big.output" 40 lines, 1659 characters
```

这次，注意光标停在哪里。再次使用 `:q` 退出。

- 3. 最后，使用光标位于文件 `buckaroo` 的第三行启动 `vi`：

Click here to view code image

```
% vi +3 buckaroo
```

```
I found myself stealing a peek at my own watch and overheard

General Catbird’s

aide give him the latest.

"He’s not even here," went the conversation.

"Who?"

"Banzai."

"Where the hell is he?"

"At the hospital in El Paso."

"What? Why weren’t we informed? What’s wrong with him?"

~

~

~

~

~

~

~

~

"buckaroo" 9 lines, 276 characters
```

再次注意光标的停留位置。

了解这两个启动选项很有帮助。特别是，我经常使用 `+/pattern` 在特定模式的首次出现处启动编辑器，但你可以用 `vi` 多年而从不知道除了命令本身名称之外的更多内容。

## Task 11.4: 搜索和替换

虽然大多数 `vi` 都很容易学习和使用，但一个总是给用户带来很大麻烦的命令就是搜索和替换。理解此命令的关键是记住 `vi` 建立在线编辑器 `ex` 之上。与其试图弄清楚某种神秘的 `vi` 序列，在这种情况下，更容易的做法是直接进入行编辑器并使用简单的冒号命令将旧模式替换为新模式。要将当前行上的现有单词替换为新单词（最简单的情况），使用 `:s/old/new/`。如果你想匹配当前行上的所有出现项，请添加 `g`（global）后缀：`:s/old/new/g`。你会知道是否忘记了 `g` 后缀，因为你只会更改每行文件中模式的首次出现，而不是所有出现。

要在整个文件中更改一个单词或短语的所有出现项，命令与前面相同，只是你必须添加范围说明符。回想一下 `$` 是 `vi` 中表示文件最后一行的记号（例如，使用 `vi +$ filename` 启动时从最后一行开始）。还回想一下范围由两个用逗号分隔的数字指定。毫不奇怪，全文件全局搜索和替换命令是 `:1,$ s/old/new/g`。

- 1. 再次使用 `buckaroo` 文件启动 `vi`，使用你已知的现有 `vi` 命令在第一行和最后一行添加额外文本，然后使用 `1G` 跳到文件顶部：

Click here to view code image

```
Excerpt from "Buckaroo Banzai" by Earl MacRauch

I found myself stealing a peek at my own watch and overheard

General Catbird’s

aide give him the latest.

"He’s not even here," went the conversation.

"Who?"

"Banzai."

"Where the hell is he?"

"At the hospital in El Paso."

"What? Why weren’t we informed? What’s wrong with him?"

Go Team Banzai! Go Team Banzai! Go Team Banzai!

~

~

~

~

~

~

~

~

~

~
```
