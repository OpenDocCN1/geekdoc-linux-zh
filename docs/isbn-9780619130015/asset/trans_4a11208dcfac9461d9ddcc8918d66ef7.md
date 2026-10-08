
## test 命令的字符串测试选项

| 选项或表达式 | 含义 | 示例 |
| :--- | :--- | :--- |
| -z | 测试字符串长度是否为零 | test -z string |
| -n | 测试字符串长度是否非零 | test -n string |
| string1 = string2 | 测试两个字符串是否相等 | test string1 = string2 |
| string1 != string2 | 测试两个字符串是否不相等 | test string1 != string2 |
| string | 测试字符串长度是否非零 | test string |

**表 7-2：test 命令的字符串测试选项**

为了演示 test 命令的字符串测试功能：

- 1. 输入 `name="Bjorn"` 并按下 Enter。
- 2. 输入 `test $name = "Bjorn"` 并按下 Enter。
- 3. 输入 `echo $?` 并按下 Enter。您的屏幕看起来与图 7-6 类似。

![](img/6d8286a85e2d8ad63e16f1801102da59_247_0.png)

在上面的示例中，test 命令返回退出状态 0，表示表达式 `$name = "Bjorn"` 为真。这意味着 $name 和 "Bjorn" 相等。

- 4. 输入 `test $name != "Barn"` 并按下 Enter。
- 5. 输入 `echo $?` 并按下 Enter。您的屏幕看起来与图 7-7 类似。

![](img/6d8286a85e2d8ad63e16f1801102da59_248_0.png)

**图 7-7：测试不相等的字符串**

在上面的示例中，test 命令返回退出状态 0，表示表达式 $name != "Barn" 为真。这意味着 $name 和 "Barn" 不相等。

- 6. 输入 `test -z $name` 并按下 Enter。
- 7. 输入 `echo $?` 并按下 Enter。您的屏幕看起来与图 7-8 类似。

![](img/6d8286a85e2d8ad63e16f1801102da59_248_1.png)

**图 7-8：测试结果为假的字符串**

上面示例中的最后一个 test 命令返回退出状态 1，表示表达式 -z $name 为假。这意味着字符串 $name 的长度不为零。

## 使用 test 命令测试文件

test 命令可以判断文件是否存在，以及是否具有指定的权限或属性（如可执行、可读、可写、目录等）。表 7-3 描述了该命令的几个文件测试选项。

| 选项 | 含义 | 示例 |
| :--- | :--- | :--- |
| -e | 如果文件存在，则为真 | test -e file |
| -r | 如果文件存在且可读，则为真 | test -r file |
| -w | 如果文件存在且可写，则为真 | test -w file |
| -x | 如果文件存在且可执行，则为真 | test -x file |
| -d | 如果文件存在且为目录，则为真 | test -d file |
| -f | 测试文件是否存在且为常规文件 | test -f file |
| -s | 如果文件存在且大小大于零，则为真 | test -s file |
| -c | 测试文件是否存在且为字符特殊文件（即面向字符的设备，如终端或打印机） | test -c file |
| -b | 测试文件是否存在且为块特殊文件（即面向块的设备，如磁盘或磁带驱动器） | test -b file |

**表 7-3：test 命令的文件测试选项**

为了演示 test 命令的文件测试功能：

- 1. 使用 touch 命令创建一个名为 test_file 的空文件。
- 2. 使用 `ls -l test_file` 命令查看文件的权限。您的屏幕应看起来与图 7-9 类似。
- 3. 注意该文件对您（所有者）具有读和写权限。然后输入 `test -x test_file` 并按下 Enter。

![](img/6d8286a85e2d8ad63e16f1801102da59_250_0.png)

- 4. 输入 `echo $?` 并按下 Enter。您的屏幕看起来与图 7-10 类似。

![](img/6d8286a85e2d8ad63e16f1801102da59_250_1.png)

`test` 命令返回退出状态 1，因为 `test_file` 不可执行。

- 5. 输入 `test -r test_file` 并按下 Enter。
- 6. 输入 `echo $?` 并按下 Enter。您的屏幕看起来与图 7-11 类似。

![](img/6d8286a85e2d8ad63e16f1801102da59_251_0.png)

test 命令返回退出状态 0，表示 test_file 可读。

## 使用 test 命令执行布尔测试

