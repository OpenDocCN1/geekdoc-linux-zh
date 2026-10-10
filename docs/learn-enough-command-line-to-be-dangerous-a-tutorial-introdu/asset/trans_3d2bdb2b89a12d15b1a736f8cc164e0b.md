

可用命令。这个工具本身是一个名为**man**（“manual”的缩写）的命令行命令。其参数是我们想要了解的命令的名称（例如**echo**）。具体细节因系统而异，但在我的系统上，运行**man echo**的结果如清单 2 所示。

![](img/4dec9c51e73c9027d3d8a4fab4408fe6_16_0.png)

在清单 2 的最后一行，请注意冒号 : 的存在，这表明下方还有更多信息。这一行的具体细节因系统而异，但在任何系统中，你都应该能够按向下箭头键逐行访问后续信息，或按空格键逐页访问。要退出 man 手册页，请按下“q”（代表“quit”/退出）。(这个 man 手册页界面与**less**程序相同，我们将在第 3.3 节中介绍。)

对本教程（第 5 节）的后续教程的重要主题，从《*Learn Enough*™ *Text Editor To Be Dangerous*》（*Learn Enough™ 危险文本编辑器*）开始。

![](img/4dec9c51e73c9027d3d8a4fab4408fe6_17_0.png)

*图 8：将 man 应用于 man。*

由于**man**本身是一个命令，我们可以将**man**应用于**man**（图 8），¹ 如清单 3 所示。

### 清单 3：运行 **man man** 的结果。

```
$ man man
man (1)                    man (1)

NAME
       man - format and display the on-line manual pages

SYNOPSIS
       man [-acdfFhkKtwW] [--path] [-m system] [-P string] [-C config file]
           [-M pathlist] [-p pager] [-B browser] [-H htmtpager] [-S section_list]
           [section] name ... 

DESCRIPTION
       man formats and displays the on-line manual pages. If you specify sec-
       tion, man only looks in that section of the manual.  name is normally
       the name of the manual page, which is typically the name of a command,
       function, or file.  However, if name contains a slash (/) then man
       interprets it as a file specification, so that you can do man ./foo.5
       or even man /cd/foo/bar.1.gz.

       See below for a description of where man looks for the manual page
       files.

OPTIONS
       -C config_file
           :
```

我们可以从清单 3 中看到，**man** 的用法大致如下：

```
`man  [-acdfFhkKtwW]  [--path]  [-m  system]  [-P  string]  ...`
```

很疯狂，对吧？这就是我在上面描述 man 手册页“通常晦涩难懂”时所指的是。事实上，在许多情况下，我发现 man 手册页的细节几乎无法理解，但能够浏览 man 手册页以获得命令的高级概述是一项非常有价值的技能，值得去掌握。为了习惯阅读 man 手册页，我建议在遇到新命令时运行 `man <command name>`。即使细节不完全清楚，阅读 man 手册页也有助于培养*技术熟练度*（框 5）这一有价值的技能。

### 框 5. 技术熟练度

在数学中，许多学科可以通过对少量假设（或*公理*）进行纯演绎推导来发展。例子包括代数、几何、数论和分析。因此，这类学科是完全自洽的，从而没有形式上的先决条件。原则上，即使是小孩子也能从零开始学习这些学科。然而，在实践中，还需要其他东西，数学家通常推荐一种非正式的先决条件——*数学成熟度*，它包括理解和撰写数学证明所需的经验和一般技巧。

在技术领域，存在一种类似的技能（或更准确地说，一组技能），以*技术熟练度*的形式存在。本质上，它由一系列杂七杂八的计算机技巧工具箱组成，结合一种让机器服从你意愿的*态度*（框 1）。如图 9 所示，技术熟练度包括寻找有希望的菜单项以及知道在 Google 中应该使用哪种类型的搜索词。这些技能很难直接教授，因此在你学习本教程和后续*Learn Enough™ 教程*的过程中，请始终留意通过向你的工具箱中添加工具（例如，通过浏览其 man 手册页来了解程序要点的技能（第 1.3 节））来提高你的技术熟练度的机会。随着时间的推移，累积效应将是，就像图 9 的作者一样，你将拥有在所有程序中做任何事情的神秘般的能力。

