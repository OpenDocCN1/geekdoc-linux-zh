

# 第3章：复合命令语法 143

使用 `kill %cat` 命令移除你的协进程（co-process）。

# 实验 3.1

e) 当你运行 `kill` 命令时发生了什么？

答案：你的交互界面应该如下所示：

```
$ kill %cat
[1] + Terminated          cat > out &
$
```

“Terminated”消息与你在实验 2.3 中已经看到的“Done”消息是一样的。如果你没有看到 "Terminated" 消息，是因为你关闭了 shell 的监控（monitor）选项。也就是说，监控选项同时控制 "Done" 和 "Terminated" 消息。

这种形式的 `kill` 命令使用 `%` 后面跟后台运行的命令名称，就像使用 `^C` 终止一个标准输入连接到你键盘的普通命令一样。如果你愿意，可以在 `kill` 中使用作业号代替命令名。

- f) 如果你现在运行另一个 `print -p` 命令会发生什么？

答案：你的交互界面应该类似于此：

```
$ print -p Hello, hello, . . . Are you there?
-ksh: print: no query process [Bad file descriptor]
$
```

你可以理解为如果没有正在运行的协进程，你就无法使用 `print -p`，但还有更多信息需要考虑。首先，错误消息来自 `ksh` —— 特别是它的内置命令 `print`。之后，`no process` 显然意味着没有协进程。（术语上的这种差异没有理由。）最后是我们之前提到的消息中的 `Bad file descriptor` 部分：协进程像流水线的一部分一样运行，但其标准输入从键盘重定向到了 `print -p` 的输出。

# 实验 3.1 自测习题

为了测试你的进度，你应该能够回答以下问题。

# 实验 3.1：命令序列

1) 如果你用 `;` 分隔两个命令，在第一个命令完成之前，shell 不会启动第二个命令，即使第一个命令运行需要很长时间。

- a) 正确
- b) 错误

2) 下列哪些命令行可能不会打印 hello？

- a) `print hello | cat`
- b) `print hello > out; cat out`
- c) `print hello > out & cat out`
- d) `print hello;`
- e) `print hello&|\|`

3) 这个流水线的作用是什么？（假设 `days` 是本实验中使用的星期几文件。）

- `cat days | tr a-z A-Z | cut -c 1-3`
- a) 什么都没做
- b) 它创建了一个名为 DAY 的新文件
- c) `cut` 命令打印错误消息
- d) 它打印 MON, TUE, WED 等。

4) 这个命令行的作用是什么？（假设确实有一个名为 `fribble` 的命令。）

- `fribble || print Fribble failure!`
- a) 它总是打印 Fribble failure!
- b) 它永远不打印 Fribble failure!
- c) 如果 `fribble` 命令没有正常退出，它会打印 Fribble failure!
- d) 如果 `fribble` 命令没有正常退出，它会打印 Fribble failure!（重复项）
- e) shell 打印 Invalid ||

5) 假设所有单独命令都存在，这条命令行的作用是什么？

`feeble && fiend && foe && fumble && \`
`print fee-fie-fo-fum!`

- a) ______ 它打印 Feeble fiends are foes of fumbles.
- b) ______ 如果其他四个命令都正常退出，它会打印 fee-fee-fo-fum。
- c) ______ 如果其他任一或多个命令正常退出，它会打印 fee-fee-fo-fum。
- d) ______ 无论其他命令如何退出，它永远不打印 fee-fee-fo-fum。
- e) ______ 它打印 I smell the blood of an Englishman!

- 6) 什么命令可以用于写入作为协进程运行的程序？
- a) ______ `print -p`
- b) ______ `write -coprocess`
- c) ______ `writecoprocess`
- d) ______ `print -coprocess`
- e) ______ `print &`

测验答案见附录 A 第3节。

# 实验 3.2

# 命令组

![](img/694fa9f0320e7078044c650b96a9b4_165.png)

在本实验中，你将学习如何使用大括号和小括号对命令行中的命令分组，以控制 I/O 重定向以及 shell 处理 `&&` 和 `||` 的顺序。大括号和小括号除了这两个用途还有其他；例如，你已经在函数定义中使用了大括号。

# 实验 3.2 练习题

# 3.2.1 {} ( )

使用大括号和小括号对命令分组有很多理由，但本实验将关注两点：(i) 你可以作为一个整体对组内的所有命令进行输出重定向；(ii) 你可以覆盖 shell 处理 `&&` 和 `||` 的从左到右的顺序。

# 第3章：复合命令语法 147

在本实验涉及的内容中大括号和小括号基本等，但 shell 解释它们的方式有显著差异。

# 示例

如果你运行以下两个，将得到不同的结果：

```
{print hello
print hello}
```

第一个会导致语法错误。为了处理这些差异，你将使用以下规则：

- 1) 在括号或括号内的每个命令之间加一个空格。
- 2) 在每个组的最后一个命令后加分号。

这些规则在实验中并不总是必要的，但你会看到它们两种方式都有效![](img/694fa9f0320e7078044c650b96a9b4_166.png)

通过将重定向运算符放在组外部，可以重定向组内所有命令的输出。

# 实验规则

在大括号内部，将 `cat` 的输出通过 `tr` 到 out![](img/694fa9f0320e7078044c650b96a9b4_166.png)

有区别吗？查看文件并验证输出是否在 `out` 中。在括号中尝试同样的。

```
{print hello; < days
```

# 3.2.2 分组到重定向

