
```
echo "Files file1.txt and file2.txt are the same."
```
else
```
echo "Files file1.txt and file2.txt differ."
```
fi

# Bash 脚本

是时候回到我们的备份脚本了。脚本有一个命令块。`bsdtar` 工具的结果决定了 Bash 是否应该执行此块。当我们遇到代码块和条件时，它是在此应用此语句的提示。

我们将 `if-else` 语句应用于 `bsdtar` 调用并处理其结果。然后我们得到了以下代码：

```
if bsdtar -cjf "$1".tar.bz2 "$@"
then
    echo "bsdtar - OK" > results.txt
else
    echo "bsdtar - FAILS" > results.txt
    exit 1
fi
```

你是否同意现在代码更容易读了？我们可以进一步简化。提前返回模式可以做到。将 `if-else` 语句替换为 `if`，如下：

```
if bsdtar -cjf "$1".tar.bz2 "$@"
then
    echo "bsdtar - FAILS" > results.txt
    exit 1
fi
echo "bsdtar - OK" > results.txt
```

代码的行为与 `if-else` 语句尽可能相同。逻辑否定反转了 `bsdtar` 工具的结果。现在，如果它失败，`if` 语句的条件变为“true”。

代码的行为与 `if-else` 语句尽可能相同。逻辑否定反转了 `bsdtar` 工具的结果。现在，如果它失败，`if` 语句的条件变为“true”。然后脚本向日志文件打印“bsdtar - FAILS”消息并终止。否则，脚本跳过 `if` 语句的命令块。后续的 `echo` 调用将“bsdtar - OK”消息写入日志文件。

提前返回模式是一种实用的技术，让你的代码更简洁易读。其原理是在错误出现时尽快终止程序。这种解决方案允许你避免嵌套的 `if` 语句。

这是一个示例。想象一个执行五个动作的算法。每个动作都取决于上一个动作的结果。如果上一个动作失败，算法就会停止。我们可以用这个实现该算法：

- https://medium.com/nested-if-statements

# Bash 脚本

我们可以通过结合 `if` 语句和 `grep` 工具来解决此任务。将 `grep` 调用放在 `if` 条件中。如果该工具执行成功，它将返回零退出状态。在这种情况下，如果条件等于 "true"，脚本将打印该消息。

`grep` 工具将其结果打印到输出流中。当我们在条件中调用该工具时，不需要这些输出。`-q` 选项禁用了 `grep` 输出。最后，我们得到了如下 `if` 语句：

```
if grep -q -R "General Public License" /usr/share/doc/bash
then
  echo "Bash has the GPL license"
fi
```

现在假设 `if` 条件在比较两个字符串或数字。Bash 有一个特殊的运算符 `[[` 用于此目的，双方括号是解释器的一个保留字。Bash 处理这些括号时不需要调用工具。

> Bourne shell（Bourne shell）没有 `[[` 运算符。POSIX 标准也没有。因此，如果你必须使用标准，请使用过时的 `test` 运算符或其同义词 `[`。永远不要在 bash 中使用 `test`。它在使用 `[[` 运算符时的功能有限。此外，它的语法容易引发错误。

让我们从一个使用 `[[` 的简单示例开始。我们需要比较两个字符串。在这种情况下，`if` 条件如下：

```
if [[ "abc" = "abc" ]]
then
  echo "The strings are equal"
fi
```

运行这段代码。你会看到字符串相等的消息。这种检查并没真正有用。通常，你想将某个变量与字符串进行比较。`[[` 运算符通过这种方式比较它们：

```
if [[ "$var" = "abc" ]]
then
  echo "The variable equals the \"abc\" string"
fi
```

在该条件下，双引号是可选的。当 Bash 在 `[[` 运算符中替换变量时，会跳过单词拆分（word splitting）。解释器在该运算符中按其原样使用变量。引号可以防止在右侧包含空格时出现问题。这里有一个此类字符串的示例：

- ^99 https://en.wikipedia.org/wiki/Reserved_word
- ^100 http://mywiki.wooledge.org/BashFAQ/03

# Bash 脚本

```
if [[ "$var" = abc def ]]
then
echo "The variable equals the \"abc def\" string"
fi
```

由于单词拆分，Bash 无法执行此 `if` 语句的条件。处理字符串时请始终使用引号。这样你就可以避免此类问题。这里是修复后的 `if` 条件：

```
if [[ "$var" = "abc def" ]]
then
echo "The variable equals the \"abc def\" string"
fi
```

`[[` 运算符比较两个变量。它看起来如下：

```
if [[ "$var" = "$filename" ]]
then
echo "The variables are equal"
fi
```

表 3-8 显示了 `[[` 运算符允许的所有字符串比较。

### 表 3-8. [[ 运算符中的字符串比较

