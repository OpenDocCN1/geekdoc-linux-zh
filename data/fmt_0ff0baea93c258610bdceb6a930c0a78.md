
| `mark-modified-lines` | 设置为 `on` 以使 Readline 在修改过的历史记录行前添加星号。默认值为 `off`。 |

## 按键绑定

你可以指定将按键序列映射到 Readline 命令的绑定，从而允许你修改或扩展默认绑定。与 emacs 编辑器一样，Readline 库包含许多未绑定到按键序列的命令。要使用未绑定的命令，你必须使用以下形式之一进行映射：

```
keyname: command_name
"keystroke_sequence" : command_name
```

在第一种形式中，你拼写出单个键的名称。例如，`CONTROL-U` 应写为 `control-u`。这种形式适用于将命令绑定到单个键。

在第二种形式中，你指定一个描述将要绑定到该命令的按键序列的字符串。你可以使用 emacs 风格的反斜杠转义序列来表示特殊键 `CONTROL (\C)`、`META (\M)` 和 `ESCAPE (\e)`。要指定反斜杠，请用另一个反斜杠对其进行转义：`\\`。同样，双引号或单引号也可以用反斜杠转义：`\"` 或 `\'`。

仅在 emacs 模式可用的 `kill-whole-line` 命令会删除当前行。将以下命令放入 `.inputrc`，可将 `kill-whole-line` 命令（默认未绑定）绑定到按键序列 `CONTROL-R`：

```
control-r: kill-whole-line
```

`bind` 输入命令 `bind -P` 可显示所有 Readline 命令的列表。如果某个命令已绑定到按键序列，则显示该序列。在 vi 模式下可使用的命令以 `vi` 开头。例如，`vi-next-word` 和 `vi-prev-word` 分别将光标移动到下一个和上一个单词的开头。不以 `vi` 开头的命令通常适用于 emacs 模式。

使用 `bind -q` 可以确定哪个按键序列绑定到某个命令：

```
$ bind -q kill-whole-line
```

```
kill-whole-line can be invoked via “\C-r”.
```

你还可以通过在双引号内包含文本来绑定文本（仅限 emacs 模式）：

```
"QQ": "The Linux Operating System"
```

此命令会在你输入 `QQ` 时，使 `bash` 插入字符串 `The Linux Operating System`。

## 条件结构

你可以使用 `$if` 指令有条件地选择 `.inputrc` 文件的部分内容。条件结构的语法为

```
$if test[=value]
    commands
   [$else
    commands]
$endif
```

其中 `test` 是 `mode`、`term` 或 `bash`。如果 `test` 等于 `value`（或者在未指定 `value` 时 `test` 为 `true`），此结构执行第一组 `commands`。如果 `test` 不等于 `value`（或者在未指定 `value` 时 `test` 为 `false`），此结构如果存在第二组 `commands` 则执行之，否则退出该结构。

`$if` 指令的威力在于它可以执行的三种类型的测试。

- 1. 你可以测试当前设置的模式。

```
$if mode=vi
```

如果当前 Readline 模式为 `vi`，则前面的测试为 `true`，否则为 `false`。你可以测试 `vi` 或 `emacs`。

- 2. 你可以测试终端类型。

```
$if term=xterm
```

如果 `TERM` 变量设置为 `xterm`，则前面的测试为 `true`。你可以测试 `TERM` 的任何值。

- 3. 你可以测试应用程序名称。

```
$if bash
```

当你正在运行 `bash` 而非其他使用 Readline 库的程序时，前面的测试为 `true`。你可以测试任何应用程序名称。

这些测试可以根据当前模式、终端类型和你正在使用的应用程序来定制 Readline 库。它们在使用 Readline 库配合 `bash` 和其他程序时，为你提供了大量的权力和灵活性。

`.inputrc` 中的以下命令将使 `CONTROL-Y` 将光标移动到下一个单词的开头，无论 `bash` 处于 vi 模式还是 emacs 模式：

```bash
$ cat ~/.inputrc
set editing-mode vi
$if mode=vi
"\C-y": vi-next-word
$else
"\C-y": forward-word
$endif
```

由于 `bash` 在启动时读取上述条件结构，您必须在 `.inputrc` 中设置编辑模式。使用 `set` 交互式地更改模式不会改变 `CONTROL-Y` 的绑定。

有关 Readline 库的更多信息，请打开 `bash` 的 man 手册页并输入命令 `/READLINE`，该命令将搜索行首的单词 `READLINE`。

## 如果 Readline 命令不起作用，请注销并重新登录

> 提示 Bourne Again Shell 在您登录时读取 `~/.inputrc`。在对该文件进行更改后，您必须注销并重新登录，更改才会生效。

## 别名

别名（alias）是 shell 将其翻译为另一个（通常更长的）名称或（复杂）命令的（通常较短的）名称。别名允许您通过替换简单命令的第一个标记来定义新命令。它们通常放置在 `~/.bashrc` 启动文件中，以便交互式子 shell 可以使用它们。

`alias` 内置命令的语法如下：

```bash
alias [name[=value]]
```

