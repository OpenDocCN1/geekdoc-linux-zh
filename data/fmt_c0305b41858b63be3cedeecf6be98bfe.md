
这个美元符号会让 shell 将变量的值传递给 `echo`，并在屏幕上显示出来。你也可以使用引号来处理变量。例如，你可以用双引号或单引号括住变量以控制输出。以下示例展示了使用双引号或单引号时的输出结果：

```bash
$ echo $car
van
$ echo '$car'
$car
$ echo "\$car"
$car
```

如果你需要在输出中保持空格，使用引号是个好办法。以下示例展示了当你需要字面意义的空格或制表符时输出会是什么样子：

```bash
$ car="Dodge Van Sport Model"
$ echo $car
Dodge Van Sport Model
```

当你需要字面意义的空格或制表符时，请务必使用引号，否则输出时屏幕上只会显示一个空格。

当你使用 `*` 等特殊字符时，使用引号也很重要。根据你当前所处的 shell，如果变量添加了特殊字符，shell 可能会展开该变量。这里展示的星号就是一个很好的例子：

```bash
$ car="van*"
$ echo "$car"
van*
```

如果你不使用引号括起变量，shell 可能会将变量的值展开为目录中找到的对象，如下例所示：

```bash
$ car=van*
$ echo $car
van.report van.summary
```

Solaris 使用特殊的单字符参数与 shell 进行交互。这些参数是绝对的，且前面带有美元符号。命令行上的每个参数都会变成一个位置参数的值，这使得你可以访问命令行参数。像 `$1`、`$#` 和 `$?` 这样的特殊参数表示与 shell 的某些交互。你不能给这些参数赋值。

位置参数允许你访问命令行参数。你在命令行上输入的每个参数都会变成一个位置参数的值。表 17.1 列出了特殊字符及其含义，表 17.2 列出了变量及其用途。

## 表 17.1：特殊字符

| 字符 | 含义 |
|:---|:---|

| 换行符 | 启动命令的执行 |
| `;` | 分隔命令 |
| `:` | 空操作，返回真退出状态 |
| `&` | 在后台执行命令 |
| `&&` | 如果左侧命令成功，则执行右侧命令 |
| `( )` | 对命令进行分组或标识函数 |
| `\|` | 在管道中分隔命令 |
| `>` | 重定向标准输出 |
| `>>` | 追加标准输出 |
| `<` | 重定向标准输入 |
| `<<` | 标识 here document |
| `*` | 标识模糊文件引用中的字符串 |
| `?` | 标识模糊文件引用中的单个字符 |
| `\\` | 对后续字符进行引用 |
| `'` | 引用字符串；不允许替换 |
| `"` | 引用字符串；允许变量和命令替换 |
| `$( )` | 执行命令替换 |
| `[ ]` | 在模糊文件引用中标识字符类 |
| `.` | 内置命令；在当前 shell 中执行命令或脚本，而不是生成新的 shell |
| `\|\|` | 逻辑或；如果左侧命令失败，则执行右侧命令 |
| `!` | 逻辑非；反转退出状态 |

## 表 17.2：变量/参数

| 变量 | 用途 |
|:---|:---|

| `$0` | 给出被调用脚本的名称。但在 shell 中，它会报告你当前所在的 shell。 |
| `$n` | 给出第 n 个命令行参数的值。 |
| `$*` | 给出所有命令行参数。 |
| `$#` | 给出命令行参数的数量。 |
| `$$` | 给出当前进程的 PID 号。 |
| `$!` | 给出最近一个后台任务的 PID 号。 |
| `$?` | 给出上一个任务的退出状态。 |

## 局部变量

在 Bourne shell 和 Korn shell 中，为变量赋值的基本约定是相同的。变量中不能有空格；它应该是一个单词，如下例所示：

```bash
$ bsos=1mn
```

你也可以使用带美元符号的变量名来产生变量的值：

```bash
$ echo $bsos
1mn
```

