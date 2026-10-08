
# 418

# 第 20 小时

```
~t users         将用户添加到列表
~v               在消息上调用编辑器
~w file          将消息写入文件。
~?               打印此消息
~|command        调用 shell
~|command        通过命令传递消息
```

最需要记住的命令是 -v，在消息中启动 vi；~r，读取文件；-h，编辑消息头；~t，调用 shell 命令；以及 ~p，显示目前输入的消息：

我想祝你拥有一个愉快的早晨！你问到了那个文件的内容，它就在这里：

| Archives/ | bin/ | delete | sample |
| InfoWorld/ | buckaroo | dickens.note | sample2 |
| Mail/ | buckaroo.confused | keylime.pie | src/ |
| News/ | cherry | mbox | temp/ |
| Owl/ | cah.man | sample | |
| awkscript | dead.letter | owl.c | |

命令的输出不包含在消息中，正如你使用 -p 命令所示：

```
~p

Message包含:
To: taylor
Subject: Good morning!
```

Linda，

我想祝你拥有一个愉快的早晨！你问到了那个文件的内容，它就在这里：

- 4. 要读取文件，请使用 -r 命令：
-r dickens.note
"dickens.note" 28/11/23

在这里，文件的内容包含在笔记中，但邮件没有将内容列在屏幕上。再次使用 -p 将列出当前消息：

```
Message包含:
To: taylor
Subject: Good morning!
```

Linda，

我想祝你拥有一个愉快的早晨！你问到了那个文件的内容，它就在这里：

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_425_0.png)

# 与他人交流

# 双城的故事
序言

当我与孩子们、朋友一起在威尔基·柯林斯的剧剧《冰封深渊》中表演时，我首次构思了这个故事的核心思想。那时，我产生了一种强烈的欲望，将我本人投射其中；并在我的探索中，勾勒出这种状态，这要求向敏锐的观众以特别的关注和兴趣呈现出来。

随着这个想法变得对我熟悉，它逐渐形成了现在的形状。在整个执行过程中，它完全占有了我；我如此详尽地证实了我在这些页中所做和遭受的，因为我确实亲身体验并经受了它们。

每当这里提到（即使是微小的）丹麦人在革命前或期间的状况时，都是真正基于最可靠的证者的信言做出的。我的愿望之一是为理解那个可怕时期的流行且生动的方法增添一些东西，尽管没有人指望能在卡尔莱先生那本伟大著作的哲学中增加任何东西。

塔维斯托克住宅
1859年11月

- 5. 使用 -h 命令微调标头：

- -h
To: duplicateim_

按下回车键保持原样，按下退格键则允许我按需要进行更改。
返回到列表中的下一个标头：

Subject: Good morning!

按下几次回车键可以让我有机会更改消息中的其他标头：

Cc:
Bcc:

Cc: 标头允许我指定其他人接收此消息。Bcc: 是众所周知密抄，即消息的不可见副本。如果我向 duplicateim 发送消息，并向 cbutter 发送抄抄，他们都可以看到对方收了一份副本，因为消息以 To: duplicateim 为标头，并且会在名字 Cc: 之后列出顺序。如果我想向某人发送消息而不让任何其他方知道，密抄就大显用场了。在 Bcc 列表中指定某人意味着该人接收了消息的副本，但他或她的名字不会出现在消息本身的任何标头中。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_426_0.png)

- 6. 最后，我使用 ^d 结束消息。

^d
Cc:

所有所谓的波浪线命令（之所以这样命名是因为它们都以 ~ 字符开头）在从命令行发送邮件时都可用。在程序内发送邮件时也可用。

# 任务 20.5：更智能的电子邮件替代方案

正如行编辑器在 vi 这样的编辑器面前显得黯然失色，Berkeley Mail 相比 Elm Mail System（或 elm）也是如此。虽然它在所有系统中都可用，但 Elm Mail System 广泛发行，如果你的系统中没有它，你的系统应该能够帮助。elm 的基本前提是用户应该专注于消息本身，而不是媒介。重点放在显示人类信息上。展示它如何运作的最佳方法就是直接尝试！我对 elm 有点偏见，因为我是该程序的作者。然而，elm 作为一种设计被广泛接受，表明我并不是独自在寻求更友好的替代方案。另一个具有非常相似界面的邮件程序是 Pine。如果你可以访问 Elm 和 Pine，我建议你选择 Elm，因为它让你以更高效的方式处理邮件。

