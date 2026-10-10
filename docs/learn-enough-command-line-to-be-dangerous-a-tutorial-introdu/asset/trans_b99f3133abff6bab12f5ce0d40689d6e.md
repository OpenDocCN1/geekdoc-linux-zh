
**列表 5：** 编辑较长的命令行命令的结果。

```
$ echo "From fairest creatures we desire increase,"
```

我通常通过组合使用 `Ctrl-A`、`Ctrl-E` 以及左右方向键在命令行中移动，但对于较长的命令，Option 点击（在 Mac 上通常是 Option+点击）会非常有帮助。（我经常改变关于我正在输入的确切命令的想法，在这种情况下，我发现按 `Ctrl-U` 重新开始通常是继续的最快方式。）

# 练习

- 1. 使用向上箭头，在屏幕上打印字符串“fee”、“fie”、“foe”和“fum”，而无需每次都重新输入 `echo`。
- 2. 从列表 4 中的那一行开始，使用 `Ctrl-A`、`Ctrl-E`、方向键或 Option 点击的任何组合，将短 *s* 的出现更改为古英语长 *s* “ſ”，以匹配原始外观（图 10）。换句话说，`echo` 的参数应读作“FRom faireft creatures we defire increase,”。*提示：* 你的键盘不太可能原生产生“ſ”，因此请从本教程的文本中复制它，或者在 Google 上搜索并从互联网上复制。

# 1.5 清理

在使用命令行时，有时能够清理屏幕（清除屏幕）会很方便，我们可以使用 `clear` 来实现：

```
$ clear
```

这个操作的键盘快捷键是 `Ctrl-L`。

同样地，当我们用完终端窗口（或标签页）并准备退出时，我们可以使用 `exit` 命令：

| 命令 | 描述 | 示例 |
|---|---|---|
| `echo <string>` | 打印字符串到屏幕 | `$ echo hello` |
| `man <command>` | 显示命令的手册页 | `$ man echo` |
| `Ctrl-C` | 摆脱困境 | `$ tail^C` |
| `Ctrl-A` | 移动到行首 | |
| `Ctrl-E` | 移动到行尾 | |
| `Ctrl-U` | 删除到行首 | |
| `Option-click` | 将光标移动到点击的位置 | |
| `Up & down arrow` | 在之前的命令中滚动 | |
| `clear` 或 `Ctrl-L` | 清除屏幕 | `$ clear` |
| `exit` 或 `Ctrl-D` | 退出终端 | `$ exit` |

*表 1：第 1 节中的重要命令。*

```
$ exit
```

这个操作的键盘快捷键是 **Ctrl-D**。

# 练习

- 1. 清除当前标签页的内容。
- 2. 打开一个新标签页，执行 `echo 'hello'`，然后退出。

# 1.6 总结

本节中的重要命令已在表 1 中总结。

# 练习

- 1. 编写一个命令，打印字符串 **Use** `"man echo"`，*包括*引号；即，注意不要打印出 **Use** `man echo`。*提示：* 在内部字符串中使用双引号，并将整个内容包裹在单引号中。
- 2. 通过运行 `man sleep`，弄清楚如何让终端“休眠”5 秒，并执行该命令。在等待了 5 秒后，执行休眠 5000 秒的命令，意识到这超过了一小时，然后使用框 4 中的说明来摆脱困境。

# 2 操作文件

因为这是一个命令行教程，我们不会假设读者熟悉用于编辑文本的程序。（这些称为*文本编辑器*的程序是序列中下一个教程的主题，*Learn Enough™ Text Editor to Be Dangerous*。）这意味着我们需要在命令行上手动创建文件。但这是一个特性，而不是缺陷（框 6），因为学习在命令行上创建文件本身是一项宝贵的技能。

**框 6. 学习说“极客”语言**

学习软件开发的一个重要部分是熟悉黑客、书呆子和极客文化，很多软件开发都源于此。例如，“这不是一个 bug，这是一个特性”是一种常见的将看似缺陷重新定义为*优点*的方式。正如 Urban Dictionary*所说*：

**这不是一个 bug，这是一个特性**  
软件开发者试图说服用户他们的程序中的一个缺陷实际上正是其应有的表现时所找的借口。

