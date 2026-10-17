
你可以通过输入两个感叹号来重复最近的命令：

`$ !! (Return)`

> 重复最后一个命令 (*csh*。)

`*ksh*` 的 `history` 命令使用 `r`（代表“repeat”）而不是感叹号。因此，要重复 `history` 列表中的第 5 个命令，你会输入：

`$ r 5 (Return)`

> 重复第 5 个命令 (*ksh*。)

该命令将在屏幕上回显：

`ls -1`

你可以通过不带编号输入 `r` 命令来重复最近的命令：

`$ r (Return)`

> 重复最后一个命令 (*ksh*。)

### 20.11 命令别名 (csh 和 ksh)

C 和 Korn Shell 允许你重命名 UNIX 命令。重命名后的命令——称为 *alias*——可用于缩短长命令或保护你免受意外删除重要文件的伤害。大多数用户会在他们的 Shell 初始化文件（`.cshrc` 或 `.kshrc`）中设置一个别名列表，以便每次启动新 Shell 时自动定义这些别名。

`alias` 命令用于在 `csh` 中定义别名。在 `.cshrc` 文件中放入以下行，告诉 Shell 将 `m` 视为 `mailx` 命令的别名：

```text
(csh)
	alias m mailx
```

`alias` 命令在 `ksh` 中的工作方式略有不同。在 `.kshrc` 文件中放入以下行，可以为 `mailx` 命令创建一个 ksh 别名：

```text
(ksh)
	alias m='mailx'
```

一旦设置好别名，你就可以使用以下命令行向用户 `bfranklin` 发送邮件

```text
$ m bfranklin (Return)
```

你可以使用 `unalias` 命令移除别名：

```text
$ unalias m (Return)
```

### 20.12 保护现有文件 (csh 和 ksh)

命令别名的一个常见用途是保护文件免受意外删除。当你在使用 `cp`、`mv` 或 `rm` 命令时指定 `-i`（“interactive”）选项时，如果你尝试执行会销毁现有文件的操作，系统将要求你确认你的意图。例如，假设你尝试使用 `rm -i` 命令删除一个名为 `oldfile` 的文件：

```text
$ rm -i oldfile (Return)
```

该命令将提示你确认这是你想要执行的：

```text
rm: remove oldfile?
```

如果你输入 `y`（代表“yes”），文件将被删除。否则，不会采取任何操作。如果你尝试覆盖现有文件，`-i` 选项在 `cp` 或 `mv` 命令中也以类似的方式工作。

如果你是 `csh` 用户，可以通过在 `.cshrc` 文件中放入以下行，为 `rm` 创建一个“安全”别名：

```text
(csh)
	alias rm 'rm -i'
```

如果你使用 `ksh`，你会将此行放入你的 `.kshrc` 文件：

```text
(ksh)
	alias rm='rm -i'
```

或者，你可以使用 `-x` 选项将命令导出到所有子 Shell，在 `.profile` 中放入以下行：

```text
alias -x rm='rm -i'
```

`-x` 选项导出别名（ksh）。

### 20.13 注释行

*comment* 是启动文件（或程序）中的文本，当文件执行时 Shell 会忽略它。注释对于提醒你文件的用途很有用。在 Shell 启动文件中，注释以井号 (`#`) 开始。例如，

```text
# This is a comment line
```

### 20.14 练习

- 1. 确保你能定义以下术语：

    - 启动文件

    - 登录初始化文件

    - Shell 初始化文件

    - 子 Shell

    - 变量

    - 特殊 Shell 变量

    - 环境变量

    - 别名

- 2. 确保你能解释以下每个文件的功能或内容：

    - `.cshrc`

    - `.exrc`

    - `.forward`

    - `.kshrc`

    - `.login`

    - `.logout`

    - `.mailrc`

    - `.mmwrc`

    - `.newsrc`

    - `.plan`

    - `.profile`

    - `.xinitrc`

- 3. 确保你能解释以下每个变量的用途：

    - `HOME`

    - `MAIL`

    - `PATH`

    - `PWD`

    - `SHELL`

    - `TERM`

