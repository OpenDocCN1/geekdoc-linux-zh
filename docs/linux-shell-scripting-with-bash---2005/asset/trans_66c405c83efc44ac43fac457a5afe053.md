

它还增强了模式匹配功能，但缺乏 Bash `test` 命令的许多特性。除非你正在将 Korn shell 脚本移植到 Bash，否则强烈建议不要使用 Korn shell 的 `test` 命令。

## 字符串

`test` 命令可以比较两个字符串。

- `-z s`—*(零长度)* 如果字符串为空，则为真
- `-n s`（或仅 *s*）—*(非空)* 如果字符串不为空，则为真
- *s1* = *s2*—如果字符串 *s1* 等于 *s2*，则为真
- *s1* != *s2*—如果字符串 *s1* 不等于 *s2*，则为真
- *s1* < *s2*—如果字符串 *s1* 小于 *s2*，则为真
- *s1* > *s2*—如果字符串 *s1* 大于 *s2*，则为真

```bash
DAY=`date '+%a'`
if [ "$DAY" = "Mon" ] ; then
    printf "The weekend is over...get to work!\n"
fi
```

`-z`（*零长度*）和 `-n`（*非零长度*）选项分别是 `=` 和 `!=` 的简写形式。请注意，没有大于等于或小于等于运算符。你可以通过结合两个测试并使用 `-a` 选项来模拟这些运算符。

如果你习惯使用其他计算机语言，请记住 `test` 命令中使用的引号并非用于字符串界定，而是用于特殊字符处理。

由于小于号和大于号运算符也用于 shell 的重定向，因此必须将这些运算符加上引号，以防止 Bash 将其解释为重定向符号，而不是传递给 `test` 命令。

```bash
COMPANY="Athabasca"
if [ "$COMPANY" \< "M" ] ; then
    printf "The company name begins with a letter less than M\n"
fi
```

字符串比较的一个常见用途是测试 shell 标志变量。*标志*是用于指示特定条件是否为真的变量。它们提供了一种记住先前测试的方法。

可以使用任意一对值来表示标志的状态，例如 true 和 false，或者 yes 和 no。然而，当标志包含诸如 "NO" 这样的意外字符串时，这可能会导致条件歧义。传统上，如果变量包含除空字符串以外的任何内容，该条件被视为真。

```bash
WEEKEND=
DAY=`date '+%a'`
if [ "$DAY" = "Sat" -o "$DAY" = "Sun" ] ; then
    WEEKEND=1
fi

# 要确定是否为周末，使用 -n（非空）和 -z（空）。
if [ -n "$WEEKEND" ] ; then
    printf "The weekend is here\n"
else
    printf "It isn't the weekend\n"
fi
```

### 算术表达式

内置的 `let` 命令执行数学计算。`let` 期望一个包含变量、等号和待计算表达式的字符串。结果将被赋值给该变量。

```bash
$ let "SUM=5+5"
$ printf %d "$SUM"
10
```

在字符串中扩展变量名时不需要使用 `$`。`let` 理解等号右侧出现的任何变量都需要将其值代入表达式中。

```bash
$ let "SUM=SUM+5"
$ printf %d "$SUM"
15
$ let "SUM=SUM-5"
$ printf %d "$SUM"
10
```

可选的美元符号是 `let` 命令的一个特殊功能，不适用于其他命令。

如果变量使用 `-i` 选项声明为整数，则 `let` 命令是可选的。

```bash
$ declare -i SUM
$ SUM=SUM+5
$ printf %d "$SUM"
15
```

如果 `SUM` 是一个字符串变量，它将被赋值为字符串 `"SUM+5"`：

```bash
$ unset SUM
$ declare SUM=0
$ SUM=SUM+5
$ printf %s "$SUM"
SUM=5
```

出现在 `let` 表达式中的任何特殊字符都必须加上引号，以防止 Bash 对其进行扩展。

`let` 命令提供四个基本数学运算符，外加一个取模运算符。只允许整数表达式（不允许小数点）。

```bash
$ let "RESULT=5 + 2"
$ printf "5 plus 2 is %d\n" "$RESULT"
5 plus 2 is 7

$ let "RESULT=5 - 2"
$ printf "5 minus 2 is %d\n" "$RESULT"
5 minus 2 is 3

$ let "RESULT=5 * 2"
$ printf "5 times 2 is %d\n" "$RESULT"
5 times 2 is 10

$ let "RESULT=5 / 2"
$ printf "5 divided by 2 is %d\n" "$RESULT"
5 divided by 2 is 2

$ let "RESULT=5 % 2"
$ printf "remainder of 5 divided by 2 is %d\n" "$RESULT"
remainder of 5 divided by 2 is 1
```

以下是按优先级排列的算术运算符。对于 C 语言程序员来说，许多这些运算符都很熟悉：

- `-,+`— 一元减号加号
- `!`— 逻辑和非取反（要使用 `!`，需禁用 shell 历史记录）
- `*, /, %`— 乘法、除法和取模
- `+, -`— 加法和减法
- `<<, >>`— 左移和右移
- `<=, >=, <, >`— 比较
- `==, !=`— 相等和不等
- `&`— 按位与
- `^`— 按位异或
- `|`— 按位或
- `&&`— 逻辑与
- `||`— 逻辑或
- `expr ? expr :`— 条件表达式
- `=, *=, /=, %=, +=, -=, <<=, >>=, &=, ^=, |=`— 自引用操作

