
```bash
fi

echo "You chose number $FRUIT as your favorite."
done
```

`$ fruit`
1) apple 3) blueberry 5) orange 7) STOP
2) banana 4) kiwi 6) watermelon

Choose your favorite fruit from these possibilities:
You choose blueberry as your favorite.
That is choice number 3.

Choose your favorite fruit from these possibilities:
无效的菜单选择会导致 `zsh` 为 `varname` 分配空字符串并执行 `do` 和 `done` 之间的命令。如果用户在不输入选择的情况下按回车，Z Shell 会重新播放菜单和 `PS3` 提示。Z Shell 将用户的响应存储在关键字变量 `REPLY` 中。

正如语法所示，你可以省略参数列表中的关键字。如果是，`select` 将使用位置参数 `$@` 的当前值。

# Here Document (在此文档)

Here document 允许你从 shell 脚本内部将输入重定向到 shell 脚本。这种文档被称为“here”（在此），因为它在 shell 脚本中可以直接访问，而不是在“there”（那里，可能在另一个文件中）。

以下脚本 `birthday` 包含一个 Here document。第一行的两个小于符号 (`<<`) 告诉 shell 后面有一个 Here document。小于符号后面紧跟着一个或多个界定 Here document 的字符——本示例使用加号 `+`。虽然起始分隔符可以与小于符号相邻，但结束分隔符必须单独占一行。shell 将两个分隔符之间的所有内容作为标准输入发送给进程。在下面的示例中，这就像是你从一个文件将标准输入重定向到 `grep`，只不过该文件嵌入在 shell 脚本中：

`zan man` 手页中未使用“Here document”术语；你必须搜索 `<<`。

![](img/aa8214d49e1cf50152c432845129fb3b_710_0.png)

`$Name` 分配给空字符串。shell 提供了以下替代方案来接受扩展后的空字符串作为变量的值：

- 为变量使用默认值。
- 使用默认值并将该值赋予变量。
- 显示错误。

你可以通过使用变量名的修饰符来选择这些替代方案之一。

# 使用默认值

`:-` 修饰符在变量为空或未设置时使用默认值，同时允许非空变量表示自身：

```bash
${name:-default}
```

shell 将 `:-` 解析为：“如果 `name` 为空或未设置，扩展 `default` 并替换 `name`；否则使用 `name`。”以下命令列出了由变量 `LIT` 指定的目录；如果 `LIT` 为空或未设置，它将列出 `/home/alex/literature`：

```bash
$ ls ${LIT:-home/alex}
```

默认值本身可以包含扩展的变量引用：

```bash
$ ls ${HOME:-HOME}
```

你可以通过省略冒号为未设置的变量提供默认值，但保持空变量不变：

```bash
$ ls ${LIT-HOME}
```

# 设置默认值

`:-` 修饰符不改变变量的值。你可能想在脚本将空或未设置变量的值更改为默认值。你可以使用 `:=` 修饰符来实现：

```bash
${name:=default}
```

（注：修正了 OCR 重复错误）

`:=` 修饰符的工作方式与 `:-` 类似，但如果变量为空或未设置，它也会将其设置为默认值。shell 按原样扩展以下内容设置变量：

```bash
$ ls ${name:=default}
```

# 字符串模式匹配

shell 提供了一组强大的字符串匹配运算符，用于处理路径名和其他字符串。这些运算符可以删除字符串中匹配模式的前缀或后缀。这四个运算符列在表 13-4 中。

| 字符串运算符 | 描述 |
|---|---|
| `#` | 删除最短前缀 |
| `##` | 删除最长前缀 |
| `%` | 删除最短后缀 |
| `%%` | 删除最长后缀 |

这些运算符的语法为：

```bash
$varname op pattern
```

在此语法中，`op` 是表 13-4 中列出的运算符之一，`pattern` 是类似于文件名生成中使用的匹配模式。这些运算符通常用于处理路径以提取或删除组件，或更改后缀：

```bash
$ SOURCEFILE=/usr/local/src/prog.c

$ echo ${SOURCEFILE##/*}

local/src/prog.c

$ echo ${SOURCEFILE##/*}/c

prog.c

$ echo ${SOURCEFILE%%/*}

/usr/local/src

$ echo ${SOURCEFILE%%%c}

$ echo ${SOURCEFILE%.c}.c

/usr/local/src/prog

$ CHOPFIRST=${SOURCEFILE##/*}

$ echo $SCHOPFIRST

local/src/prog.c

$ NEXT=${CHOPFIRST%%/*}

$ echo $NEXT

local
```

# 文件名生成

大多数 shell 的一个重要功能是通过提供描述一个或多个文件名的模式来引用文件。例如，书中讨论的所有 shell 都使用 `*.c` 作为模式，描述所有以 `.c` 结尾的文件。shell 会扩展以下

将此模式转换为匹配该模式的文件名列表。这种文件名与模式匹配的过程称为通配符（globbing）。通配符用于使用单个模式指定多个文件，以及用短字符串指定长文件名。

设置 `noglob` (`set -o noglob`) 选项会关闭所有模式匹配，因此你必须提供精确的文件名：`*` 仅指代由三个字符序列 `*` 组成的文件。请参见第 157 页的“文件名生成/路径扩展”。

## 内置命令 (Builtins)

内置于 shell 的命令在执行时不会派生新进程。以下章节将讨论 `exec` 和 `trap` 内置命令，随后是第 670 页的表 13-6，该表列出了许多 shell 内置命令。

## exec: 执行命令

`exec` 内置命令有两个主要：在不创建新进程的情况下运行命令，或者在脚本内部重定向标准输入、输出或错误。当 shell 执行不是 shell内置的命令时，它通常会创建一个新进程。新进程继承父进程的环境（全局或导出的）变量，但不会继承父进程未导出的变量。请参考：“export: 使变量全局化”（第 571 页）。相比之下，`exec exec` 会替换（覆盖）原始进程来运行命令。

在 `exec` 替换原始进程运行命令方面，它与 `.` (dot) 命令（第 581 页）类似。然而，`.` 命令只能运行脚本，而 `exec` 既可以运行脚本也可以运行编译程序。此外，`.` 命令完成后会将控制权返回给原始脚本，而 `exec` 不会。最后，`.` 命令赋予新进程访问本地变量的权限，而 `exec` 内置命令的语法为

## exec 命令参数

因为使用 `exec` 时 shell 不创建新进程，所以命令运行更快。但由于 `exec` 不会将控制权返回给原始程序，`exec` 内置命令只能用于脚本中想要运行的最后一个命令。以下脚本显示控制权没有返回给脚本：

```
$ exec_demo

who

exec date

echo This echo builtin is never executed.

$ exec_demo

jenny pts/7 May 30 7:05 (bravo.corp.com)

hls pts/1 May 30 6:59 (:0.0)

Thu May 30 11:42:56 PDT 2002
```

![](img/aa8214d49e1cf50152c432845129fb3b_714_0.png)

下一个示例是 `out` 脚本（第 632 页）的修改版本，它使用执行最后的命令脚本。由于 `out` 运行 `cat` 或 `less` 然后退出，新版本 `out2` 同时对 `cat` 和 `less` 使用了 `exec`：

## $ cat out2

```
if [ $ -eq 0 ]
then echo "Usage: out2 [-v] filenames" 1>&2
    exit 1
if [ "$1" = "-v" ]
then
    shift
    exec less "$@"
else
    exec cat -- "$@"
```

`exec` 的第二个主要用途是在脚本内部重定向标准输入、输出或错误。在脚本中执行以下命令后，所有脚本的输入都将重定向自名为 `infile` 的文件：

```
exec < infile
```
