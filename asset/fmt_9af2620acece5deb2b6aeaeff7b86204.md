
这种结构被称为“管道”（pipeline）。我们将在第 15 和 16 章中讨论它。

## 使用 Shell：变量与选项

| SHELLS | 变量 | 含义 |
| --- | --- | --- |
| B K . | `CDPATH` | `cd` 命令搜索的目录 |
| B K . T | `COLUMNS` | 屏幕或窗口的宽度（以字符为单位） |
| B K C T | `EDITOR` | 默认文本编辑器 |
| B K . | `ENV` | 环境变量文件名 |
| B K . | `FCDIT` | 历史列表：`fc` 命令使用的编辑器 |
| B K . | `HISTFILE` | 历史列表：用于存储命令历史的文件名 |
| B K . | `HISTSIZE` | 历史列表：要存储的最大行数 |
| B K C T | `HOME` | 你的家目录 |
| B . T | `HOST` | 你的计算机名称 |
| B . T | `HOSTYPE` | 计算机类型 |
| B . . | `IGNOREEOF` | 在结束 shell 之前忽略的 eof 信号 (^D) 数 |
| B K C T | `LOGNAME` | 当前用户 ID |
| B . T | `MACTYPE` | 系统描述 |
| B K C T | `MAIL` | 检查新邮件的文件 |
| B K C T | `MAILCHECK` | shell 检查新邮件的间隔（秒） |
| B K . | `MAILPAT` | 检查新邮件路径 |
| B K . | `OLDPWD` | 你之前的的工作目录 |
| B . T | `OSTYPE` | 操作系统系统的描述 |
| B K C T | `PAGER` | 显示数据的默认程序（通常是较小的） |
| B K C T | `PATH` | 搜索程序的目录 |
| B K . | `PS1` | 你的 shell 提示符（通过更改此变量自定义） |
| B K . | `PS2` | 用于延续行的特殊 shell 提示符 |
| B K C T | `PWD` | 你的[当前]工作目录 |
| B K . | `RANDOM` | 0 到 32,767 之间的随机数 |
| B K . | `SECONDS` | 自 shell 被调用以来的时间（秒） |
| B K C T | `SHELL` | 你的登录 shell 路径 |
| B K C T | `TERM` | 你正在使用的终端类型 |
| B K . | | 如果你不输入命令，到自动注销的秒数 |
| B C T | `TZ` | 时区信息 |
| B K T | `USER` | 当前用户 ID |
| B K C T | `VISUAL` | 默认文本编辑器（覆盖 `EDITOR`） |

图 12-2：最重要的环境变量

默认情况下，Unix 系统使用大量的环境变量。你在系统中发现的内容取决于你正在使用的操作系统和 shell。

最左侧的一列显示了哪些 shell 支持每个变量：B = Bash；K = Korn Shell；C = C-Shell；T = Tch。点（.）表示该 shell 不支持该选项。

显示环境变量：`env`, `printenv`

## 第 12 章

### 显示 shell 变量：`set`

要显示所有 shell 变量及其值，你可以使用不带任何选项或参数的 `set` 命令：

```
set
```

此命令非常简单，适用于所有 shell。然而，有一个重要的点需要记住。

对于 C-Shell 家族，你看到的 shell 变量名称都是小写的。根据定义，它们是局部变量。

对于 Bourne shell 家族，shell 变量名称都是全大写的。然而，你无法仅通过名称判断特定变量是局部变量还是全局变量。如果它是 shell 变量，它就是局部的；如果它既是 shell 变量又是环境变量，那么它既是局部的也是全局。（记住，在 Bourne shell 家族中，没有纯粹的全局变量。）这意味着当你使用 `set` 列出变量时，没有简单的方法知道哪些还没有导出到环境中。

> 提示
> 奇妙的是：确定 Bourne shell 变量未导出的唯一方法是将 `set` 的输出与 `env` 的输出进行比较。如果一个变量被 `set` 列出但未被 `env` 列出，它是一个 shell 变量。如果该变量被 `set` 和 `env` 都列出，它既是 shell 变量也是环境变量。

显然，这很令人困惑。但这并不重要，因为 Bourne shell 家族并不使用 shell 变量。为了保险见，当你编写脚本时，你会根据需要创建局部（shell）变量。但对于日常交互式工作，重要的是环境变量，而不是 shell 变量。

在 C-Shell 家族中，情况不同。有大量的 shell 变量，其中许多用于控制 shell 的行为。早些我提到了其中几个：`cwd`, `home`, `term` 和 `user`。作为参考，图 12-3 显示了这些变量，以及我认为最重要的其他变量。完整列表请参见附录 G。（事实上，你现在可能想花点看看 C-Shell 家族实际上使用了多少 shell 变量）。

这给我们留下了一个问题。C-Shell 家族使用变量来控制 shell 的行为，那么 Bourne shell 家族使用什么？答案是：一个名为“shell options”的简单系统，我们将在本章后面的部分讨论。不过首先，我们需要涵盖一些与使用变量相关的基本概念。

