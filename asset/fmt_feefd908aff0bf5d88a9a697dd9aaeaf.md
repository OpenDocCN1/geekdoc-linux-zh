
Although the white space around the semicolons in the earlier example makes the command line easier to read, it is not necessary. None of the command separators needs to be surrounded by SPACE.

### Command Separation and Grouping

Although the white space around the semicolons in the earlier example makes the command line easier to read, it is not necessary. None of the command separators needs to be surrounded by SPACE.

### The `\`

Although the white space around the semicolons in the earlier example makes the command line easier to read, it is not necessary. None of the command separators needs to be surrounded by SPACE.

### The `|`

Although the white space around the semicolons in the earlier example makes the command line easier to read, it is not necessary. None of the command separators needs to be surrounded by SPACE.

### The `&`

Although the white space around the semicolons in the earlier example makes the command line easier to read, it is not necessary. None of the command separators needs to be surrounded by SPACE.

## 命令分离与分组 307

OPTIONAL (继续)

bbbbbbbbbbbbbbbbbbbbbbbbb

cccccccccccccccccccccc

aaaaaaaaaaaaaaaaaaaaaaaa

bbbbbbbbbbbbbbbbbbbbbbbbb

bbbbbbbbbbbbbbbbbbbbbbbbb

bbbbbbbbbbbbbbbbbbbbbbbbb

cccccccccccccccccccccc

cccccccccccccccccccccc

cccccccccccccccccccccc

cccccccccccccccccccccc

cccccccccccccccccccccc

```bash
bash$ a & b & c
[1] 14738
[2] 14739
[3] 14740
bash$ aaaaaaaaaaaaaaaaaaaaa
bbbbbbbbbbbbbbbbbbbbbbbbb
cccccccccccccccccccccc
bbbbbbbbbbbbbbbbbbbbbbbbb
bbbbbbbbbbbbbbbbbbbbbbbbb
bbbbbbbbbbbbbbbbbbbbbbbbb
cccccccccccccccccccccc
cccccccccccccccccccccc
cccccccccccccccccccccc
cccccccccccccccccccccc
cccccccccccccccccccccc
aaaaaaaaaaaaaaaaaaaaaaaaaaaaa
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
bbbbbbbbbbbbbbbbbbbbbbbbb
```

## 命令分组

你可以使用括号来对命令。shell 会为每个组创建一个自身的副本，称为子壳（subshell），将每组命令视为一个作业，并创建一个新进程来执行每条命令（有关创建子壳的更多信息请参见第315页的“进程结构”）。每个子壳（作业）都有自己的环境——除外，它拥有一套与其他子壳可能不同的值。

以下命令在后台顺序执行命令 `a` 和 `b`，同时在前台执行。当 `c` 完成执行后，shell 提示符返回。

```bash
bash$ ( a ; b ) & c
[1] 15007
```

此示例与之前的示例 `a & b & c` 不同之处在于，任务 `a` 和 `b` 是顺序启动的，而不是并发的。

## 308 第 10 章：Bourne Again Shell

### OPTIONAL (继续)

同样，以下命令行在后台顺序执行 `a` 和 `b`，同时在后台顺序执行 `c` 和 `d`。运行 `a` 和 `b` 的子壳与运行 `c` 和 `d` 的子壳并发执行。提示符立即返回。

```bash
bash
(a; b) & (c; d) &
[1] 15020
[2] 15020
bash
```

在以下脚本中，第二对括号创建了一个子壳来运行管道后的命令。由于这些括号的存在，尽管中间插入了 `cd` 命令，第一个 `tar` 命令的输出仍然可以供第二个 `tar` 命令使用。如果没有括号，第一个 `tar` 命令的输出将发送给 `cd`，因为 `cd` 不接受来自标准输入（standard）的内容。`S1` 和 `S2` 是代表第一个和第二个命令行参数的变量（第333页）。第一对括号创建一个子壳来运行前两个命令，这是必要的，因为这样用户可以使用相对路径调用 `cpdir`。如果没有这些括号，第一条 `cd` 命令将更改脚本的工作目录（随之，也会更改第二条 `cd` 命令的工作目录），而使用括号时，更改的是子壳的工作目录。

```bash
bash cat cpdir
(cd $1; tar -cf - & (cd $2; tar -xf -))
bash cpdir/home/alex/sources /home/alex/memo/biblio
```

上述命令行将 `/home/alex/sources` 目录下的文件和子目录复制到指定的 `/home/alex/memo/biblio`。此 shell 脚本与带有 `-r` 选项的 `cp` 相同。关于子壳的更多信息请参阅第二部分。关于 `cp`（第692页）和 `tar`（第872页）的更多信息。

## 重定向标准错误

第5章涵盖了标准输出的概念，并解释了如何将命令的输出重定向到另一个地方：标准错误。除了标准输出外，命令还可以将其输出发送到地方。命令可以将消息发送到标准错误，以防止它们与发送到标准输出的信息混杂。与标准输出一样，除非你重定向，否则 shell 将命令输出发送到终端。除非你重定向其中之一，否则你可能不知道命令发送到标准输出的输出与发送到标准错误的输出之间的区别。

