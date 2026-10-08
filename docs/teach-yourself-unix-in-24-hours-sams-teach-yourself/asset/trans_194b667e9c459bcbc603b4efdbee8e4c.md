

# vi 编辑器简介

| | | | | |
|---|---|---|---|---|
| md | ttusU | Dec 2 08:45 | (muller) |
| jac | ttysa | Dec 3 18:18 | (localhost) |
| eichsted | ttsyb | Dec 3 23:21 | (pc1) |
| sweett | ttysc | Dec 3 22:40 | (dov) |
| wellman | ttsyd | Dec 3 23:01 | (dov) |

注意，有一行新信息被拉到了屏幕顶部，以替换你删除的空行。

如果你尝试使用 `u` 命令，会发生什么呢？

我快要完了。按几次回车键，我就到了 janitor（清洁工）账户的条目。使用 `ed` 也会删除该行：

| | | | | |
|---|---|---|---|---|
| Dec 1 18:27 | | Dec 3 22:38 | (expert) |
| tuyhinwa | ttyRX | Dec 3 22:14 | (dov) |
| hollest | ttyrb | Nov 28 23:03 | (age) |
| holmes | ttyj | Dec 3 21:59 | (age) |
| yuxi | ttyrn | Dec 1 14:19 | (pc1) |
| frodo | ttyrc | Dec 3 22:01 | (mentor) |
| labeck | ttyrt | Dec 3 22:02 | (dov) |
| chenx2 | ttyru | Dec 3 21:53 | (mentor) |
| leungct | ttus0 | Nov 28 15:51 | (gold) |
| cdmmert | ttys5 | Dec 3 23:00 | (mentor) |
| yuenca | ttys6 | Dec 3 23:17 | (dov) |
| mathishb | ttys8 | Dec 3 18:18 | (age) |
| janitor | ttys9 | Dec 2 15:16 | (solaria) |
| cs541 | ttycC | Dec 1 14:34 | (math) |
| yansong | ttyLs | Nov 30 19:39 | (localhost) |
| md | ttusU | Dec 2 08:45 | (muller) |
| jac | ttysa | Dec 3 18:18 | (localhost) |
| eichsted | ttsyb | Dec 3 23:21 | (pc1) |
| sweett | ttysc | Dec 3 22:40 | (dov) |
| wellman | ttsyd | Dec 3 23:01 | (dov) |
| janitor | ttyse | Dec 3 23:03 | (indy) |

被删除行之后的每一行都会向上移动以填充空白，而新行将从后续屏幕移动进来。我想回到文件修复一些极其糟糕的错误！我并不在乎是否保存对该文件的修改，所以我将使用 `:q` 退出，并放弃这些对输出文件的更改。重新进入 vi：

我发现自己正在偷看自己的手表，并听到
猫头鸟将军的
助手 正在向他汇报最新情况。
“他甚至不在儿，”对话是这样。
“万岁（Banzai）。”
“他到底在哪儿？”
“在埃帕索的医院。”
“什么？为什么我们没被通知？和他在一起？”

你可以快速完成几处修复。第一个是修改第四行的对话。要移动到那里，按两次回车键，然后使用 `w` 向前移动直到光标位于你正在编辑的单词的首字母：

我发现自己正在偷看自己的手表，并听到
猫头鸟将军的
助手正在向他汇报最新情况。
“他甚至不在儿，”对话是这样。
“万岁（Banzai）。”
“他到底在哪儿？”

然后使用 `dw` 命令：

我发现自己正在偷看自己的手表，并听到
猫头鸟将军的
助手正在向他汇报最新情况。
“他甚至不在儿，”对话是这样。
“万岁（Banzai）。”
“他到底在哪儿？”

现在输入 `i` 进入插入模式，输入单词的正确拼写，然后按下 `Escape`。

我发现自己正在偷看自己的手表，并听到
猫头鸟将军的
助手正在向他汇报最新情况。
“他甚至不在儿，”对话是这样。
“万岁（Banzai）。”
“他到底在哪儿？”

6. 那是一个修复。现在向下移动几行修复医院（hospital）的拼写错误：

“万岁（Banzai）。”
“他到底在哪儿？”
“在埃帕索的医院。”
“什么？为什么我们没被通知？和他在一起？”

再次使用 `dw` 删除单词，输入 `i` 进入插入模式，输入 `hospital`，然后按下 `Escape`。现在这一行完全正常了：

“万岁（Banzai）。”
“他到底在哪儿？”
“在埃帕索的医院。”
“什么？为什么我们没被通知？和他在一起？”

嗯，几乎所有的地方都好了。Paso 的首字母需要大写。通过输入 `w` 向前移动几个单词：

“万岁（Banzai）。”
“他到底在哪儿？”
“在埃帕索的医院。”
“什么？为什么我们没被通知？和他在一起？”

