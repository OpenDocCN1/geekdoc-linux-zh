
如果你想在脚本的 `Shell` 和子 `Shell` 中使用同一个变量的值，可以两次定义该变量，在每个脚本中各定义一次，并赋予它们相同的值。在上一个示例中，`dispfile` 和 `printfile` 中都定义了 `myfile` 变量。用户执行 `b` 脚本，它会带行号显示列表。`dispfile` 脚本执行时，它生成了自己的 `Shell`，并在其中定义了 `myfile` 变量。在显示文件内容后，该脚本执行了另一个脚本 `printfile`。当 `printfile` 执行时，它生成了自己的 `Shell`。它在自己的 `Shell` 中定义了 `myfile` 变量，并将文件发送到打印机。

如果你想在一个 `Shell` 中定义一个变量，并在任何子 `Shell` 中引用它的值怎么办？例如，如果你想在 `dispfile` 脚本中定义 `myfile` 变量，并在 `printfile` 脚本内部引用它的值 `List`，而不是在 `printfile` 中显式地定义另一个变量。由于变量对于其定义的 `Shell` 是局部的，因此使用普通变量无法实现。但是，有一种被称为**环境变量**的变量，它允许其值被任何子 `Shell` 引用。环境变量为 `Shell` 及其生成的任何子 `Shell`（无论嵌套多深）构成了一个环境。

你可以在三种主要类型的 `Shell`（Bourne、Korn 和 C）中定义环境变量。在 Bourne 和 Korn `Shell` 中实现环境变量的策略与 C `Shell` 非常不同。在 Bourne 和 Korn `Shell` 中，环境变量是被**导出（export）**的。这意味着在每个子 `Shell` 中都会创建一个环境变量的副本。从某种意义上说，`myfile` 变量被导出了，每个子 `Shell` 自动为你定义了一个副本。相反，在 C `Shell` 中，环境变量只定义一次，可以被任何子 `Shell` 直接引用。

## Shell 环境变量

在 Bourne、BASH 和 Korn `Shell` 中，环境变量可以被看作具有额外能力的普通变量。要创建一个环境变量，你对已经定义的变量使用 `export` 命令。`export` 命令指示系统为每个生成的新的 `Shell` 定义一个该变量的副本。每个新 `Shell` 都将拥有该环境变量的副本。这个过程被称为导出变量。

在下一个示例中，变量 `myfile` 定义在 `dumpfile` 脚本中。它将使用 `export` 命令被转换为环境变量。因此，`myfile` 变量将被导出到任何子 `Shell` 中，例如执行 `printfile` 时生成的子 `Shell`。

```
dumpfile
myfile="List"
export myfile
```

```
echo "Displaying $myfile"
pr -t -n $myfile
```

```
printfile
echo "Printing $myfile"
lp $myfile &
```

`dumpfile` 脚本的运行如下：

```
$ dumpfile
Displaying List
1 screen
2 modem
3 paper
Printing List
$
```

当执行 `printfile` 时，它将获得一个自己的 `myfile` 副本，并可以在自己的 `Shell` 中引用该副本。你不再需要在 `printfile` 中显式地定义另一个 `myfile` 变量了。

将导出的环境变量视为全局变量是错误的。新 `Shell` 永远无法引用自身之外的变量。相反，会为新 `Shell` 生成一个变量的副本。你可以将导出变量理解为将变量导出到 `Shell`，而不是变量本身。对于熟悉编程结构的人来说，导出变量可以被看作是值传递（call-by-value）的形式。

## TCSH 和 C Shell 环境变量

在 TCSH 和 C `Shell` 中，环境变量使用单独的定义命令 `setenv`。在这方面，环境变量实际上与普通局部变量是完全不同类型的变量。`Shell` 环境的操作方式更像全局变量。它可以被任何子 `Shell` 直接引用。这与 Bourne、BASH 和 Korn `Shell` 不同，在后者中，只有环境变量的副本被传递给并由子 `Shell` 使用。

要定义一个环境变量，首先使用 `setenv` 命令，随后是变量名，然后是值。没有赋值运算符。在下一个示例中，定义并为环境变量 `myfile` 赋值了值 `List`。