*Jargon File*，其中包含大量有趣的*黑客*术语*词典*，在其关于*特性*的条目中对这一主题进行了扩展：

未记录的特性是 *bug* 的一种常见且据称幽默的委婉说法。还有一个相关的玩笑，有时被称为

![](img/4dec9c51e73c9027d3d8a4fab4408fe6_26_0.png)

*图 11：这不是一个 bug，这是一个特性。*

> “单问题极客测试”。你对某人说：“我今天看到一辆大众甲壳虫，车牌号是 FEATURE（特性）”。如果他/她笑了，那么他/她就是一个*极客*。
>
> 这里的玩笑在于，因为“bug”（甲虫）是大众甲壳虫的常见俚语，带有 FEATURE（特性）车牌的甲壳虫是“这不是一个 bug，这是一个特性”（图 11）在现实中的体现。

## 2.1 重定向和追加

让我们（或多或少）从第 1 节离开的地方继续，使用一个 **echo** 命令来打印出莎士比亚第一首十四行诗的第一行（列表 4）：

```
$ echo "From fairest creatures we desire increase,"
From fairest creatures we desire increase,
```

我们现在任务是创建一个包含这一行的文件。即使没有文本编辑器的帮助，我们也可以使用*重定向运算符* `>` 来做到这一点：

```
$ echo "From fairest creatures we desire increase," > sonnet_1.txt
```

（请记住，你可以使用向上箭头检索之前的命令，而不是从头开始输入。）这里，右尖括号 `>` 获取 **echo** 输出的字符串并将其内容重定向到一个名为 **sonnet_1.txt** 的文件。

我们如何判断重定向是否成功？我们将在第 3 节学习一些更高级的命令行工具来检查文件，但眼下我们将使用 **cat** 命令，它只是将文件的内容转储到屏幕上：

```
$ cat sonnet_1.txt
From fairest creatures we desire increase,
```

**cat** 这个名字是“**c**oncate**n**ate”（连接）的缩写，这是一个提示，说明它可以用来合并多个文件的内容，但上述用法（转储单个文件的内容）极其常见。把 **cat** 想象成查看特定文件内容的“快速且凌乱”的方式（图 12）。[^11]

为了添加十四行诗的第二行（使用现代拼写），我们可以按如下方式使用*追加运算符* `>>`：

[^11]: 图像取自 https://www.flickr.com/photos/tiffanyday/4076289864，日期为 2015-07-22

![](img/4dec9c51e73c9027d3d8a4fab4408fe6_28_0.png)

图 12：使用 **cat** 查看文件。

```
$ echo "That thereby beauty's Rose might never die," >> sonnet_1.txt
```

这只是将该行添加到给定文件的末尾。和之前一样，我们可以使用 cat 查看结果：

```
$ cat sonnet_1.txt
From fairest creatures we desire increase,
That thereby beauty's Rose might never die,
```

（为了得到这个命令，希望你只是按了两次向上箭头，而不是重新输入。如果是这样，你肯定已经掌握了。）上面的结果显示，双右尖括号 >> 将 echo 中的字符串追加到了文件 sonnet_1.txt，符合预期。

十四行诗的现代改编版本有时会将 Rose 改为 rose（从而模糊了可能的含义），我们可以使用两次额外的 echo 调用来制作一个遵循此约定的第二个文件：

```
$ echo "From fairest creatures we desire increase," > sonnet_1_lower_case.txt
$ echo "That thereby beauty's rose might never die," >> sonnet_1_lower_case.txt
```

为了促进对相似但不完全相同的文件进行比较，Unix 系统附带了有用的 diff 命令：

```
$ diff sonnet_1.txt sonnet_1_lower_case.txt
< That thereby beauty's Rose might never die,
---
> That thereby beauty's rose might never die,
```

在讨论计算机文件时，diff 经常被用作名词（“那些文件之间的 diff 是什么？”）和动词（“你应该 diff 那些文件以查看发生了什么变化。”）。与许多技术术语一样，这有时也会渗透到日常用法中，例如“将当前的观点与过去各种文化的观点进行 diff，看看你能得到什么。”[^12]

