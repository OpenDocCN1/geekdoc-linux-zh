
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

上面的第二个命令将次级提示符更改为 `secondary prompt: `（后面紧跟一个空格）。一个多行的 `echo` 演示了新提示符的效果。

## 第 10 章：Thene Again Shell

### CDPATH

`CDPATH` 变量允许你使用简单的文件名作为 `cd` 的参数，将工作目录更改为当前工作目录的子目录。如果你有几个不同的目录需要工作，这个变量可以提高速度并节省你不断使用较长模式 `cd` 在它们之间切换的枯燥时间。

当 `CDPATH` 未设置且你指定一个简单文件名作为 `cd` 的参数时，`cd` 会在工作目录中搜索同名的子目录。如果该子目录不存在，`cd` 会发出错误信息。当设置了 `CDPATH` 时，`cd` 会在 `CDPATH` 列表中的一个目录中搜索命名适当的子目录。如果找到了，它将成为工作目录。通过 `CDPATH`，你可以使用 `cd 简单文件名` 来将工作目录更改为 `CDPATH` 列表中任何目录的子目录。

`CDPATH` 变量取的值是一个由冒号分隔的目录路径列表（类似于 `PATH` 变量），通常在 `.bash_profile` 中通过如下命令行行进行设置：

```bash
CDPATH+=$HOME:$HOME/literature
export CDPATH
```

这导致 `cd` 在你输入命令时，先搜索你的工作目录，然后是 `literature` 目录，最后又是你的工作目录。如果你没有在 `CDPATH` 中包含所有其他目录，`cd` 会在每次搜索后搜索工作目录。如果你想让 `cd` 优先搜索工作目录，请将工作目录作为 `CDPATH` 的第一个项（以点 `.` 开头）。`csh` 和 `tcsh` 的工作方式不同，它们会自动先搜索你的目录。

```bash
CDPATH+=:$HOME:$HOME/literature
export CDPATH
```

如果 `cd` 的参数是绝对文件名——即以斜杠 `/` 开头的文件——`bash` 不会咨询 `CDPATH`。

### 使用点 Dot 命令运行 .bash_profile

在编辑 `.bash_profile` 文件以更改关键字 shell 变量的值后，你不需要等到下一次就可以让更改生效。你可以使用内置命令 `.`（点）运行 `.bash_profile`。对于所有其他命令，`.` 在命令行中必须后跟一个空格，但 `.` 是作为当前进程的一部分运行脚本的。因此，如果你使用 `.` 从登录 shell（login shell）运行脚本，你在脚本内部对变量所做的更改将影响登录 shell。你可以使用 `.` 命令运行任何 shell 脚本，而不仅仅是 `.bash_profile`，但可能会产生不良的副作用（例如你依赖的 shell 变量值发生了改变）。如果你作为普通 shell 脚本运行 `.bash_profile` 而不使用内置命令 `.`，新变量将只在运行脚本的子 shell 中生效。参见第 323 页的“Export Builtin”。

以下 `.bash_profile` 文件设置了 `TERM`、`PATH`、`PSI` 和 `CDPATH` 变量，并将行终止键设置为 `CONTROL-U`。内置命令 `.` 使新值生效。

```bash
bash cat .bash_profile
export TERM=vt100
export PATH=$usr/usr:/usr/bin:/sbin:/home/alex/bin:
```

### 参数与变量

```bash
export PS1=alex: ""
export CDPATH=$HOME
stty kill '^U'
bash$ .bash_profile
alex:
```

`source` 内置命令与 `.` 内置命令是同的。

### 位置参数

当你调用一个 shell 脚本时，位置参数是命令名和参数。它们被称为“位置”参数是因为你是根据它们在命令行上的位置来引用它们的。虽然你可以引用它们，但不能为位置参数赋值（例外情况请参见第 335 页的 `set Builtin`）。

### 调用程序的名称

shell 在 `$0` 变量中存储你用于调用程序时使用的命令名称。这个第一个命令行参数通常是脚本本身的名称。

### 命令行参数

当你引用位置参数时，请用双引号括起来。这在使用位置参数作为参数时尤为重要，因为空的位置参数会消失。

