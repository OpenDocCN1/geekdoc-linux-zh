

```
{
for (i = 1; i <= NF; i++) {
words[$i]++;
}
}

END {
for (word in words) {
printf("%s occurred %d time(s)\n", word, words[word]);
}
}
```

这里有一个动作，即 `for` 动作。`for` 命令是一种循环结构，类似于 C 语言中的 `for` 循环。它的工作机制如下：

1.  首先，将变量 i 设置为 1。
2.  接下来，将 i 与 NF 进行比较。如果 i 小于或等于 NF，则执行循环体。
3.  在循环体执行完毕后，变量 i 自增。（有趣的记法 `VAR++` 表示将 VAR 加 1。）
4.  返回步骤 2。

循环体非常有趣。语句 `words[$i]++` 会递增一个数组变量。数组的名称是 `words`；索引是第 i 个字段的值。因此，整个 `for` 循环遍历行中的每个字段，以该字段值作为索引来递增数组元素。

请注意，我没有初始化 `words` 数组。如果像之前那样在表达式中引用一个不存在的数组元素，`awk` 会自动创建该元素并将其初始值设为零。这很实用，因为它省去了在操作变量之前测试变量是否存在的麻烦。

当所有输入读取完毕后，第二个 `for` 循环会执行。这个第二个循环采用了不同的形式：

```
for (VAR in ARRAY) BODY
```

`for` 的这第二种形式会将数组的索引依次赋值给变量。每次执行赋值时，它都会执行循环体。在这个例子中，它遍历 `words` 中的所有索引，并打印每个单词及其在输入中出现的次数。

`printf` 语句类似于 C 语言中的格式化输出语句。它打印其第一个参数，但会进行某些被称为“百分号替换”的替换操作。在这个例子中，`printf` 将 `word` 的值作为字符串替换 `%s`，将 `words[word]` 的值作为十进制数替换 `%d`。最后的 `\n` 会被转换为换行符。

通过输入以下内容来测试脚本：

```
$ awk -f countwords.awk
I like awk and awk likes me
Do I like awk?
^D
awk occurred 1 time(s)
me occurred 1 time(s)
likes occurred 1 time(s)
and occurred 1 time(s)
I occurred 2 time(s)
awk occurred 2 time(s)
Do occurred 1 time(s)
like occurred 2 time(s)
```

在上面的示例中，`^D` 表示输入 **Control+D**，即终端的文件结束符。

如您所见，`awk` 会统计您输入的单词。请注意，它将 `awk` 和 `awk?` 视为不同的单词。还要注意，单词输出的顺序是不可预测的——第二个 `for` 循环以未指定的顺序遍历数组。这是因为关联数组的低级实现细节所致。

## awk 表达式

许多 `awk` 语句使用表达式来控制其行为。例如，`for` 语句的第一种形式使用三个表达式来控制循环。

`awk` 表达式类似于 C 表达式。它由一系列值和运算符组成。`awk` 运算符按优先级降序排列，见表 30.3。

**表 30.3：awk 运算符**

| 运算符 | 含义 |
|:---------|:---------|
| ( ... ) | 分组。括号改变正常的优先级规则。 |
| $ | 字段引用。 |
| ++ 和 - | 前缀和后缀递增与递减。前缀运算符递增或递减变量并返回新值；后缀运算符递增或递减变量并返回旧值。 |
| ^ 或 ** | 幂运算。 |
| * , / , 和 % | 乘法、除法和取模。 |
| + 和 - | 加法和减法。 |
| 空格 | 字符串连接。 |
| <, <=, >, 和 >= | 关系运算符。 |
| == 和 != | 比较运算符。 |
| ~ 和 !~ | 正则表达式匹配。例如，如果 *regexp* 匹配 *expr*，则 `expr ~ regexp` 返回 1；否则返回 0。 |
| in | 数组成员关系。如果 *array* 包含索引为 *expr* 的元素，则 `expr in array` 返回 1。 |
| & & | 逻辑与。如果两个操作数都非零，则为真。 |
| \| \| | 逻辑或。如果任一操作数非零，则为真。 |
| ?: | C 条件运算符。表达式 `expr1 ? expr2 : expr3` 在 *expr1* 非零时返回 *expr2*，否则返回 *expr3*。只有 *expr2* 或 *expr3* 中的一项会被计算。 |
| = | 赋值。支持加法、减法、乘法、除法、取模和幂运算的各种复合赋值运算符。例如，`var += val` 等价于 `var = var + val`，不同之处在于 `var` 只被计算一次。 |