| 操作 | 描述 | 示例 |
|---|---|---|
| > | 左侧的字符串在字典序*上大于右侧的字符串 | [[ "bb" > "aa" ]] && echo "The bb string is larger than \"aa\"" |
| < | 左侧的字符串在字典序上小于右侧的字符串 | [[ "ab" < "ac" ]] && echo "The ab string is smaller than \"ac\"" |
| or == | 字符串相等 | [[ "abc" = "abc" ]] && echo "The strings are equal" |
| != | 字符串不等 | [[ "abc" != "ab" ]] && echo "The strings are not equal" |
| -z | 字符串为空 | [[ -z "$var" ]] && echo "The string is empty" |
| -n | 字符串不空 | [[ -n "$var" ]] && echo "The string is not empty" |

> *^301 https://en.wikipedia.org/wiki/Lexicographic_order

# Bash 脚本

### 表 3-8. [[ 运算符中的字符串比较

| 操作 | 描述 | 示例 |
|---|---|---|
| -v | 变量被赋值为任何值 | [[ -v var ]] && echo "The string is set" |
| = or == | 在左侧的字符串中搜索右侧的模式。模式不加引号 | [[ "$filename" = READ* ]] && echo "The filename starts with \"READ\"" |
| != | 检查右侧的模式未出现在左侧的字符串中。模式不加引号 | [[ "$filename" != READ* ]] && echo "The filename does not start with \"READ\"" |
| ~ | 在左侧搜索右侧的正则表达式* | [[ "$filename" ~ READ* ]] && echo "The filename starts with \"READ\"" |

你可以在 `[[` 运算符中使用逻辑操作 AND、OR 和 NOT。它们将表达式组合成一个单一条件。表 3-9 提供了此类条件的示例。

### 表 3-9. [[ 运算符中的逻辑操作

| 操作 | 描述 | 示例 |
|---|---|---|
| && | 逻辑与 | [[ -n "$var" && "$abc" ]] && echo "The string is not empty and it is smaller than \"abc\"" |
| || | 逻辑或 | [[ "abc" < "$var" ]] && echo "The string is larger than \"abc\" or it is empty" |
| ! | 逻辑非 | [[ "1" < "$var" ]] && echo "The string is larger than \"abc\"" |

# Bash 脚本

你可以使用括号在 `[[` 运算符中对表达式。这里有一个示例：

```
[[ (a || b) && c ]]
```

> $301 https://en.wikipedia.org/wiki/RegularExpression

# Bash 脚本

### 表 3-11. [[ 运算符中的整数比较

| 操作 | 描述 | 示例 |
|---|---|---|
| -eq | 左侧的数字等于右侧的数字 | [[ "$var" -eq 5 ]] && echo "The variable equals 5" |
| -ne | 数字不等 | [[ "$var" -ne 5 ]] && echo "The variable is not equal to 5" |
| -gt | 大于 (>) | [[ "$var" -gt 5 ]] && echo "The variable is greater than 5" |
| -ge | 大于等于 | [[ "$var" -ge 5 ]] && echo "The variable is greater or equal to 5" |
| -lt | 小于 (<) | [[ "$var" -lt 5 ]] && echo "The variable is less than 5" |
| -le | 小于等于 | [[ "$var" -le 5 ]] && echo "The variable is less or equal to 5" |

表 3-11 提出了问题。这些操作是 < 和 =。为什么在 `[[` 运算符的通常数字比较中不使用 <、> = 等比较符号？为了回答这个问题，让我们看看该运算符的历史。

`[[` 运算符进入 Bash 是为了取代其过时的 `test` 对应物。该工具在 1979 年的 Bourne shell 第一版本中实现了 `test` 命令。该命令从 1981 年的 System III shell 版本开始变为内置。但这种变化没有影响 `test` 的语法。原因是向后兼容。软件开发者在 1981 年已经编写了大量的 shell 代码。因此，新的 System III shell 版本必须支持它。

让我们看看该运算符的语法。当它是一个工具时，输入参数的格式必须遵循 Bourne shell 规则。例如，这里有一个比较 `var` 变量与数字五的典型测试：

```
test "$var" -eq 5
```

此命令没有引起任何问题。在这里我们向 `test` 工具传递了三个参数：

+   1. `var` 变量的值。
2. `-eq` 选项。
3. 数字 5。

我们可以这样在 `if` 条件中使用该调用：

```bash
if test "$var" -eq 5
then
    echo "The variable equals 5"
fi
```

Bourne shell 引入了 `[` 作为测试运算符。它们之间唯一的区别在于是否存在右括号。`test` 操作符不需要它，但这个同义词需要。

使用 `[` 同义词，我们这样重写 `if` 条件：

```bash
if [ "$var" -eq 5
then
    echo "The variable equals 5"
fi
```

