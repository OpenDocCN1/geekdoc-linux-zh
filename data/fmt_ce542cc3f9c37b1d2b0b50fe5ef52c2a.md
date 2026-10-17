
将进程从前台移到后台很有用，如果我们从命令行启动图形程序，但忘记通过附加尾部的`&`将其置于后台。

为什么要从命令行启动图形程序？有两个原因。首先，你想要运行的程序可能未列在窗口管理器的菜单上（如 `xlogo`）。其次，通过从命令行启动程序，你可能能够看到如果图形方式启动则不可见的错误信息。有时，程序在从图形菜单启动时无法启动。通过改为从命令行启动，我们可能会看到一个错误信息，从而揭示问题所在。此外，一些图形程序具有许多有趣且有用的命令行选项。

## 信号

`kill` 命令用于“杀死”进程。这使我们能够终止需要被终止的程序。以下是一个示例：

```
[me@linuxbox ~]$ xlogo &
[1] 28401
[me@linuxbox ~]$ kill 28401
[1]+  Terminated              xlogo
```

我们首先在后台启动 `xlogo`。shell 打印后台进程的 `jobspec` 和 `PID`。接下来，我们使用 `kill` 命令并指定要终止的进程的 `PID`。我们也可以使用 `jobspec`（例如，`%1`）而不是 `PID` 来指定进程。

虽然这看起来很简单，但事情远不止于此。`kill` 命令并不完全“杀死”进程，而是向它们发送信号。信号是操作系统与程序通信的几种方式之一。我们已经在使用 `Ctrl-c` 和 `Ctrl-z` 时看到了信号的实际作用。当终端接收到这些按键时，它会向前台程序发送一个信号。在 `Ctrl-c` 的情况下，会发送一个名为 `INT`（中断）的信号；对于 `Ctrl-z`，则发送一个名为 `TSTP`（终端停止）的信号。程序反过来会“监听”信号，并在接收到时可能对其采取行动。程序能够监听并对信号采取行动这一事实，使得程序能够在收到终止信号时执行诸如保存正在进行的工作等操作。

## 使用 kill 向进程发送信号

`kill` 命令用于向程序发送信号。其最常见的语法如下所示：

```
kill [-signal] PID...
```

如果在命令行上未指定信号，则默认发送 `TERM`（终止）信号。`kill` 命令最常用于发送以下信号：

表 10-4：常见信号

| Number | Name | Meaning |
|---|---|---|
| 1 | HUP | Hangup. This is a vestige of the good old days when terminals were attached to remote |

让我们试试 `kill` 命令：

```
[me@linuxbox ~]$ xlogo &
[1] 13546
[me@linuxbox ~]$ kill -1 13546
[1]+  Hangup                  xlogo
```

在这个例子中，我们在后台启动 `xlogo` 程序，然后用 `kill` 向它发送 `HUP` 信号。`xlogo` 程序终止，shell 提示后台进程已收到挂断信号。你可能需要在看到消息前按几次回车键。请注意，信号可以用数字或名称指定，包括以字母`SIG`开头的名称：

```
[me@linuxbox ~]$ xlogo &
[1] 13601
[me@linuxbox ~]$ kill -INT 13601
[1]+  Interrupt                xlogo
[me@linuxbox ~]$ xlogo &
[1] 13608
[me@linuxbox ~]$ kill -SIGINT 13608
[1]+  Interrupt                xlogo
```

重复上面的例子并尝试其他信号。请记住，你也可以用 `jobspecs` 代替 `PID`。

进程与文件一样有所有者，只有你是进程的所有者（或超级用户）时，才能用 `kill` 向其发送信号。

除了上面最常与 `kill` 一起使用的信号列表外，系统还经常使用其他信号。以下是其他常见信号的列表：

### 表 10-5：其他常见信号

| Number | Name | Meaning |
|---|---|---|
| 3 | QUIT | Quit. |
| 11 | SEGV | Segmentation Violation. This signal is sent if a program makes illegal use of memory, that is, it tried to write somewhere it was not allowed to. |
| 20 | TSTP | Terminal Stop. This is the signal sent by the terminal when the Ctrl-z key is pressed. Unlike the STOP signal, the TSTP signal is received by the program but the program may choose to ignore it. |
| 28 | WINCH | Window Change. This is a signal sent by the system when a window changes size. Some programs, like top and less will respond to this signal by redrawing themselves to fit the new window dimensions. |

对于好奇的人，可以通过以下命令查看完整的信号列表：

```
[me@linuxbox ~]$ kill -l
```

## 使用 killall 向多个进程发送信号

也可以使用 `killall` 命令向匹配指定程序或用户名的多个进程发送信号。以下是语法：

```
killall [-u user] [-signal] name...
```

为了演示，我们将启动几个 `xlogo` 程序实例然后终止它们：

```
[me@linuxbox ~]$ xlogo &
[1] 18801
[me@linuxbox ~]$ xlogo &
[2] 18802
[me@linuxbox ~]$ killall xlogo
[1]- Terminated              xlogo
[2]+ Terminated              xlogo
```

请记住，与 `kill` 一样，你必须具有超级用户权限才能向不属于你的进程发送信号。

## 更多与进程相关的命令

由于监控进程是重要的系统管理任务，因此有许多相关命令。以下是一些可以尝试的命令：

### 表 10-6：其他进程相关命令

| Command | Description |
|---|---|
| pstree | Outputs a process list arranged in a tree-like pattern showing the parent/child relationships between processes. |
| vmstat | Outputs a snapshot of system resource usage including, memory, swap and disk I/O. To see a continuous display, follow the command with a time delay (in seconds) for updates. For example: `vmstat 5`. Terminate the output with `Ctrl-c`. |
| xload | A graphical program that draws a graph showing system load over time. |
| tload | Similar to the `xload` program, but draws the graph in the terminal. Terminate the output with `Ctrl-c`. |

## 小结

大多数现代系统都具有管理多个进程的机制。Linux 为此提供了丰富的工具集。鉴于 Linux 是全球部署最广泛的服务器操作系统，这很有意义。然而，与某些其他系统不同，Linux 主要依赖命令行工具进行进程管理。虽然 Linux 也有图形化进程工具，但命令行工具因其速度快和占用资源少而更受青睐。虽然 GUI 工具看起来很漂亮，但它们本身往往会产生大量系统负载，这在某种程度上违背了初衷。

# Part 2 – 配置与环境

## 11 – 环境

正如我们之前讨论的，shell 在我们的 shell 会话期间维护了一组称为 `environment` 的信息。存储在环境中的数据被程序用来确定有关我们配置的事实。虽然大多数程序使用配置文件来存储程序设置，但某些程序也会查找存储在环境中的值以调整其行为。了解这一点后，我们就可以使用环境来自定义我们的 shell 体验。

在本章中，我们将使用以下命令：

- `printenv` – 打印环境的部分或全部内容
- `set` – 设置 shell 选项
- `export` – 将环境导出到随后执行的程序
- `alias` – 为命令创建别名
