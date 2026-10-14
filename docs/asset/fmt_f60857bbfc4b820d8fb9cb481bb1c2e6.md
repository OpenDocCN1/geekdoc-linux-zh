
尝试识别几个与我检查的文件名称相似的文件，并看看 `file` 对它们说明了什么：

```
% cat /dev
dev audio spx sr0 tty
dev: executable script
audio: character special (6/0)
spx: character special (37/35)
sr0: block special (16/0)
tty: character special (2/0)
```

UNIX 有两种不同类型的设备（或外设）可以连接：一种按块提供信息的，另一种按字节提供信息的。前者称为块设备（block devices），后者称为字符设备（character devices）。你不需要担心这些差异，但请注意 `file` 可以区分它们：`audio`、`spx` 和 `tty` 都是字符文件，而 `sr0` 是块设备。

每个文件描述后括号中的两个数字被称为文件的主设备号（major number）和小设备号（minor number）。第一个表示设备类型，第二个表示由该特定外设控制的插口、卡或其他硬件的物理位置。

好消息是，你不需要担心 `/dev` 中有什么文件，或者除了你的主目录以外的任何目录。每天有成千上万的人工作却从未意识到这些其他目录的存在，更不用说里面有什么。重要的是，你已经学会了 `file` 命令在识别各种类型的 UNIX 系统文件方面非常强大。当你浏览文件系统时，甚至当你只是试图记住你自己的目录中哪些是是文件时，它都是一个非常有用的工具。

## 任务 7.3：使用 head 查看前几行

现在你已经有了在文件系统中移动所需的工具，双重检查你所在的位置并识别不同文件的类型，是时候学习 UNIX 提供的许多查看文件内容的工具了。列表上的第一个是 `head`，这是一个查看系统上任何文件第一行的简单程序。

`head` 程序比听起来要灵活得多：实际上，你可以用它查看非常长文件的前几百行。要指定你想查看的行数，只需要将行数作为起始参数指定，并在所需的行数前加上连字符。

`img/f32f6f53c129deebafcd2b4ff01bc9_143.png`

`head` 命令是许多 UNIX 命令之首，这些命令倾向于在起始参数的常规规则上使用自己的变体。与其使用典型的 UNIX 命令参数 `-33` 来指定 33 行，`head` 使用 `-n33` 来指定相同的信息。

`img/f32f6f53c129deebafcd2b4ff01bc9_144_0.png`

`img/f32f6f53c129deebafcd2b4ff01bc9_144_1.png`

1. 首先回到你的主目录并查看你的 `.cshrc` 文件的前几行：

```
% cd
% .cshrc
## Default .cshrc file (/bin/sh initialization).
```

```
set path=~/ /bin /usr/bin /usr/ucb /usr/local /etc /usr/local/bin /usr/unix/bin
## Set up shell environment:
```

```
alias diff '/usr/bin/diff -c -'
```

你的 `.cshrc` 文件内容无疑很长，但请注意程序只列出了文件的前几行。

2. 要指定不同的行数，使用 `-n` 格式（其中 `n` 是行数）。我将查看 `.login` 文件的前四行：

```
% head -4 .login
## #($) Revision: 62.2 $
```

```
setenv VTM 100
```

3. 你可以通过向 `head` 指定多个文件来轻松地检查多个文件：

```
% head -5 /etc/passwd /etc/group
```

4. 更重要的是，`head` 可以作为管道的一部分，其中一个程序的输出是下一个程序的输入。这种操作的特殊符号是管道（`|`）。

`img/f32f6f53c129deebafcd2b4ff01bc9_144_2.png`

## 任务 7.4：使用 tail 查看几行

`head` 程序向你显示指定文件的前 10 行。那么你认为 `tail` 会做什么？我希望你猜对了正确答案：它显示文件的最后 10 行。像 `head` 一样，`tail` 也理解指定查看行数的相同格式。

接下来，可以使用以下命令行显示家目录中 `LISTS` 文件的最后四行：

```
% tail -5 LISTS
College of Education
Arizona State University
Tempe, AZ 85287-2411
602-965-2692
```

不要纠结于弄清楚我的文件里到底有什么：有时候连我自己都不清楚。

3. 这里有一个值得深思的问题。当你使用 `head` 查看文件的前 `n` 行，而使用 `tail` 查看文件的后 `n` 行时。你可以尝试结合这两者的方法，这样你就能看到所有文件的第十行和十二行。

```
% head -12 .bashrc | tail -3
alias diff /usr/bin/diff -c -w
alias from "* -n"
alias ll "* -I '
```

使用 UNIX 命令管道，这非常简单！

将 `head` 和 `tail` 两个命令结合可以让你在查看 UNIX 系统文件的片段时变得强大。尝试以不同的方式组合它们以获得不同的效果。

## 任务 7.5：使用 cat 查看文件内容

`head` 和 `tail` 都提供了查看文件片段（顶部或底部）的能力，但无论长度如何，它们都无法查看整个文件。对于这项工作，`cat` 程序是正确的选择。

`cat` 程序的名字来源于它在 UNIX 早期版本中的功能；它的功能是连接（或合并）多个文件。遗憾的是，它并不是指猫皮或任何其他奇特的东西！

`cat` 程序还有一个宝贵的秘密功能，通过使用 `-v` 标志，你可以使用 `cat` 显示系统上的任何文件（无论是否可执行），并且所有通常不会打印（或会导致你的屏幕溢出）的字符将以一种我称为“控制键表示法”的特殊格式显示。在控制表示法中，每个字符都表示为 `^n`，其中 `n` 是一个特定的打印字符或符号。值为 0 的字符（也称为空字符或 null character）显示为 `^^`，值为 1 的字符显示为 `^A`，值为 2 的字符为 `^B`，以此类推。

另一个对某些文件有用的 `cat` 标志是 `-s`，它可以抑制文件中的多个空行。这并不一眼看出有什么帮助，但有些文件可能包含整屏（或更多）的空行。为了避免看着它们飞速掠过，你可以使用 `cat -s` 将它们全部压缩为单个空行。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_147_0.png)

1. 再次回到家目录，并使用 `cat` 显示 `.cshrc` 文件的完整内容：

```
% cd
% cat .cshrc
## 默认用户 .cshrc 文件 (/bin/csh 初始化).
set path=(~ /usr/bin /usr/bin /usr/ucb /usr/local /etc
usr/etc/usr/local/bin /usr/unset /bin)
```

```
## 设置 shell 环境：
alias diff    /usr/bin/diff -c w
alias from    "frm -n"
alias ll      "ls -l"
alias ls      /bin/ls -F"
alias mail
alias mailq  /usr/lib/sendmail -bp
```

```
alias newaliases "echo you mean newalias..."
alias rd      *readmsg S| page"
alias rn      *usr/local/bin/rn -dHOME -L -M -m -e -S/
```

```
# 如果我们在交互式 shell 中，则进行一些特殊处理
($ ?prompt) # shell 是交互式的。
```

```
alias cd      *chdir \*; setprompt
alias env     *printenv
```

```
@@@@@@@@@@@@@@@@@@@@@@@ `@@ ` `@@ ` ` ` ` ` ` ` ` ` ` ` ` ` ` 文件的内容的 ` ` ` ` `。
```

1. 使用 `cat` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ` ``。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_148_0.png)

## 查看文件
