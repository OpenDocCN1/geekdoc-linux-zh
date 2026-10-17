
```
GNU bash, version 1.16.6(1)
内部定义的 shell 命令。输入 'help' 查看此列表。
输入 'help name' 了解更多关于函数 'name'的信息。
使用 'info bash' 了解更多关于 shell 的通用信息。

名称旁边的 (*) 表示该命令已禁用。
%[DIGITS | WORD] [&] [filename]
: [arg...]
alias [name=value] ...] bg [job_spec]
bind [-lvd] [-m keymap] -f filename break [n]
builtin [shell-build [arg ...] case WORD in [PATTERN] [[PATTERN]].
cd dir command [arg ...]
continue [n] declare [[-frxi]] name=[value] 
dirs [-1] echo [-neE] [arg ...]
enable [-n] [name ...] eval [arg ...]
exec [-] file [redirection ...] exit [n]
export [-n] [-f] [name ... ] or exp fc [-name] [-nlr] [first] [last
fg (job_spec) for NAME [IN WORDS ...]; do ,
function NAME ( COMMANDS ; ) or na getopts optstring name [arg]
hash [-r] [name ... ] help [pattern ...]
history [n] [-awn] [filename] if COMMANDS; then COMMANDS; (elif
jobs [-n] [Jobspec ...] | jobs - kill [-s sigspec] [-sigspec] [pid
let arg ... ] local name [value]
logout popd [+n] | -n]
pushd [dir | +n | -n]
read [-name ... ] readonly [-n] [-f] [name ...] or r
return [-n] select NAME [in WORDS ...]; do CD
set [-abefhknotuxvdHCP] -o opt shift [n]
source filename suspend [f]
test [expr] times
trap [arg] [signal_spec] type [-all] [-type -path] [name
typeset [-frxii] name[value] ... ulimit [-Shacdmstpnuv [limit]]
umask [-S] alias [a] [name ...]
unset [-v] [name ... ] until COMMANDS; do COMMANDS; done
variables - Some variable names wait [n]
while COMMANDS; do COMMANDS; done ( COMMANDS )
```

# Elvis 文本编辑器

在 Linux 中，文本编辑的工作由几个不同的编辑器承担，它们在功能上差异很大。正如你从第 2 章所记得的，我们提供了关于安装哪些文本编辑器的建议。接下来，我们将关注我们建议安装的编辑器之一：**elvis**（它会自动安装），而将 **emacs** 的讨论留到第 5 章，那时你对 X Window 系统 有了经验。我们不会为了 vi 或 emacs 爆发“宗教战争”，我们将对两者都进行解释。

# 使用 Elvis 文本编辑器

全屏 vi 文本编辑器是 vi 编辑器的克隆版本，它出现在大多数（但并非所有）UNIX 系统上。（因为从技术上说你并没有与其他 UNIX 系统相同的 vi，我们在这里将使用准确的术语并称之为 `elvis`。然而，每当你在命令中看到 `elvis` 时，如果你习惯使用 vi，可以将其替换为 `vi`。）

`Elvis` 用于编辑 vi (ASCII) 文件，这些文件在 Linux 操作系统中有广泛的应用——文本文件用于 shell 脚本、文本处理器的输入、电子邮件的输入以及编程源代码文件。`Elvis` 从命令行工作，你可以在不加载文件的情况下调用它：

```
gilbert:$ elvis
```

或者在加载文件的情况下：

```
gilbert:$ elvis textfile
```

在没有文件的情况下，`elvis` 的界面类似于图 4.3 所示。

![](img/05da311512608405596dd882623b9142_280_0.png)

图 4.3 未加载文件的 Elvis。

在加载文件后，`elvis` 的界面类似于图 4.4 所示。

| stgsgs |

| sg |

| sg |

| sdgsgsgs |

| sdgsgsgs |

| gsgsgsgs |

| sgsgsgsgs |

| sgsgsgsgs |

| sgsgsgsgs |

| sgsgsgs |

| sgsgsgs |

