

要移动到文件的第三行，我输入 3 然后按 G：

Click here to view code image

```
leungtc ttyrV Dec 1 18:27 (magenta)
tuyinhwa ttyrX Dec 3 22:38 (expert)
hollenst ttyrZ Dec 3 22:14 (dov)
brandt ttyrb Nov 28 23:03 (age)
holmes ttyrj Dec 3 21:59 (age)
yuxi ttyrn Dec 1 14:19 (pc)
frodo ttyro Dec 3 22:01 (mentor)
labeck ttyrt Dec 3 22:02 (dov)
chenlx2 ttyru Dec 3 21:53 (mentor)
leungtc ttys0 Nov 28 15:11 (gold)
chinese ttys2 Dec 3 22:53 (excalibur)
cdemmert ttys5 Dec 3 23:00 (mentor)
yuen ca ttys6 Dec 3 23:00 (mentor)
janitor ttys7 Dec 3 18:18 (age)
mathisbp ttys8 Dec 3 23:17 (dov)
janitor ttys9 Dec 3 18:18 (age)
cs541 ttysC Dec 2 15:16 (solaria)
yansong ttyL Dec 1 14:44 (math)
mdps ttysO Nov 30 19:39 (localhost)
md ttysU Dec 2 08:45 (mueller)
jac ttysa Dec 3 18:18 (localhost)
eichsted ttysb Dec 3 23:21 (pcl)
sweett ttysc Dec 3 22:40 (dov)
```

注意光标位于文件的第三行。

## 2. 现在是时候搜索了。根据我之前在这个文件中的浏览，我知道最后一行是账户 ajones 的，但与其直接使用 G 移动到那里，我可以使用 / 搜索命令来搜索指定的模式。

输入 / 会立即将光标移动到屏幕底部：

Click here to view code image

```
md ttysU Dec 2 08:45 (mueller)
jac ttysa Dec 3 18:18 (localhost)
eichsted ttysb Dec 3 23:21 (pcl)
sweett ttysc Dec 3 22:40 (dov)
/_
```

现在我可以输入模式 ajones：

```
fitzgejs ttyso  Dec  3 23:18  (dov)
doerrhb ttysp  Dec  3 23:20  (dov)
cdemmert ttysq  Dec  3 23:00  (xsun)
frazierw ttysr  Dec  3 23:01  (dov)
buckeye ttyss  Dec  3 23:20  (mac2)
mtaylor ttyst  Dec  3 23:22  (dov)
look ttysu  Dec  3 23:12  (age)
janitor ttysw  Dec  3 18:29  (age)
ajones ttysx  Dec  3 23:23  (rassilon)
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

## 3. 如果我输入 n 来再次搜索该模式，会在底部出现一个斜杠以显示 vi 理解了我的请求。但光标保持在原位，这意味着该模式在这个文件中只有一个出现。

## 4. 查看这个文件，我注意到账户 janitor 有各种各样的会话正在运行。要向后搜索该账户的出现，我可以使用 ? 命令：

```
~ 
?janitor_
```

第一次搜索将光标向上移动一行，这使得屏幕看起来几乎相同：

Click here to view code image

```
cdemmert ttysk  Dec  3 22:37  (xsun)
jrlee ttysn  Dec  3 22:53  (mac1)
fitzgejs ttyso  Dec  3 23:18  (dov)
doerrhb ttysp  Dec  3 23:20  (dov)
cdemmert ttysq  Dec  3 23:00  (xsun)
frazierw ttysr  Dec  3 23:01  (dov)
buckeye ttyss  Dec  3 23:20  (mac2)
mtaylor ttyst  Dec  3 23:22  (dov)
look ttysu  Dec  3 23:12  (age)
janitor ttysw  Dec  3 18:29  (age)
ajones ttysx  Dec  3 23:23  (rassilon)
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

```
?janitor
```

这里 n，即下一个匹配，就派上用场了。如果我这次输入 n，并且文件中还有该模式的另一个出现，vi 会直接将我移动到匹配处：

Click here to view code image

```
yuxi      ttyrn   Dec  1 14:19   (pc)
frodo     ttyro   Dec  3 22:01   (mentor)
labeck    ttyrt   Dec  3 22:02   (dov)
chenlx2   ttyru   Dec  3 21:53   (mentor)
leungtc   ttys0   Nov 28 15:11   (gold)
chinese   ttys2   Dec  3 22:53   (excalibur)
cdemmert  ttys5   Dec  3 23:00   (mentor)
yuen ca   ttys6   Dec  3 23:00   (mentor)
janitor   ttys7   Dec  3 18:18   (age)
mathisbp  ttys8   Dec  3 23:17   (dov)
janitor   ttys9   Dec  3 18:18   (age)
cs541     ttysC   Dec  2 15:16   (solaria)
yansong   ttysL   Dec  1 14:44   (math)
mdps      ttysO   Nov 30 19:39   (localhost)
md        ttysU   Dec  2 08:45   (mueller)
jac       ttysa   Dec  3 18:18   (localhost)
eichsted  ttysb   Dec  3 23:21   (pcl)
sweett    ttysc   Dec  3 22:40   (dov)
wellman   ttysd   Dec  3 23:01   (dov)
tuttleno  ttyse   Dec  3 23:03   (indy vax)
wu        tty sf  Dec  3 23:10   (tern01)
daurismj  tty sg  Dec  3 23:10   (dov)
cs414     tty sh  Dec  3 23:12   (xds)
```

在你自己的文件中尝试一个出现多次的模式。完成后，使用 :q 退出 vi。

vi 的命令不是几十个而是数百个。与其用所有命令淹没你，我选择向你展示最重要的命令。事实上，这本书就是这样组织的；毕竟，如果你想要一个庞大的命令参考，你会去读 man 手册，对吧？等你完成这一小时后，你对 vi 命令的了解将是实质性的，并且你将能够轻松使用该编辑器。

此任务专注于搜索模式，这是一个常见需求，也是任何编辑器的有帮助功能。此外，你还学会了如何移动到文件顶部 (1G) 和文件底部 (G)，以及两者之间的任意位置。

# Task 11.2: vi 中的冒号命令

不用太多解释，你已经学习了几个冒号命令——也就是说，以冒号为第一个字符的命令。冒号会立即将光标移动到屏幕底部以供进一步输入。这些命令实际上是相当大的一组命令的子集，所有这些命令都是 vi 所基于的 ex 编辑器的一部分。

还记得我在上一小时开头告诉你的关于 vi 是 ex 编辑器的可视化外壳的事情吗？事实证明 ex 在系统上仍然是一个部分。

