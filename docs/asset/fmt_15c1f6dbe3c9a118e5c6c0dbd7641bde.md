
```
#!/bin/bash

# test-integer2: evaluate the value of an integer.
INT=-5

if [[ "$INT" =~ ^-?[0-9]+$ ]]; then
    if [ $INT -eq 0 ]; then
        echo "INT is zero."
    else
        if [ $INT -lt 0 ]; then
            echo "INT is negative."
        else
            echo "INT is positive."
        fi
        if [ $((INT % 2)) -eq 0 ]; then
            echo "INT is even."
        else
            echo "INT is odd."
        fi
    fi
else
    echo "INT is not an integer." >&2
    exit 1
fi
```

通过应用正则表达式，我们能够将`INT`的值限制为仅以可选的减号开头，后跟一个或多个数字的字符串。此表达式还排除了空值可能性。

`[[ ]]`的另一个新增功能是`==`运算符支持与路径名展开相同方式的模式匹配。例如：

```
[me@linuxbox ~]$ FILE=foo.bar
[me@linuxbox ~]$ if [[ $FILE == foo.* ]]; then
> echo "$FILE matches pattern 'foo.*'"
> fi
foo.bar matches pattern 'foo.*'
```

这使得`[[ ]]`在评估文件和路径名时非常有用。

#### `(( ))` - 专为整数设计

除了`[[ ]]`复合命令之外，`bash`还提供了`(( ))`复合命令，它对于操作整数很有用。它支持完整的算术求值集，我们将在第 35 章中全面介绍该主题。

`(( ))`用于执行算术真值测试。算术真值测试如果算术求值结果非零则返回 true。

```
[me@linuxbox ~]$ if ((1)); then echo "It is true."; fi
It is true.
[me@linuxbox ~]$ if ((0)); then echo "It is true."; fi
[me@linuxbox ~]$
```

使用`(( ))`，我们可以稍微简化`test-integer2`脚本，如下所示：

```
#!/bin/bash

# test-integer2a: evaluate the value of an integer.

INT=-5

if [[ "$INT" =~ ^-?[0-9]+$ ]]; then
    if ((INT == 0)); then
        echo "INT is zero."
    else
        if ((INT < 0)); then
            echo "INT is negative."
        else
            echo "INT is positive."
        fi
        if (( (INT % 2) == 0)); then
            echo "INT is even."
        else
            echo "INT is odd."
        fi
    fi
else
    echo "INT is not an integer." >&2
    exit 1
fi
```

请注意，我们使用小于号和大于号，并且使用`==`来测试相等性。这是在处理整数时更自然的语法。请注意，因为复合命令`(( ))`是`shell`语法的一部分而不是一个普通的命令，它只处理整数，能够按名称识别变量并且不需要进行展开。我们将在第 35 章进一步讨论`(( ))`以及相关的算术展开。

#### 组合表达式

也可以组合表达式以创建更复杂的求值。表达式是通过使用逻辑运算符组合的。我们在第 18 章学习`find`命令时见过这些。`test`和`[[ ]]`有三种逻辑操作。它们是 AND、OR 和 NOT。`test`和`[[ ]]`使用不同的运算符来表示这些操作：

Table 28-4: Logical Operators

| Operation | `test` | `[[ ]]` and `(( ))` |
|-----------|--------|---------------------|
| AND | `-a` | `&&` |
| OR | `-o` | `||` |
| NOT | `!` | `!` |

下面是一个 AND 操作的示例。以下脚本确定一个整数是否在值范围内：

```
#!/bin/bash

# test-integer3: determine if an integer is within a
# specified range of values.

MIN_VAL=1
MAX_VAL=100

INT=50

if [[ "$INT" =~ ^-?[0-9]+$ ]]; then
    if [[ INT -ge MIN_VAL && INT -le MAX_VAL ]]; then
        echo "$INT is within $MIN_VAL to $MAX_VAL."
    else
        echo "$INT is out of range."
    fi
else
    echo "INT is not an integer." >&2
    exit 1
fi
```

在此脚本中，我们确定整数`INT`的值是否介于`MIN_VAL`和`MAX_VAL`的值之间。这是通过一次使用`[[ ]]`实现的，其中包含两个由`&&`运算符分隔的表达式。我们也可以使用`test`编写此代码：

```
if [ $INT -ge $MIN_VAL -a $INT -le $MAX_VAL ]; then
    echo "$INT is within $MIN_VAL to $MAX_VAL."
else
    echo "$INT is out of range."
fi
```

`!`否定运算符会反转表达式的结果。如果表达式为假，则返回真；如果表达式为真，则返回假。在以下脚本中，我们修改了求值的逻辑以查找`INT`的值位于指定范围之外的情况：

```
#!/bin/bash

# test-integer4: determine if an integer is outside a
# specified range of values.

MIN_VAL=1
MAX_VAL=100

INT=50

if [[ "$INT" =~ ^-?[0-9]+$ ]]; then
    if [[ ! (INT -ge MIN_VAL && INT -le MAX_VAL) ]]; then
        echo "$INT is outside $MIN_VAL to $MAX_VAL."
    else
        echo "$INT is in range."
    fi
else
    echo "INT is not an integer." >&2
    exit 1
fi
```

我们还对表达式加上了括号以进行分组。如果没有包含这些括号，否定只会应用于第一个表达式，而不会应用于两个表达式的组合。使用`test`编写此代码的方式如下：

```
if [ ! \( $INT -ge $MIN_VAL -a $INT -le $MAX_VAL \ ) ]; then
    echo "$INT is outside $MIN_VAL to $MAX_VAL."
else
    echo "$INT is in range."
fi
```

由于`test`使用的所有表达式和运算符都由`shell`作为命令参数处理（不像`[[ ]]`和`(( ))`），对`bash`具有特殊意义的字符，例如`<`、`>`、`(`和`)`，必须加引号或转义。

既然`test`和`[[ ]]`做的事情大致相同，哪一个更可取？`test`是传统的（并且是 POSIX 的一部分），而`[[ ]]`是`bash`特有的。了解如何使用`test`很重要，因为它被广泛使用，但`[[ ]]`显然更有用且更容易编码。

#### 可移植性是小人的恶魔

如果你与“真正的” Unix 人交谈，你很快就会发现他们中的许多人并不太喜欢 Linux。他们认为它是不纯洁和不干净的。Unix 追随者的一项信条是，一切都应该是“可移植的”。这意味着你编写的任何脚本都应该能够在任何类 Unix 系统上不加修改地运行。

Unix 人有充分的理由相信这一点。在见识到 POSIX 之前，命令和 shell 的专有扩展对 Unix 世界造成的破坏后，他们自然会对 Linux 对他们钟爱的 OS 的影响保持警惕。
