
## 列表 12.3 跳出循环

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

## continue 语句

`continue` 语句会使循环立即跳回顶部并重新评估测试条件。循环中剩余的语句将不会被执行。列表 12.4 是另一个示例，它使用“无限循环”程序并进行稍作修改。

## 列表 12.4 在循环结束前重启循环

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

条件语句仅在某个或某些条件为真时才执行。它们通常有三种形式：*if* 语句、*case* 语句以及逻辑 AND/OR 语句。这些是编程中非常基础且有用的结构；流程控制依赖于它们（根据条件的结果执行特定的代码块），程序在接收到某些预期参数时正确表现的能力也依赖于它们（这通常由 case 语句处理）。

### if 语句

*if* 语句测试数值表达式。如果条件为真，则 *if* 块内的语句被执行。如果条件为假，可能会发生以下两种情况之一：

-   什么都不会发生。*if* 块内的语句不被执行，程序继续执行，仿佛它们根本不存在。
-   如果 *if* 块中包含了 *else* 语句，则当条件为假时，这些语句将被执行。换句话说，这可用于编写“如果条件为真则执行此操作，如果条件为假则执行此操作，但不要同时执行两者”类型的程序控制。

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

### 使用 else 语句

我们可以通过包含一个 `else` 语句来使该程序对用户更友好，该语句告诉用户如何正确使用程序，而不是像当前这样简单地不做任何操作就退出。列表 12.5 显示了修改后的示例。请注意，第 3 行中的操作数是数字 1，而不是小写字母 L。

## 列表 12.5 前一个程序更友好的版本

```bash
#!/bin/sh
# ifprog: Demonstrate one way to use if statements.
if [ $# -ge 1 ]
then
    echo "You supplied $# command line arguments."
else
    echo "Usage: $0 file1 file2..."
    echo
    exit 1
fi
echo
echo "Program exiting..."
echo
```

现在，如果命令行参数的数量小于 1，程序将执行 else 语句并向用户显示使用信息（请记住，`$0` 包含被调用命令的名称）。还要注意第 9 行，它告诉程序立即退出并将退出状态设置为 1（表示程序因错误而终止）。如果程序执行了 else 语句，则第 10–14 行将永远不会被执行。

if 语句的 then 部分是必需的。else 部分是可选的。如你所见，if 语句的 then 部分在 if 测试的表达式求值为真时执行操作。然而，有时你可能希望仅在表达式求值为假时执行操作，而在表达式求值为真时什么都不做。你可以使用冒号作为占位符来实现这一点。这是一个示例：

```bash
if [ $myvar -gt 5 ]
then
    # Do nothing and continue after end of if block
else
    # Statements to execute if condition is false go here.
fi
```

## 使用 elif 语句

有时你可能想要测试两个或更多不同的条件，并根据结果执行不同的操作。`elif` 语句实现了这一点。

`elif` 是 “else if” 的缩写。当使用 `elif` 语句时，程序将进入 `if` 语句。如果其求值为真，将执行其操作，然后程序流程将跳转到 `if` 块结束后的第一条语句（`fi` 所在的位置）。如果其求值为假，则检查第一个 `elif`。如果它为真，则执行其中的语句，流程跳转到 `if` 块的末尾。如果它为假，则评估第二个 `elif` 语句，依此类推。基本上，评估过程会一直进行，直到程序到达一个求值为真的表达式。如果没有任何条件求值为真，要么什么也不发生，要么执行 `else` 内部的语句（如果存在的话）。

列表 12.6 使用了迄今为止你所学到的大部分内容，包括 `if`、`elif` 和 `else`，来玩一个简单的猜数字游戏。请注意，第 10 行使用了 `jot`，这是一个小的命令行随机数生成工具。在这种情况下，其 `-r` 选项的参数是返回的结果数量（1），下限（1）和上限（`$up_limit`）。

## 列表 12.6 一个简单的猜数字游戏

```bash
#!/bin/sh
# Number guessing game
clear
guess_count=1 # Initialize the guess counter to 1
echo
echo "Number guessing game written in bourne shell script."
echo
echo -n "Enter upper limit for guess: "
read up_limit
rnd_number=`jot -r 1 1 $up_limit` # Get a random number
echo
echo "I've thought of a number between 1 and $up_limit."
echo
echo -n "Please guess a number between 1 and $up_limit: "
read guess
# Check the guess against the random number.
while true
do
    if [ $guess -gt $rnd_number ]
    then
        echo
        echo "Your guess was too high. Please try again."
        guess_count=`expr $guess_count + 1`
        echo -n "Please guess a number between 1 and $up_limit: "
        read guess
    elif [ $guess -lt $rnd_number ]
    then
        echo
        echo "Your guess was too low. Please try again."
        guess_count=`expr $guess_count + 1`
        echo -n "Please guess a number between 1 and $up_limit: "
        read guess
    else
        break
    fi
```