7. 是时候使用秘密 vi 命令了！与其输入 `x` 删除字母，输入 `i` 进入插入模式输入正确的字母，然后按下 `Escape` 返回命令模式，有一种更快的方法切换大小：`~`（波浪号）。输入一次 `~`，发生如下：

正确，不是吗？回到单词开头再次输入几次 `~` 查看发生了什么。注意每次输入 `~`，字母的大小就会切换——并且光标移动到下一个字符。输入四次，你应该得到这个：

“万岁（Banzai）。”
“他到底在哪儿？”
“在埃帕索的医院。”
“什么？为什么我们没被通知？和他在一起？”

回到单词开头并输入 `~` 直到单词正确。8. 再进行一次微调，文件就修复了！移动到文件的最后一行，单词中多余的单引号，输入 `x` 删除该字符。屏幕现在应该是这样的：

```
我发现自己正在偷看自己的手表并听到
猫头鸟将军的
助手正在向他汇报最新情况。
“他甚至不在儿，”对话是这样。
“万岁（Banzai）。”
“他到底在哪儿？”
“在埃帕索的医院。”
“什么？为什么我们没被通知？和他在一起？”
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_239_0.png)

看起来极了！是时候保存了。使用 `:wq` 快捷键写入更改并立即退出。你不仅学会了 vi 的多种删除选项，还学习了一些快捷命令：切换大小以及 `:wq` 写入并退出。你应该感到很愉快；你是一个高效且博学的用户，可以修改文件，无论简单还是困难。回到你的系统并进一步实验，至少这样可以修复问题了！

## 搜索文件

有了这两个额外功能，你已经准备好面对任何 vi 专家了，展示你对编辑器的技巧和知识，并且你能够快速穿过文件。这两个新功能用于在文件中查找单词或短语并移动到特定行。类似于在页面搜索，`/` 命令在文件中向前搜索指定的模式，而 `?` 则向后搜索指定的模式。要重复上一次搜索，使用该命令让 vi 在相同方向搜索模式的下一个实例。你可以使用 `G` 或跳转行命令移动到文件的任何行。如果你在 `G` 之前输入一个数字，光标将移动到文件的该行。如果你直接输入 `G`，光标将跳跳转到文件的最后一行（默认设置）。

1. 使用大输出启动 vi：

| | | | |
|---|---|---|---|
| leungtc | ttrV | Dec 1 18:27 | (magenta) |
| tuyinhwa | ttyX | Dec 3 22:38 | (expert) |
| hollenst | ttrZ | Dec 3 22:14 | (dov) |
| brandt | ttyb | Nov 28 23:03 | (age) |
| holmes | ttyj | Dec 3 21:59 | (age) |
| yuskl | ttyn | Dec 1 14:19 | (pci) |
| frodo | ttyr | Dec 3 22:01 | (mentor) |
| labeck | ttyt | Dec 3 22:02 | (dov) |
| chenitx | ttyru | Dec 3 21:53 | (mentor) |
| leungtc | tty9 | Nov 28 15:11 | (gpld) |
| chinese | ttys | Dec 3 22:53 | (excalibur) |
| cdmemert | tty5 | Dec 3 23:00 | (mentor) |
| yuenca | tty6 | Dec 3 23:00 | (mentor) |
| janitor | ttyS | Dec 2 15:18 | (age) |
| mathisb | ttysp | Dec 3 23:17 | (dov) |
| janitor | ttys | Dec 3 23:18 | (dov) |
| cs541 | ttyAc | Dec 2 15:16 | (solaria) |
| yansong | ttySl | Dec 1 14:44 | (satin) |
| mdpds | tty0 | Nov 30 19:39 | (localhost) |
| md | ttyU | Dec 2 08:45 | (muller) |
| jac | ttya | Dec 3 18:18 | (dov) |
| eichsta | ttyba | Dec 3 23:21 | (localhost) |
| sweett | ttyc | Dec 3 22:40 | (dov) |

记得我提前使用了 `:q` 退出，所以某些更改没有保留。移动到文件的最后一行，我输入 `G` 并看到这个：

| | | | |
|---|---|---|---|
| cdmmert | ttysk | Dec 3 22:37 | (xsun) |
| jlree | ttysn | Dec 3 22:53 | (mac1) |
| fitggejs | ttyso | Dec 3 23:18 | (dov) |
| doernh | ttysp | Dec 3 23:20 | (dov) |
| cdmmert | ttysq | Dec 3 23:01 | (xsun) |
| frazierw | ttyrw | Dec 3 23:01 | (dov) |
| buckey | ttyss | Dec 3 23:20 | (mac2) |
| ntaylor | ttyst | Dec 3 23:22 | (dov) |
| took | ttysu | Dec 3 22:12 | (age) |
| janitor | ttyew | Dec 3 18:29 | (age) |
| ajones | ttysx | Dec 3 23:23 | (rassilon) |