```bash
bash showwards
echo "I was called with $# arguments, the first is $1."
bash showwards $3 a
I called with 3 arguments, the first is a.
bash showwards "$3" b
I called with 4 arguments, the first is .
```

在这个示例中，`showwards` 被调用了两次。每次第一个参数看起来都是第三个。然而，它被空值替换了。在第一次，命令行显示 a b；shell 传递了三个参数。在第二次，命令行显示 `""`，导致 `showwards` 有四个参数。两次 `showwards` 的差异说明了在使用位置参数时必须注意的微妙问题。

## 第 10 章：The Again Shell

### Shift 内置命令

`shift` 命令会将命令行参数向前移动。第二个参数（之前由 `$2` 表示）变为第一个（现在由 `$1` 表示），第三个变成第二个，第四个变成第三个，依此类推。原始参数被丢弃了。由于没有 `unshift` 命令，无法找回已经丢弃的参数。

```bash
bash cat demo_shift
echo "arg1=$1 arg2=$2 arg3=$3"
shift
echo "arg1=$1 arg2=$2 arg3=$3"
shift
echo "arg1=$1 arg2=$2 arg3=$3"
shift
echo "arg1=$1 arg2=$2 arg3=$3"
shift
bash demo_shift alice helen
arg1 alice arg2=helen arg3=jenny
arg1 helen arg2=jenny arg3=
arg1 jenny arg2=arg3=
arg1= arg2=arg3=
shift: shift count must be << $
```

`shift` 是带参数调用的。在 `echo` 的参数上使用双引号可以保留输出显示。程序显示参数并反复移动它们，直到没有更多参数可以移动为止。当脚本在耗尽变量后执行 `shift` 时，shell 会显示错误信息。

### 位置参数

在原始的 Bourne Shell 中，位置参数被限制在 `$1-$9`，因此接受超过九个参数的 shell 脚本被迫使用 `shift` 获取后面的参数。Bourne Again

### 参数与变量

Shell 对位置参数的数量没有限制，因此 `shift` 的这种用法已经有所减少。然而，在期望任意数量参数的 shell 脚本中反复使用 `shift` 是遍历所有命令行参数的一种方便方法。请参阅第 374 页查看使用此技术的示例 shell 程序。

### 内置命令 set

当你带上一个或多个参数调用 `set` 内置命令时，它会将这些参数作为位置参数的值，从 `$1` 开始计数。以下脚本使用 `set` 为位置参数 `$1`、`$2` 和 `$3` 赋值：

```bash
bash$ cat set_it
set this is it
echo $2 $1
bash$ set_it
it is this
```

```-将命令替换（第 327 页）的使用与 `set` 内置命令结合起来，是一种获取命令标准输出的方便方法，并在 shell 脚本中对其进行处理。以下脚本展示了如何使用 `date` 和 `set` 以实用的格式提供日期。第一个命令使用命令替换将位置参数设置为 `date` 程序的输出。下一个命令 `echo` 显示了 `dataset` 脚本的内容。脚本中的第一个命令使用了 `*`，它代表由上一个 `set` 产生的所有位置参数。（关于 `$*` 的讨论请参见下一节）。后续命令显示了参数 `$1`、`$2`、`$3` 和 `$4` 的值。最后一个命令以适用于信函或报告的格式显示日期。你还可以使用 `date` 的 `format` 参数来修改其输出格式。关于 `date` 的更多信息，请参阅第二部分的第 709 页。

```bash
bash$ date
Sun Dec 8 14:07:38 PST 1996
bash$ cat dateset
set $(date)
echo $*
echo "Argument 1: $1"
echo "Argument 2: $2"
echo "Argument 3: $3"
echo "Argument 4: $4"
echo
echo "$2 $3, $6"
```

```bash
bash$ dateset
Sun Dec 8 14:07:42 PST 1996
```

```text
Argument 1: Sun
Argument 2: Dec
Argument 3: 8
Argument 4: 14:07:42