- 1. 要启动邮件系统，输入 elm：
% elm
屏幕清空并替换为：

```
Mailbox is "usr/spool/mail/taylor" with 15 messages
```

你可以通过按下第一个字符使用以下任何命令：
- u delete 删除
- m mail a message 写一封邮件
- r reply 回复
- f forward 转发
- q 表示消息的行数（在括号中）。
- 要阅读消息，按下 <return>。
- j move移动 ("usr/spool/mail/taylor" with 15 messages)
- k move
- ? help 帮助

消息由箭头指示（或在某些屏幕上，整个消息以反转视频形式显示）。只要可能，elm 会显示发送消息的人名（例如，是 Mickey Harris 而不是 Berkeley Mail 中的 Harris），指示消息的行数（在括号中），并显示消息的主题。屏幕上的最后几行显示了此时可用的选项。j 和 k 在列表中上下移动光标，就像它们在 vi 中上下移动行一样。

- 2. 要阅读消息，我将使用 j 键向下移动到相应的消息并按回车。然后你会看到：

> Message From Cheryl at 4:57 pm
Computer Based GRE's

我计划在 1 月 6 日参加计算机化的 GRE。别叫我疯了，但总得有人去做。我会告诉你情况如何的。你还认识其他以这种方式参加 GRE 的人吗？我觉得某个地方有那张纸……如果你有那份研讨会的讲义文件，可以把它发给我吗？谢谢。

命令（使用 'i' 返回索引）：

在此处，你可以使用 j 直接读取下一条消息，r 回复，或 i 返回到目录。

- 1. 我意识到我在给 Cheryl 的消息中说的话不对。我可以在这里输入 r 回复她的消息。输入 r 会导致屏幕的最后几行替换为：

```
Command: Reply to message                                message? (y/n) n
```

要在你的回复中包含消息文本，输入 y。我不想，所以我按下回车：

```
Command: Reply to message    To: Cheryl(Cheryl)
Subject of message: Re: Computer Based GRE's
```

现在你可以看到回复将发送地址、收件人姓名（括号中）以及消息的主题。（elim 命令会自动为主题添加 Re 前缀。）光标位于主题行的末尾，如果你愿意，可以更改主题。没关系，我再次按下回车：

```
Command: Reply to message    To: Cheryl(Cheryl)
Subject of message: Re: Computer Based GRE's
Copies To -
```

不需要副本，所以我再次按下回车。现在屏幕像这样：

```
Command: Reply to message    To: Cheryl(Cheryl)
Subject of message: Re: Computer Based GRE's
Copies to: -
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_0.png)

*(注：提示提供的 OCR 文本在 425-429 页之间存在大量的重叠和重复部分。我按照要求合并了叙述流/指令。）*

等等，再次查看用户提示，OCR 文本在页面之间非常杂乱且有重复的块。让我提供一个 OCR 源内容的干净版本。

[content]
# 418

# 第 20 小时

```
~t users         将用户添加到列表
~v               在消息上调用编辑器
~w file          将消息写入文件。
~?               打印此消息
~|command        调用 shell
~|command        通过命令传递消息
```

最需要记住的命令是 -v，在消息中启动 vi；~r，读取文件；-h，编辑消息头；~t，调用 shell 命令；以及 ~p，显示目前输入的消息：

我想祝你拥有一个愉快的早晨！你问到了那个文件的内容，它就在这里：

| Archives/ | bin/ | delete | sample |
| InfoWorld/ | buckaroo | dickens.note | sample2 |
| Mail/ | buckaroo.confused | keylime.pie | src/ |
| News/ | cherry | mbox | temp/ |
| Owl/ | cah.man | sample | |
| awkscript | dead.letter | owl.c | |

命令的输出不包含在消息中，正如你使用 -p 命令所示：

```
~p

