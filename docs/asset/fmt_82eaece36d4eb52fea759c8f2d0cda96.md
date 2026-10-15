
关于 `aspell` 的更多信息请参阅第 1089 页。

## until

`until` 和 `while` 结构非常相似，区别在于循环顶部测试的含义。图 13-6 显示 `until` 结构在测试为假时执行循环，而 `while` 则在测试为真时执行。`until` 结构在测试命令返回真退出状态时停止循环。这些特殊字符连同 `$line` 变量的值，是一个正则表达式（第 1383 页）。`grep` 的输出被重定向到 `/dev/null`（第 150 页），因为不需要输出；只有退出代码很重要。`if` 语句检查 `grep` 的取反退出状态（前面的否定符号或改变退出状态的含义——真变为假，反之亦然），只有在找到匹配行时，状态为 0 或真（取反后为假）。如果退出状态不是 0 或假（取反后为真），则该单词不在正确拼写文件中。`echo` 内置命令在标准输出上显示...。一旦检测到 EOF（文件末尾），`read` 内置命令返回假的退出状态，控制权移出 `while` 结构，脚本终止。

在你在使用 `spell_check` 之前，请检查一个你经常使用但不在标准字典中的正确拼写单词文件。例如，如果你在一家名为 Blankenship and Klimowski Attorneys 的律师事务所工作，你会将 Blankenship 和 Klimowski 放入文件中。下面的示例了 `spell_check` 如何检查名为 `memo` 的文件的拼写，并从输出列表中移除 Blankenship-Klimowski。

```
$ aspell -1 memo

Blankenship

Klimowski

target

hte

$ cat word_list

Blankenship

Klimowski

$ spell_check word_list memo

target

hte
```

### until 示例

```bash
until [ $var -eq "value" ]
do
    echo "Testing..."
    read var
done
```

![](img/aa8214d49e1cf50152c432845129fb3b_702_0.png)

# 图 13-7 用例流程图

`case` 结构如下：

```
case test-string in
  pattern-1)
    commands-1
    ;
  pattern-2)
    commands-2
    ;
  pattern-3)
    commands-3
    ;
esac
```

# 第 13 章 编写 Bourne Shell

以下 `case` 结构使用了用户输入的字符串的字符。如果 `test-string` 的值为 `A`，该结构将执行模式 `A` 之后的命令。右括号 `)` 是 `case` 控制结构的一部分，而不是模式的一部分。如果 `test-string` 的值为 `B` 或 `C`，该结构将执行匹配模式之后的命令。星号 (`*`) 表示任何字符字符串，并在没有匹配项时作为通用捕获（catchall）。如果没有模式匹配 `test-string` 且没有通用捕获 (`*`) 模式，控制权将传递到 `esac` 语句之后的命令，而 `case` 结构不执行任何操作。`case1` 的第二次示例执行显示了用户输入了小写的 `b`。由于 `test-string` 不匹配大写的 `B` 或 `case` 语句中的任何其他模式，程序将执行后续的通用模式并显示消息：

```
$ case1
echo "Enter A, B, or C: "
read letter
case "$letter" in
A)
    echo "You entered A"
    ;;
B)
    echo "You entered B"
    ;;
C)
    echo "You entered C"
    ;;
*)
    echo "You did not enter A, B, or C"
    ;;
esac
```

```
$ case1
Enter A, B, or C: B
You entered B
$ case1
Enter A, B, or C: b
You did not enter A, B, or C
```

`case` 结构中的模式类似于歧义的文件引用。该模式可以包含表 13-2 所示的任何特殊字符和字符串。

# 模式表 13-2

| 模式 | 描述 |
| :--- | :--- |
| * | 匹配任何字符字符串。将其用于默认情况。 |
| ? | 匹配任何单个字符。 |

# 模式（续接）

| 模式 | 描述 |
| :--- | :--- |
| [...] | 定义一个字符类。括号内的任何字符都被逐一尝试，以匹配单个字符。两个字符之间的连字符指定了一个字符范围。 |
| \| | 分隔满足 `case` 结构特定分支的备选方案。 |

下一个脚本接受大写和小写字母：

```bash
$ cat case2
echo -n "Enter A, B, or C: "
read letter
case $letter in
  a|A)
    echo "You entered A"
    ;;
  b|B)
    echo "You entered B"
    ;;
  c|C)
    echo "You entered C"
    ;;
  *)
    echo "You did not enter A, B, or C"
    ;;
esac
$ case2
Enter A, B, or C: b
You entered B
$
```

## 可选项

以下示例显示了你如何使用 `case` 结构创建一个简单的菜单。`command_menu` 脚本使用 `echo` 显示菜单项并提示用户进行选择。`case` 结构根据用户的选择执行相应的实用程序：

> 2. Bourne Again 和 Z Shell 具有一个菜单控制结构，可以自动处理此程序的大部分工作。请参见第 658 页的 `select`。

# 第 13 章 编写 Bourne Again Shell

```bash
$ cat command_menu
#!/bin/bash
# 简单命令的菜单界面
echo "\n COMMAND MENU\n"
echo "\a. Current date and time"
echo "\b. Users currently logged in"
echo "\c. Name of the working directory"
echo "\d. Contents of the working directory\n"
echo -n "Enter a, b, c, or d: "
read answer
echo
case ${answer} in
  a)
    date
    ;
  b)
    who
    ;
  c)
    pwd
    ;
  d)
    ls
    ;
  *)
    echo "There is no selection: $answer"
    ;
esac
```
