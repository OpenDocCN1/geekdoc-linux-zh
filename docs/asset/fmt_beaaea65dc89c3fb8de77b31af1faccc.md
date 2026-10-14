
通过应用正则表达式，我们可以将`INT`的值限制为仅包含以可选减号开头、后跟一个或多个数字的字符串。该表达式还排除了空值的可能性。

`[[ ]]`的另一个附加功能是，`==`运算符支持与路径名展开相同方式的模式匹配。这里有一个示例：

```
[me@linuxbox ~]$ FILE=foo.bar
[me@linuxbox ~]$ if [[ $FILE == foo.* ]]; then
> echo "$FILE matches pattern 'foo.*'"
> fi
foo.bar matches pattern 'foo.*'
```

这使得`[[ ]]`在评估文件和路径名时非常有用。

## `(( ))` — 专为整数设计

`(( ))`用于执行算术真值测试。如果算术求值的结果为非零，则算术真值测试的结果为真。

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
        if (( ((INT % 2)) == 0)); then
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

注意，我们使用了小于号和大于号，并使用`==`来测试相等性。对于处理整数来说，这是一种更自然的语法。还要注意，由于复合命令`(( ))`是 shell 语法的一部分，而非普通命令，并且它只处理整数，因此它能够按名称识别变量，并且不需要执行展开。我们将在第 34 章进一步讨论`(( ))`及相关算术展开。

### 组合表达式

也可以组合表达式以创建更复杂的求值。表达式通过使用逻辑运算符来组合。我们在第 17 章学习`find`命令时见过这些运算符。`test`和`[[ ]]`有三种逻辑运算，即 AND、OR 和 NOT。`test`和`[[ ]]`使用不同的运算符来表示这些操作，如表 27-4 所示。

表 27-4：逻辑运算符

| 运算 | `test` | `[[ ]]` 和 `(( ))` |
| --- | --- | --- |
| AND | `-a` | `&&` |
| OR | `-o` | `\|\|` |
| NOT | `!` | `!` |

下面是一个 AND 运算的示例。以下脚本确定一个整数是否在某个值范围内：

```
#!/bin/bash

# test-integer3: determine if an integer is within a
# specified range of values.

MIN_VAL=1
MAX_VAL=100

INT=50
if [[ "$INT" =~ ^-?[0-9]+$ ]]; then
    if [[ "$INT" -ge "$MIN_VAL" && "$INT" -le "$MAX_VAL" ]]; then
        echo "$INT is within $MIN_VAL to $MAX_VAL."
    else
        echo "$INT is out of range."
    fi
else
    echo "INT is not an integer." >&2
    exit 1
fi
```

在此脚本中，我们确定整数`INT`的值是否介于`MIN_VAL`和`MAX_VAL`之间。这是通过单次使用`[[ ]]`来完成的，其中包含两个由`&&`运算符分隔的表达式。我们也可以使用`test`来编写：

```
if [ "$INT" -ge "$MIN_VAL" -a "$INT" -le "$MAX_VAL" ]; then
    echo "$INT is within $MIN_VAL to $MAX_VAL."
else
    echo "$INT is out of range."
fi
```

`!`否定运算符会反转表达式的结果。如果表达式为假，则返回真；如果表达式为真，则返回假。在以下脚本中，我们修改了求值逻辑，以找出指定范围之外的`INT`值：

```
#!/bin/bash

# test-integer4: determine if an integer is outside a
# specified range of values.

MIN_VAL=1
MAX_VAL=100

INT=50

if [[ "$INT" =~ ^-?[0-9]+$ ]]; then
    if [[ ! ( "$INT" -ge "$MIN_VAL" && "$INT" -le "$MAX_VAL" ) ]]; then
        echo "$INT is outside $MIN_VAL to $MAX_VAL."
    else
        echo "$INT is in range."
    fi
else
    echo "INT is not an integer." >&2
    exit 1
fi
```

我们还在表达式周围加上括号，以便进行分组。如果不加这些括号，否定将只应用于第一个表达式，而不是两个表达式的组合。使用`test`编写此代码的方式如下：

```
if [ ! \( "$INT" -ge "$MIN_VAL" -a "$INT" -le "$MAX_VAL" \) ]; then
    echo "$INT is outside $MIN_VAL to $MAX_VAL."
else
    echo "$INT is in range."
fi
```

由于 `test` 使用的所有表达式和运算符都被 shell 当作命令参数处理（不像 `[[ ]]` 和 `(( ))`），对 `bash` 具有特殊含义的字符，例如 `<`、`>`、`(` 和 `)`，必须加引号或转义。

既然 `test` 和 `[[ ]]` 做的事情大致相同，哪一个更可取？`test` 是传统的（并且是 POSIX 标准 shell 规范的一部分，常用于系统启动脚本），而 `[[ ]]` 是 `bash` 特有的（以及少数其他现代 shell）。了解如何使用 `test` 很重要，因为它被广泛使用，但 `[[ ]]` 明显更有用且更容易编码，因此在现代脚本中更受青睐。

> **可移植性是小人之心**
> 
> 如果你和“真正的”Unix 人交谈，你很快就会发现他们中的许多人不怎么喜欢 Linux。他们认为它不纯洁、不干净。Unix 用户的一个信条是，一切都应该是“可移植的”。这意味着你写的任何脚本都应该能够在任何类 Unix 系统上不加修改地运行。
> 
> Unix 人之所以这样认为是有充分理由的。在见识到 POSIX 之前，命令和 shell 的专有扩展对 Unix 世界造成的破坏后，他们自然对 Linux 对他们钟爱的系统的影響保持警惕。
> 
> 但 *可移植性* 有一个严重的缺点。它阻碍了进步。它要求一切都必须使用“最低公分母”技术来完成。在 shell 编程中，这意味着要与 `sh`，即原始的 Bourne shell 保持兼容。
> 
> 这个缺点正是专有软件供应商用来为其专有扩展辩护的借口，他们只是称之为“创新”。但它们实际上只是锁定客户的手段。

GNU 工具，如 `bash`，并没有这样的限制。它们通过支持标准并普遍可用来鼓励可移植性。你可以在几乎任何系统上，甚至 Windows 上免费安装 `bash` 和其他 GNU 工具。因此，请随意使用 `bash` 的所有功能。它真的很可移植。

### 控制运算符：另一种分支方式

`bash`提供了两个可以执行分支的控制运算符。`&&`（AND）和`||`（OR）运算符的工作方式与`[[ ]]`复合命令中的逻辑运算符类似。下面是`&&`的语法：

```
command1 && command2
```

下面是`||`的语法：

```
command1 || command2
```