等号周围不允许有空格。如果 `value` 包含空格或制表符，您必须用引号将 `value` 括起来。别名不会接受 `value` 中的命令行参数。当需要使用参数时，请使用函数（见第 349 页）。

别名不会替换自身，这避免了处理如下别名时发生无限递归的可能性：

```bash
$ alias ls='ls -F'
```

您可以嵌套别名。别名在非交互式 shell（即 shell 脚本）中是禁用的。要查看当前别名的列表，请输入命令 `alias`。要查看特定名称的别名，请输入命令 `alias` 后跟别名名称。您可以使用 `unalias` 内置命令删除别名。

当您不带任何参数输入 `alias` 内置命令时，shell 会显示所有已定义别名的列表：

```bash
$ alias
alias 1l='ls -1'
alias 1='ls -ltr'
alias ls='ls -F'
alias zap='rm -i'
```

Ubuntu Linux 定义了一些别名。输入 `alias` 命令以查看当前生效的别名。您可以从相应的启动文件中删除不想要的别名。

## 别名中的单引号和双引号

当别名包含变量时，选择使用单引号还是双引号在别名语法中具有重要意义。如果您用双引号将 `value` 括起来，`value` 中出现的任何变量在创建别名时会被展开。如果您用单引号将 `value` 括起来，变量将在别名被使用时才展开。以下示例说明了这种区别。

`PWD` 关键字变量保存工作目录的路径名。Max 在主目录工作时创建了两个别名。由于他在创建 `dirA` 别名时使用了双引号，shell 在他创建此别名时替换了工作目录的值。`alias dirA` 命令显示 `dirA` 别名，并表明替换已经发生：

```bash
$ echo PWD
/home/max
$ alias dirA='echo Working directory is $PWD'
$ alias dirA
alias dirA='echo Working directory is /home/max'
```

当 Max 创建 `dirB` 别名时，他使用了单引号，这阻止了 shell 展开 `PWD` 变量。`alias dirB` 命令显示 `dirB` 别名仍包含未展开的 `PWD` 变量：

```bash
$ alias dirB='echo Working directory is $PWD'
$ alias dirB
alias dirB='echo Working directory is $PWD'
```

在创建 `dirA` 和 `dirB` 别名后，Max 使用 `cd` 将 `cars` 设置为工作目录，并将每个别名作为命令执行。他使用双引号创建的别名显示创建该别名时所在目录的名称作为工作目录（这是错误的）。相比之下，`dirB` 别名显示了正确的工作目录名称：

```bash
$ cd cars
$ dirA
Working directory is /home/max
$ dirB
Working directory is /home/max/cars
```

## 如何阻止 shell 调用别名

*提示* Shell 仅检查简单的、未加引号的命令，以查看它们是否为别名。作为相对或绝对路径名给出的命令以及加引号的命令不会被检查。当您想输入一个已有别名的命令但不希望使用别名时，请在命令前加反斜杠，指定命令的绝对路径名，或将命令写为 `/.command`。

## 别名示例

以下别名允许您输入 `r` 来重复上一条命令，或输入 `r abc` 来重复以 `abc` 开头的上一条命令：

```bash
$ alias r='fc -s'
$ !!
```

如果您经常使用命令 `ls -ltr`，您可以创建一个别名，在输入命令 `l` 时替换为 `ls -ltr`：

```bash
$ alias l='ls -ltr'
$ l
total 41
-rw-r--rw- 1 max group 30015 2009-03-01 14:24 flute.ps
-rw-r---rw- 1 max group 3089 2010-02-11 16:24 XTerm.ad
-rw-r---rw- 1 max group 641 2010-04-01 08:12 fixtax.icn
-rw-r---rw- 1 max group 484 2010-04-09 08:14 maptax.icn
drwxrwxr-x 2 max group 1024 2010-08-09 17:41 Tiger
drwxrwxr-x 2 max group 1024 2010-09-10 11:32 testdir/
drwxr-xr-x 1 max group 485 2010-09-21 08:03 floor
drwxrwxr-x 2 max group 1024 2010-09-27 20:19 Test_Emacs
```

别名的另一个常见用途是防止您犯错误。以下示例在输入命令 `zap` 时替换为 `rm` 实用程序的交互式版本：

```bash
$ alias zap='rm -i'
$ zap f*
rm: remove 'fixtax.icn'? n
rm: remove 'flute.ps'? n
rm: remove 'floor'? n
```

`-i` 选项使 `rm` 询问您确认要删除的每个文件，从而帮助您避免删除错误的文件。您也可以使用 `rm -i` 命令为 `rm` 创建别名：`alias rm='rm -i'`。

下一个示例中的别名使 shell 在您输入 `ll` 命令时每次替换为 `ls -l`，在您使用 `ls` 时每次替换为 `ls -F`：