### 显示和使用变量的值：`echo`, `print`

如果你想一次显示所有环境变量的值，可以使用 `env` 或 `printf` 命令。如果你想显示所有 shell 变量，可以使用 `set`。然而，在很多时候，你想要显示单个变量的值。在这种情况下，使用 `echo` 命令。

`echo` 命令的作用是显示你提供的任何内容的值。例如，如果你输入：

```
echo
```

> 提示
> 当你使用 `echo` 命令显示标点符号时，请使用双引号告诉 Shell 不要将这些标点符号解释为元字符。

当你使用 `echo` 命令时，你有很大的灵活性。例如，你可以显示多个变量：

```
echo $HOME $TERM $PATH $SHELL
```

如果你想使用一个与其相邻字符相连的变量，必须使用大括号来界定。例如，假设变量 `ACTIVITY` 的值为 `surf`。
命令：

```
echo "My favorite sport is ${ACTIVITY}"
```

将显示：

My favorite sport is surfing-

> 提示
> 如果你编写脚本，你会发现自己经常使用 `echo` 命令。花点时间查看一下 man页（`man echo`），在那里你可以找到许多用于控制输出格式和内容的选项和功能。

> 给 KORN SHELL 的提示
> 所有的 Shell 都允许你使用 `echo` 命令显示文本和变量。在 Korn shell 中，你还可以使用 `print` 命令：
```
print "The terminal type is $TERM"
```
Korn shell 的开发者 David Korn（参见第 11 章）创建了 `print` 来取代 `echo`。这样做是因为当时 Unix 的两个主要版本 System V 和 BSD（第 2 章）使用的 `echo` 特性略有不同。这意味着使用 `echo` 的脚本并不总能在系统之间进行移植。
为了解决这个问题，Korn 设计了 `print` 可以在所有系统上运行。这在今天已经不像在 Korn 时代那样是一个问题了。尽管如此，如果你编写一个已知将在多台计算机上运行的 Korn 脚本，使用 `print` 而不是 `echo` 是明智的。

### BOURNE SHELL 家族：使用变量：`export`, `unset`

在 Bourne shell 家族中，创建变量很容易。你只需要输入一个名称，后面跟一个 `=`（等号）字符，然后是一个值。该值必须是一个字符字符串。语法为：

```
NAME=value
```

正如我之前提到的，变量名可以使用字母、数字或下划线（`_`）。然而，变量名不能以数字开头。
你可以尝试这个示例（如果需要，可以使用你自己的名字）。注意不要在等号周围加上空格：

```
HARLEY=cool
```

当你用这种方式创建一个变量时，我们称之为 **SET**（设置）它。因此，我们可以说之前的示例设置了变量 `HARLEY` 并给它赋值为 **cool**。
如果你想使用包含空格（空格或制表符；参见第 10 章）的值，请将该值放在双引号中：

```
WEEDLY="a cool cat"
```

一旦变量存在，你可以使用相同的语法来更改它的值。例如，一旦你创建了 `HARLEY`，你可以使用以下命令将其值从 **cool** 更改为 **smart**：

```
HARLEY=smart
```

在 Bourne shell 家族中，每个新变量自动成为 shell 变量。要将变量导出到环境中，你使用 **export** 命令。输入 **export 后跟一个或多个变量的名称**。以下示例导出了 **HARLEY** 和 **WEEDLY**：

```
export HARLEY WEEDLY
```

现在，**HARLEY** 和 **WEEDLY** 都从 shell 变量变为了 shell+环境变量变量。
正如我们在第 10 章中讨论的，你可以通过分号分隔在同一行输入多个命令。因为创建变量并立即导出它是很常见的操作，所以同时输入这两个命令是有意义的，例如：

```
P=less; export PAGER
```

这比输入两个独立的命令要快，你也会经常看到这种模式，特别是在 Unix 文档和 shell 脚本中。然而，还有一种更好的方法。**export** 命令实际上允许你在设置变量的同时将其导出。语法为：

```
export NAME=[value]...
```

这里有一个简单的示例：

```
export PAGER=less
```

仔细观察语法。注意，**export** 允许你指定一个或多个变量，每个变量都可能带有一个值。因此，你可以通过一个命令完成很多工作：

```
export HARLEY WEEDLY LITTLENIPPER

export PAGER=less EDITOR=vi PATH=/usr/local/bin:/usr/bin:/bin
```

> 提示
> 通常情况下，老 Unix 用户倾向于快速思考。因此，他们青睐越越于输入的命令。出于这种原因，设置和导出变量的首选方法是使用单个命令：
```
export PAGER=less
```
尽管许多人使用两个命令来设置和导出变量，但使用单个命令完成双重工作会标志着你是一个聪明且与众的人。

正如我提到的，当你创建一个变量时，我们称之为你 **set** 了它。当你删除一个变量时，我们称之为你 **unset**（取消设置）。你很少需要 unset 一个变量，但如果有需要，可以使用 `unset` 命令来完成。语法非常简单：

