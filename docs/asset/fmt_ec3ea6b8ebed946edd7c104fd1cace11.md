
在脚本中维护目录的优势在于，它省去了一些额外的文件操作，例如打开和读取——如果目录数据保存在单独的文件中，这些操作是必需的。这样做的结果是程序运行得更快。

完成以下章内练习将加深你对 C shell 的 here 文档特性的理解。

## 练习 15.3

在你的系统上创建 `dext` 脚本并运行它。尝试尽可能多不同的输入。脚本是否正常工作？

## 15.5 中断（信号）处理

我们在第 10 章讨论了信号的基本概念，将其定义为可以发送给进程的软件中断。我们还指出，接收信号的进程可以采取以下三种可能的操作之一：

1. 接受由 UNIX 内核决定的默认操作
2. 忽略该信号
3. 采取程序员定义的操作

在 UNIX 中，有多种类型的信号可以发送给进程。其中一些信号可以通过硬件设备（如键盘）发送，但所有这些信号都可以通过 `kill` 命令发送，如第 10 章和第 13 章所述。导致硬件中断（以及信号）的最常见事件是在你按下 `<Ctrl+C>` 时产生的，这被称为键盘中断。该事件作为其默认操作，会导致前台进程终止。其他导致进程接收信号的事件包括：子进程终止、进程访问不属于其地址空间（即程序拥有并被允许访问的主内存区域）的主内存位置，以及执行不带任何信号编号的 `kill` 命令所造成的软件终止信号。表 15.2 列出了一些重要的信号、它们的编号（可用于通过 `kill` 命令生成这些信号）及其用途。

### 表 15.2 一些重要信号、其编号及其用途

| 信号名称 | 信号编号 | 用途 |
|---|---|---|
| SIGHUP（挂起） | 1 | 当运行该进程的用户注销时通知进程，并终止进程 |
| SIGINT（键盘中断） | 2 | 当用户按下 `<Ctrl+C>` 时通知进程，并终止进程 |
| SIGQUIT（退出信号） | 3 | 当用户按下 `<Ctrl+\>` 或 `<Ctrl+/>` 时通知进程，并终止进程 |
| SIGKILL（确定终止） | 9 | 当用户通过 `kill -9` 命令向进程发送此信号时终止进程 |
| SIGSEGV（段违规） | 11 | 当进程试图访问不属于它的内存空间时，因内存错误而终止进程 |
| SIGTERM（软件终止） | 15 | 当使用不带任何信号编号的 `kill` 命令时终止进程 |
| SIGTSTP（挂起/停止信号） | 18 | 挂起进程，通常是 `<Ctrl+Z>` |
| SIGCHLD（子进程执行完毕） | 20 | 通知进程其某个子进程已终止 |

C shell 的信号处理特性允许你编写无法通过终端中断（`<Ctrl+C>`）来终止的程序。与 Bourne shell 对信号处理的支持相比，该特性非常有限。用于拦截和忽略 `<Ctrl+C>` 的命令是 `onintr`。下面是该命令的简要说明。

#### 语法

```
onintr [options]
```

用途：忽略终端中断（`<Ctrl+C>`）或拦截它并将控制权转移到任意命令

- 常用的选项/特性：
  - 忽略终端中断
  - `label`：将控制权转移到“`label`”处的命令

当你在没有指定任何选项的情况下使用 `onintr` 命令时，如果进程正在运行期间按下 `<Ctrl+C>`，就会执行进程终止的默认操作。因此，不使用任何选项的 `onintr` 命令是多余的。在这里，我们增强了第 14 章 `while_demo` 文件中的脚本，以便你无法通过 `<Ctrl+C>` 终止该程序的执行。增强版本位于 `onintr_demo` 文件中，如下一个会话所示。注意，当你按下

`<Ctrl+C>` 在执行此程序时。标签处的代码是一个 `goto` 命令，将控制转移到 `onintr` 中断命令，以重置代码的中断处理能力，从而有效地忽略 `<Ctrl+C>`。一个示例运行说明了这一点。

```
% cat onintr_demo

#!/bin/csh

# Intercept <Ctrl+C> and transfer control to the command at

# backagain:

onintr interrupt

# Set the secret code

set secretcode = agent007

# Get user input

echo "Guess the code!"

echo -n "Enter your guess: "

set yourguess = `head -1`

# As long as the user input is not the secret code (agent007 in

# this case), loop here: display a message and take user input

# gain. When the user input matches the secret code, terminate the

# loop and execute the following echo command.

while ( "$secretcode" != "$yourguess" )

 echo "Good guess but wrong. Try again!"

 echo -n "Enter your guess: "

 set yourguess = `head -1`

end

echo "Wow! You are a genius!"

exit 0

# Code executed when you press <Ctrl+C>

interrupt:

 echo "Nice try -- you cannot terminate me by <Ctrl+C>!"

 goto backagain
% ./onintr_demo

Guess the code!

Enter your guess: codecracker

Good guess but wrong. Try again!

Enter your guess: <Ctrl+C>

Nice try -- you cannot terminate me by <Ctrl+C>!

Guess the code!

Enter your guess: Lionking

Good guess but wrong. Try again!

Enter your guess: agent007
```

```
Wow! You are a genius!

%
```

在前面的脚本中使用 `onintr` 命令的净效果是忽略键盘中断。您可以通过使用带 `-` 选项的命令来实现相同的效果。因此，`onintr_demo` 程序中的整个中断处理代码可以用 `onintr -` 命令替换；在任何标签处都不需要代码，但这样当您按下 `<Ctrl+C>` 时，代码不会为你显示任何消息。

要终止忽略终端中断的程序，您必须使用 `kill` 命令。您可以通过按下 `<Ctrl+Z>` 挂起进程，使用 `ps` 命令获取进程的进程 ID（PID），然后使用 `kill` 命令终止它来实现。

您可以修改 `onintr_demo` 文件中的脚本，使其忽略键盘中断，清除显示屏并关闭回显。这样，无论您在键盘上输入什么，都不会显示。接下来，它会提示您两次输入代码词。如果您两次输入的代码词不同，它会提醒您短期记忆不好并退出。如果您输入相同的代码词，它会清除显示屏并提示您再次猜测代码词。如果您没有输入原始代码词，屏幕将被清除并提示您再次猜测。程序不会在您输入原始代码词之前终止。当您输入它时，显示屏将被清除，一条消息显示在屏幕左上角，回显被打开。由于终端中断被忽略，您无法通过按下 `<Ctrl+C>` 来终止程序。`stty -echo` 命令关闭回显。因此，当您输入原始代码词（或任何猜测）时，它不会显示在屏幕上。`clear` 命令清除显示屏并将光标定位在左上角。`stty echo` 命令打开回显。 resulting 脚本在 `canleave` 文件中，如以下会话所示。

```
% cat canleave

#!/bin/csh

# File Name:      ~/unix3e/CShell/canleave

# Author:         Syed Mansoor Sarwar

# Written:        August 18, 2004

# Modified:       May 8, 2004, September 15, 2014

# Purpose:        To allow a user to leave his/her terminal for a

#                 short duration of time by locking the terminal

#                 after taking a code from the user. Terminal is

#                 unlocked only when the user re-enters the same

#                 code. Ignores command line arguments. Does not
```
