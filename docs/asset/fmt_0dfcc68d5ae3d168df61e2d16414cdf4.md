
```bash
if [ -n "$FRUIT_BASKET" ]; then
echo "Your fruit basket has the following fruit: $FRUIT_BASKET"
else
echo "Your fruit basket is empty";
fi
```

注意，在这个示例中 `$FRUIT_BASKET` 被加了引号。这是为了防止变量未设置时出现错误。如果 `$FRUIT_BASKET` 未加引号，将显示错误信息：

```
test: argument expected
```

显示此错误信息的原因是 shell 没有对 `$FRUIT_BASKET` 的空值加引号。结果 `test` 命令看起来像：

```
[ -z ]
```

由于缺少字符串，`test` 报错缺少必要的参数。通过给 `$FRUIT_BASKET` 加引号，`test` 看起来像：

```
[ -z "" ]
```

## 检查两个字符串是否相等

`test` 命令允许你确定两个字符串是否相等。如果两个字符串包含完全相同的字符序列，则认为它们相等。例如，字符串

```
"There are more things in heaven and earth"
"There are more things in heaven and earth"
```

是相等的，但以下字符串

```
"than are dreamt of in your philosophy"
"Than are dreamt of in your Philosophy"
```

因为大小写不同，是不相等的。

检查两个字符串是否相等的基本语法为

```
test string1 = string2
```

或者

```
[ string1 = string2 ]
```

这里 `string1` 和 `string2` 是正在比较的两个字符串。

使用字符串比较的简单示例如下：

```bash
if [ "$FRUIT" = apple ]; then
    echo "An apple day keeps the doctor away."
else
    echo "You must like doctors, your fruit $FRUIT is not an apple."
fi
```

如果使用 `!=` 代替 `=`，当两个字符串不等，`test` 返回真。使用 `!=` 运算符，你可以如下重写先的命令：

```bash
if [ "$FRUIT" != apple ]; then
    echo "You must like doctors, your fruit $FRUIT is not an apple."
else
    echo "An apple a day keeps the doctor away."
fi
```

### 数值比较

`test` 命令允许你比较两个整数。基本语法为

```
test int1 operator int2
```

或者

```
[ int1 operator int2 ]
```

这里 `int1` 和 `int2` 可以是任何正整数或负整数，`operator` 是表 10.3 中给出的运算符之一。如果 `int1` 或 `int2` 是字符串而不是整数，则被视为 0。

shell 脚本中最常见的任务之一是执行程序并检查其状态。通过使用数值比较运算符，你可以检查命令的返回或退出状态，并在命令成功或失败时执行不同的操作。

例如，考虑以下命令：

```
ln -s /home/ranga/bin/bash /usr/local/bin
```

如果你在命令行执行此命令，你可以看到任何错误信息并打算修复问题。在 shell 脚本中，错误信息会被忽略，脚本将继续执行。因此，有必要检查程序是否执行成功。

正如你通过 `test` 命令看到的，退出状态 0 表示成功，而非零值表示某种类型的失败。上一个命令的退出状态存储在变量 `$?` 中，你可以按照如下方式检查命令是否成功：

```bash
if [ $? -eq 0 ]; then
    echo "Command was successful."
fi
```

```
echo "An error was encountered."
exit
```

如果命令以退出代码 0 退出，则输出“良好”信息；否则，输出错误信息并退出。这可以简化为：

```bash
if [ $? -ne 0 ]; then
echo "An error was encountered."
exit
fi
echo "Command was successful."
```

### 表 10.3 数值比较

| 运算符 | 说明 |
| :--- | :--- |
| `-eq` | 如果 `int1` 等于 `int2`，则为真 |
| `-ne` | 如果 `int1` 不等于 `int2`，则为真 |
| `-lt` | 如果 `int1` 小于 `int2`，则为真 |
| `-le` | 如果 `int1` 小于或等于 `int2`，则为真 |
| `-gt` | 如果 `int1` 大于 `int2`，则为真 |
| `-ge` | 如果 `int1` 大于或等于 `int2`，则为真 |

### 复合表达式

到为止你已经看到了单独的表达式，但很多时候你需要组合表达式。你可以使用 `-a` 和 `-o` 运算符创建复合表达式。

### 表 10.4 创建复合表达式的运算符

| 运算符 | 说明 |
| :--- | :--- |
| `-a` | 如果两个表达式都为真，则为真 |
| `-o` | 如果任一表达式为真，则为真 |
| `!` | 如果表达式为假，则为真 |

### 使用内置运算符

使用内置运算符创建复合表达式的语法为

```
test expr1 -a expr2
```

或者

```
[ expr1 -a expr2 ]
```

这里 `expr1` 和 `expr2` 是被组合的表达式，运算符是 `-a`。

## 使用逻辑运算符

使用逻辑运算符创建复合表达式的语法为

```
test expr1 && expr2
```

或者

```
[ expr1 && expr2 ]
```

这里 `expr1` 和 `expr2` 是被组合的表达式，运算符是 `&&`。

同样，对于逻辑或操作：

```
test expr1 || expr2
```

或者

```
[ expr1 || expr2 ]
```

这里运算符是 `||`（对应于 `-o`）。

## 复合表达式示例

以下是演示如何创建复合表达式的两个等效示例：

```bash
if [ -z "$DHOME" ] && [ -d /usr/dt ]; then DHOME=/usr/dt ; fi
if [ -z "$DHOME" ] -a d /usr/dt ]; (此处原文有误)
```

第一个版本的执行方式如下：

1. 首先执行测试

```
[ -z "$DHOME" ]
```

2. 如果此测试返回 0，则执行第二个测试

```
[ -d /usr/dt ]
```

否则，if 语句结束。

3. 如果第二个测试返回 0，则执行变量赋值

```
DHOME=/usr/dt
```

否则，if 语句结束。

第二个版本的执行方式类似：

1. 首先评估表达式

```
-z "$DHOME"
```

2. 如果此表达式求值为 0，则评估表达式

```
-d /usr/dt
```

否则，if 语句结束。

3. 如果第二个表达式求值为 0，则执行变量赋值

```
DHOME=/usr/dt
```

否则，if 语句结束。

某些程序员倾向于使用逻辑运算符的版本，因为各个测试是隔离的。另一些人则倾向于第二种形式，因为它只调用一次 `test` 命令，在旧硬件或大量测试时可能会略微提高效率。

如果你对对旧系统的最大可移植性，你应该使用逻辑运算符。在现代 shell 中，两者的效果都很好，因此你可以使用任何一种。

在这个示例中，你只使用了两个表达式。你并不限于两个。事实上，任何数量的表达式都可以组合成一个复合表达式。

# 表达式否定

复合表达式的最后一种类型是对表达式取反。取反会反转表达式的结果。真表达式被视为假表达式，反之亦然。

取反操作符的基本语法

```
test ! expr
```

或者

```
[ ! expr ]
```

其中 `expr` 是任意合法的测试表达式。

一个简单的示例是以下命令：

```
$ if [ -d $HOME/bin ] ; then mkdir $HOME/bin ; fi
```

在这里，如果 `$HOME/bin` 目录不存在，则创建该目录。执行过程如下：

- 1. 首先执行测试

```
-d $HOME/bin
```
