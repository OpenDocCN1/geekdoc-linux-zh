
v[msg-list] 用 `vi` 编辑指定的消息。

z+ 向前 (+) 或向后 (-) 滚动标题列表（参见 `h` 命令）。

# 邮件环境

你可以通过在 `~/.mailrc` 中使用 `set` 命令为邮件变量赋值，用来建立你的邮件环境。`set` 命令的格式如下：

```
set [name=value]|
```

name 是你正在设置的邮件变量名，value 是你赋给变量的可选值。该值可以是字符串或数字。如果你使用 `set` 但不提供值，`mail` 会将变量赋值为 `null`（某些邮件变量的值并不重要，重要的是它们被设置了）。

以下是一些较重要的邮件变量列表。

- ask: 提示输入每条消息的主题。
- askcc: 提示接收你发送的邮件副本的人员姓名。
- crit-number: 如果包含此行或更多行的邮件消息通过变量 `PAGER` 传递，则给此变量分配一个数字。如果你使用的是标准终端，将 `number` 设置为 2。
- dot: 如果设置，你可以通过在单独的一行输入句号 (.) 来终止邮件。除非也设置了 `ignore`，否则在某行输入 `CONTROL-D` 仍然可以终止邮件。
- ignore: 在你编写和发送消息时忽略中断。如果你在嘈杂的线路工作，设置 `ignore` 可以让你的工作更轻松。
- record=filename: 将发出的消息复制到 `filename`。
- ignoreof: 导致在编写消息时退出时，`mail` 不保存你的消息。
- PAGER=pathname: 设置你用于不适应屏幕显示的消息的分页器位置为 `pathname`。默认的分页器是 `vi`。
- VISUAL=editor: 设置你在编写消息时 `mail` 使用的编辑器。

默认情况下，Bourne Shell 每隔 60 秒检查一次新邮件。如果有新邮件到达，`bash` 会在下一个提示符之前显示一条消息。你可以通过设置 `MAILCHECK` 变量来更改检查频率，设置为你希望 shell 在两次检查新邮件之间等待的秒数。如果没有设置 `MAILCHECK`，shell 将不会检查新邮件。

# 示例

以下示例展示了使用 `mail` 读取消息。在调用 `mail` 并看到有两条消息后，他给出命令显示第二条消息（只需输入 `2` 即可），然后按 `RETURN`：

```
$ mail
p 2
Mail version 8.1
Type ? for help.
(text of message)
```

在读完第二条消息后，Alex 尝试通过按 `RETURN` 读取第一条消息。`mail` 工具告诉他他已到达信箱末尾（At EOF），因此他他给出命令 `p 1` 然后按 `RETURN` 来查看他的第一封邮件。读完后，他选择将副本保存到文件中。由于文件已存在，它会被追加到该文件中。最后，他决定不想删除第二条消息，并且想以后再读两条消息，因此他通过命令退出了 `mail`，将两条消息都留在了信箱中：

```
RETURN
At EOF
p 1
(text of message)
s mail_msgs
x
```

# make

## 保持一组程序更新

make [options] [target-files] [arguments]

GNU make 工具根据程序及其所依赖的源文件之间修改时间的差异，保持一组可执行程序的更新。可执行程序（或 target-files）依赖于一个或多个先决文件（prerequisites）。目标文件与先决文件之间的关系在makefile 中的依赖行中指定。构建命令紧随依赖行之后，指定了 `make` 如何更新目标文件。

关于 makefiles 的更多信息，请参阅第 849 页。请参阅 make info 页面以及 www.gnu.org/manual/make 上的 GNU Make 手册。

## 参数

target-files 指向makefile 中的依赖行。当你没有指定 target-file 时，`make` 会更新makefile 中第一行依赖对应的目标。`name=value` 格式的参数会将makefile 内部的变量名设置为值。更多信息请参见“讨论（Discussion）”。

## 选项

如果不使用 `-f` 选项，`make` 将从工作目录中名为 `GNUmakefile`、`makefile` 或 `Makefile` 的文件（按此顺序）读取输入。随后，该文件被称为 `make`。许多用户倾向于使用 `Makefile` 这个名字，因为它在目录列表中显示得早。

- -f input file: 同时运行多达 `n` 条命令而不是默认的一条。如果你在多处理器系统上运行 GNU/Linux，这尤其特别有效。
- -n jobs: 当构建命令失败时，继续处理 target-files 列表下一个文件而不是退出。
- -n no execution: 显示为了使目标文件保持最新而将执行的命令，但不执行这些命令。
- -s silent: 不显示正在执行的命令名称。
- -touch: 更新目标文件的修改时间但不执行任何构建命令。请参阅第 1359 页的 `touch`。

# 讨论

尽管 `make` 最常用的用法是从源代码构建程序，但它也是一种通用的构建工具，适用于广泛的用途。任何你可以定义一组依赖关系从一种状态转换到另一种状态的地方，都是 `make` 的理想候选。

`make` 的强大很大程度上源于可以在 makefile 内部使用的功能。例如，你可以使用与 Bourne Shell 相同的语法来定义变量。务必在 makefile 内部定义 `SHELL` 变量；将其设置为运行构建命令时想要使用的 shell 路径。要定义该变量并为其赋值，请参考 makefile 顶部的该行：

```
SHELL=/bin/sh
```

*(注：由于原始文本存在大量重复的 OCR 错误块，译文已根据逻辑流进行了去重处理)*

