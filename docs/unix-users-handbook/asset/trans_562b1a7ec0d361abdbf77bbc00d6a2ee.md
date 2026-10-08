

CLEARCASE_BLD UMASK=02
_INIT_UTS_PLATFORM=SUNW,SPARCstation-10
marty$ 

正如你所见，除了 PATH 之外，其他环境变量也能让你在使用 UNIX 系统时更加便捷。你可能还需要执行与 ksh 变量相关的其他命令。表 6-4 总结了您可能需要在系统中执行的一些与 ksh 相关的变量命令。

![](img/75f39fc91296b889c0653851accdfd46_356_0.png)

# 表 6-4  ksh 相关变量命令

| 命令 | 描述 |
| :--- | :--- |
| **env** | 列出所有环境变量（已导出）。这些变量通常是大写的，并传递给子进程。 |
| **set** | 打印所有本地和已导出的 set 变量。 |
| **set -o** | 列出所有设置为 *on* 或 *off* 的内置变量。 |
| **typeset** | 显示所有变量及其关联属性、函数和整数。 |
| **typeset +** | 仅显示变量的名称。 |

您可能希望在系统中尝试所有这些命令，以查看为您设置了哪些变量。

如果您想知道特定环境变量的值，可以使用 echo 命令来查看其值，如下所示的环境变量 HOME 的示例：

```
marty$ echo $HOME
/home/marty
```

同样，若要查看这台特定计算机的操作系统类型，您可以执行以下命令：

```
martyp $ echo $OSTYPE
solaris2
```

环境变量名称前的“$”指定将该变量的值发送到标准输出。在这种情况下，环境变量 $HOME$ 的值为 $/home/marty$，这意味着当前用户的主目录为 $/home/marty$。

您可以使用以下语法在 **ksh** 中定义自己的环境变量：

![](img/75f39fc91296b889c0653851accdfd46_357_0.png)

```
export NAME=value
```

许多用户喜欢自定义 **ksh** 提示符。大多数系统默认提供四个 **ksh** 提示符。通常您可以修改前两个提示符。第一个称为 **PS1**，是主提示符。第二个称为 **PS2**，在您部分输入命令并按下 *enter* 键后出现。默认情况下，**PS1** 设置为 $，**PS2** 设置为 >。

以下示例将 **PS1** 设置为我们主目录、一个空格、当前历史记录编号、一个空格以及美元符号：

```
PS1="`pwd` ! $ "
```

![](img/75f39fc91296b889c0653851accdfd46_357_1.png)

我们将 **PS2** 保持为默认的 >。以下序列展示了在新的 **PS1** 提示符下发出命令以及默认的 **PS2** 提示符：

```
/home/marty 187 $ print "This is new PS1
> but default PS2"
This is new PS1
but default PS2
/home/marty 188 $
```

此示例展示了新的 **PS1**，包括历史记录条目从 187 增加到 188，以及当发出未完成的 **print** 命令时的默认 **PS2**。

您还可以使用以下格式在现有变量的末尾追加内容：

```
export NAME="$NAME:appended_information"
```

例如，若要向现有的 *PATH* 环境变量添加 **/home/marty/programs**，您执行以下命令：

```
export PATH="$PATH:/home/marty/programs"
```

这将路径 **/home/marty/programs** 追加到环境变量 *PATH* 中。

在处理 **ksh** 时有很大的灵活性。您应该查看您的所有变量，并更新那些让工作更轻松的变量。一些自定义设置，如更新 **PS1** 和您的 **PATH**，也可以让工作更轻松。

![](img/75f39fc91296b889c0653851accdfd46_358_0.png)

## 后台作业和作业控制

当您运行命令时，正如我们在前面的许多示例中所做的那样，在命令完成之前，您无法返回提示符。这些命令是在前台运行的。某些命令可能需要很长时间才能完成，在这种情况下，您将等待很长时间的提示符返回。作为等待提示符返回的替代方案，您可以在后台运行命令，这意味着它在幕后运行，同时您可以执行其他工作。由于 UNIX 是多任务操作系统，它很高兴在后台运行许多命令，同时仍然为您提供提示符以发出更多命令。

要在后台运行命令，只需在命令行的末尾添加一个 ampersand (&) 即可。当您在命令后加上 ampersand 时，命令将在后台运行，提示符会立即返回。

现在让我们在我们的 Solaris 系统上运行一些命令。我们首先运行一个命令来查找 **/usr** 中所有以 ".c" 结尾的文件，这需要一些时间才能完成。我们将在 **find** 字符串前加上 **time** 命令，以便我们知道命令完成需要多长时间：

![](img/75f39fc91296b889c0653851accdfd46_359_0.png)

```
marty $ time find /usr -name \*.c
      :
      :
      :
      :
/usr/demo/link_audit/src/dumpbind.c
/usr/demo/link_audit/src/env.c
/usr/demo/link_audit/src/hash.c
/usr/demo/link_audit/src/perf_cnt.c
/usr/demo/link_audit/src/symbindrep.c
/usr/demo/link_audit/src/truss.c
/usr/demo/link_audit/src/who.c
find: cannot read dir /usr/aset: Permission denied

real    1m21.04s
user    0m1.51s
sys     0m12.67s
```

