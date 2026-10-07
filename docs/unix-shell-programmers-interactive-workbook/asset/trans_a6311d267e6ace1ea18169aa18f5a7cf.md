

# 第11章：I/O 与 TRAP 处理 539

第11049 行的命令清除了 INT 处理器，第11050行显示仅剩余 KEYBD trap 的设置状态。

+   h) 每次按下 Ctrl-C 会发生什么？
答案：你的交互应该类似于以下：
```
[11051]: tt2
/home/vickery/bin/tt2: Resetting
/home/vickery/bin/tt2: Resetting
/home/vickery/bin/tt2: Exiting Normally
/home/vickery/bin/tt2: Exit Trap
[11052]:
```

该脚本演示了为一个脚本设置两个 trap 程序。每当你按下 Ctrl-C 时，INT 处理器都会打印“Resetting”消息并启动一个新的 sleep 命令。最后，当你在 30 秒内没有按下 Ctrl-C 时，脚本会打印“Exiting Normally”消息并结束，然后 EXIT 处理器运行并打印“Exit Trap”消息，shell 发出一个新提示符。

+   i) 程序终止时打印了什么？
答案：你的交互应该类似于以下：
```
[11052]: tt2 &
[1]
 280
[11053]: kill -INT &1
/home/vickery/bin/tt2: Resetting
[11054]: kill -USR1 &1
/home/vickery/bin/tt2: Exit Trap
[1] + User signal 1 tt2 &
[11055]:
```

首先，我们看到脚本捕获了一个 INT 信号，当我们投递 USR1 信号时，它按通常的方式打印消息。对于脚本没有设置 trap 的消息，程序立即终止，不会打印“Exiting Normally”消息。然而，即使脚本没有到达结尾，EXIT trap 仍然会被处理。

EXIT trap 对于“清理”工作非常有用，即使异常情况阻止了脚本完成其全部工作。

![](img/694fa9f0320e707804a4c650b96a9b4_558_0.png)

# 540 实验 11.3：拦截和生成 Traps

# 11.3.2 答案

+   a) 执行 tt3 时发生了什么？
答案：你的交互应该如下：
[11055]: tt3
[3]+ print This is the first command in this script
This is the first command in this script
[4]+ print This is the second command in this script
This is the second command in this script
[5]+ print This is the last command in this script
[5]+ 1> /dev/null
[11056]:

`set -x` 命令开启 shell 的 xtrace 功能。（你可以通过 `set +x` 命令将其关闭）。如你所见，shell 执行的每一条命令在执行之前都会被打印出来，并带上它在脚本中的行号。请注意，第三个 print 命令上的输出重定向被 shell 视为独立命令。这与 shell 允许你在没有命令的情况下使用重定向（例如创建文件）的事实是一的。

![](img/694fa9f0320e707804a4c650b96a9b4_559_0.png)

你可以通过给变量 `PS4` 赋值，在 xtrace 模式下改变 shell 在每个命令左侧打印的内容。如上所示，PS4 的默认值为“[$LINENO]+”。

如你所见，这可以是一个发现你的程序正在做什么的有用工具，尽管输出可能非常大量。（如果你设置了 KEYBD trap，不要尝试在命令行中开启它！你每输入一个字符都会得到一行输出！）

+   b) 执行 tt4 时发生了什么？
答案：你的交互应该如下：
[11056]: tt4
Variable values are: X= Y= Z=
Variable values are: X=abc Y=cba Z=bac
Variable values are: X=hello Y=cba Z=bac
Variable values are: X=hello Y=greetings! Z=bac
[11057]:

# 第二章：I/O 与 TRAP 处理 541

DEBUG trap 处理器会在每条命令执行之前的之前执行。与仅仅打印即将执行的命令的 xtrace 选项不同，trap 处理器可以执行你 world的任何操作。在这种情况下，我们定义了一个函数来打印某些变量的值。自然地，你可以在这样的函数内部放置任意数量的命令。

![](img/694fa9f0320e707804a4c650b96a9b4_560_0.png)

调试是一项需要对异常程序进行仔细分析的技能。如果程序进入了死循环，可以通过在代码的不同位置开启关闭 xtrace 选项来定位问题。如果某个值计算错误，明智地使用 DEBUG trap 来打印关键值可以帮助你定位问题。

LAB 11.3

![](img/694fa9f0320e707804a4c650b96a9b4_560_1.png)

调试是一项需要对运行错误的程序进行仔细分析的技能。如果程序进入了死循环，可以通过在代码的不同位置开启关闭 xtrace 来定位问题。如果某个值计算错误，明智地使用 DEBUG trap 打印关键值可以帮助你定位问题。

LAB 11.3

![](img/694fa9f0320e707804a4c650b96a9b4_560_1.png)

通过增量编写和测试可以节省大量的调试工作。如果测试期间出现问题，确保光标在脚本退出前位于开头。这是由于那部分代码的原因。

# 11.3 自测

为了测试你的进度，你应该回答以下问题：

+   1) trap 命令的作用是什么？
a) 向进程发送信号。
b) 接收信号。
c) 告诉在信号发生时要执行什么。
d) 停止脚本。
e) 打印时间。

# 542 实验 11.3：拦截和生成 Traps

+   2) 向进程发送信号的两种方式是？
a) 按 Ctrl-C 或运行 kill 命令。
b) 使用 trap 或运行命令。
c) 使用 trap。
d) 使用信号。

+   3) 信号处理器会自动传递给 shell。
a) 是
b) 否

+   4) shell 的 xtrace 选项有什么用？
a) 设置 trap。
b) 显示变量的值。
c) 在执行前打印每条命令。
d) 拦截信号。

+   5) 这条命令会做什么：trap 'print ouch!'; INT
a) 当用户按下一次 Ctrl-C 时，打印 "ouch"。
b) 每执行一条命令时都会打印 "ouch"。
c) 当用户第二次按下 Ctrl-C 时打印 "ouch"。
d) 什么都不做，因为不能放在 trap 里面。

# 第11章：I/O 与 TRAP 处理

# # 第11 章

# # 测试思考

本节中的项目旨在利用你在整个章节中获得的所有技能。这些项目的答案可以在以下配套网站找到：

http://www.phptr.com/phptrinteractive

定期访问该网站。

![](img/694fa9f0320e707804a4c650b96a9b4_562_0.png)