Dec 8, 1996
```

## 第 10 章：Bourne Again Shell

在不带任何参数的情况下，`set` 会列出已设置的 shell 变量列表。这包括作为关键字变量的用户创建的变量。这与 `declare` 在不带任何参数被调用用时提供的输出相同。

`set` 内置命令还接受许多选项，允许你自定义 `bash` shell 的行为。这些许多选项的值现在应该很清楚了；其他将在本章的剩余部分进行解释。这里列出了一些实用的选项及其影响：

- `-a export` 导致你创建或修改的每个变量都自动导出。
- `- notify` 如果任何后台作业终止，`bash` 将立即通知你，而不是等到下一次提示符再通知你。`set` 的此选项与设置 shell 变量 `notify` 的效果相同。
- `- noclobber` 与设置 shell 变量 `noclobber` 的效果相同。它可以在你使用重定向运算符 `>` 和 `>>` 时保护文件不被覆盖。
- `- nohash` 通常情况下，`bash` 将命令哈希到内存中的快速访问列表中，以便在需要执行时加快查找速度。此选项禁用了快速访问列表，使得 shell 在每次执行时都必须搜索命令。
- `- glob` 阻止 `bash` 进行文件名扩展（通配）。
- `- hextand` 开启历史扩展。此选项在交互式 shell 中默认开启。
- `- local` 使 `for` 控制结构（第 380 页）中的控制变量名对该命令是局部的，这样在执行命令后，它的值与执行命令之前的值相同。
- `- monitor` 启用作业控制（第 310 页）。此选项在交互式 shell 中默认开启。
- `- noexec` 导致 `bash` 读取并对命令进行扩展，但不执行它们。如果你想检查 shell 脚本的语法错误，此选项将大有用场；它在交互式 shell 中会被忽略。
- `- option` 允许你设置 `bash` 名称可用的其他选项。请参阅下表获取这些选项列表。在不带任何参数的情况下，此选项显示所有选项的状态。
- `- privileged` 在启动交互式 shell 时关闭对变量的评估，并忽略环境中的任何函数（通常 `bash` 子 shell 会从其父 shell 继承函数）。此选项稍微提高了安全性，通常在命令行上设置。
- `- exit Read` 执行单条命令然后退出。

### 参数与变量

- `- nounset` 当你尝试扩展未设置的变量时，导致 `bash` 返回错误。当未设置此选项时，`bash` 将未设置的变量扩展为空字符串。当设置此选项时，脚本会在未设置的变量解除绑定时终止且不执行当前命令。
- `-v` 导致 `bash` 按其读取时的 shell 形式打印输入行。
- `-x` 导致 `bash` 在扩展每个命令后显示它。这对于跟踪 shell 脚本的执行非常有用。

可以使用 `-o` 选项通过名称设置某些选项，包括以下：

- `- braceexpand` 当（默认），`bash` 执行大括号扩展（第 351 页）。
- `- emacs` 当（默认），`bash` 使用 emacs 风格的编辑。
- `- vi` 当（默认），`bash` 使用 vi 风格的命令行编辑。
- `- interactive` 当（默认），`bash` 为交互式 shell 保存历史记录。
- `- history` 当（默认），`bash` 将历史保存到文件中。此选项允许你在 shell 会话之间共享历史记录。
- `- pipefail` 当（默认），`bash` 返回管道中最后一个以非零状态退出的命令的退出状态，而不是最后一个命令。
- `- monitor` 当（默认），`bash` 为每个命令行输入启用作业控制。
- `- nilde` 当（默认），`bash` 扩展波号。
- `- extglob` 当（默认），`bash` 启用扩展通配。
- `- exthist` 当（默认），`bash` 启用历史扩展。
- `- optset` 当（默认），`bash` 使用 options 命令。
- `- wordset` 当（默认），`bash` 使用 wordset-line 命令。
- `- wordspace` 当（默认），`bash` 使用 wordspace 进行命令行编辑。
- `- wordfail` 当（默认），当未找到单词时 `bash` 返回错误。
- `- errfail` 当（默认），当未找到命令时 `bash` 返回错误。
- `- errormsg` 当（默认），当引用的函数未定义时 `bash` 返回错误。 （注：原文此处存在大量重复的 OCR 错误，译文已根据逻辑进行了去重处理）

### 参数与变量

下面的脚本示例演示了 shell 在运行脚本时会创建一个新进程。`id2` 脚本显示了正在运行的进程 PID 号（而不是它调用的进程——`$$` 的替换是由派生（fork）来运行 `id2` 的 shell 完成的）。

```bash
bash$ cat id2
echo $0 PID=$ $$
bash$ echo $$
88