```bash
$ alias ls='ls -F'
$ alias ll='ls -l'
$ ll
total 41
drwxrwxr-x 2 max group 1024 2010-09-27 20:19 Test_Emacs/
drwxrwxr-x 2 max group 1024 2010-08-09 17:41 Tiger/
-rw-r---rw- 1 max group 3089 2010-02-11 16:24 XTerm.ad
-rw-r---rw- 1 max group 641 2010-04-01 08:12 fixtax.icn
-rwxr-xr-x 1 max group 485 2010-09-21 08:03 floor*
-rw-r---rw- 1 max group 484 2010-04-09 08:14 maptax.icn
drwxrwxr-x 2 max group 1024 2010-09-10 11:32 testdir/
```

`-F` 选项使 `ls` 在目录名末尾打印斜杠（`/`），在可执行文件名的末尾打印星号（`*`）。在此示例中，替换别名 `ll (ls -l)` 的字符串本身包含一个别名 (`ls`)。当它用其值替换别名时，shell 会查看替换字符串的第一个单词，以检查它是否是一个别名。在上面的示例中，替换字符串包含别名 `ls`，因此发生第二次替换以生成最终命令 `ls -F -l`。（为了避免*递归深入*，替换文本中的 `ls`，尽管是一个别名，但不会被再次展开。）

当不带 `等号或值` 字段给出别名列表时，`alias` 内置命令通过显示每个已定义别名的值来响应。如果别名未定义，`alias` 内置命令会报告错误：

```bash
$ alias ll l ls zap wx
alias ll='ls -l'
alias l='ls -ltr'
alias ls='ls -F'
alias zap='rm -i'
bash: alias: wx: not found
```

您可以通过在带别名的命令前加反斜杠 (`\`) 来避免别名替换：

```bash
$ \ls
Test_Emacs  XTerm.ad       flute.ps   maptax.icn
Tiger        fixtax.icn     floor      testdir
```

由于用别名值替换别名名称不会改变命令行的其余部分，因此任何参数仍会被执行的命令接收：

```bash
$ ll f*
-rw-r--r--  1 max group   641 2010-04-01 08:12  fixtax.icn
-rw-r--r--  1 max group 30015 2009-03-01 14:24  flute.ps
-rwxr-xr-x  1 max group   485 2010-09-21 08:03  floor*
```

您可以使用 `unalias` 内置命令删除别名。当 `zap` 别名被删除后，它将不再通过 `alias` 内置命令显示，其后续使用会导致错误消息：

```bash
$ unalias zap
$ alias
    alias ll='ls -l'
    alias l='ls -ltr'
    alias ls='ls -F'
$ zap maptax.icn
bash: zap: command not found
```

## 函数

Shell 函数类似于 shell 脚本，因为它存储一系列命令以便稍后执行。但是，由于 shell 将函数存储在计算机的主内存（RAM）中，而不是存储在磁盘文件上，shell 可以比访问脚本更快地访问函数。Shell 还会对函数进行预处理（解析），使其比脚本启动更快。最后，shell 执行一个与其调用者相同的 shell 中运行。如果你定义了过多的函数，启动子 shell（如运行脚本时）的开销可能会变得不可接受。你可以在 `~/.bash_profile` 启动文件中、使用函数的脚本中，或者直接从命令行声明一个 shell 函数。你可以使用 `unset` 内建命令移除函数。注销后，shell 不会保留函数。

## 移除变量和函数

**提示** 如果你有一个 shell 变量和一个函数具有相同的名称，使用 `unset` 会移除 shell 变量。如果你再次使用 `unset` 处理相同的名称，它将移除该函数。

声明 shell 函数的语法如下

```
[function] function-name ()
{
    commands
}
```

其中 `function` 是可选的，`function-name` 是你用来调用函数的名称，而 `commands` 构成了函数在调用时执行的命令列表。`commands` 可以是 shell 脚本中包含的任何内容，包括对其他函数的调用。

左花括号（`{`）可以出现在与函数名称相同的行上。别名和变量在读取函数时进行展开，而不是在执行时。你可以在函数内使用 `break` 语句（第 976 页）来终止其执行。

Shell 函数不仅可作为简写使用，还可用于定义特殊命令。以下函数在后台启动名为 `process` 的过程，并将 `process` 通常显示的输出保存至 `.process.out`：

```
start_process() {
    process > .process.out 2>&1 &
}
```

下一个示例创建一个简单的函数，该函数显示日期、标题以及当前登录在系统中的人员列表。此函数运行与第 300 页描述的 `whoson` 脚本相同的命令。在此示例中，函数是通过键盘输入的。大于号（`>`）是次要 shell 提示符（`PS2`）；请勿输入它们。

```
$ function whoson ()
> {
>    date
>    echo "Users Currently Logged On"
>    who
> }
$ whoson
Mon Aug  9 15:44:58 PDT 2010
Users Currently Logged On
hls       console       2010-08-08 08:59    (:0)
max       pts/4         2010-08-08 09:33    (0.0)
zach      pts/7         2010-08-08 09:23    (bravo.example.com)
```

![](img/2344fc4a798f29dca9e8b5ed7288171a_401_0.png)

如果你希望 `whoson` 函数始终可用，而无需每次登录时都输入它，请将其定义放入 `~/.bash_profile` 中。然后使用 `.`（点）命令运行 `.bash_profile` 以立即使更改生效：
