

无模式程序（modeless）：无模式程序无论用户正在做什么，始终以相同的方式解释按键。

切换大小：将大写字母转换为小写，或将小写字母转换为大写。

# 问题

- 如果你尝试使用 `:qw` 退出 vi 会发生什么？在尝试之前，你认为它能生效吗？
- 如果熟悉 Mac 或 Windows 环境下的文字处理程序，你会认为它们是模态的（modal）还是无模态（modeless）的？
- `d` 命令是一个理解地址命令的命令示例。你可能见过很多命令。测试它们，看看你是否能找出与 `D` 命令动作相反的命令。
- 这三个命令得到的结果相同吗？

```
D
d$
dg
```

- 想象你正处于屏幕中间某行的中间的命令模式。描述一下输入以下每个内容会发生什么：

```
BadLuck
Window
blad$
```

- 如果你使用以下启动标志会发生什么？

```
vi +test
vi +joe/names
vi +hjjjj
vi +:q test
```

# 下一小时预览

接下来的一个小时将扩展你对 vi 编辑器的知识。它引入了命令的数字重复前缀、修改字符（而不是删除和插入）、搜索和替换、启用方向键的键映射，以及在 vi 中操作 UNIX。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_253_0.png)

# 第 12 小时
高级 vi 技巧、工具和技术

在上一个小时中，你学习了 50 个 vi 命令，让你能够轻松地在文件中移动、插入文本、删除文本、搜索特定模式以及在不离开程序的情况下切换文件。这一小时将通过展示更强大的 vi 命令来扩展你的专业知识。在开始这一小时之前，我强烈建议使用 vi 处理几个文件。确保你已经熟悉该程序的不同模式。

# 本小时目标

在这一小时中，你将学习如何

- 使用修改（change）和替换（replace）命令。
- 使用数字重复前缀。
- 为文件行编号。
- 搜索和替换。

# 第 12 小时

使用 `:zmap` 命令映射按键。

移动句子和段落。

使用 `:t` 命令访问 UNIX 命令。

这看起来像是一个短列表，但包含了很多内容。我坦诚地说：不看这一小时，你在 vi 中也可以过得很好。你已经学会了插入和删除文本、保存或不保存退出，你也可以搜索模式——即使在第一次启动 vi 时从命令行就可以做到！另一方面，vi 就像任何其他复杂主题一样。你越愿意研究和学习，这个程序就越能满足你的需求。这意味着你每天可以完成各种不同的任务。

# 任务 12.1：修改和替换命令

描述在上一个小时中，你看到我如何通过删除单词并将其替换为新单词来解决各种问题。事实上，有一种简单得多的方法可以，那就是使用修改（change）或替换（replace）命令。

每个命令都有小写和大写两个版本，且两者都完全不同。`r` 命令将光标所处的字符替换为输入的下一个字符，而 `c` 命令则让你进入替换模式，这样你输入的任何内容都会覆盖行上已有的内容，直到你停止。相比之下，`c` 用你输入的内容替换行上的所有内容。（这是一个细微的差别，但我会演示给你，所以不用担心。）`e` 命令是它们中最强大的。修改命令的工作方式与 `c` 命令相同，正如上一个小时所述。你可以将 `e` 命令与任何地址命令配合使用，它可以让你修改文本到该地址，无论是一个单词、一行还是文档的剩余部分。

操作

1. 使用 `buckaroo.confused` 文件启动 vi。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_255_0.png)

# 高级 vi 技巧、工具和技术

> “万岁。”
> “他妈的在哪儿？”
> “在埃尔帕索医院。”
> “什么？为什么不通知我们？他怎么了？”

"buckaroo.confused" 16 行，542 个字符

现在完全移动光标，输入 `R`。什么都没有发生，或者看起来如此。现在输入单词 `Excerpt from "Buckaroo Banzai"`，观察发生了什么：

```
Excerpt from "Buckaroo Banzai"at my own watch and overheard
General Catbird's
I found myself stealing peek at my own watch and overheard
General Catbird's
give give him the latest.
"He's not even here," went the conversation.
```

现在按下 Escape 键，注意你在屏幕上看到的与文件中的完全一致。

2. 然而，这并不是我想要的。我可以使用 `d` 或 `ds` 删除到行尾，但有点笨拙。相反，我将使用 `o` 回到行首。你也这样做：

```
Excerpt from "Buckaroo Banzai" at my own watch and overheard
General Catbird's
I found myself stealing a peek at my own watch and overheard
General Catbird's
aide him the latest.
"He's not even here," went the conversation.
```

这次，输入 `c` 修改行的内容。在你输入新文本的任何字符之前，注意现在行现在的样子：

> Excerpt from "Buckaroo Banzai" at my own watch and overheard
General Catbird$
I found myself stealing a peek at my own watch and overheard
General Catbird's
aide give him the latest.
"He's not even here," went the conversation.

这里开始出现了一个细微的差别！看当前行的最后一个字符。当你按下 `c` 时，原本是 `s` 的地方，程序现在放置了一个 `s` 来显示命令将修改的文本范围。按一次 Tab 键，然后输入 `Excerpt from "Buckaroo Bansai" by Earl MacRauch`。

> Excerpt from "Buckaroo Bansai" by Earl MacRauchheard General
Catbird$
I found myself stealing a peek at my own watch and overheard
General Catbird's
aide give him the latest.
"He's not even here," went the conversation.

这次，当我按下 Escape 键时发生了什么：

> Excerpt from "Buckaroo Banzai" by Earl MacRauch
I found myself stealing a peek at my own watch and overheard
General Catbird's
aide give him the latest.
"He's not even here," went the conversation.

3. 我认为我又搞错了。书名实际上是 `Buckaroo Banzai`（带 `z`），但我把它拼成了 `s`。这是使用 `r` 命令的机会。

使用光标键将光标移动到错误的字母。我会使用 `b` 回退单词，然后多次 `h` 移动到单词中间。我的屏幕现在是：

> Excerpt from "Buckaroo Bangai" by Earl MacRauch
I found myself stealing a peek at my own watch and overheard
General Catbird's
aide give him the latest.
"He's not even here," went the conversation.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_257_0.png)

# 高级 vi 技巧、工具和技术

现在输入 `r`。再次，什么都没有发生；光标没有移动。再次输入 `r` 以确保它起作用：

> Excerpt from "Buckaroo Banrai" by Earl MacRauch
I found myself stealing a peek at my own watch and overheard
General Catbird's
aide give him the latest.
"He's not even here," went the conversation.

那不太好。它把 `s` 替换成了 `r`，这绝对不对。再次输入 `r`，你应该得到：

> Excerpt from "Buckaroo Banzai" by Earl MacRauch
I found myself stealing a peek at my own watch and overheard
General Catbird's
aide give him the latest.
"He's not even here," went the conversation.

4. 好了，这些都是简单的。现在是时候看看 `c` 能为你做什么了。事实上，它是极其强大的。你可以从文件的当前点向任何方向修改任何范围的信息！为了移动，到文件的中间，即第二个段落所在：

> Excerpt from "Buckaroo Banzai" by Earl MacRauch
I found myself stealing a peek at my own watch and overheard
General Catbird's
aide give him the latest.
"He's not even here," went the conversation.
"Banzai."
"Where the hell is he?"
"At the hospital in El Paso.
"What? Why weren't we informed? What's wrong with him?"
aide give him the latest.
"He's not even here," went the conversation.
"Banzai."
"Where the hell is he?"
"At the hospital in El Paso.
"What? Why weren't we informed? What's wrong with him?"