同义词 `[` 提高了代码的可读性，这是其背后的设计理念。对于同义词来说，Bourne shell 中的 `if` 语句看起来与其他编程语言（如 C、C++）一样。问题在于 `[` 测试操作符是等价的，人们很容易忽视这一点。这通常发生在你有其他语言的经验时。预期行为与实际行为之间的不匹配会导致错误。

例如，程序员经常忘记在括号 `[` 和后续字符之间留空格。这样，他们得到了类似这样的条件：

```bash
if ["var" -eq 5
then
    echo "The variable equals 5"
fi
```

将括号 `[` 替换为条件中的测试调用。这时错误变得显而易见：

```bash
if test"$var" -eq 5
then
    echo "The variable equals 5"
fi
```

命令名与其参数之间必须有一个空格。

让我们回到关于数字比较符号的问题。假设有以下测试调用：

# Bash 脚本

test "var" > 5

正如你记得，`>` 符号是重定向运算符 `>` 的简形式。因此，你的测试调用执行了以下步骤：

1. 调用内置的 `test` 命令并将变量 `var`传递给它。
2. 将测试输出重定向到当前目录下名为 `5` 的文件中。

我们期望的是另一种行为。这种错误很容易产生且难以检测。为了防止这种情况，shell 开发者引入了双字母比较操作。Bash 运算符 `[[` 继承了这些操作，这是为了向后兼容。

假设 `[[` 运算符用比较符号替换了双字母操作。现在有一段用 Bourne shell 编写的遗留代码，你想将其迁移到 Bash。遗留代码中有如下 `if` 语句：

```bash
if [ "var1" -gt 5 -o 4 -lt "$var2" ]
then
echo "The var1 variable is greater than 5 or var2 is less than 4"
fi
```

在这里，你将 `-gt` 操作替换为 `>`，将 `-lt` 替换为 `<`。在此过程中很容易出错。在表达式的开头和结尾加上额外的括号要简单得多。这回答了我们的问题。

只有在配合 `[[` 运算符时才能对字符串使用比较符号。为什么这里没有向后兼容问题呢？第一版本的 `test` 工具不支持字符串的字典序比较。因此，该工具没有 `<` 和 `>` 比较符号。它们出现在 POSIX 标准的扩展中。标准仅允许字符串使用比较符号。由于遗留代码数量巨大，为数字添加这些符号已经太晚了。根据标准，你应该这样转义比较符号：`/\` 和 `/\>`。`[[` 运算符接收了它们并去掉了转义。

练习 3-5. [[ 运算符

编写一个脚本比较两个名为 "dir1" 和 "dir2" 的目录
脚本应该打印一个目录存在而另一个目录中不存在的所有文件。

# Case 语句

程序经常根据某些值选择它们的动作。如果变量有一个值，程序执行一件事。当值不同时，它执行另一件事。条件语句提供了这种行为。

# Bash 脚本

我们已经考虑了 `if` 语句。Bash 中有另一种替代方案 `case` 语句。在某些情况下，它比 `if` 更方便。

让我们来看一个例子。假设你正在编写一个归档文档的脚本。脚本有三种运行模式：

1. 不压缩归档。
2. 压缩归档。
3. 解压缩。

你可以通过命令行选项选择模式。表 3-12 显示了可能的选项示例。

表 3-12 归档脚本的选项

| 选项 | 模式 |
| :--- | :--- |
| -a | 不压缩归档 |
| -c | 压缩归档 |
| -x | 解压缩 |

> 在选择脚本³⁶选项和参数格式时，始终遵循 POSIX 协议³⁴ 及其 GNU 扩展³⁵。

你可以在 `if` 语句中检查脚本选项。列表 3-12 显示了这样做的示例。

列表 3-12 归档文档脚本

```bash
1 #/bin/bash

2

3 operation="$1"

4

5 if [[ "$operation" == "-a" ]];
6 then
7 bsdtar c -f documents.tar ~Documents
8 elif [[ "$operation" == "-c" ]];
9 then
10 bsdtar c -j -f documents.tar.bz2 ~Documents
11 elif [[ "$operation" == "-x" ]];
12 then
13 bsdtar -x -f documents.tar*
14 else
15 echo "Invalid option"
16 exit 1
17 fi
```

位置参数 `$1` 保留了脚本选项。为了方便，将其写入 `operation` 变量。然后根据这个变量，为 `bsdtar` 调用选择参数。带有 `elif` 块的 `if` 语句阻塞操作值。
现在我们将 `if` 语句替换为 `case` 语句。列表 3-13 显示了一个示例。

列表 3-13 归档文档脚本

```bash
#!/bin/bash
operation="$1"
case "$operation" in
  "-a")
    bsdtar c -f documents.tar ~Documents
    ;;
  "-c")
    bsdtar c -j -f documents.tar.bz2 ~Documents
    ;;
  "-x")
    bsdtar -x -f documents.tar*
    ;;
  *)
    echo "Invalid option"
```