### 练习

- 1. 根据 man 手册页，在你的系统上 `echo` 的官方描述是什么？

致各位家长、祖父母、同事和其他“非计算机人士”：

我们并不是魔法般地知道如何在每个程序中做每一件事。当我们帮助你时，我们通常只是在这样做：

![](img/4dec9c51e73c9027d3d8a4fab4408fe6_20_0.png)

请打印此流程图并将其贴在你的屏幕附近。恭喜你，你现在是当地的计算机专家了！

> 图 9：“*技术支持作弊表*”（来自 xkcd.com）。唯一缺少的是“你试过重启吗？”

- 2. 运行 **echo** 的通常方式包括一个*换行符*（“enter”或“return”），它将新提示符放在单独的一行上，但有一个命令行选项可以防止这种情况。通过阅读 **echo** 的 man 手册页，确定打印“hello”但不带尾部换行符所需的命令，并使用你的终端验证它是否按预期工作。*提示*：结果应该看起来像 `helloworld`[ . . . ]$ ，其中 [ . . . ] 代表你的提示符中不重要的细节。(*注意*：在某些旧版本的 Macintosh OS X 上使用默认终端程序时，此练习可能会失败。在这种情况下，我建议安装 iTerm（无论如何这都不是个坏主意）。)

## 1.4 编辑行

命令行包含几个功能，以便轻松重复以前的命令，可能以编辑后的形式。最基本的功能是“向上箭头”，它只是获取上一条命令。再次按下向上箭头会进一步向上移动命令列表，而向下箭头则向底部移动。

在输入新命令或处理以前的命令时，能够在线内快速移动通常很方便。例如，假设我们输入了

```
$ goodbye
```

但意识到我们想在其前面加**echo**。我们可以使用左箭头键到达行首，但输入`Ctrl-A`更简单，它可以立即让我们到达那里。类似地，`Ctrl-E`移动到行尾。最后，`Ctrl-U`清除到行首并让我们重新开始。

`Ctrl-A`、`Ctrl-E` 和 `Ctrl-U` 的组合在大多数系统上都能正常工作，但如果你在编辑较长行（例如包含威廉·莎士比亚*十四行诗第一首*第一行的这一行（清单 4）），它们对你没什么用。

![](img/4dec9c51e73c9027d3d8a4fab4408fe6_22_0.png)

*图 10：莎士比亚第一首十四行诗的原始外观。*

### 清单 4：打印莎士比亚第一首十四行诗的第一行。

```
$ echo "From fairest creatures we desire increase,"
```

假设我们要将“From”改为“F**R**om”，以更紧密地匹配原始十四行诗中的文本（图 10）。¹⁰ 我们可以输入`Ctrl-A`，然后按几次右箭头键，但在某些系统上，通过结合键盘和鼠标使用 Option-单击可以直接移动到所需位置。也就是说，你可以按住键盘上的 Option 键，然后用鼠标指针点击命令中你想要光标所在的位置。这将使我们直接移动到“From”中的“o”，允许我们删除“r”，直接得到清单 5。

> ⁹ 图像取自 https://commons.wikimedia.org/wiki/File:Jazz_at_Knicks_man_to_man_defense.jpg，检索于 2015-07-22

> ¹⁰ 请注意，莎士比亚英语的*原始发音*（OP）与现代发音不同。一般来说，莎士比亚的十四行诗包含许多在现代英语中不押韵但在 OP 中押韵的词对。在图 10 的情况下，单词“*memory*’”应发音为“MEM-or-aye”，从而导致第 2 行和第 4 行（分别以 *die* 和 *memory* 结尾）之间押韵。图像取自 https://commons.wikimedia.org/wiki/File:Sonnet_1.jpg，检索于 2015-07-20

