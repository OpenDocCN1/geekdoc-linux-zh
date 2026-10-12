
设置 `noclobber` 可以启用保护现有文件免受重定向输出的影响。使用 `noclobber` 功能，如果你将输出重定向到一个已存在的文件，该文件将不会被标准输出覆盖。原始文件将被保留。在某些情况下，你可能会使用已经给现有文件使用的名称作为重定向输出的名称。`noclobber` 功能防止你不意外覆盖原始文件：

```
> set noclobber
> cat preface > myfile
myfile: file exists$
```

有时你可能想用重定向输出覆盖文件。在这种情况下，你可以在重定向操作符后放置一个感叹号。这将覆盖 `noclobber` 功能，用标准输出替换文件内容：

```
> cat preface !myfile
```

### `noglob`

设置 `noglob` 可以启用禁用用户 shell 中特殊字符的功能。字符 `*`、`?`、`[` 和 `–` 将不再被展开以匹配文件名。如果由于某种原因，你的文件名中包含特殊字符，那么此功能将非常有帮助。在接下来的示例中，用户需要引用一个带有 `answers?` 字符的文件。用户使用 `noglob` 选项关闭特殊字符。现在命令行上的问号被视为文件名的一部分，而不是特殊字符，用户可以引用 `answers` 文件。

```
$ set noglob
$ ls answers?
answers?
```

## 用于配置系统的 TCSH/C 特殊 Shell 变量

在 `BASH` shell 中，你可以使用 `TCSH` 中的特殊 shell 变量来配置系统。某些变量由系统初始定义，你可以用新值重新定义它们。另一些则必须由你初始定义。最常用的特殊变量之一是 `prompt` 变量，你用它创建自己的命令行提示符。另一个是 `history` 变量，你用它决定要跟踪多少历史事件。

在 `TCSH` 中，特殊 shell 变量的名称和功能与 `BASH` 或域内核 Shell (`PDKSH`) 中的相似。有些是大写字母，但大多数是小写字母。`EXIT` 和 `TERM` 变量保留了大写形式。然而，`history` 和 `cdpath` 是小小写的。其他特殊变量可能执行某些功能，但实现方式非常不同。例如，`mail` 变量包含了 `BASH` 中 `MAIL`、`MAILPATH` 和 `MAILCHECK` 变量的所有信息。

### `prompt`, `prompt2`, `prompt3`

`prompt`、`prompt2` 和 `prompt3` 变量持有命令行的提示符。你可以将提示符配置为任何你符号或字符串。要让命令行显示不同的符号作为提示符，你只需使用 `set` 命令将符号分配给 `prompt` 变量。在接下来的示例中，用户将 `+` 号分配给 `prompt` 变量，使其成为新的提示符。

```
> set prompt = "+"
```

你可以使用一组预定义的代码来使提示符配置变得简单。通过这些代码，你可以让时间、用户名或目录路径成为提示符的一部分。

![](img/6ac214f13c9ea7c0ad85ba43163f14a1_144_0.png)

# 第二部分：Linux Shell 与文件结构

### `.login`

`TCSH` shell 拥有自己的登录初始化文件，称为 `.login` 文件，该文件包含了用于配置您的 shell 的 shell 命令和特殊变量定义。`.login` 文件对应于 `BASH` 和 `PDKSH` shell 中使用的 `.profile` 文件。

登录文件包含 `setenv` 命令，这些命令用于为特殊环境变量（如 `TERM`）赋值。你可以通过任何一个标准编辑器编辑 `.login` 文件来更改这些已赋值的值。你还可以添加新变量。但是，请记住，在 `TCSH` shell 中，为环境赋值赋值的命令是 `setenv`。在下一个示例中，定义了 `EXINIT` 变量，并为其分配了 Vi 编辑器的行号和自动缩进选项。

```bash
> setenv EXINIT set nu ai
```

在编辑 `.login` 文件时要小心。无意的编辑可能会导致变量设置错误或完全未设置。在编辑之前，为 `.login` 文件创建一个备份是明智的。

如果你对 `.login` 文件做了更改，并希望这些更改在当前登录会话中生效，你需要重新执行该文件。你可以使用 `source` 命令来实现此操作。`source` 命令将准确地执行任何初始化文件，包括 `.tshrc` 和 `logout` 文件。在下一个示例中，用户重新执行了 `.login` 文件。