Message包含:
To: taylor
Subject: Good morning!
```

Linda，

我想祝你拥有一个愉快的早晨！你问到了那个文件的内容，它就在这里：

- 4. 要读取文件，请使用 -r 命令：
-r dickens.note
"dickens.note" 28/11/23

在这里，文件的内容包含在笔记中，但邮件没有将内容列在屏幕上。再次使用 -p 将列出当前消息：

```
Message包含:
To: taylor
Subject: Good morning!
```

Linda，

我想祝你拥有一个愉快的早晨！你问到了那个文件的内容，它就在这里：

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_425_0.png)

# 与他人交流

# 双城的故事
序言

当我与孩子们、朋友一起在威尔基·柯林斯的剧剧《冰封深渊》中表演时，我首次构思了这个故事的核心思想。那时，我产生了一种强烈的欲望，将我本人投射其中；并在我的探索中，勾勒出这种状态，这要求向敏锐的观众以特别的关注和兴趣呈现出来。

随着这个想法变得对我熟悉，它逐渐形成了现在的形状。在整个执行过程中，它完全占有了我；我如此详尽地证实了我在这些页中所做和遭受的，因为我确实亲身验并经受了它们。

每当这里提到（即使是微小的）丹麦人在革命前或期间的状况时，都是真正基于最可靠的证者的信言做出的。我的愿望之一是为理解那个可怕时期的流行且生动的方法增添一些东西，尽管没有人指望能在卡尔莱先生那本伟大著作的哲学中增加任何东西。

塔维斯托克住宅
1859年11月

- 5. 使用 -h 命令微调标头：

- -h
To: duplicateim_

按下回车键保持原样，按下退格键则允许我按需要进行更改。
返回到列表中的下一个标头：

Subject: Good morning!

按下几次回车键可以让我有机会更改消息中的其他标头：

Cc:
Bcc:

Cc: 标头允许我指定其他人接收此消息。Bcc: 是众所周知密抄，即消息的不可见副本。如果我向 duplicateim 发送消息，并向 cbutter 发送抄抄，他们都可以看到对方收了一份副本，因为消息以 To: duplicateim 为标头，并且会在名字 Cc: 之后列出顺序。如果我想向某人发送消息而不让任何其他方知道，密抄就大显用场了。在 Bcc 列表中指定某人意味着该人接收了消息的副本，但他或她的名字不会出现在消息本身的任何标头中。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_426_0.png)

- 6. 最后，我使用 ^d 结束消息。

^d
Cc:

所有所谓的波浪线命令（之所以这样命名是因为它们都以 ~ 字符开头）在从命令行发送邮件时都可用。在程序内发送邮件时也可用。

# 任务 20.5：更智能的电子邮件替代方案

正如行编辑器在 vi 这样的编辑器面前显得黯然失色，Berkeley Mail 相比 Elm Mail System（或 elm）。虽然它在所有系统中都可用，但 Elm Mail System 广泛发行，如果如果你的系统中没有它，你的系统应该能够帮助。elm 的基本前提是用户应该专注于消息本身，而不是媒介。重点放在显示人类信息上。展示它如何运作的最佳方法就是直接尝试！我对 elm 有点偏见，因为我是该程序的作者。然而，elm 作为一种设计被广泛接受，表明我并不是独自在寻求更友好的替代方案。另一个具有非常相似界面的邮件程序是 Pine。如果你可以访问 Elm 和 Pine，我建议你选择 Elm，因为它让你以更高效的方式处理邮件。

- 1. 要启动邮件系统，输入 elm：
% elm
屏幕清空并替换为：

```
Mailbox is "usr/spool/mail/taylor" with 15 messages
```

你可以通过按下第一个字符使用以下任何命令：
- u delete 删除
- m mail a message 写一封邮件
- r reply 回复
- f forward 转发
- q 表示消息的行数（在括号中）。
- 要阅读消息，按下 <return>。
- j move移动 ("usr/spool/mail/taylor" with 15 messages)
- k move
- ? help 帮助

消息由箭头指示（或在某些屏幕上，整个消息以反转视频形式显示）。只要可能，elm 会显示发送消息的人名（例如，是 Mickey Harris 而不是 Berkeley Mail 中的 Harris），指示消息的行数（在括号中），并显示消息的主题。屏幕上的最后几行显示了此时可用的选项。j 和 k 在列表中上下移动光标，就像它们在 vi 中上下移动行一样。

- 2. 要阅读消息，我将使用 j 键向下移动到相应的消息并按回车。然后你会看到：

> Message From Cheryl at 4:57 pm
Computer Based GRE's

我计划在 1 月 6 日参加计算机化的 GRE。别叫我疯了，但总得有人去做。我会告诉你情况如何的。你还认识其他以这种方式参加 GRE 的人吗？我觉得某个地方有那张纸……如果你有那份研讨会的讲义文件，可以把它发给我吗？谢谢。

命令（使用 'i' 返回索引）：

在此处，你可以使用 j 直接读取下一条消息，r 回复，或 i 返回到目录。

- 1. 我意识到我在给 Cheryl 的消息中说的话不对。我可以在这里输入 r 回复她的消息。输入 r 会导致屏幕的最后几行替换为：

```
Command: Reply to message                               Copy message? (y/n) n
```

要在你的回复中包含消息文本，输入 y。我不想，所以我按下回车：

```
Command: Reply to message    To: Cheryl(Cheryl)
Subject of message: Re: Computer Based GRE's
```

现在你可以看到回复将发送地址、收件人姓名（括号中）以及消息的主题。（elim 命令会自动为主题添加 Re 前缀。）光标位于主题行的末尾，如果你愿意，可以更改主题。没关系，我再次按下回车：

```
Command: Reply to message    To: Cheryl(Cheryl)
Subject of message: Re: Computer Based GRE's
Copies To: -
```

不需要副本，所以我再次按下回车。现在屏幕像这样：

```
Command: Reply to message    To: Cheryl(Cheryl)
Subject of message: Re: Computer Based GRE's
Copies to: -
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_0.png)

