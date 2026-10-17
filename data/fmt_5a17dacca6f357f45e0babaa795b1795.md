
## 退出状态

你可以以类似的方式使用 `continue` 命令来控制 `for/foreach` 和 `while` 循环。`continue` 命令作用于与其关联的最内循环。`continue` 语句将执行立即传回 `while` 测试，跳过最内循环中的所有后续命令。如果与 `foreach` 循环配合 `continue`，`continue` 语句将退出循环当前的迭代并处理列表中的下一项。

当命令或 shell 函数终止时，它会向调用的 shell 返回一个退出状态。退出状态是一个数值，指示程序是否运行成功以及命令中发生了某些事件。每个运行的命令都有退出状态，该状态是由程序员在编写命令时设置的。通常，退出状态 0 表示程序执行成功。任何非零值（通常为 1 或 -1）都表示程序失败。程序员并不总是遵循这一约定。检查命令的帮助页以确定其退出状态。例如，`grep` 命令返回三个状态值之一：0 表示找到了搜索模式，1 表示无法找到模式，2 表示 `grep` 命令无法打开或找到搜索的文件。

### Bourne Shell 退出状态

对于 Bourne shell，`$?` 变量持有最后执行的命令的退出状态。通常，0 表示成功，1 表示失败。

```
$pwd
/home/child/winsor
echo $?
0
$ cd /home3
/home1: bad directory
echo $?
1
```

### C Shell 退出状态

C shell 中名为 `status` 的变量由 shell 自动设置为最后执行命令的退出状态。你可以使用 `echo` 命令在提示符处显示退出状态。

```
oak% grep root /etc/passwd
root:x:0:0000-Admin(0000):/root:/bin/sh
oak% echo $status
0
oak% grep anthony /etc/passwd
oak% echo $status
1
oak% grep root /etc/password
grep: can't open /etc/password
oak% echo $status
2
oak%
```

编写 shell 脚本时，可以在末尾添加 `exit 0` 来表示成功完成。以其他值退出会让调用你脚本的任何程序知道发生了问题。

## 数学运算

对于所有 shell，你只能对整数（全数）进行数学运算。如果你想进行更复杂的运算，使用 `awk` 或 `bc` 命令。

在 Bourne shell 中执行数学运算，使用 `expr` 命令。`expr` 命令具有以下语法。

```
expr arguments
```

你必须在数学运算符（如表98所示）和操作数之间留空。

表98 数学运算符

| 运算符 | 描述 |
| --- | --- |
| + | 加法 |
| - | 减法 |
| * | 乘法 |
| / | 除法 |
| % | 余数（模） |

乘法、除法和取余运算符的优先级高于加法或减法运算符。使用括号进行分组。

### Bourne Shell 数学运算

下面的 Bourne shell 示例使用了 `expr` 命令。

```
i=4
expr $i + 1
expr $i - 1
expr $i \* 2
expr $i / 2
expr $i % 2
nj=2
expr $i + $j
```

### Korn Shell 数学运算

Korn shell 提供了 `let` 和内置的 `$((...))` 表达式来进行算术运算。

你可以使用 `let` 命令进行整数算术。`let` 命令的语法为 `let "arithmetic-expression"`。`arithmetic-expression` 可以包含常量、运算符和 Korn shell 变量。对于包含空格或对 Korn shell 有特殊含义运算符的算术表达式，请使用双引号。

以下示例将变量 `x` 设置为 2 + 2 的和。

```
$ let "x=x + 2"
$ print $x
```

然后你可以像下面所示增加 `x` 的值。

```
$ let "x=x + 1"
$ print $x
```

注意，只有在算术表达式中才能通过名称引用普通变量。你不需要在变量前加 `$` 来执行替换。你可以在算术表达式中在变量前加 `$`，但参数执行的速度比直接引用变量要慢。

`$((arithmetic-expression))` 被替换为双括号内算术表达式的值。`arithmetic-expression` 的处理方式类似于双引号，不同之处是表达式内部的双引号不会被特殊处理。shell 会展开表达式中的所有标记进行参数扩展、命令替换和引号去除。接下来，shell 将该表达式视为算术表达式并替换为表达式的值。

下面的几个简单示例使用 `$((...))` 表达式进行算术扩展。

```
echo $((2+2))
echo $((8192*16384%23))
```

### Shell 数学运算

C shell 的 `@` 命令与 Bourne 和 Korn shell 的 `expr` 命令类似。`@` 命令对表达式进行数学求值并将结果赋值给 shell 变量，如表 99 所示。

表达式可以是数学的，也可以是逻辑的。数学表达式通常使用表 99 所示的运算符。逻辑表达式通常使用以下运算符之一，并产生 1（真）或 0（假）值。

```
< > <= == != !
```

以下示例显示了 C shell 的数值。

```
oak% @ total = 5 + 3
oak% echo $total
8
oak% @ total++
oak% echo $total
9
oak% @ total += 4
oak% echo $total
13
oak% @ newtotal = ($total > 5)
oak% echo $newtotal
1
oak%
```

## 用户定义函数

表 99 C Shell 数学运算符

| 语法 | 描述 |
| --- | --- |
| @ variable = (expression) | 将变量的值赋值为表达式。 |
| @ variable += (expression) | 执行加法。 |
| @ variable -= (expression) | 执行减法。 |
| @ variable *= (expression) | 执行乘法。 |
| @ variable /= (expression) | 执行除法。 |
| @ variable ++ | 加 1。 |
| @ variable -- | 减 1。 |

你可以在 Bourne 和 Korn shell 中编写自己的函数，以便将其作为其他脚本的一部分。

> 注意。并非所有的 Bourne shell 都支持函数。然而，Solaris shell 支持函数。

如果你有一系列想要重复使用的命令，那么用户定义函数就会非常有用。为应用程序服务器编写的函数就是用户定义函数的示例。第 498 页的“示例脚本”中提供了一些函数示例。当你定义一个函数时，在想要执行该函数包含的系列命令的地方使用函数名。

通常，你在脚本的开头定义函数，但也可以在单独文件中定义它们并在脚本之间共享。一旦函数定义完成，你就可以无限次使用它。

使用以下语法定义函数。

```
function_name() {
  (函数的主体)
}
```

Shell 函数使用位置参数和特殊变量作为 `*` 和 `#` 的方式与 shell 脚本完全相同。通常，你在脚本的开头定义函数，但也可以在单独文件中定义它们并在脚本之间共享。一旦函数定义完成，你就可以无限次使用它。

要调用函数，在想要执行该函数包含的系列命令的地方使用函数名。

Shell 函数使用位置参数和特殊变量作为 `*` 和 `#` 的方式与 shell 脚本完全相同。通常，你在脚本的开头定义函数，但也可以在单独文件中定义它们并在脚本之间共享。一旦函数定义完成，你就可以无限次使用它。

要调用函数，在想要执行该函数包含的系列命令的地方使用函数名。

可以为问题提供一些见解。Bourne shell 的解析顺序与 Korn shell 相似，但省略了历史和别名替换。

![](img/fc66b89f230af58e50f0f6d09ca0496d_534_0.png)

图 77 Korn Shell 解析顺序

## 编写 Shell 脚本

图 78 显示了 C shell 解析顺序的简化版本。

![](img/fc66b89f230af58e50f0f6d09ca0496d_535_0.png)

图 78 C Shell 解析顺序

以下 Bourne shell 脚本失败是因为变量在重定向之后才进行替换。
