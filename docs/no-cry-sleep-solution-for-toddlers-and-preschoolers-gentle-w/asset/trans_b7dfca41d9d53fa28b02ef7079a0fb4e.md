

## 测试操作

使用 test 命令，你可以比较整数、比较字符串，甚至执行逻辑操作。该命令由关键字 test 组成，后跟被比较的值，这些值由一个选项分隔，该选项指定正在进行的比较类型。可以将该选项视为运算符，但它与其他选项一样，使用连字符和字母代码书写。例如，-eq 是表示相等比较的选项。然而，有两个字符串操作实际上使用运算符而不是选项。当你比较两个字符串是否相等时，使用等号，=。对于不等，使用 !=。表 8-6 列出了 test 使用的一些常用选项和运算符。test 命令的语法如下所示：

```
test value -option value
test string = string
```

TABLE 8-6
BASH Shell
Test Operators

| Integer Comparisons | Function |
| -gt | Greater-than |
| -lt | Less than |
| -ge | Greater-than-or-equal-to |
| -le | Less-than-or-equal-to |
| -eq | Equal |
| -ne | Not equal |
| String Comparisons |  |
| -z | Tests for empty string |
| = | Equal strings |
| != | Not-equal strings |
| Logical Operations |  |
| -a | Logical AND |
| -o | Logical OR |
| ! | Logical NOT |
| File Tests |  |
| -f | File exists and is a regular file |
| -s | File is not empty |
| -r | File is readable |
| -w | File can be written to, modified |
| -x | File is executable |
| -d | Filename is a directory name |

在下一个示例中，用户比较两个整数值以查看它们是否相等。在这种情况下，你需要使用相等选项，-eq。检查 test 命令的退出状态以了解测试操作的结果。shell 特殊变量 $? 保存最近执行的 Linux 命令的退出状态。

```
$ num=5
$ test $num -eq 10
$ echo $?
1
```

除了使用关键字 test 作为测试命令外，你还可以使用包围的方括号。命令 test $greeting = "hi" 可以写成

```
$ [ $greeting = "hi" ]
```

同样，测试命令 test $num -eq 10 可以写成

```
$ [ $num -eq 10 ]
```

方括号本身必须用空白字符包围：空格、TAB 或 ENTER。没有空格，它将无效。

## 条件控制结构

BASH shell 拥有一组条件控制结构，允许你选择要执行的 Linux 命令。其中许多与编程语言中发现的条件控制结构相似，但存在一些差异。if condition 测试 Linux 命令的成功与否，而不是表达式。此外，if-then 命令的结束必须用关键字 fi 表示，而 case 命令的结束用关键字 esac 表示。条件控制结构列在表 8-7 中。
if 结构对命令施加条件。该条件是特定 Linux 命令的退出状态。如果命令成功，返回退出状态 0，则执行 if 结构内的命令。如果退出状态不是 0，则命令失败，if 结构内的命令不会执行。if 命令以关键字 if 开始，后跟一个 Linux 命令，其

| Condition Control Structures: if, else, elif, case | Function |
|---|---|
| if command then
command
fi | if executes an action if its test command is true. |
| if command then
command
else
command
fi | if-else executes an action if the exit status of its test command is true; if false, then the else action is executed. |

| Condition Control Structures: if, else, elif, case | Function |
|---|---|
| if command then
command
elif command then
command
else
command
fi | elif allows you to nest if structures, enabling selection among several alternatives; at the first true if structure, its commands are executed and control leaves the entire elif structure. |
| case string in
(pattern)
command;;
esac | case matches the string value to any of several patterns; if a pattern is matched, its associated commands are executed. |
| command && command | The logical AND condition returns a true 0 value if both commands return a true 0 value; if one returns a non-zero value, then the AND condition is false and also returns a non-zero value. |
| command || command | The logical OR condition returns a true 0 value if one or the other command returns a true 0 value; if both commands return a non-zero value, then the OR condition is false and also returns a non-zero value. |
| ! command | The logical NOT condition inverts the return value of the command. |
| Loop Control Structures: while, until, for, for-in, select |  |
| while command
do
command
done | while executes an action as long as its test command is true. |
| until command
do
command
done | until executes an action as long as its test command is false. |
| for variable in list-values
do
    command
done | for-in is designed for use with lists of values; the variable operand is consecutively assigned the values in the list. |
| for variable
do
    command
done | for is designed for reference script arguments; the variable operand is consecutively assigned each argument value. |