需要注意的是，通常没有必要更改在 `/etc/profile` 中初始化的变量的值。如果你必须更改变量的值，在 Bourne shell 或 Korn shell 中，请在主目录下的 `.profile` 中进行操作。在 C shell 中，你会使用 `.login`。关键字变量可以是局部的或全局的，可以由用户定义或是内置的。为了使局部变量在所有 shell 中可用，必须通过命令行或将其添加到初始化文件中进行导出。

要设置局部变量，请参照以下示例：

```bash
$ MN=/adm/manu
$ echo $MN
/adm/manu
$ cd $MN
$ pwd
/adm/manu
$ unset MN
$ echo $MN
$ cd
$ pwd
/home/admin
```

要显示局部变量，在命令行中输入 `set`。

## 全局变量

使用不同的约定来区分全局变量和局部变量。大写字母用于全局变量，混合或大写字母用于其他变量。除非你使全局变量可用，否则其他从原始 shell 派生的 shell 和程序无法访问全局变量。可以在 `sh` 和 `ksh` 中使用 `export` 内置命令使变量在子进程中可用。如果你在 C shell 中，在使用 `export` 之前需要使用 `setenv`。以下示例展示了如何在不以任何方式改变父进程的情况下将变量导出到子进程：

```bash
$ cat dealers1
van=dodge
echo 'dealer1 1: $van'
dealers2
echo 'dealers1 2: $van'

$ cat dealers2
echo 'dealers2 1: $van'
van=sport
echo 'dealers2 2: $van'

$ dealers1
dealers1 1: dodge
dealers2 1:
dealers2 2: sport
dealers1 2: dodge
```

在这个示例中，`dealers2 1` 不会显示任何内容，因为它是该子 shell 中未声明的变量。

当 shell 遇到由美元符号后跟变量名组成的令牌时，会发生变量扩展。shell 将令牌替换为变量的值。`$VARIABLE` 与更通用的 `${VARIABLE}` 的不同之处在于，花括号将变量名与其周围的内容隔离开。以下示例展示了输出结果的差异：

```bash
$ PREF=window
$ KIND=$PREFpane
$ TYPE=$PREFglass
$ echo $KIND $TYPE

$ PREF=window
$ KIND=${PREF}pane
$ TYPE=${PREF}glass
$ echo $KIND $TYPE
windowpane windowglass
```

由于 `PREFpane` 和 `PREFglass` 是有效的变量名，而脚本中没有设置这些名称，因此此脚本将无效。根据你所在的 shell，你将在输出行上得到一个空行或错误消息。然而，如果你在 `PREF` 变量周围使用花括号，结果将如下所示。使用花括号可以提高代码的可读性，即使它们在技术上并非必要。使用花括号可以将错误降到最低。

## 导出变量

在命令行上导出变量会使其对当前 shell 及其所有子进程可用。如果在子 shell 中设置了变量，它不会被导出到父 shell。不过，它将对在子 shell 之后打开的任何 shell 可用。

要在命令行上导出变量，请参照以下示例： `VAR=val;export VAR` （或 `export VAR=val`）

> **提示** Bourne shell 不允许你同时定义和导出变量。必须分两个独立的步骤完成。

这个示例演示了导出过程：

```bash
$ cat dealers2
export dodge
dodge=dayton
echo 'dealers 2 1: $dodge'
anyone
echo 'dealers 2 2: $dodge'

$ cat anyone
echo 'anyone 1: $dodge'
dodge=silver
echo 'anyone 2: $dodge'

$ dealers2
dealers 2 1: dayton
anyone 1: dayton
anyone 2: silver
dealers 2 2: dayton
```

在这个示例中，父进程保留 `dodge` 的值，而 `dayton` 被传递给子进程，子进程将其更改为 `silver`，但由于它是子进程，对 `dodge` 的更改不会传回父进程。

`read` 命令经常与用户创建的变量一起使用。当必须在桌面上输入响应时，这很有帮助。此命令允许你接受用户输入并将其存储在变量中以便进一步使用：

```bash
$ cat read8
echo 'catalog pages: \c'
read answerline
echo 'Enter P1ease: \sanswerline'

$ read8
catalog pages: annual sale
Enter P1ease: annual sale
```

本示例展示了 `echo` 命令如何提示用户做出响应。在响应行中使用了引号，因为用户的响应可能多种多样。
