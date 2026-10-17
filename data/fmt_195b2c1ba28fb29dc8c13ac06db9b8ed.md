
在逻辑与 (`&&`) 的情况下，如果两个命令都执行成功，则逻辑命令执行成功。对于逻辑或 (`||`)，如果任一个命令执行成功，则或操作执行成功并返回退出状态 `0`。逻辑命令允许你将逻辑操作作为控制结构中的测试命令。

# case 结构

`case` 结构允许你的程序在多个可能的替代方案中进行选择。通过将一个值与多个可能的模式进行比较来实现。每个可能的值与一组操作相关。如果找到匹配项，则执行相关的操作。

`case` 结构以关键字 `case` 开始，随后是对变量的评估和关键字 `in`。紧接着是一组模式。每个模式都是一个以右括号结尾的正则表达式。在右括号之后，列出与该模式相关的命令，随后在另起的一输入双分号 `;;`，表示这些命令的结束。在所有列出的模式之后，关键字 `case` 结束。语法看起来如下：

```bash
case string in
pattern)
  commands
;;
pattern)
  commands
;;
*)
  default commands
;;
esac
```

提示：模式可以包含 `*`、`[]` 和 `?`。shell 特殊字符是 `*`、`[]` 和 `?`。你可以用 `*` 指定默认模式。该字符匹配任何模式，因此充当默认选项。如果所有其他模式都不匹配，`*` 将匹配。这样，就会执行默认操作，而你不需要专门包含它。`case` 结构通常用于实现菜单。在下一个示例中，要求用户输入以不同方式列出文件的选择。注意那个警告无效输入的默认选项：

```bash
# 允许用户选择不同列出方式程序
echo "s. List Sizes"
echo "1. List All Information"
echo "c. List Files"
echo -n "Please enter choice:"
read choice

case $choice in
s)
  ls -s
  ;;
1)
  ls -1
  ;;
c)
  ls -l
  ;;
*)
  echo "Invalid Option"
;;
esac
```

`lschoice` 脚本的运行结果在此：

```
$ lschoice
s. List Sizes
1. List All Information
c. List Files
Please enter choice: c
[file list...]
$
```

在模式中使用元字符可以给你带来更大的灵活性。例如，在上一个示例中，只允许小写版本的模式；大写会被视为无效。如果你在模式中使用 `*` 字符，它将允许你指定多个可能的匹配项。例如，`*` 模式将同时匹配大写和小写。元字符在大多数 UNIX 和 Linux 文本中都有讨论。

## 一分钟训练

- 你会使用什么操作符来测试空字符串？
- 你是否可以使用 `case` 结构完成与 `if` 结构完成相同的任务？
- 测试表达式中的 `-z` 操作符。
- 是；对于嵌套结构使用 `elif`。

# 循环：while, until, for-in 和 for

BASH shell 拥有一组循环控制结构，允许你重复 Linux 命令：`while`、`for` 和 `for-in` 结构。与 `if` 结构类似，`while` 和 `until` 测试 Linux 命令的结果。然而，`for-in` 结构并不执行测试。相反，它们只是简单地遍历值列表，将每个值赋值给指定的变量。此外，`while` 和 `until` 结构的工作方式与编程语言中的对应结构相似，而 `for` 和 `for-in` 结构与它们的编程结构非常不同。循环控制结构列在表 3-3 中。

| 循环控制结构 | 描述 |
| :--- | :--- |
| `while do command` | 只要测试命令为真，`while` 就会执行操作 |
| `until do command` | 只要测试命令为假，`until` 就会执行操作 |
| `for variable in list-values do command` | `for-in` 设计用于值列表；变量操作数被赋值列表中的值 |
| `for variable do command` | `for` 设计用于引用参数；变量操作数被赋值每个参数 |
| `select string in item-list do command` | `select` 根据 `item-list` 中的项目创建菜单，然后执行命令；该命令通常是一个 `case` |

表 3-3 BASH Shell 循环

# while 循环

`while` 循环重复执行命令。`while` 循环以关键字 `while` 开始，随后紧跟一个 Linux 命令。关键字出现在下一行。循环的结束由关键字 `done` 指定。以下是 `while` 命令的语法：

```bash
while command
  do
    commands
  done
```

在 `while` 结构中使用的 Linux 命令通常是由圆括号括起来的测试命令。在下一个示例 `myname` 脚本中，要求你输入一个名称。然后打印该名称。通过使用括号测试变量 `again` 的值来控制循环。

```bash
again=yes
while [ "$again" = yes ]
  do
    echo -n "Please enter a name: "
    read name
    echo -n "The name you entered is $name"

    echo -n "Do you wish to continue? "
    read again
    # 如果用户输入 yes，循环重复
  done
echo Good-bye
```

`myname` 脚本的运行如下：

```bash
$ myname
Please enter a name: George
The name you entered is George
Do you wish to continue? no
Good-bye
```

# 模块 3：BASH Shell 控制结构 71

提示：`while` 循环通常用于执行性任务，例如输入或输出。你可以结合 `while` 和 `case` 结构驱动菜单。

# 项目 2-1：基础循环

关系操作通常用于管理循环和条件等控制结构。`helloprg` 程序显示三次 hello。它利用 `let` 小于等于操作来管理循环 `let again <= 3`，并增加变量 `again` `let again = again + 1`。注意，在增加 `again` 时不需要进行评估。先前的 `let` 命令会自动评估使用的变量。

## 步骤

1. 使用文本编辑器创建一个名为 `helloprg` 的文件。
2. 定义名为 `again` 的变量并赋值为 `1`。这是用于控制循环的变量初始化。
3. 输入 `while` 命令，其中用于测试的 Linux 语句是 `let` 命令（见模块 2）。检查 `again` 变量的值是否小于等于 `3`。
4. 输出 `again` 变量的值和单词 `Hello`。
5. 使用带有算术赋值操作的 `let` 命令增加 `again` 变量。
6. 使用 `done` 命令结束 `while` 循环。

`helloprg` 脚本所示：

```bash
again=1
while let again <= 3
do
  echo $again Hello
  let again = again + 1
done
```

# 72 Linux 编程：初学者指南

以下是 `helloprg` 脚本的运行结果：

```
$ helloprg
1 Hello
2 Hello
3 Hello
```

# until 结构

`until` 结构的操作与 `while` 结构非常相似。然而，`until` 测试的是 Linux 命令执行的结果。只要 Linux 命令失败，`until` 结构就会继续循环。从某种意义上说，`until` 检查的是一个假的测试条件。这一点来看，`until` 结构与编程语言中的循环结构非常不同。相反，`until` 更像编程语言中测试假表达式运算符。以下是 `until` 结构的语法：

```bash
until Linux command
do
  commands
done
```

# for-in 结构

`for-in` 结构用于顺序引用值列表。每个结构接受两个操作数：一个变量和一个值列表。列表中的每个值被逐一赋值给 `for-in` 结构中的变量。像 `while` 命令一样，`for-in` 结构是一个循环。在循环的每次迭代中，列表中的下一个值会被赋值给变量。当到达列表末尾时，循环停止。与 `while` 循环一样，`for-in` 循环体以关键字 `do` 开始，以关键字 `done` 结束。`for-in` 循环的语法所示：

```bash
for variable in list of values
do
  commands
done
```

## 专家问

**问题：** `for-in` 循环可以用于引用目录中的文件名吗？