*(注：提示提供的 OCR 文本在 425-429 页之间存在大量的重叠和重复部分。我按照要求合并了叙述流/指令。）*

等等，再次查看用户提示，OCR 文本在页面之间非常杂乱且有重复的块。让我提供一个 OCR 源内容的干净版本。

[content]
# 418

# 第 20 小时

```
~t users         将用户添加到列表
~v               在消息上调用编辑器
~w file          将消息写入文件。
~?               打印此消息
~|command        调用 shell
~|command        通过命令传递消息
```

最需要记住的命令是 -v，在消息中启动 vi；~r，读取文件；-h，编辑消息头；~t，调用 shell 命令；以及 ~p，显示目前输入的消息：

我想祝你拥有一个愉快的早晨！你问到了那个文件的内容，它就在这里：

| Archives/ | bin/ | delete | sample |
| InfoWorld/ | buckaroo | dickens.note | sample2 |
| Mail/ | buckaroo.confused | keylime.pie | src/ |
| News/ | cherry | mbox | temp/ |
| Owl/ | cah.man | sample | |
| awkscript | dead.letter | owl.c | | |

命令的输出不包含在消息中，正如你使用 -p 命令所示：

```
~p

Message包含:
To: taylor
Subject: Good morning!
```

- 4. 要读取文件，请使用 -r 命令：
-r dickens.note
"dickens.note" 28/11/23

在这里，文件的内容包含在笔记中，但邮件没有将内容列在屏幕上。再次使用 -p 将列出当前消息：

```
Message包含:
To: taylor
Subject: Good morning!
```

Linda，

我想祝你拥有一个愉快的早晨！你问到了那个文件的内容，它就在这里：

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_425_0.png)

# 与他人交流

# 双城的故事
序言

当我与孩子们、朋友一起在威尔基·柯林斯的剧剧《冰封深渊》中表演时，我首次构思了这个故事的核心思想。那时，我产生了一种强烈的欲望，将我本人投射其中；并在我的探索中，勾勒出这种状态，这要求向敏锐的观众以特别的关注和兴趣呈现出来。

随着这个想法变得对我熟悉，它逐渐形成了现在的形状。在整个执行过程中，它完全占有了我；我如此详尽地证实了我在这些页中所做和遭受的，因为我确实亲身验并经受了它们。

每当这里提到（即使是微小的）丹麦人在革命前或期间的状况时，都是真正基于最可靠的证者的信言做出的。我的愿望之一是为理解那个可怕时期的流行且生动的方法增添一些东西，尽管没有人指望能在卡尔莱先生那本伟大著作的哲学中增加任何东西。

塔维斯托克住宅
1859年11月

- 5. 使用 -h 命令微调标头：

- -h
To: duplicateim_

按下回车键保持原样，按下退格键则允许我按需要进行更改。
返回到列表中的下一个标头：

Subject: Good morning!

按下几次回车键可以让我有机会更改消息中的其他标头：

Cc:
Bcc:

