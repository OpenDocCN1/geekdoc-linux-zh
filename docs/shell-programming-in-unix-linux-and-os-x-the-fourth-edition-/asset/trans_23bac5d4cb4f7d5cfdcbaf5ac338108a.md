
如果 set 命令的 monitor 选项已打开，那么当每个作业完成时，shell 会打印一条消息。如果你在尝试退出 shell 时仍有作业，系统会打印一条消息来提醒你。如果你立即再次尝试退出，shell 就会退出。monitor 选项默认对交互式 shell 启用。

## 停止作业

如果 shell 运行在支持作业控制的系统上，并且 set 命令的 monitor 选项已启用，则前台运行的作业可以放到后台，反之亦然。通常，Ctrl+z 会停止当前作业，bg 命令会将已停止的作业放到后台。fg 命令会将后台或已停止的作业带到前台。

每当后台作业尝试从终端读取时，它会被停止，直到被带到前台。后台作业的输出通常输出到终端。如果执行了 stty tostop，后台作业的输出会被禁用，而向终端写入的作业会被停止，直到被带到前台。当 shell 退出时，所有已停止的作业都会被终止。

## 命令摘要

本节概述 shell 的内置命令。实际上，其中一些命令（如 echo 和 test）可能不是 shell 内置的，或者可能有一个精简版本内置于 shell 中，而更复杂的版本作为单独的程序提供。在所有情况下，这些功能都必须由符合 POSIX 标准的系统作为实用程序提供。它们内置于 Bash 和 Korn shell 中，几乎用于所有 shell 脚本。

## `:` 命令

*一般格式：* `:`

这本质上是一个 *空* 命令。它常用于满足必须有命令出现的要求。

*示例*

```
if who | grep jack > /dev/null ; then
    :
else
    echo "jack's not logged in"
fi
```

`:` 命令返回的退出状态为零。

## `.` 命令

*一般格式：* `. file`

“点”命令使 shell 读取并执行指定的文件，就像文件中的行是在该处输入的一样。请注意，`file` 不需要可执行，只需可读。此外，shell 使用 PATH 变量来查找 `file`。

*示例*

```
. progdefs                         Execute commands in progdefs
```

上述命令使 shell 在当前 PATH 中搜索文件 `progdefs`。找到后，它会读取并执行该文件中的命令。

请注意，由于 `file` 不是由子 shell 执行的，因此在 `file` 中的命令执行完之后，在 `file` 中设置和/或更改的变量仍然有效。

## `alias` 命令

*一般格式：* `alias name=string [name=string ...]`

`alias` 命令将 `string` 赋给别名 `name`。每当 `name` 被用作命令时，shell 会替换 `string`，并在 `string` 就位后执行命令行替换。

*示例*

```
alias ll='ls -l'
alias dir='basename $(pwd)'
```

如果别名以空格结尾，则还会检查别名后面的单词，看它是否也是一个别名。

格式

```
alias name
```

会打印出 name 的别名。

```
alias
```

不带参数的 alias 会列出所有别名。

`alias` 返回退出状态零，除非给出了 `name`（如 `alias name`），且尚未为该名称定义别名。

## `bg` 命令

*一般格式：* `bg job_id`

如果启用了作业控制，则由 `job_id` 标识的作业会被放入后台。如果没有给出参数，则最近被挂起的作业会被放入后台。

*示例*

```
bg %2
```

## `break` 命令

*一般格式：* `break`

执行此命令会导致最内层的 `for`、`while` 或 `until` 循环立即终止。然后继续执行紧随循环之后的命令。

如果使用格式

```
break n
```

则 *n* 个最内层循环的执行会自动终止。

## `case` 命令

*一般格式：*

```
case value in
    pat₁) command
          command
          ...
          command;;
    pat₂) command
          command
          ...
          command;;
          ...
    patₙ) command
          command
          ...
          command;;
esac
```

单词 *值* 会依次与 *模式₁、模式₂、...、模式ₙ* 进行比较，直到找到匹配项。随后，匹配模式之后紧跟的命令会被执行，直到遇到双分号（`;;`）。此时，case 的执行终止。

如果没有模式与 *值* 匹配，则 case 内的命令都不会执行。模式 `*` 可匹配任何内容，通常用作 case 中的最后一个模式，作为默认或“兜底”情况。

Shell 元字符

- `*`（匹配零个或多个字符），
- `?`（匹配任意单个字符），以及
- `[...]`（匹配方括号内的任意单个字符）