该命令花费了大约 1 分 21 秒完成。由于是在前台运行，在命令运行期间我们无法发出其他任何命令，因为我们要等待提示符返回。

在前台运行命令的替代方案是在命令后加一个 ampersand 来发出命令，在这种情况下，作业将在后台运行，提示符会立即返回，如下例所示：

```
marty $ time find /usr -name \*.c > cprogs 2>&1 &
[3]  16279
marty $
real    2m10.20s
user    0m1.31s
sys     0m8.62s
```

在后台运行此命令的结果会产生一个括号内的作业编号，以及进程 ID（PID），即第二个数字。该命令的所有输出，包括错误，都写入文件 cprogs。在发出命令后，提示符立即返回，完成后，time 的输出发送到屏幕上。我们在后台发出命令后，本可以立即开始发出额外的命令。

您可以控制前台作业和后台作业。要挂起前台作业，您同时按下 "control" 和 "z" 键，如下例所示：

```
marty $ find /usr -name *.c
/usr/openwin/share/include/X11/Xaw/Template.c
/usr/openwin/share/src/dig_samples/DnD/main.c
/usr/openwin/share/src/dig_samples/DnD/owner.c
/usr/openwin/share/src/dig_samples/DnD/requestor.c
/usr/openwin/share/src/dig_samples/Tooltalk/olit_tt.c
/usr/openwin/share/src/dig_samples/Tooltalk/tt_callbacks.c
/usr/openwin/share/src/dig_samples/Tooltalk/tt_code.c
/usr/openwin/share/src/dig_samples/ce1/ce_mapl.c
/usr/openwin/share/src/dig_samples/ce2/ce_simple.c
/usr/openwin/share/src/dig_samples/dnd_olit/oltdnd.c
/usr/openwin/share/src/dig_samples/dnd_xview1/xview_dnd.c
/usr/openwin/share/src/dig_samples/dnd_xview2/xview_dnd2.c
/usr/openwin/share/src/dig_samples/selection_olit/olit_sel.c
/usr/openwin/share/src/dig_samples/tooltalk_simple/tt-send.c
/usr/openwin/share/olit/oldials/oldials.c
/usr/openwin/share/olit/olitbook/ch10/draw.c
^Z[3] + Stopped (SIGTSTP) find /usr -name *.c
```

按下 ctrl-z 后，find 命令在您输入 ctrl-z 的时刻被中断。此时命令被挂起，您将看到作业编号，在此例中为 "3"，其状态列为 "Stopped"。该命令只是被挂起，并没有永远消失。您可以使用 fg 在前台启动此进程，或使用 bg 在后台运行它。使用 bg 运行命令的效果就像您在后面加了一个 "&" 一样。它将从您中断的地方开始运行

![](img/75f39fc91296b889c0653851accdfd46_360_0.png)

![](img/75f39fc91296b889c0653851accdfd46_361_0.png)

您不需要在发出 **fg** 或 **bg** 命令时提供作业编号，因为默认是对最后一个作业执行指定操作，在此例中是作业编号 3。

请注意，在此示例中我们停止了编号为 3 的作业。这意味着还有其他编号更低的作业正在运行。您可以使用 **jobs** 命令获取所有作业及其状态的列表。然后，您可以通过发出如 **fg** 后跟 "%" 和作业编号在前台运行命令，或 **bg** 后跟 "%" 和作业编号在后台运行命令来控制这些作业。如果您希望完全终止某个作业，您可以发出 **kill** 命令，后跟 "%" 和作业编号。

在创建本节示例的过程中，我已经启动并挂起了许多作业。以下示例展示了使用 **jobs** 命令列出所有作业，使用 **kill** 终止作业 1 和 2，以及在后台运行作业 3：

```
marty $ jobs
[3] + Stopped (SIGTSTP)  find /usr -name *.c
[2] - Running              time find / -name gnu* > gnu 2>&1 &
[1]   Running              time find / -name *.c > cprogs 2>&1 &
marty $ kill %1
[1]  Terminated            time find / -name *.c > cprogs 2>&1 &
marty $ kill %2
[2] - Terminated           time find / -name gnu* > gnu 2>&1 &
marty $ bg %3
[3]    find /usr -name *.c &
marty $
```

请注意，当我们要求作业 3 在后台运行时，添加了 ampersand。终止作业 1 和 2 并在后台运行作业 3 会返回提示符，以便您可以执行额外的工作。

![](img/75f39fc91296b889c0653851accdfd46_361_1.png)

## umask 和权限

与 **ksh** 相关的另一个需要涵盖的主题是文件权限以及它们与 **umask** 的关系。这很重要，因为您可能写

![](img/75f39fc91296b889c0653851accdfd46_361_2.png)