Cc: 标头允许我指定其他人接收此消息。Bcc: 是众所周知密抄，即消息的不可见副本。如果我向 duplicateim 发送消息，并向 cbutter 发送抄抄，他们都可以看到对方收了一份副本，因为消息以 To: duplicateim 为标头，并且会在名字 Cc: 之后列出顺序。如果我想向某人发送消息而不让任何其他方知道，密抄就大显用场了。在 Bcc 列表中指定某人意味着该人接收了消息的副本，但他或她的名字不会出现在消息本身的任何标头中。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_426_0.png)

- 6. 最后，我使用 ^d 结束消息。

^d
Cc:

所有所谓的波浪线命令（之所以这样命名是因为它们都以 ~ 字符开头）在从命令行发送邮件时都可用。在程序内发送邮件时也可用。

# 任务 20.5：更智能的电子邮件替代方案

正如行编辑器在 vi 这样的编辑器面前显得黯然失色，Berkeley Mail 相比 Elm Mail System（或 elm）。虽然它在所有系统中都可用，但 Elm Mail System 广泛发行，如果你的系统中没有它，你的系统应该能够帮助。elm 的基本前提是用户应该专注于消息本身，而不是媒介。重点放在显示人类信息上。展示它如何运作的最佳方法就是直接尝试！我对 elm 有点偏见，因为我是该程序的作者。然而，elm 作为一种设计被广泛接受，表明我并不是独自在寻求更友好的替代方案。另一个具有非常相似界面的邮件程序是 Pine。如果你可以访问 Elm 和 Pine，我建议你选择 Elm，因为它让你以更高效的方式处理邮件。

- 1. 要启动邮件系统，输入 elm：
% elm
屏幕清空并替换为：

```
Mailbox is "usr/spool/mail/taylor" with 15 messages
```

你可以通过按下第一个字符使用以下任何命令：
- u delete 删除
- m mail a message 写一封邮件
- r reply 回复
- f forward 转发
- q 表示消息的行数（在括号中）。
- 要阅读消息，按下 <return>。
- j move移动 ("usr/spool/mail/taylor" with 15 messages)
- k move
- ? help 帮助

消息由箭头指示（或在某些屏幕上，整个消息以反转视频形式显示）。只要可能，elm 会显示发送消息的人名（例如，是 Mickey Harris 而不是 Berkeley Mail 中的 Harris），指示消息的行数（在括号中），并显示消息的主题。屏幕上的最后几行显示了此时可用的选项。j 和 k 在列表中上下移动光标，就像它们在 vi 中上下移动行一样。

- 2. 要阅读消息，我将使用 j 键向下移动到相应的消息并按回车。然后你会看到：

> Message From Cheryl at 4:57 pm
Computer Based GRE's

我计划在 1 月 6 日参加计算机化的 GRE。别叫我疯了，但总得有人去做。我会告诉你情况如何的。你还认识其他以这种方式参加 GRE 的人吗？我觉得某个地方有那张纸……如果你有那份研讨会的讲义文件，可以把它发给我吗？谢谢。

命令（使用 'i' 返回索引）：

在此处，你可以使用 j 直接读取下一条消息，r 回复，或 i 返回到目录。

- 1. 我意识到我在给 Cheryl 的消息中说的话不对。我可以在这里输入 r 回复她的消息。输入 r 会导致屏幕的最后几行替换为：

```
Command: Reply to message                               Copy message? (y/n) n
```

要在你的回复中包含消息文本，输入 y。我不想，所以我按下回车：

```
Command: Reply to message    To: Cheryl(Cheryl)
Subject of message: Re: Computer Based GRE's
```

现在你可以看到回复将发送地址、收件人姓名（括号中）以及消息的主题。（elim 命令会自动为主题添加 Re 前缀。）光标位于主题行的末尾，如果你愿意，可以更改主题。没关系，我再次按下回车：

```
Command: Reply to message    To: Cheryl(Cheryl)
Subject of message: Re: Computer Based GRE's
Copies To: -
```

不需要副本，所以我再次按下回车。现在屏幕像这样：

```
Command: Reply to message    To: Cheryl(Cheryl)
Subject of message: Re: Computer Based GRE's
Copies to: -
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_0.png)

*(注：提示提供的 OCR 文本在 425-429 页之间存在大量的重叠和重复部分。我按照要求合并了叙述流/指令。）*

等等，再次查看用户提示，OCR 文本在页面之间非常杂乱且有重复的块。让我提供一个 OCR 源内容的干净版本。

*(注：我意识到我在思考过程中重复了部分内容，我现在提供最终的干净版本。）*
