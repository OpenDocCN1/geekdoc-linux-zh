

### 1.7 从脚本执行命令

当 shell 被用作编程语言时，命令和 shell 控制结构会被输入到编辑器中并保存到一个文件中，称为脚本。shell 会逐行读取并执行文件中的内容。这些程序是解释执行的，而不是编译的。编译程序在执行前会被转换为机器语言。因此，shell 程序通常比二进制可执行文件慢，但它们更容易编写，主要用于自动化简单任务。shell 程序也可以在命令行交互式编写，对于非常简单的任务来说，这是最快的方式。然而，对于更复杂的脚本编写，在编辑器中编写脚本会更容易（除非你是一个非常出色的打字员！）。下面的脚本可以由任何 shell 执行以输出相同的结果。图 1.15 及其后面的说明展示了名为 dot 的脚本的创建过程，以及它如何与已有的 UNIX 程序/实用程序/命令配合使用。

**Figure 1.15 Creating a generic shell script.**

![](img/60a0b5d254bd6007403850f972cbfad8_69_0.png)

```
#!/bin/csh
echo hello
ls
who
cat
date
pwd
.
.
.
```

### EXPLANATION

- 1. 打开你喜欢的编辑器并输入一组 UNIX/Linux 可执行文件，每行一个。通过在第一行 #! 之后放置 shell 的路径名来指定你想要使用的 shell。该程序由 C shell 执行，其名称为 dot。
- 2. 保存你的文件并打开执行权限，以便你可以运行它。
- 3. 就像运行其他任何 UNIX/Linux 命令一样执行你的程序。

## Chapter 2: Shell Programming QuickStart

![](img/60a0b5d254bd6007403850f972cbfad8_70_0.png)

### 2.1 Taking a Peek at Shell Scripts

如果你阅读、编写或维护程序，以下示例将为你快速概述 shell 脚本的构造和风格，并向你介绍这些程序中使用的一些结构和语法。注意：如果不熟悉编程，请跳过本章并转到第 3 章。在你学会如何编写脚本后，你可能希望返回本章作为快速参考以刷新记忆。

C shell 和 TC shell 模拟了 C 语言语法，而 Bourne shell 则基于一种名为 Algol 的较老编程语言。

Bash 和 Korn shell 倾向于结合 Bourne shell 和 C shell，尽管这些 shell 源自 Bourne shell。

为了说明 shell 之间的差异，提供了四个示例程序，每个 shell 一个（C shell 和 TC shell 在这里一起呈现）。在每个程序上方，都列出了正在检查的 shell 的基本结构。

### 2.2 Sample Scripts: Comparing the Major Shells

在每个特定 shell 的部分末尾，你会找到一个小型程序来说明如何编写完整的脚本。乍一看，每个 shell 的程序看起来非常相似。它们确实相似。它们都做同样的事情。主要区别在于语法。在使用这些 shell 一段时间后，你会迅速适应差异并开始形成自己对哪个 shell 是你最喜欢的看法。C/TC、Bourne、Bash 和 Korn shell 之间差异的详细比较可在附录 B 中找到。

### Before Getting Started

你必须对 UNIX/Linux 命令有很好的掌握。如果你不了解基本命令，就无法在 shell 编程中做太多事情。接下来的三章将教你如何使用一些主要的 UNIX/Linux 命令，而本书后面的附录 A 则列出了最常用的命令（也称为实用程序）。

### The Purpose

在每个部分末尾提供的示例脚本会向一组用户发送邮件消息，邀请他们参加聚会。聚会的时间和地点设置在变量中。宾客名单从名为 guests 的文件中选取。程序会检查宾客文件是否存在，如果不存在，程序将退出。食物清单存储在词列表（数组）中。循环用于遍历宾客名单。每位用户都会收到一封电子邮件邀请，告知他/她聚会的时间和地点，并请他/她从食物清单中带一样东西。条件语句用于检查名为 root 的用户，如果他在宾客名单上，他将被排除在外；也就是说，他不会收到电子邮件邀请。循环将继续直到宾客名单为空。每次循环，都会从列表中移除一个食物项目，以便每位客人被要求带不同的食物。然而，如果用户多于食物，列表将被重置。这是通过标准的循环控制语句处理的。

### 2.3 The C and TC Shell Syntax and Constructs

C 和 TC shell 的基本语法和结构列在表 2.1 中。

**Table 2.1 C and TC Shell Syntax and Constructs**

| Construct | Description |
| --- | --- |
| The shbang line | “shbang” 行是脚本的第一行，让内核知道将解释脚本中各行的 shell 是什么。shbang 行由井号 #、感叹号 !（称为 bang）组成，后跟 shell 的完整路径名以及任何 shell 选项。任何以 # 开头的其他行都用作注释。<br><br>**Example:**<br>`#!/bin/csh` 或 `#!/bin/tcsh` |
| Comments | 注释是以 # 号开头的描述性内容；它们不是可执行语句。它们一直有效到行尾，可以在行的任何位置开始。<br><br>**Example:**<br>`# This is a comment` |