*(注：第 281 页表格的 OCR 文本似乎损坏或为占位符；根据周围内容的上下文，它代表命令列表或视觉表示，但内容无法识别。）*

## 第 4 章：基础 Linux 工具

然而，`elvis` 有一个特殊之处（顺便说一下，它与 `vi` 保持兼容）：左、右光标方向键（← 和 →）仅用于在当前文本行中移动。如果你在行尾并期望使用右光标方向键（→）移动到下一行，你会听到蜂鸣声，并且光标会卡在最后一个字符上；只有向上和向下光标方向键（↑ 和 ↓）可以在行与之间移动。

在大多数情况下，光标和翻页键应该满足你在 `elvis` 中的滚动需求。然而，你可能需要一些额外的功能，表 4.13 列出了其他实用的光标和滚动命令。

### 表 4.13 Elvis 光标与滚动命令

| 命令 | 结果 |
|---|---|
| 0 (零) | 将光标移动到当前行的开头。 |
| b | 将光标移动到当前单词的开头。 |
| ) | 将光标移动到文档末尾。 |
| $ | 将光标移动到当前行的末尾。 |
| e | 将光标移动到当前单词的末尾。 |
| w | 将光标移动到下一个单词的开头。 |
| nG | 将光标移动到第 n 行的开头。 |
| H | 将光标移动到文件的开头。 |
| G | 将光标移动到文件中最后行的开头。 |

### 撤销上一个命令

`Elvis` 可以撤销上一个命令（除非你已将文件保存到磁盘，在这种情况下所有更改都已固定）；要执行此操作，按 `Esc` 进入命令模式并输入 `u`（代表 `undo`）。

### 关于 Elvis 的更多信息

这就是你对 `elvis` 需要知道的所有内容了。老实说，并不是一个非常复杂的应用程序，考虑到你可能的文本处理需求，没有必要花费大量时间掌握它的每一个细微差别。`elvis` 还有许多其他选项，但其中大多数只对硬核用户感兴趣。要查看你可以使用 `elvis` 执行哪些额外操作，请使用以下命令行：

```
gilbert~$ elvis
```

在结束对 `elvis` 的讨论之前，我们想指出，我们在涵盖这个话题时没有开过任何关于“国王”的廉价笑话。

## 打印文件

当你安装 Linux 时，系统会提示你连接到 PC 的打印机位置。如果你像世界上 99% 的 PC 用户那样，你有一个连接到并行口的打印机。如果你在 UNIX 网络上安装 Linux，你将使用之前安装的打印机，或者根据 UNIX 打印系统设置打印机（该系统差异很大）。

在本节中，我们假设你已经在并行端口上安装了打印机并告知 Linux 这一安装。（如果情况并非如此，请查阅标准的 UNIX 文本以查看 UNIX 网络上是如何处理打印机的。）要查看 Linux 认为哪些打印机已连接到网络，请使用 `lpc`：

```
gilbert~$ lpc
lpc>
```

此命令将向你展示一系列选项。这些，在大多数情况下，这些命令都与在特定打印机上打印特定文件有关。

> 注意：本节假设你直接从命令行打印文件。其他一些应用程序——主要是 Ghostscript——会处理打印机，你将在第 5 章中学习。

你也可以使用标准的 `lpr` 命令来打印文件：

```
gilbert:/$ lpr filename
```

其中 `filename` 是你要打印的文件名。该命令将 `filename` 复制到打印队列目录，然后从那里实际打印文件。在你运行 `lpr` 命令后，你可以编辑正在打印的文件，但更改不会反映在打印的页面上。

要检查打印请求的状态，请使用 `lpq` 命令：

```
gilbert:/$ lpq
```

你将获得关于打印机的信息、待处理作业的状态（正在打印什么，下一个排队的是）以及任务 ID（job ID）。如果你想取消打印请求，这个 ID 就非常重要；对于此，你将结合任务 ID 使用 `lprm` 命令：

```
gilbert:/$ lprm
```