```
% setenv myfile list
```

```
dispfile
echo "Displaying $myfile"
cat -n $myfile
printfile
```

```
printfile
echo "Printing $myfile" &
lpr $myfile
```

`dispfile` 脚本的运行如下：

```
% dispfile
Displaying List
1 screen
2 modem
3 paper
Printing List
$
```

在上一个示例中，变量 `myfile` 在 `dispfile` 脚本中被定义为环境变量。注意这里使用的是 `setenv` 而不是 `set`。现在可以在任何子 `Shell` 中引用 `myfile` 变量，例如执行 `printfile` 时生成的子 `Shell`。

# 第 4 章：Shell 脚本与编程

## 控制结构

你可以使用控制结构在 `Shell` 脚本中控制 Linux 命令的执行。控制结构允许重复命令并选择某些命令。控制结构由两个主要部分组成：测试（`test`）和命令。如果测试成功，则执行命令。

有两种不同类型的控制结构：循环和条件。循环重复命令，而条件在满足时时执行命令。BASH 有三种循环结构：`while`、`for` 和 `for-in`。有两种条件结构：`if` 和 `case`。控制结构的测试是命令的执行。所有 Linux 命令在完成后都会返回退出状态。如果命令成功，其退出状态将为 0。如果命令因原因失败，其退出状态将反映失败的类型。控制结构检查退出状态是否为 0 或其他值。在 `if` 和 `while` 结构的情况下，如果退出状态为 0，命令继续。

## 测试操作

通过 `test` 命令，你可以比较整数、比较字符串，甚至执行逻辑操作。该命令由关键字 `test` 以及由正在比较的值组成。选项可以是运算符的形式，但它与其他选项一样，带有减号和字母代码。例如，`-eq` 是表示相等比较的选项。然而，有两个字符串操作实际上使用的是运算符，对于不等时你使用 `!=`。表 4-1 列出了 `test` 使用的一些常用选项和运算符。`test` 命令的语法如下：

```
test value -option value
test string = string
```

在下一个示例中，用户比较两个整数值以查看它们是否相等。在这种情况下，你需要使用相等选项 `-eq`。命令测试是为了找出测试操作的结果。`Shell` 特殊变量 `$?` 存储了最近执行的 Linux 命令的状态。

```
$ num=5
test $num -eq 10
echo $?
```

与其使用 `test` 关键字作为 `test` 命令，你可以可以使用括号。命令 `test $greeting = "hi"` 可以写为：

```
$ $greeting = "hi"
```

同样，测试命令 `$num -eq 10` 可以写为：

```
[ $num -eq 10 ]
```

# 第二部分：Linux Shell 与文件结构

| 整数比较 | 功能描述 |
| :--- | :--- |
| `-gt` | 大于 |
| `-lt` | 小于 |
| `-ge` | 大于等于 |
| `-le` | 小于等于 |
| `-eq` | 等于 |
| `-ne` | 不等于 |
| 字符串比较 | |
| `-z` | 测试字符串是否为空 |
| `=` | 测试字符串是否相等 |
| `!=` | 测试字符串是否不等 |
| 逻辑运算符 | |
| `-a` | 逻辑与 (AND) |
| `-o` | 逻辑或 (OR) |
| `!` | 逻辑非 (NOT) |
| 文件测试 | |
| `-f` | 文件存在且是普通文件 |
| `-s` | 文件为空 |
| `-r` | 文件可读 |
| `-w` | 文件可写可修改 |
| `-x` | 文件可执行 |
| `-d` | 目录 |

**表 4-1** BASH `Shell` 测试运算符

括号本身必须被空格包围：一个空格、TAB 或回车。如果没有空格，它们是无效的。

### 条件控制结构

BASH `shell` 拥有一组条件控制结构，允许你选择执行哪些命令。其中许多结构与编程语言中的条件控制结构相似，但它们存在一些差异。`if` 条件测试的是 Linux 命令的执行成功与，而不是一个表达式。此外，`if-then` 命令的结束必须用关键字 `fi` 表示，而 `case` 命令的结束则用关键字 `esac` 表示。条件控制结构列如表 4-2 所示。
