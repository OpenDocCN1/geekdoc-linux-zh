
`% nawk 'pattern' filename`

`% nawk '{action}' filename`

`% nawk 'pattern {action}' filename`

下面是一个名为 `employees` 的示例文件：

# 示例 6.1

```
% cat employees
Tom Jones    4424  5/12/66  543354
Mary Adams   5346  11/4/63  28765
Sally Chang  1654  7/22/54  65000
Billy Black  1683  9/23/44  336500
% nawk '/Mary/' employees
Mary Adams   5346  11/4/63  28765
```

# 解释

`Nawk` 打印包含模式 `Mary` 的所有行。

# 示例 6.2

```
% cat employees
Tom Jones    4424  5/12/66  543354
Mary Adams   5346  11/4/63  28765
Sally Chang  1654  7/22/54  650000
Billy Black  1683  9/23/44  336500
% nawk '{print $1}' employees
Tom
Mary
Sally
Billy
```

# 解释

`Nawk` 打印文件 `employees` 的第一个字段，其中字段从行的左边界开始，并以空白字符分隔。

# 示例 6.3

```
% cat employees
Tom Jones    4424  5/12/66  543354
Mary Adams   5346  11/4/63  28765
Sally Chang  1654  7/22/54  650000
Billy Black  1683  9/23/44  336500
% nawk '/Sally/{print $1, $2}' employees
Sally Chang
```

# 解释

如果行中包含模式 `Sally`，`Nawk` 就会打印文件 `employees` 的第一个和第二个字段。请记住，字段分隔符是空白字符。

### 6.2.2 从命令输入

`UNIX/Linux` 命令或命令的输出可以被管道传输到 `awk` 进行处理。`Shell` 程序通常使用 `awk` 来操作命令。

# 格式

```
% command | nawk 'pattern'
% command | nawk '{action}'
% command | nawk 'pattern {action}'
```

# 示例 6.4

```
1 % df | nawk '$4 > 75000'
/oracle (/dev/dsk/c0t0d0s7):399780 blocks 105756 files
/opt (/dev/dsk/c0t0d0s8):1943994 blocks 49187 files
```

```
2 % rusers | nawk '/root$/ {print $1}'
owl
crow
bluebird
```

# 解释

- 1 `df` 命令报告文件系统上的可用磁盘空间。`df` 命令的输出被管道传输到 `nawk`。如果第四个字段大于 75,000 个块，则打印该行。
- 2 `rusers` 命令打印在网络上远程机器上登录的用户。`rusers` 命令的输出作为输入被管道传输到 `nawk`。如果正则表达式 `root` 与行尾匹配（`$`），则打印第一个字段；也就是说，打印所有 `root` 已登录的机器名称。

# 6.3 awk 的工作原理

在深入了解 `awk` 的所有细节之前，让我们一步步看看它是如何完成工作的。我们来看一个名为 `names` 的简单三行文件：

```
Tom Savage 100
Molly Lee 200
John Doe 300
```

`awk` 命令如下：

```
% nawk '{print $1, $3}' names
```

- 1. `Awk` 读取一行输入（来自文件或管道）并将其放入名为 `$0` 的内部变量中。每行也称为记录，默认情况下以换行符终止。

![](img/60a0b5d254bd6007403850f972cbfad8_197_0.png)

- 2. 接下来，该行被拆分为由空白字符分隔的字段（单词）。每个字段存储在编号变量中，从 `$1` 开始。可以多达 100 个字段。

![](img/60a0b5d254bd6007403850f972cbfad8_198_0.png)

3. `awk` 如何知道空白字符分隔了字段？还有另一个内部变量，称为 `FS`，用来指定字段分隔符。初始时，`FS` 被赋值为空白字符——制表符和空格。如果字段由其他字符分隔，例如冒号或连字符，你可以更改 `FS` 的值来指定新的字段分隔符。参见第 169 页的“字段分隔符”。

4. 当 `awk` 打印字段时，使用 `print` 函数如下：

```
{print $1,$3}
```

输出显示每个字段之间用空格分隔，如

Tom 100
Molly 200
John 300

`awk` 在 `Tom` 和 `100` 之间提供输出空格，是因为在 `$1` 和 `$3` 之间放置了一个逗号。逗号是特殊的。它映射到另一个内部变量，称为输出字段分隔符 `OFS`。`OFS` 的默认值为一个空格。逗号会生成分配给 `OFS` 变量的字符。

5. 在 `awk` 显示其输出后，它获取文件中的下一行并将其存储在 `$0` 中，覆盖之前的内容。然后它将该行拆分为字段并进行处理。这会一直持续到文件中的所有行都被处理完毕。

# 6.4 格式化输出

### 6.4.1 print 函数

`awk` 命令的动作部分用大括号括起来。如果未指定动作并且匹配到模式，`awk` 会采用默认动作，即将匹配的行打印到屏幕上。`print` 函数用于打印不需要花哨格式的简单输出。对于更复杂的格式，则使用 `printf` 或 `sprintf` 函数。如果你熟悉 `C`，那么你已经知道 `printf` 和 `sprintf` 的工作原理。`print` 函数也可以在 `awk` 的动作部分中显式使用，如 `{print}`。`print` 函数接受变量、计算值或字符串常量作为参数。字符串必须用双引号括起来。逗号用于分隔参数；如果未提供逗号，则参数会被连接在一起。逗号求值为 `OFS` 的值，默认是一个空格。

`print` 函数的输出可以重定向或通过管道传递给另一个程序，并且另一个程序的输出也可以通过管道传递给 `awk` 以进行打印。参见第 25 页的“重定向”和第 28 页的“管道”。

#### EXAMPLE 6.5

```
% date
Wed Jul 28 22:23:16 PDT 2004
% date | awk '{ print "Month: " $2 "\nYear: " , $6 }'
Month: Jul
Year: 2004
```

### EXPLANATION

`UNIX` `date` 命令的输出将被通过管道传递给 `awk`。字符串 `Month:` 会被打印，后跟第二个字段，包含换行字符的字符串 (`\n`)，以及 `Year:`，后跟第六个字段 (`$6`)。

### Escape Sequences.

转义序列由反斜杠和字母或数字表示。它们可以在字符串中使用来表示制表符、换行符、换页符等（参见表 6.1）。

### Table 6.1 print Escape Sequences

| Escape Sequence | Meaning |
|---|---|
| `\b` | Backspace |
| `\f` | Form feed |
| `\n` | Newline |
| `\r` | Carriage return |
| `\t` | Tab |
| `\047` | Octal value 47, a single quote |
| `\c` | c represents any other character, e.g., `\` |

#### EXAMPLE 6.6

Tom Jones 4424 5/12/66 543254
Mary Adams 5346 11/4/63 28765
Sally Chang 1654 7/22/34 650000
Billy Black 1683 9/23/44 336500

```
% awk '/Sally/{print "\t\tHave a nice day, "$1, $2 "\"!"}' employees
Have a nice day, Sally Chang!
```
