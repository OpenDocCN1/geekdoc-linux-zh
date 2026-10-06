

# 50 Linux 管理：入门指南

命令。在任何时候，你都可以通过输入此命令查看 Bash 正在跟踪多少任务：

```bash
$master@server -$ jobs
[1]+ Running firefox &
```

列出的正在运行程序将处于两种状态之一：运行（running）或已停止（stopped）。上面的示例输出显示 Firefox 程序正处于运行状态。输出还显示了第一列中的数字——[1]。

要将任务带回前台——也就是说，如果你想重新夺回对终端的控制权——你可以使用 `fg`（foreground）命令，如下所示：

```
$master@server -$ fg NUMBER
$master@server -$ fg 1
firefox
```

在这里，NUMBER 是你想要在前台运行的任务编号。例如，要将早先启动的 Firefox 程序（任务号为 1）放到前台，请输入以下命令：

如果一个任务停止了（处于停止状态），你可以再次在后台启动它，这让你能保持对终端的控制并恢复任务。已停止的任务可以在前台运行，这将终端的控制权交还给程序。

要将正在运行的任务放入后台，请输入以下命令：

```bash
$master@server -$ bg NUMBER
```

在这里，NUMBER 是你想要放入后台的任务编号。

> 注意：你可以将任何进程放入后台。需要终端输入或输出的应用程序在放入后台后将进入停止状态。例如，你可以通过输入 `top &` 在后台运行 `top` 实用程序。然后使用 `jobs` 命令检查该任务的状态。

#环境变量

每个 shell 实例、每个运行中的进程都有它们自己的“环境”——这些是赋予其特定外观、感受以及在某些情况下赋予行为的设置：这些设置通常由环境变量控制。某些环境变量对 shell 有特殊含义，但并没有阻止你定义自己的变量并将其用于你的需求。正是通过使用环境变量，大多数 shell 脚本才能够执行有趣的操作，并记住用户输入的结果以及程序输出的结果。如果你已经熟悉 Windows 200x/XP/Vista/7/8/10 中环境变量的概念，你会发现你所知道的很多内容也适用于 Linux；唯一的区别在于它们是如何设置、查看和删除的。

# 打印环境变量

要列出所有的环境变量，请使用 `printenv` 命令。这是一个示例：

```bash
[master@server ~$ printenv
HOSTNAME=server
TERM=xterm
SHELL=/bin/bash
HISTSIZE=1000
...<OUTPUT TRUNCATED>...
```

要显示特定的环境变量，请将该变量作为 `printenv` 的参数。例如，这里是查看环境变量 `TERM` 的命令：

```bash
[master@server ~$ printenv  TERM
xterm
```

# 设置环境变量

要设置环境变量，请使用以下格式：

```
variable=value
```

在这里，variable 是变量名，value 是你想要赋予变量的值。例如，要将环境变量 `FOO` 设置为值 `BAR`，请输入以下命令：

```bash
[master@server ~$ FOO=BAR
```

当你以这种方式设置环境变量时，它们将局限于当前运行的 shell。如果你想让该值传递给其他启动的进程，请使用 `export` 内置命令。`export` 命令的格式如下：

```bash
export variable
```

在这里，variable 是变量名。在设置变量 `FOO` 的示例中，你输入此命令：

```bash
[master@server ~$ export FOO
```

> 提示：你可以将设置环境变量的步骤与 `export` 命令结合起来，如下：
$ export FOO=BAR

如果你要设置的环境变量值包含空格，请用引号括起变量。使用前面的示例，将 `FOO` 设置为“Welcome to the BAR of FOO.”，请输入：

```bash
[master@server ~$ export FOO="Welcome to the BAR of FOO."
```

# 52 Linux 管理：入门指南

通过 `printenv` 命令查看你设置的环境变量 `FOO` 的值：

```bash
[master@server ~$ printenv FOO
Welcome to the BAR of FOO.
```

