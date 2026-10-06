

# select

Bourne Again Shell 的 `select` 控制结构基于 Korn Shell 中的实现，并与 zsh 中的 `select` 控制结构对应。它会显示一个菜单，根据用户对项目的选择为变量分配值，并执行一系列命令。`select` 结构的语法如下：

```bash
select varname [in arg ... ]
do
  commands
done
```

首先，`select` 会生成并显示 `arg` 项的菜单。菜单在每个项目前都有数字。例如，一个以 `select fruit in apple blueberry kiwi orange watermelon STOP` 开始的 `select` 结构将显示如下菜单：

+ 1) apple
2) banana
3) blueberry
4) kiwi
5) orange
6) watermelon
7) STOP

参数列表中可以有很多项。`select` 结构使用 `LINES` 和 `COLUMNS` 变量的值来确定显示区域。（`LINES` 的默认值为 24；`COLUMNS` 的默认值为 80。）当将 `COLUMNS` 设置为 20 时，菜单看起来如下：

+ 1) apple
2) banana
3) blueberry
4) kiwi
5) orange
6) watermelon
7) STOP

显示菜单后，`select` 会显示特殊的 select 提示符 `PS3`。`PS3` 的默认值是字符 `#?`，但通常你会将 `PS3` 设置为更有意义的值。

如果在前面的菜单中输入了一个数值（范围内的数字），`select` 将 `varname` 的值设置为与输入数字对应的参数，并执行 `do` 和 `done` 之间的命令。`select` 结构会发出 `PS3` 提示并等待再次输入，重复此过程，直到某些内容导致其退出 `do` 和 `done` 之间的语句（通常是 `break`、`return` 或 `exit` 语句）。`break` 语句退出循环。在函数内部，`return` 将控制权返回给调用函数的程序。`exit` 语句退出当前 shell。以下脚本说明了 `select` 的用法：

```bash
$ cat fruit
!/bin/bash
PS3="Choose your favorite fruit from these possibilities: "
select FRUIT in apple banana blueberry orange watermelon STOP
do
  if [ "$FRUIT" = "STOP" ]; then
    echo "Thanks for playing!"
    break
  fi
  echo "You chose number $FRUIT as your favorite."
done
```

$ fruit
1) apple 3) blueberry 5) orange 7) STOP
2) banana 4) kiwi 6) watermelon

Choose your favorite fruit from these possibilities:
You choose blueberry as your favorite.
That is choice number 3.

Choose your favorite fruit from these possibilities:
无效的菜单选择会导致 zsh 为 `varname` 分配空字符串并执行 `do` 和 `done` 之间的命令。如果用户在不输入选择的情况下按回车，Z Shell 会重新播放菜单和 `PS3` 提示。Z Shell 将用户的响应存储在关键字变量 `REPLY` 中。

正如语法所示，你可以省略参数列表中的关键字。如果是，`select` 将使用位置参数 `$@` 的当前值。

# Here Document (在此文档)

Here document 允许你从 shell 脚本内部将输入重定向到 shell 脚本。这种文档被称为“here”（在此），因为它在 shell 脚本中可以直接访问，而不是在“there”（那里，可能在另一个文件中）。

以下脚本 `birthday` 包含一个 Here document。第一行的两个小于符号 (`<<`) 告诉 shell 后面有一个 Here document。小于符号后面紧跟着一个或多个界定 Here document 的字符——本示例使用加号 `+`。虽然起始分隔符可以与小于符号相邻，但结束分隔符必须单独占一行。shell 将两个分隔符之间的所有内容作为标准输入发送给进程。在下面的示例中，这就像是你从一个文件将标准输入重定向到 `grep`，只不过该文件嵌入在 shell 脚本中：

zan man 手页中未使用“Here document”术语；你必须搜索 `<<`。

![](img/aa8214d49e1cf50152c432845129fb3b_710_0.png)

[$Name] 分配给空字符串。shell 提供了以下替代方案来接受扩展后的空字符串作为变量的值：

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
$ ls ${HOME:-HOME}```

你可以通过省略冒号为未设置的变量提供默认值，但保持空变量不变：

```bash
$ ls ${LIT-HOME}```

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
| # | 删除最短前缀 |
| ## | 删除最长前缀 |
| % | 删除最短后缀 |
| %% | 删除最长后缀 |

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