```bash
> source .login
```

如果你还计划在 Linux 系统上使用 `PDKSH` shell，你需要在 `.login` 文件中定义一个变量，并将其赋值为 `PDKSH` shell 初始化文件的名称。如果你以后决定从 `TCSH` shell 进入 `PDKSH` shell，系统可以为你找到并执行 `PDKSH` shell 初始化文件。在接文所示的 `.login` 文件示例中，你会看到最后一条命令通过 `ENV` 变量将 `PDKSH` shell 初始化文件设置为 `.kshrc`：`setenv ENV $HOME/.kshrc`。

```bash
setenv term vt100
setenv EXINIT 'set nu ai'
setenv ENV $HOME/.kshrc
```

### `.tshrc`

`.tshrc` 初始化文件在每次进入 `TCSH` shell 或生成任何子 shell 时都会执行。如果 `TCSH` shell 是你的登录会话，那么在登录时 `.tshrc` 文件将与你的 `.login` 文件一起执行。如果你从另一个 shell 进入 `TCSH` shell，`.tshrc` 文件将自动执行，其中包含的变量和别名定义将被定义。

`.tshrc` shell 文件实际上在每次生成 shell 时都会执行，例如当你运行脚本时。换句话说，每当创建一个子 shell 时，`.tshrc` 文件就会执行。这允许你在 `.tshrc` 初始化文件中定义局部变量，并在某种意义上将它们导出到每个子 shell 中。尽管像历史记录（`history`）这样的用户自定义特殊变量是局部的，但它们为每个生成的子 shell 都定义。通过这种方式，每个子 shell 都设置了历史记录。然而，每个子 shell 都有自己的本地历史变量：你甚至可以更改一个子 shell 中的本地历史变量，而不会影响其他子 shell 中的任何变量。在 shell 初始化文件中定义变量允许你像处理 `BASH` 导出的变量一样处理它们。`BASH` 或 `PDKSH` shell 中导出的变量只会向任何子 shell 传递自身的一个副本。更改副本不会影响原始变量。

`.tcsh` 文件还包含了别名（aliases）的定义以及用于开启功能的特性变量。别名和特性在 shell 内部是局部定义的。但 `.tcsh` 文件会在每个 shell 中定义它们。因此，`.tcsh` 通常持有像为 `rm`、`cp` 和 `mv` 命令定义的那些别名。下一个示例是一个包含许多标准定义的 `.tcsh` 文件。

```bash
.tcsh
set shell=/usr/bin/csh
set path=$PATH (/bin/usr/bin .)
set cpath=/home/chris/reports /home/chris/letters
set prompt="$cd > "
set history=20
set ignoredups
set noclobber
alias rm 'rm -i'
alias mv 'mv -i'
alias cp 'cp -i'
```

局部变量与环境变量不同，它们使用 `set` 命令定义。你在 `.tcsh` 中定义的任何局部变量都应该使用 `set`。任何使用 `setenv` 作为环境变量定义的变量（如 `TERM`）应该存放在登录文件中。下一个示例显示了 `.tcsh` 文件中常见的定义类型。注意，`history` 和 `noclobber` 变量是使用 `set` 命令定义的。

```bash
set history=20
set noclobber
```

你可以编辑分配给这些变量的任何值。然而，在编辑分配给 `path` 或 `cpath` 的路径名时，请记住这些包含在一个数组中。数组中的每个元素都用空格分隔。如果你添加了一个新的路径名，你需要确保它与其他路径名之间有空格。

如果你对 `.tcsh` 做了更改并希望这些更改在当前登录会话中生效，请记住使用 `source` 命令重新执行 `.tcsh` 文件：

```bash
> source .tcsh
```

### `.logout`

`.logout` 文件也是一个初始化文件，但它是在用户注销时执行的。它设计用于执行你在注销时进行的任何操作。变量定义不同，`logout` 文件通常包含执行关机程序的命令。例如，一个常见的注销命令是检查任何活跃的后台作业；另一个是清除屏幕并发出告别信息。

## 第 6 章：Linux 文件、目录与存档 117