当你执行程序时，运行的进程会打开三个文件描述符，程序向这些地方发送输入输出：0（标准输入）、1（标准输出）和 2（标准错误）。重定向输出符号 `>` 是 `>1` 的简写，它告诉 shell 重定向标准输出。同样，`<` 是 `<0` 的简写，重定向标准输入。符号 `>2` 重定向标准错误。程序并不“知道”它的输入来自哪里，也不知道它的输出去向哪里；由 shell 负责。更多信息，请参见第487页的“文件描述符”。

## 重定向标准错误 309

以下示例演示了如何将标准输出和标准错误重定向到同一个文件。当你运行 `cat` 以及一个不存在的文件名和一个存在的文件名时，它会将错误消息发送到标准错误，并将存在的文件复制到标准输出。除非你重定向它们，否则消息都会出现在终端上。

```bash
bash cat y
This is y.
bash cat x y
cat: x: No such file or directory
```

（注：上述 OCR 输出包含一些重复和乱码文本。我已根据源文本进行了处理。）

# 作业控制 311

后台作业。在下面的示例中，`jobs` 没有显示消息，因为你当前没有运行的后台作业。

```bash
bash$ jobs
bash$
```

## 使用 fg 将作业调至前台

如第 305 页所述，shell 会为你在后台运行的任何命令分配一个作业号。在接下来的示例中，在后台启动了几个作业。对于每个作业，shell 在显示提示符之前会列出作业号和 PID 号。

```bash
bash$ xman &
[1] 1246
bash$ date &
[2] 1247
bash$ Sat Dec 7 11:44:40 PST 1996
      date
[2]+ Done
bash$ find /usr -name ace -print > found &
[2] 1269
bash$ jobs
[1]- Running         xman &
[2]+ Running      find /usr -name ace -print > found &
```

`jobs` 命令列出作业列表，`xman` 列为作业 1。`date` 命令没有出现在 `jobs` 中，因为它在运行 `jobs` 之前已经完成了。由于 `date` 命令在运行 `find` 之前完成，`find` 命令变成了作业 2。

要将作业移动到前台，请使用内置命令 `fg`，并以百分号（%）加上作业号作为参数。下面的示例将作业 2 移动到前台：

```bash
bash$ fg %2
```

你也可以通过在百分号后跟一个能够唯一标识作业启动命令行开头的字符串来引用作业。例如，与上面的命令相比，你可以使用 `fg %find` 或 `fg %%%%`，因为其中任何一个都能唯一标识作业 2。如果你在百分号后跟一个问号（?）和一个字符串，则该字符串将匹配命令行中的任何位置。在上面的示例中，`%?case` 也指向作业 2。

通常，你希望调入前台的作业是后台运行的唯一作业。在这种情况下，你可以在不带任何参数的情况下使用 `fg`。

## 使用 fg 将作业放入后台

要将当前的前台作业放入后台，你必须先按下 `CONTROL-Z` 或 `CONTROL-Y` 来挂起作业。按下 `CONTROL-Z` 会立即停止作业；`CONTROL-Y` 会导致作业继续运行直到尝试从终端读取输入，此时作业会被挂起。一旦你使用内置命令 `bg` 恢复作业执行，它就会进入后台。

```bash
bash$ bg
```

## 312 第 10 章：再次 Bourne Shell

如果后台作业尝试从终端读取内容，shell 会停止它（将其置于睡眠状态——见第 94 页和 316 页）并通知你作业已停止并正在等待输入。当发生这种情况时，你必须将作业移动到前台，以便它可以从终端读取。shell 在将作业移到前台时会显示命令行。

```bash
bash$ sleep 5; cat > mytext)
[1] 1234
bash$ date
Sat Dec 7 11:58:20 PST 1996
[1]+ Stopped (tty input) (sleep 5; cat > mytext)
bash$ fg
(sleep 5; cat > mytext)
记得让 cat 出来！
CONTROL-D
bash$
```

在此示例中，shell 在作业启动后立即显示该后台作业的作业号和 PID 号，然后显示提示符。此时，用户输入 `date`，其输出出现在屏幕上。shell 直到它发出提示符（在 `date` 完成后）才会通知你作业 1 正在等待输入。这是因为该通知不会中断你的工作——这是 shell 的默认行为。当作业进入前台后，输入完成（随后按 `CONTROL-D` 表示文件结束），shell 会显示另一个提示符。

shell 会持续向你通报作业状态的变化：当后台作业启动、完成或等待从终端获取输入时，它会通知你。当一个前台作业被挂起时，它也会让你知晓。由于关于后台运行作业的通知可能会中断你的工作，shell 会延迟这些通知，直到准备好显示下一个提示符。请参阅第 336 页了解如何更改 shell 的行为，以便在作业状态发生变化时立即收到通知。

