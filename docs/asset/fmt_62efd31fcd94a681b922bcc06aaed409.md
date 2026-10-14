
如果存在大写的 `D` 命令，那么你完全可以认为存在小写的 `d` 命令。删除命令是一系列更复杂的 vi 命令中的第一个，后面紧跟一个第二个命令，指示你想对该命令执行什么操作。你已经知道 `w` 是在文件中移动一个单词；它们在 vi 中被称为地址命令（addressing commands）。你可以跟随这些地址命令之一来指定你想删除的内容。例如，要删除一个单词，只需输入 `dw`。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_230_0.png)

有时你可能会变得有些过猛，删除了比预期的多的内容。这并不是问题——好吧，不是大问题——因为 vi 会记住上一次操作之前的文件状态。要撤销删除（或者插入），请使用 `u` 命令。要撤销一行的更改，也请使用 `u` 命令。请注意，一旦你离开了该行，`u` 命令就无法恢复它了！

## 省时技巧

### 动作

1. 使用你之前使用的 `big.output` 文件重新启动 vi：

| leungto ttyR Dec 1 18:27 (magenta) |

| tuyinhwa ttyrX Dec 3 22:38 (expert) |

| hollenst ttyZ Dec 3 22:14 (dov) |

| brandit ttyRB Nov 28 22:03 (age) |

| holmes ttyR Dec 3 21:59 (age) |

| yuxi ttyRN Dec 1 14:19 (pc) |

| frodo ttyro Dec 3 22:01 (mentor) |

| labeck ttyro Dec 3 22:02 (dov) |

| chenx2 ttyro Dec 3 21:53 (mentor) |

| chinese ttyS0 Nov 28 22:51 (gold) |

| cdmert ttyS5 Dec 3 22:53 (excalbur) |

| yuencal ttyS6 Dec 3 23:00 (mentor) |

| janitor ttyS Dec 3 18:18 (age) |

| janitsb ttySB Dec 3 23:17 (dov) |

| cs841 ttyC Dec 2 15:16 (colaria) |

| yansong ttyL Dec 1 14:44 (math) |

| mdps ttyOS Nov 30 19:39 (localhost) |

| md Dec 2 08:45 (miller) |

| jac ttySU Dec 3 18:18 (localhost) |

| eichsted ttySC Dec 3 23:21 (pc1) |

| sweett ttySC Dec 3 22:40 (dov) |

| "big.output" 40 lines, 1659 characters |

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_230_1.png)

输入几次 `x` 来删除文件开头的几个字符：

```
gtc ttyrV Dec 1 18:27 (magenta)
tuyinhwa ttyrX Dec 3 22:38 (expert)
hollenst ttyrZ Dec 3 22:14 (dov)
brandt ttyrB Nov 28 23:03 (age)
holmes ttyrJ Dec 3 21:59 (age)
```

现在你输入 `u` 来撤销删除：

```
pgtc ttyrV Dec 1 18:27 (magenta)
tuyinhwa ttyrX Dec 3 22:38 (expert)
hollenst ttyrZ Dec 3 22:14 (dov)
brandt ttyrB Nov 28 23:03 (age)
holmes ttyrJ Dec 3 21:59 (age)
```

如果你再次输入 `u`，你认为会发生什么？

```
gtc ttyrV Dec 1 18:27 (magenta)
tuyinhwa ttyrX Dec 3 22:38 (expert)
hollenst ttyrZ Dec 3 22:14 (dov)
brandt ttyrB Nov 28 23:03 (age)
holmes ttyrJ Dec 3 21:59 (age)
```

`u` 命令在最后一次操作和未发生的操作之间切换。为了更好地解释这一点，`u` 命令本身也是操作。当你第二次输入 `u` 时，你是在撤销上一次“撤销”操作，因此，它会恢复之前被删除的内容。多次输入 `u` 可以让你回到操作前的状态。

2. 如果你想删除某行，但想更精确地控制删除范围。你可以通过使用 `dw` 来删除特定的单词。例如，输入两次 `dw` 会删除当前位置后的两个单词。这看起来应该是这样：

（注：原文后续部分存在大量重复乱码，已处理核心逻辑。）

## vi 编辑器简介

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