可用于模式中。字符 `|` 可用于指定两个模式的逻辑或，如下所示：

```
pat₁ | pat₂
```

这意味着匹配 *模式₁* 或 *模式₂*。

*示例*

```
case $1 in
    -i) lopt=TRUE;;
    -w) wopt=TRUE;;
    -c) copt=TRUE;;
    *) echo "Unknown option";;
esac
case $choice in
    [1-9]) valid=TRUE;;
    *) echo "Please choose a number from 1-9";;
esac
```

## `cd` 命令

*一般格式：* `cd directory`

执行此命令会使 shell 将 *目录* 设为当前目录。如果省略目录，shell 会将 HOME 变量中指定的目录设为当前目录。

如果 shell 变量 CDPATH 为空，则 *目录* 必须是完整目录路径（例如 `/users/steve/documents`），或相对于当前目录指定（例如 `documents` 或 `../pat`）。

如果 CDPATH 非空且 *目录* 不是完整路径，则 shell 会在 CDPATH 的冒号分隔目录列表中搜索包含 *目录* 的目录。

*示例*

```
$ cd documents/memos        Change to documents/memos directory
$ cd                       Change to HOME directory
```

参数 `-` 会使 shell 将用户移回前一个目录。并打印出新的当前目录的路径名。

*示例*

```
$ pwd
/usr/lib/uucp
$ cd /
$ cd -
/usr/lib/uucp
$
```

cd 命令将 shell 变量 PWD 设为新的当前目录，将 OLDPWD 设为前一个目录。

## `continue` 命令

*一般格式：* `continue`

在 `for`、`while` 或 `until` 循环内执行此命令会导致 `continue` 之后的任何命令被跳过。然后循环执行照常继续。

如果使用格式

`continue n`

则 *n* 个最内层循环中的命令会被跳过。然后循环执行照常继续。

## `echo` 命令

*一般格式：* `echo args`

此命令会将 *参数* 写入标准输出。*参数* 中的每个单词以空格分隔。末尾会写入一个换行符。如果省略 *参数*，其效果是简单地跳过一行。

某些反斜杠转义字符对 `echo` 有特殊含义，如表 A.8 所示。

表 A.8 `echo` **转义字符**

| 字符 | 输出 |
| --- | --- |
| `\a` | 警报 |
| `\b` | 退格 |
| `\c` | 不包含终止换行符的行 |
| `\f` | 换页 |
| `\n` | 换行 |
| `\r` | 回车 |
| `\t` | 制表符 |
| `\v` | 垂直制表符 |
| `\\` | 反斜杠字符 |
| `\0nnn` | ASCII 值为 *nnn* 的字符，其中 *nnn* 是一个以零开头的一到三位八进制数 |

请记住引用这些字符，以便由 `echo` 命令而不是 shell 来解释它们。

*示例*

| 命令/输出 | 说明 |
| --- | --- |
| `$ echo *`<br>`bin docs mail misc src` | 列出当前目录中的所有文件 |
| `$ echo` | 跳一行 |
| `$ echo X\tY`<br>`X　　 Y` | 打印 X 和 Y，以制表符分隔 |
| `$ echo "\n\nSales Report"`<br><br>`Sales Report`<br>`$ echo "Wake up!!\a"`<br>`Wake up!!`<br>`$` | 在显示 Sales Report 前先跳过两行<br><br>打印消息并使终端发出蜂鸣声 |

## `eval` 命令

*一般格式：* `eval args`

执行此命令会使 shell 计算 *参数* 的值，然后执行其结果。这可用于使 shell 有效地“双重扫描”命令行。

*示例*

```sh
$ x='abc def'
$ y='$x'
$ echo $y
$x
$ eval echo $y
abc def
$
```

将 $x 赋给 y。

## `exec` 命令

*一般格式：* `exec command args`

当 shell 执行 exec 命令时，它会用指定的参数开始执行指定的 *命令*。与其他命令不同，*命令* 会替换当前进程（也就是说，不会创建新进程）。*命令* 开始执行后，不会返回发起 exec 的程序。

如果仅指定了 I/O 重定向，则 shell 的输入和/或输出会被相应地重定向。

*示例*

| 命令 | 说明 |
| --- | --- |
| `exec /bin/sh` | 用 `sh` 替换当前进程 |
| `exec < datafile` | 将标准输入重新指定为 `datafile` |