如果你在有已停止作业的情况下尝试退出 shell，shell 会给出一个警告且不允许你退出。如果你在警告之后使用 `jobs` 检查作业列表或再次尝试退出 shell，shell 将允许你终止和已停止的作业。在后台运行（未停止）的作业将继续运行。在下面的示例中，在第二次退出终止了 shell 后，`find` 作业 1 继续运行，而 `cat`（作业 2）被终止了。（GNU `find` 不需要 `-print` 选项。）

```bash
bash$ find -size +100k ~/bigfiles2>&1
[1] 1426
bash$ cat > mytext &
[2] 1428
bash$ exit
exit
```

有已停止作业。

- [2]+ Stopped (tty input) cat > mytext
bash$ exit

login:

## 目录栈操作 313

通过 bash，你可以存储一个你正在操作的目录列表，使你能够在它们之间轻松移动。该列表被称为栈（stack）。你可以将其想象成一叠盘子，你通常从顶部添加或移除盘子。

## 使用 dirs 显示栈的内容

`dirs` 显示目录栈的内容。如果目录栈为空时调用 `dirs`，它将显示工作目录的名称。该命令使用波浪号（`~`）表示用户的家目录。接下来的节中的示例假设你指的是图 10-1 所示的目录结构。

## 使用 pushd 将目录推入栈

为了在切换目录的同时向栈的顶部添加新目录，请使用内置命令 `pushd`。接下来的示例如图 10-2 所示：

```bash
54 > pushd ../demo
~/demo
55 > pwd
/home/scott/demo
56 > pushd ../names
~/names
57 > pwd
/home/scott/names
58 >
```
示例中使用的目录结构

## 314 第 10 章：再次 Bourne Shell

当你不带参数使用 `pushd` 时，它会交换栈中的两个目录，并将新的顶部目录（第二个目录）变为工作目录。此操作如图 10-3 所示。

```bash
58 > pushd demo
~/library
59 > pwd
/home/scott/demo
```

通过这种方式使用 `pushd` 可以轻松在两个目录之间移动。要访问栈中的另一个目录，请带百分号的数字参数调用 `pushd`。栈中的目录从顶部目录（数字 0）开始嵌套：

```bash
60 > pushd +2
~/library ~/demo
61 > pwd
/home/scott/library
```

## 使用 popd 从栈中移除目录

从栈中移除目录，请使用内置命令 `popd`。图 10-4 显示，不带参数的 `popd` 会从栈中移除顶部目录并将工作目录改为新的顶部目录。

```bash
bash$ popd demo ~/names
bash$pwd
/home/scott/demo
```

要移除栈中除顶部以外的目录，请带百分号的数字参数使用 `popd`。如果你移除的是栈上的 0 号目录，此命令不会更改工作目录。

```bash
bash$ popd +1 ~/demo
bash$pwd
/home/scott/demo
```

## 进程

进程是 Linux 执行命令。登录时启动的 shell 是一个命令，也是一个进程。每你在命令行给出 Linux 工具的名称时，就会启动进程。当你运行 shell 脚本时，会启动另一个进程，并为脚本中的每个命令创建额外的进程。取决于你如何调用 shell 脚本，脚本由新 shell 或当前 shell 的子 shell 运行。当你从命令行或脚本内部运行如 `cd` 等内置命令时，不会启动进程。

## 进程结构

与文件结构一样，进程结构也是层次化的。它有父进程、子进程甚至根进程。父进程派生子进程，子进程也可以派生其他进程（你也可以使用 `spawn`；两者通用）。Fork 是创建新进程的操作程序或系统调用的名称。机器启动时 Linux 执行的任务之一是启动一个名为 `init` 的进程号 1 进程。该进程在进程结构中的位置与文件结构中的根目录相同。它是每个用户使用的进程的祖先。如果系统连接了终端，它为每个终端派生一个进程，等待用户登录。登录的操作将进程最终转换为用户的 shell 进程。

## 进程标识

Linux 在每个进程创建时分配一个唯一的标识号（PID）。只要进程存在，它就保留该 PID。在一个会话期间，进程始终在执行登录 shell。当你运行一个新进程时（例如，使用编辑器时），新的（子）进程的 PID 号与其父进程不同。当你回到 shell 时，你会发现它仍然由同一个进程执行，并且 PID 与登录时相同。

下面的交互显示了运行 shell 的进程（是 `ps` 进程的父进程）。当你带 `-l` 参数调用 `ps` 时，它会显示关于每个进程的详细列表。`ps` 输出中 `COMMAND` 列为 `bash` 的该行指向运行 shell 的进程。名称前的连字符（-）表示这是由登录 shell 启动的。PID 列显示 PID 号。PPID 列显示 PPID 号，你可以看到运行 shell 的进程（PID 88）是运行 `ps` 的进程（PID 4516）的父进程：`ps` 的父 PID 与 shell 的 PID 号相同。参阅第二部分第 826 页获取有关进程及其 `-l` 参数显示的所有列的更多信息。

```bash
ps -l
F UID PID PPID NI SIZE RSS WCHAN STAT TTY TIME COMMAND
0 402 88 1 0 344 336 11000c S p 3 0:00 -bash
0 402 4516 88 27 0 140 296 0 R p 3 0:00 -l
```
