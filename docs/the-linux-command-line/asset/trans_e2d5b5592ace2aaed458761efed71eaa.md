

## test-integer：评估整数的值。

```
# test-integer: evaluate the value of an integer.

INT=-5

if [ -z "$INT" ]; then
    echo "INT is empty." >&2
    exit 1
fi

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
```

脚本有趣的部分在于它如何判断一个整数是偶数还是奇数。通过对数字执行取模 2 操作，该操作将数字除以二并返回余数，就能判断出数字是奇数还是偶数。

## test 的一个更现代版本

bash 的最近版本包含了一个复合命令，它作为 test 的增强替代品。其使用以下语法：

[[ expression ]]

其中，与 test 类似，expression 是一个求值为真或假结果的表达式。[[ ]] 命令与 test 非常相似（它支持 test 的所有表达式），但增加了重要的新字符串表达式：

string1 =~ regex

如果 string1 与扩展正则表达式 regex 匹配，则返回 true。这为执行诸如数据验证之类的任务提供了许多可能性。在我们之前整数表达式的示例中，如果常量 INT 包含除整数以外的任何内容，脚本就会失败。脚本需要一种方法来验证常量是否包含整数。使用带有 =~ 字符串表达式运算符的 [[ ]]，我们可以这样改进脚本：

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

通过应用正则表达式，我们能够将 INT 的值限制为仅以可选的减号开头，后跟一个或多个数字的字符串。此表达式还排除了空值可能性。

[[ ]] 的另一个新增功能是 == 运算符支持与路径名展开相同方式的模式匹配。例如：

```
[me@linuxbox ~]$ FILE=foo.bar
[me@linuxbox ~]$ if [[ $FILE == foo.* ]]; then
> echo "$FILE matches pattern 'foo.*'"
> fi
foo.bar matches pattern 'foo.*'
```

这使得 [[ ]] 在评估文件和路径名时非常有用。

## (( )) - 专为整数设计

除了 [[ ]] 复合命令之外，bash 还提供了 (( )) 复合命令，它对于操作整数很有用。它支持完整的算术求值集，我们将在第 35 章中全面介绍该主题。

(( )) 用于执行算术真值测试。算术真值测试如果算术求值结果非零则返回 true。

```
[me@linuxbox ~]$ if ((1)); then echo "It is true."; fi
It is true.
[me@linuxbox ~]$ if ((0)); then echo "It is true."; fi
[me@linuxbox ~]$
```

使用 (( ))，我们可以稍微简化 test-integer2 脚本，如下所示：

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

请注意，我们使用小于号和大于号，并且使用 == 来测试相等性。这是在处理整数时更自然的语法。请注意，因为复合命令 (( )) 是 shell 语法的一部分而不是

