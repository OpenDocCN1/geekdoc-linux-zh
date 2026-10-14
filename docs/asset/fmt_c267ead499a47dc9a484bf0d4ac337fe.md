
该脚本评估分配给常量 `FILE` 的文件，并在评估过程中显示其结果。关于此脚本，有两点值得注意。首先，注意参数 `$FILE` 在表达式中是如何被引用的。这不是为了在语法上完成表达式所必需的；而是为了防止参数为空或仅包含空白。如果 `$FILE` 的参数扩展导致空值，将会导致错误（运算符将被解释为非空字符串而不是运算符）。在参数周围使用引号可确保运算符始终跟随一个字符串，即使该字符串为空。其次，注意脚本末尾附近的 `exit` 命令的存在。`exit` 命令接受一个单一的可选参数，该参数成为脚本的退出状态。当未传递参数时，退出状态默认为最后执行的命令的退出状态。以这种方式使用 `exit` 允许脚本在 `$FILE` 扩展为不存在的文件名时指示失败。脚本最后一行的 `exit` 命令只是出于形式。当脚本“运行到末尾”（到达文件末尾）时，它将以最后执行的命令的退出状态终止。

类似地，shell 函数可以通过在 `return` 命令中包含整数参数来返回退出状态。如果我们将之前的脚本转换为 shell 函数以包含在更大的程序中，我们可以将 `exit` 命令替换为 `return` 语句并获得所需的行为。

```
test_file () {
    # test-file: Evaluate the status of a file
    
    FILE=~/.bashrc
    
    if [ -e "$FILE" ]; then
        if [ -f "$FILE" ]; then
            echo "$FILE is a regular file."
        fi
        if [ -d "$FILE" ]; then
echo "$FILE is a directory."
fi
if [ -r "$FILE" ]; then
    echo "$FILE is readable."
fi
if [ -w "$FILE" ]; then
    echo "$FILE is writable."
fi
if [ -x "$FILE" ]; then
    echo "$FILE is executable/searchable."
fi
else
    echo "$FILE does not exist"
    return 1
fi
}
```

### 字符串表达式

表 27-2 列出了用于评估字符串的表达式。

表 27-2：`test` 字符串表达式

| 表达式 | 在以下情况下为真： |
|---|---|
| `string` | `string` 不为空。 |
| `-n string` | `string` 的长度大于零。 |
| `-z string` | `string` 的长度为零。 |
| `string1 = string2`<br>`string1 == string2` | `string1` 和 `string2` 相等。可使用单等号或双等号。强烈建议使用双等号，但它不符合 POSIX 标准。 |
| `string1 != string2` | `string1` 和 `string2` 不相等。 |
| `string1 > string2` | `string1` 在排序中位于 `string2` 之后。 |
| `string1 < string2` | `string1` 在排序中位于 `string2` 之前。 |

#### 警告

使用 `test` 时，`>` 和 `<` 表达式操作符必须加引号（或使用反斜杠转义）。如果不这样做，它们将被 shell 解释为重定向操作符，可能导致破坏性结果。另请注意，虽然 `bash` 文档说明排序顺序符合当前区域设置的排序顺序，但实际上并非如此。在 `bash` 4.0 及更早版本中，使用的是 ASCII（POSIX）顺序。该问题在 4.1 版本中已修复。

下面是一个包含字符串表达式的脚本：

```
#!/bin/bash

# test-string: evaluate the value of a string

ANSWER=maybe

if [ -z "$ANSWER" ]; then
    echo "There is no answer." >&2
    exit 1
fi

if [ "$ANSWER" = "yes" ]; then
    echo "The answer is YES."
elif [ "$ANSWER" = "no" ]; then
    echo "The answer is NO."
elif [ "$ANSWER" = "maybe" ]; then
    echo "The answer is MAYBE."
else
    echo "The answer is UNKNOWN."
fi
```

在此脚本中，我们评估常量 `ANSWER`。我们首先确定字符串是否为空。如果为空，我们终止脚本并将退出状态设置为 1。请注意应用于 `echo` 命令的重定向。这会将错误消息“ There is no answer.”重定向到标准错误，这是处理错误消息的正确做法。如果字符串不为空，我们将评估字符串的值，查看它是否等于“yes”、“no”或“maybe”。我们通过

使用 `elif`，即“else if”的缩写。通过使用 `elif`，我们能够构建更复杂的逻辑测试。

### 整数表达式

要将值作为整数而不是字符串进行比较，我们可以使用表 27-3 中列出的表达式。

表 27-3：`test` 整数表达式

| 表达式 | 在以下情况下为真： |
|---|---|
| `integer1 -eq integer2` | `integer1` 等于 `integer2`。 |
| `integer1 -ne integer2` | `integer1` 不等于 `integer2`。 |
| `integer1 -le integer2` | `integer1` 小于或等于 `integer2`。 |
| `integer1 -lt integer2` | `integer1` 小于 `integer2`。 |
| `integer1 -ge integer2` | `integer1` 大于或等于 `integer2`。 |
| `integer1 -gt integer2` | `integer1` 大于 `integer2`。 |

下面是一个演示它们的脚本：

```
#!/bin/bash

# test-integer: evaluate the value of an integer.

INT=-5

if [ -z "$INT" ]; then
    echo "INT is empty." >&2
    exit 1
fi

if [ "$INT" -eq 0 ]; then
    echo "INT is zero."
else
    if [ "$INT" -lt 0 ]; then
        echo "INT is negative."
    else
        echo "INT is positive."
    fi
fi
if [ $((INT % 2)) -eq 0 ]; then
else  echo "INT is even."
fi  echo "INT is odd."
fi
```

脚本有趣的部分在于它如何确定整数是偶数还是奇数。通过对数字执行取模 2 操作，该操作将数字除以 2 并返回余数，它可以判断数字是奇数还是偶数。

### test 的更现代版本

现代版本的 `bash` 包含一个复合命令，可作为 `test` 的增强替代品。它使用以下语法：

```
[[ expression ]]
```

其中，与 `test` 类似，`expression` 是一个求值为真或假结果的表达式。`[[ ]]` 命令与 `test` 类似（它支持所有表达式），但增加了重要的新字符串表达式。

```
string1 =~ regex
```

如果 `string1` 与扩展正则表达式 `regex` 匹配，则返回 true。这为执行诸如数据验证等任务提供了许多可能性。在我们之前整数表达式的示例中，如果常量 `INT` 包含除整数以外的任何内容，脚本就会失败。脚本需要一种方法来验证常量是否包含整数。使用 `[[ ]]` 与 `=~` 字符串表达式操作符，我们可以这样改进脚本：

```
#!/bin/bash

# test-integer2: evaluate the value of an integer.

INT=-5

if [[ "$INT" =~ ^-?[0-9]+$ ]]; then
    if [ "$INT" -eq 0 ]; then
echo "INT is zero."
else
  if [ "$INT" -lt 0 ]; then
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