bash$ id2
./id2 PID= 6292
bash$ echo $$
88
```

示例中的第一个 `echo` 显示登录 shell (S0) 的 PID 码以及 shell 的 PID。最后，最后一个 `echo` 显示当前进程再次是登录 shell。

shell 将你在后台运行的进程的 PID 码值存储在 `$!` 中。接下来的示例将 `ps` 作为一个后台任务执行，然后使用 `echo` 显示 `$! ` 的值：

```bash
bash$ ps &
[1] 6326
bash$ PID TTY TIME COMMAND
88 p J S 0:00 -bash
6326 p1 R 0:00 ps
echo $!
6326
[1]+ Done
```

尽管此示例中的提示符看起来是有序的，但事实并非如此。由于两个进程调度的可变性，两者的输出可能会以几种不同的方式交错。在这种情况下，shell 在显示后台进程的 PID 号后显示提示符。后台进程的输出紧随提示符之后。`echo` 命令是对提示符的响应，尽管该命令并没有紧接着提示符后面。如果你想在发布命令之前看到另一个提示符，可以按回车。

### 退出状态

当进程由于任何原因停止时，它会向父进程返回一个退出状态。退出状态也被称为状态码或返回码。shell 将上一个命令的退出状态存储在 `$$` 变量中。

按照习惯，非零退出状态表示假值，意味着命令失败。零表示真，且命令成功。下面，第一个 `ls` 命令成功了，而第二个失败了：

```bash
bash$ ls es
es
bash$ echo $?
0
bash$ ls xxx
ls: xxx: No such file or directory
bash$ echo $?
1
```

你可以通过使用 `exit` 内置命令后跟数字来终止脚本并指定退出状态。如果你不带数字使用 `exit` 来终止脚本，则脚本的退出状态是其运行的最后一个命令的退出状态。下面的示例显示了数字如何指定退出状态：

```bash
bash cat es
echo This program returns an exit status of 7.
exit 7
bash$ es
This program returns an exit status of 7.
bash$ echo $?
7
bash$ echo $?
```

`es` 脚本显示一条消息，然后使用 `exit` 命令终止执行并返回退出状态 7，这是该脚本中用户定义的退出状态。然后 `echo` 显示第一个 `echo` 的退出状态值。第二个 `echo` 也显示第一个 `echo` 的退出状态值，因为第一个 `echo` 执行成功了。

### HISTORY

历史机制是一个改编自 C Shell 的功能，维护了一个最近发布的命令行列表，也称为事件（events）。它为重新执行列表中的任何事件提供了快捷方式。这种快捷方式还允许你执行以前命令的变体并复用它们的参数。这种快捷方式可以让你轻松复制之前在此会话或上一个会话中使用的复杂命令和参数，从而输入一系列在细微处有所不同的命令。历史列表也是你所做过的记录。当你犯了错误且不确定自己做了什么，或者当你想要保留包含一系列命令的过程的记录时，它非常有帮助。

`HISTSIZE` 的值决定了在会话期间历史列表中保留的事件数量。虽然 `HISTSIZE` 的默认值为 500，但你可能想将其设置为一个更方便的值，例如 100。

当你退出 shell 时，最近执行的命令会被保存在名为 `HISTFILE` 的文件中（默认是你的家目录）。下次启动 shell 时，该文件将用于初始化历史列表。`HISTFILES` 变量的值（默认值为 500）并不一定等于 `HISTSIZE`。`HISTSIZE` 存储会话期间记住的事件数量，而 `HISTFILE` 存储历史列表的文件名。

Bourne Again Shell 为你的每个命令行分配一个顺序事件编号。你可以将此事件编号作为 `bash` 提示符的一部分显示（见第330页的“PS1”）。本节中的示例在有助于说明命令或命令组的行为时显示了带编号的提示符。