```
unset NAME...
```

这里有一个示例：

```
unset HARLEY WEEDLY
```

> 提示
> 有趣的是，在 Bourne shell 家族中，没有简单的方法从环境中移除变量。一旦变量被导出，取消导出的唯一方法就是将其 unset 。换句话说，唯一的方法是……

### C-SHELL 家族：使用变量：`setenv`, `unset`, `set`, `unset`

在 C-Shell 家族中，环境变量和 shell 变量之间存在区别。要设置环境变量，你使用 `setenv` 命令。语法为：

```
setenv NAME [value]
```

其中 NAME 是变量名；value 是你想要设置的值。注意，与 Bourne shell 不同，我们不使用 `=`（等号）字符。

这里是一些示例：

```
setenv PATH /usr/local/bin:/usr/bin:/bin

setenv HARLEY cool

setenv WEEDLY "a cool cat"

setenv LITTLENIP
```

前三个命令设置了变量并赋予它们值。在第三个示例中，我们使用双引号包含空格。在最后一个示例中，我们指定了一个没有值的变量名（LITTLENIP）。这会创建一个空值的变量。要取消环境变量，你使用 `unsetenv` 命令。语法为：

```
unsetenv NAME
```

其中 NAME 是变量名。例如，要取消（删除）变量 `HARLEY`，你可以使用：

```
unsetenv HARLEY
```

要设置 shell 变量，你使用 `set` 命令，语法如下：

```
set name=[value]
```

其中 name 是 shell 变量的名称；value 是你想要设置的值。

这里有几个示例：

```
set term=vt100

set path=/usr/bin /usr/ucb

set ignoreeof
```

第一个示例非常直观。我们设置的是 shell 变量 `term` 的值为 `vt100`。

第二个示例说明了一个重要的点。当你使用 C-Shell 家族的变量时，有时需要将一组字符字符串放在括号内。这样做时，它定义了一个可以单独访问的字符串集。在这种情况下，`path` 的值被设置为括号内的三个字符字符串。

在最后一个示例中，我们指定了一个没有值的 shell 变量。这种情况下，变量 `ignoreeof` 的存在会让 shell 忽略 eof 信号。这要求我们使用 `logout` 命令来结束 shell。（参见第 7 章。）

一旦 shell 变量存在，你可以通过 `unset` 命令来删除它。语法为：

```
unset variable
```

其中 variable 是变量的名称。例如，如果你想告诉 shell 关闭 `ignoreeof` 功能，你可以使用：

```
unset ignoreeof
```

`unset ignoreeof`

请确保你理解将变量设置为空与删除变量之间的区别。请考虑以下三条命令：

```bash
set harley=cool

set harley

unset harley
```

第一条命令创建了一个名为 harley 的 shell 变量，并赋予它值 cool。第二条命令将 harley 的值设置为空。最后一条命令则完全删除了该变量。

### Shell 选项：`set -o`, `set +o`

正如之前讨论的，在 C-Shell 家族中，我们使用 shell 变量来控制 shell 行为的各个方面。在 Bourne shell 家族中，我们使用 SHELL OPTIONS（shell 选项）。例如，我们使用选项来控制 shell 是交互式的还是非交互式的。

Shell 选项就像开启/关闭开关。当你开启一个选项时，我们称为你 **SET**（设置）了它。这告诉 shell 以某种方式运行。当你关闭一个选项时，我们称为你 **UNSET**（取消）了它。这告诉 shell 停止那种方式运行。

例如，shell 支持一种名为“作业控制”（job control）的功能，让你能在后台运行程序。（我们将在 26 章讨论这一点。）要开启作业控制，请设置 monitor 选项。如果你想关闭作业控制，请取消 monitor 选项。默认情况下，交互式 shell 的 monitor 是开启的。

> 提示 “set”和“unset”这两个词的含义取决于我们是在论论选项还是变量。

Shell 选项要么关闭，要么开启；它们不需要被创建。那么，当我们设置一个 shell 选项时，我们是开启了它。当我们取消一个选项时，我们是关闭了它。

变量则不同。当我们设置一个变量时，我们实际上是在创建它。当我们取消一个变量时，我们是删除了它。

shell 选项有两种设置或取消的方法。首先，在 shell 启动时，可以用通常的方法指定选项，即通过命令指定一个或多个选项（参见第 10 章）。例如，以下命令启动了一个带有 monitor 选项（已开启）的 shell：

```bash
ksh -m
```

除了标准的命令行选项外，还有另一种开启和关闭 shell 选项的方法，即使用 `set` 命令的变体。语法如下。要设置一个选项，使用：

```bash
set -o option
```

要取消一个选项，使用：

```bash
set +o option
```

其中 *option* 是选项的“长名称”（参见图 12-4）。例如，假设 shell 正在运行，且你想设置 monitor 选项。使用：

```bash
set -o monitor
```

要取消 *monitor* 选项，使用：

```bash
set +o monitor
```