`awk` 表达式可以作为模式使用。以下命令仅打印包含一个或多个字段的行。这是抑制文件中空行的简单方法。

$ awk 'NF > 0 { print $0 }' input_file

## 控制语句

控制语句是内置的 `awk` 语句，用于控制程序流程或输入处理。我们已经见过创建循环的 *for* 语句。控制语句如下：

- `if (expr) stmt1 [else stmt2]`
- `while (expr) statement`
- `do statement while (expr)`
- `for (expr1; expr2; expr3) statement`
- `for (var in array) statement`
- `break`
- `continue`
- `delete array[index]`
- `delete array` (仅限 GNU gawk。)
- `exit [expr]`
- `{ statements }` 花括号引入复合语句，即将多个语句组合为一个。

## if 语句

语句 `if (expr) stmt1 [else stmt2]` 会评估表达式 *expr*。如果结果非零，`awk` 执行 *stmt1*。否则，如果存在 `else` 子句，`awk` 执行 *stmt2*。示例如下：

```
{
  if (NF % 2) {
    print S0 ": Odd number of fields"
  } else {
    print S0 ": Even number of fields"
  }
}
```

对于每一行输入，`awk` 会回显该行，并打印其中包含偶数还是奇数字段数的提示。

## while 语句

语句 `while (expr) statement` 执行以下操作：

1.  评估 *expr*。如果结果为零，则终止 `while` 语句。
2.  执行循环体 *statement*。
3.  返回步骤 1。

## do 语句

`do` 语句类似于 `while` 语句，不同之处在于循环体至少会执行一次。`do` 的操作如下：

1.  执行循环体 *statement*。
2.  评估 *expr*。如果结果为零，则终止 `do` 语句。
3.  否则，返回步骤 1。

## for 语句

您已经见过 `for` 语句的工作情况。以下是其工作原理的正式描述：

1.  评估 *expr1* 并丢弃结果。
2.  评估 *expr2*。如果结果为零，则终止 `for` 循环。
3.  执行循环体语句。
4.  评估 *expr3* 并丢弃结果。
5.  返回步骤 2。

## break 和 continue 语句

在循环体内，`break` 会立即终止循环。`continue` 会使循环在下一次迭代时重新开始。对于 `while` 循环，`awk` 会跳转到之前说明的算法的步骤 1。对于 `do` 循环，它跳转到步骤 2。对于 `for` 循环，它跳转到步骤 4（评估 *expr2* 的步骤）。

## delete 语句

`delete` 语句删除指定的数组元素。一个 GNU 扩展允许您仅提供数组名称来删除数组中的所有元素。

## exit 语句

`exit` 语句使 `awk` 停止处理任何进一步的输入。如果存在任何 `END` 动作，它们将被执行。如果 `exit` 出现在 `END` 块内部，它会立即停止程序。如果在关键字 `exit` 之后提供表达式，`awk` 在终止时会将其用作操作系统的退出值。

## I/O 语句

`AWK` 有许多用于执行输入和输出的语句。这些语句总结见表 30.4。

**表 30.4：I/O 语句**

| 语句 | 含义 |
| --- | --- |
| close(file) | 关闭文件或管道。 |
| getline | 获取下一个输入记录，并设置 $0, NF, NR, 和 FNR。 |
| getline < file | 从指定文件读取下一个记录，并设置 $0 和 NF。 |
| getline var | 将 var 设置为下一个输入记录，并设置 NF 和 FNR。 |
| getline var < file | 将 var 设置为来自文件 file 的下一个输入记录。 |
| next | 停止处理当前记录，并开始处理下一个记录。 |

