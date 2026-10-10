
这个程序中值得注意的行如下：

- **第 3 行**—这一行启动了一个 `while` 循环。你会记得在“处理命令行参数”部分中，魔术变量 `$#` 包含命令行参数的数量。只要 `$#` 的值不等于零，这个 `while` 循环就会继续。当 `$#` 的值等于零时，所有命令行参数都已用完，循环结束。
- **第 5 行**—这一行打印 `$1` 的当前值。请注意，要在屏幕上实际打印字符串 `$1`，你必须使用反斜杠转义 `$` 字符，以防止 shell 赋予 `$` 特殊含义。
- **第 6 行**—当第 6 行的 `shift` 命令运行时，变量向左移动一个位置。`$1` “掉出”末端且不再可用，`$2` 变为 `$1`，`$3` 变为 `$2`，等等。

`shift`（以及 `for` 循环）最常见的应用之一是在 shell 程序中，这些程序接受文件名作为命令行参数，然后对命令行中指定的每个文件执行一组操作。

## true 和 false 语句

在 shell 编程中，`true` 和 `false` 语句的唯一目的是分别返回 `true`（0）或 `false`（1）的值。你可以使用这些语句创建无限循环。只要存在可以打破无限循环的某些条件，编写创建无限循环的代码就可能是有用的。这就是那些持续运行并监听输入的程序（例如 Web 服务器）的设计方式。以下示例显示了一个将无限循环的程序：

```bash
#!/bin/sh

# The following program loops indefinitely.

while true

do

    echo "This line will print forever."

done

echo "This line will never print since the program will"

echo "never get past the loop."

exit 0 # The program will never exit cleanly since it will

# never get to this point.
```

显然，本章无法显示此程序的输出，因为它将永远继续下去。第 3 行测试一个为真的条件。由于其测试的参数（`true`）永远不会返回 `false` 值，循环将无限重复。第 7、8、9 和 10 行永远不会被执行，因为程序永远无法通过循环。（要结束此程序，请在键盘上按 Ctrl+C。）

## 跳出循环

有时，你可能想在退出循环所需的条件发生之前跳出循环。有两个语句可用于跳出循环。第一个是 `break` 语句。第二个是 `continue` 语句。

### break 语句

当遇到 `break` 语句时，它会立即终止循环，无论满足退出循环所需的条件是否已达成。清单 12.3 展示了之前“无限循环”程序的一个微小修改。

#### 列表 12.3 跳出循环

```bash
#!/bin/sh

# The following program loops indefinitely.

while true

do

    echo "This line will print forever... But..."

    break

done

echo

echo "The break statement in the loop causes the loop"

echo "to terminate immediately and go the first statement"

echo "after the loop."
```

该程序的输出如下：

```text
This line will print forever... But...

The break statement in the loop causes the loop
to terminate immediately and go to the first statement
after the loop.

bash$
```

在更复杂的实现中，你可以拥有一个循环，等待从用户控制台或网络输入某种类型的输入；该循环可以连续测试某个文件的存在或某个变量的值，如果该条件变为真，`break` 可以结束循环。通常认为，编写那些退出条件经过精心构造以正确响应合适输入并尽可能避免使用 `break` 的循环更为优雅。然而，在足够复杂的程序中，`break` 往往正是你摆脱困境所需的关键。

### continue 语句

`continue` 语句会使循环立即跳回顶部并重新评估测试条件。循环中剩余的语句将不会被执行。列表 12.4 是另一个示例，它使用“无限循环”程序并进行稍作修改。

#### 列表 12.4 在循环结束前重启循环

```bash
#!/bin/sh

# The following program loops indefinitely.

while true

do

    echo "This line will print forever."

    continue

    echo "But this line will never print even though it is inside"

    echo "the loop because the preceding continue statement"

    echo "causes the loop to jump back to the top and re-evaluate"

    echo "the test."

done

echo "This line will never print since the program will"

echo "never get past the loop."

exit 0 # The program will never exit cleanly since it will

# never get to this point.
```

该程序将无限期地输出 *"This line will print forever."*。循环中其余的 `echo` 语句永远不会被打印，因为它们之前的 `continue` 语句会导致循环立即跳回顶部并重新评估测试条件。

## 条件语句

条件语句仅在某个或某些条件为真时才执行。它们通常有三种形式：*if* 语句、*case* 语句以及逻辑 AND/OR 语句。这些是编程中非常基础且有用的结构；流程控制依赖于它们（根据条件的结果执行特定的代码块），程序在接收到某些预期参数时正确表现的能力也依赖于它们（这通常由 `case` 语句处理）。

### if 语句

*if* 语句测试数值表达式。如果条件为真，则 *if* 块内的语句被执行。如果条件为假，可能会发生以下两种情况之一：

- 什么都不会发生。*if* 块内的语句不被执行，程序继续执行，仿佛它们根本不存在。
- 如果 *if* 块中包含了 *else* 语句，则当条件为假时，这些语句将被执行。换句话说，这可用于编写“如果条件为真则执行此操作，如果条件为假则执行此操作，但不要同时执行两者”类型的程序控制。

例如，以下程序使用 *if* 语句来测试提供给程序的命令行参数数量。如果命令行参数为一个或更多，程序将执行 *then* 块内的操作。如果没有提供命令行参数，程序将不做任何操作直接退出：

```bash
#!/bin/sh

# ifprog: Demonstrate one way to use if statements.

if [ $# -ge 1 ]

then

    echo "You supplied $# command line arguments."

fi

echo

echo "Program exiting..."

echo
```

以下是两次运行示例：

**运行 1：**

```bash
bash$ ./ifprog file1 file2 file3

You supplied 3 command line arguments.

Program exiting...

bash$
```

**运行 2：**

```bash
bash$ ./ifprog

Program exiting...

bash$
```

第 3 行中的 `if` 语句检查提供的命令行参数数量是否大于或等于 1（使用魔术变量 `$#`，它存储命令行参数的数量）。如果是，则 `then` 和 `fi` 之间的语句将被执行。（“`fi`” 是 `if` 的倒序拼写。它标记 `if` 块的结束。）如果不是，则 `if` 块内的语句将被跳过，程序跳转到 `fi` 之后的第一条语句，在本例中，该语句只是通知用户程序正在退出。

#### 使用 else 语句

我们可以通过包含一个 `else` 语句来使该程序对用户更友好，该语句告诉用户如何正确使用程序，而不是像当前这样简单地不做任何操作就退出。列表 12.5 显示了修改后的示例。请注意，第 3 行中的操作数是数字 1，而不是小写字母 L。

#### 列表 12.5 前一个程序更友好的版本

```bash
#!/bin/sh

# ifprog: Demonstrate one way to use if statements.

if [ $# -ge 1 ]

then
```