test 命令的布尔运算符允许您以 AND（与）和 OR（或）关系组合多个表达式。您还可以使用布尔否定运算符。表 7-4 描述了布尔运算符。

| 选项 | 含义 | 示例 |
| :--- | :--- | :--- |
| -a | 逻辑与 | test expression1 -a expression2 |
| -o | 逻辑或 | test expression1 -o expression2 |
| ! | 逻辑否定 | test !expression |

**表 7-4：test 命令的布尔运算符**

-a 运算符将两个表达式组合起来，并测试它们之间的逻辑与关系。使用 -a 选项的 test 命令形式为：

```
test expression1 -a expression2
```

如果 expression1 和 expression2 都为真，则 test 命令返回真（退出状态为 0）。但是，如果 expression1 或 expression2 中任意一个为假，则 test 命令返回假（退出状态为 1）。

-o 运算符也组合两个表达式。它测试逻辑或关系。使用 -o 选项的 test 命令形式为：

```
test expression1 -o expression2
```

如果 expression1 或 expression2 中任意一个为真，则 test 命令返回真（退出状态为 0）。但是，如果两个表达式都为假，则 test 命令返回假（退出状态为 1）。

! 运算符否定表达式的值。这意味着如果表达式通常导致 test 返回真，则它反而返回假。同样，如果表达式通常导致 test 返回假，则它反而返回真。使用 ! 运算符的 test 命令形式为：

```
test !expression
```

为了演示 test 命令的布尔运算符：

- 1. 回想您在上一练习中创建的 test_file 文件具有读和写权限。输入 `test -r test_file -a -w test_file` 并按下 Enter。

此命令使用 AND（与）关系测试两个表达式：-r test_file 和 -w test_file。如果两个表达式都为真，则 test 命令返回真。

- 2. 输入 `echo $?` 并按下 Enter。您的屏幕看起来与图 7-12 类似。

![](img/6d8286a85e2d8ad63e16f1801102da59_252_0.png)

**图 7-12：使用布尔运算符测试文件**

test 命令返回退出状态 0，表示 test_file 可读且可写。

- 3. 输入 `test -x test_file -o -r test_file` 并按下 Enter。

此命令使用 OR（或）关系测试两个表达式：-x test_file 和 -r test_file。如果这两个表达式中任意一个为真，则 test 命令返回真。

- 4. 输入 `echo $?` 并按下 Enter。您的屏幕看起来与图 7-13 类似。

![](img/6d8286a85e2d8ad63e16f1801102da59_253_0.png)

**图 7-13：使用 OR 运算符进行测试**

test 命令返回退出状态 0，表示 test_file 是可执行的 OR 可读的。

- 5. 输入 `test ! -r test_file` 并按下 Enter。

此命令否定表达式 -r test_file 的结果。如果表达式为真，则 test 命令返回假。同样，如果表达式为假，则 test 命令返回真。

- 6. 输入 `echo $?` 并按下 Enter。您的屏幕看起来与图 7-14 类似。

![](img/6d8286a85e2d8ad63e16f1801102da59_254_0.png)

**图 7-14：使用否定运算符进行测试**

test 命令返回退出状态 1，表示表达式 ! -r test_file 为假。

接下来，您使用 test 命令来确定某个目录是否存在。这可以让您正确设置环境，以运行您在课程 B 中完成的 shell 脚本。在下个练习中，您将确定主目录中是否有 source 目录。如果没有，您将创建一个并将其添加到 PATH 变量中。这使您可以运行存储在该处的脚本文件，而无需在文件名前输入 ./。

为了确定某个目录是否存在：

- 1. 输入 `test -d source ; echo $?` 并按下 Enter。此命令确定 source 是否存在以及它是否为目录。由于 `echo $?` 命令包含在同一行中，按下 Enter 后退出状态会立即显示。如果退出状态为 0，则您已经拥有 source 目录。如果情况如此，请跳至步骤 3。否则，请继续步骤 2。
- 2. 如果您在步骤 1 中输入的命令导致退出状态为 1，则您必须创建 ~/source 目录。输入 `mkdir source` 并按下 Enter。
- 3. 在第 6 章中，您创建了文件 corp_phones 和 shell 脚本 phmenu 和 phoneadd。通过输入 `test -e corp_phones ; echo $?` 并按 Enter 来确定您是否拥有 corp_phones 文件。如果您看到退出状态 0，则文件存在。