- 4. 假设一个 `sh` 用户想创建一个名为 *myhome* 的变量，用于保存其主目录的路径名。

    - a. 应该将什么命令放入登录初始化文件，以便 *myhome* 仅可被登录 Shell 使用？

    - b. 什么命令可确保 *myhome* 对所有子 Shell 可用？（变量 `HOME` 包含主目录的路径名。）

- 5. 假设 `ksh` 是登录 Shell，重复上一个问题。

- 6. 假设 `csh` 是登录 Shell，重复上一个问题。

## 21 教程：使用 SH 或 KSH 启动文件

如果你是 C shell 用户，请跳过本章。

如果你使用 Bourne Shell (`sh`) 或 Korn Shell (`ksh`)，你的登录初始化文件将被命名为 `.profile`。如果你是 Korn Shell 用户，你可能还有一个名为 `.kshrc` 的 shell 初始化文件。在本章中，你将学习如何创建和修改此类文件。

### 21.1 使用 `set` 列出变量

- 列出环境变量的当前设置。这可以通过不带参数的 `set` 命令来完成：

```
$ set (Return)
```

shell 将显示变量列表及其当前设置。你可能会看到以下一些变量：

`$` 是 `sh` 和 `ksh` 的默认提示符，并将在本章中使用。

| 变量 | 内容 |
| :--- | :--- |
| `HOME` | 你的主目录路径名 |
| `MAIL` | 你的系统邮箱路径名 |
| `PATH` | shell 查找命令的目录 |
| `PS1` | “提示字符串 1”——主要提示符（默认：$） |
| `PS2` | “提示字符串 2”——次要提示符（默认：>） |
| `PWD` | 你当前的工作目录 |
| `SHELL` | shell 的路径名（/bin/sh 或 /bin/ksh） |
| `TERM` | 你终端的 *termcap* 代码 |
| `USER` | 你的用户名 |

### 21.2 使用 `echo` 显示变量值

你可以使用 `echo` 命令逐个检查这些变量的值。

- **输入 `echo` 命令，指定你要检查的变量。** 你必须输入美元符号 (`$`) 作为变量名的前缀。因此，要查看 `PS2` 变量的内容，请输入

```
$ echo $PS2 (Return)
```

`PS2` 包含次要提示符。其默认值为

```
>
```

如果你省略美元符号前缀，则显示的是变量的*名称*，而不是其内容：

```
$ echo PS2 (Return)
PS2
```

### 21.3 次要提示符

次要提示符是一个符号，表示 shell 正在等待你完成一条不完整的命令行。在本节中，你将看到它是如何工作的。

1. **输入一条不完整的命令行。** 尝试输入以下行，确保不要输入任何结束引号：

```
$ echo "This is an (Return)
```

由于你没有提供结束引号，shell 假设还有更多内容，并显示存储在 `PS2` 中的次要提示符：

```
>
```

2. **输入命令行的其余部分。** 务必在按 (Return) 之前用双引号结束它：

```
>incomplete command line." (Return)
```

shell 将回显整个消息：

```
This is an incomplete command line.
```

### 21.4 创建启动文件的备份

创建 `.profile` 的第一步是查看你是否已经有这样的文件。如果是，你应该准备一个备份副本。

1. 如有必要，进入你的主目录。请记住，不带参数的 `cd` 命令会带你进入主目录：

```
$ cd (Return)
```

2. 列出主目录中的所有文件。输入 `ls -a`（“列出 - 所有”）命令：

```
$ ls -a (Return)
```

如果你看到一个名为 `.profile` 的文件，这意味着在你的账户创建时已在你的主目录中放置了该文件。在编辑此文件之前，你可能需要咨询你的导师或系统管理员。如果你是 `ksh` 用户，也请注意你是否已经有 `.kshrc` 文件。

3. 创建现有启动文件的备份副本。

```
$ cp .profile .profile.BAK (Return)
$ cp .kshrc .kshrc.BAK (Return)
```

### 21.5 登录消息