例如，要四舍五入到最近的 10，请执行以下操作：

```bash
$ declare -i COST=5234
$ COST=$((COST+5)/10*10)
$ printf '%d\n' $COST
5230
```

必须转义括号，以防止 shell 将其视为对子 shell 的引用。

`let` 命令还可以处理八进制和十六进制值。

```bash
$ declare -i OCTAL=0
$ let "OCTAL=0775"
$ printf '%d\n' "$OCTAL"
509
```

这些操作将在下一节中描述。

### 逻辑表达式

在 `let` 中，真由值 1 表示，假由 0 表示。除 1 或 0 以外的任何值都被视为真，但逻辑运算符本身仅返回 1 或 0。

请记住，逻辑真（值大于零）与命令的成功（状态代码为零）不同。在这方面，`test` 和 `let` 是相互对立的。

要在 shell 提示符下使用逻辑取反，必须禁用 shell 历史记录选项，否则 Bash 会将 `!` 解释为历史记录查找请求。

```bash
$ let "RESULT=!0"
$ printf "logical negation of 0 is %d\n" "$RESULT"
logical negation of 0 is 1

$ let "RESULT=!1"
$ printf "logical negation of 1 is %d\n" "$RESULT"
logical negation of 1 is 0

$ let "RESULT=1 && 0"
$ printf "logical and of 1 with 0 is %d\n" "$RESULT"
logical and of 1 with 0 is 0

$ let "RESULT=1 || 0"
$ printf "logical or of 1 with 0 is %d\n" "$RESULT"
logical or of 1 with 0 is 1
```

没有逻辑异或运算符。

### 关系操作

与字符串比较不同，`let` 提供了一套完整的数值比较。这些比较的价值有限，因为大多数比较都是使用 `if` 命令中的 `test` 命令进行测试的，从而导致两套测试。在逻辑表达式中，0 表示失败。

```bash
$ let "$RESULT=1 > 0"
$ printf "1 greater than 0 is %d\n" "$RESULT"
1 greater than 0 is 1

$ let "$RESULT=1 >= 0"
$ printf "1 greater than or equal to 0 is %d\n" "$RESULT"
1 greater than or equal to 0 is 1

$ let "$RESULT=1 < 0"
$ printf "1 less than 0 is %d\n" "$RESULT"
1 less than 0 is 0

$ let "$RESULT=1 <= 0"
$ printf "1 less than or equal to 0 is %d\n" "$RESULT"
1 less than or equal to 0 is 0

$ let "$RESULT=1 == 0"
$ printf "1 equal to 0 is %d\n" "$RESULT"
1 equal to 0 is 0

$ let "$RESULT=1 != 0"
$ printf "1 not equal to 0 is %d\n" "$RESULT"
1 not equal to 0 is 1
```

### 位操作

还有一组位运算符，如下所示。

```bash
$ let "$RESULT=~5"
$ printf "bitwise negation of 5 is %d\n" "$RESULT"
bitwise negation of 5 is -6

$ let "$RESULT=5 >> 2"
$ printf "5 right-shifted by 2 is %d\n" "$RESULT"
5 right-shifted by 2 is 1

$ let "$RESULT=5 << 2"
$ printf "5 left-shifted by 2 is %d\n" "$RESULT"
5 left-shifted by 2 is 20

$ let "RESULT=5 & 3"
$ printf "bitwise and of 5 with 3 is %d\n" "$RESULT"
bitwise and of 5 with 3 is 1

$ let "RESULT=5 | 3"
$ printf "bitwise or of 5 with 3 is %d\n" "$RESULT"
bitwise or of 5 with 3 is 7

$ let "RESULT=5 ^ 3"
$ printf "bitwise exclusive-or of 5 with 3 is %d\n" "$RESULT"
bitwise exclusive-or of 5 with 3 is 6
```

## 自引用操作

自引用运算符是结合赋值与其他基本操作之一的简写形式。该操作使用赋值变量执行，然后将结果赋给赋值变量。例如，`RESULT+=5` 是 `RESULT=RESULT+5` 的简写形式。

```bash
$ let "RESULT=5"
$ let "RESULT+=5"
$ printf "The result is %d\n" "$RESULT"
The result is 10
```

其他自引用运算符包括乘法 (*=)、除法 (/=)、取模 (%=)、减法 (-=)、右移 (<<=)、左移 (>>=)、按位与 (&=)、按位异或 (^=) 和按位或 (|=)。

请注意，某些类型的自引用操作无法用简写运算符表达。`RESULT=RESULT-10` 可以写为 `RESULT-=10`，但 `RESULT=10-RESULT` 必须完整写出。

递增 (++) 运算符为变量加一。递减运算符 (-- ) 使变量减一。

```bash
$ let "CNT=0"
$ let "CNT++"
$ printf "%d\n" "$CNT"
1
```

当在另一个表达式中使用递增或递减时，运算符的位置很重要。如果运算符放在变量之前，表示应在表达式的其余部分之前更新变量。如果运算符放在变量之后，更新将在表达式求值之后发生。

```bash
$ let "CNT=5"
$ let "PRODUCT=0"
$ let "PRODUCT+=CNT*5"
$ printf "%d\n" "$PRODUCT"
25
```

