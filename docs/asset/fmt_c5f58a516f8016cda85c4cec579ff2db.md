
```bash
if [[ 30 < $age && $age < 60 ]]; then
```

你也可以使用 `test` 的关系运算符 `-gt`, `-ge`, `-lt`, `-le`, `-eq` 和 `-ne`：

```bash
if [[ 30 -lt $age && $age -lt 60 ]]; then
```

`test` 内置命令测试字符串是否相等。`[[ ]]` 语法为字符串运算符增加了比较测试。`>` 和 `<` 运算符比较字符串的顺序，例如 `"aa" < "bbb"`。该运算符用于模式匹配，而不仅仅是相等性检查：如果字符串匹配模式，则 `[[ string = pattern ]]` 为真。此运算符不是对称的；模式必须出现在符号的右侧。例如，`[[ artist = a* ]]` 为真 `0`，而 `[[ a* = artist ]]` 为假 `1`：

```bash
$ [[ artist = a* ]]
$ echo $?
0
$ [[ a* = artist ]]
$ echo $?
1
```

下一个示例使用了一个以复合条件开始的命令列表。该条件测试目录 `bin` 和文件 `src/myscript.bash`。如果为真，`cp` 将 `src/myscript.bash` 复制到 `bin/myscript`。如果复制成功，`chmod` 使 `myscript` 可执行。如果这些步骤中任一失败，`echo` 将显示消息。

```bash
$ [[ -d bin && -f src/myscript.bash ]] && cp src/myscript.bash bin/myscript || echo "Cannot make executable version of myscript*"
```

## 模式匹配

Bourne Shell 提供了字符串匹配运算符，可以操作模式和其他字符串。表 27-7 列出了这四个运算符。

表 27-7 字符串运算符

| 运算符 | 功能 |
| :--- | :--- |
| # | 删除匹配的前缀 |
| ## | 删除最大匹配的前缀 |
| % | 删除匹配的后缀 |
| %% | 删除最大匹配的后缀 |

这些运算符的语法为

```bash
${varnameopat}
```

其中 `op` 是表 27-7 中列出的运算符之一，`pattern` 是匹配模式。这些运算符通常用于提取或删除文件名组件：

```bash
$ SOURCEFILE=/usr/local/src/prog.c

$ echo ${SOURCEFILE#}

local/src/prog.c

$ echo ${SOURCEFILE##}

src/prog.c

$ echo ${SOURCEFILE%}

usr/local/src/prog

$ echo ${SOURCEFILE%%}

usr/local/src/prog.c

$ CHOPFIRST=${SOURCEFILE#}

local/src/prog.c

$ NEXT=${CHOPFIRST%}

local/src/prog
```

字符串长度运算符 `${#name}` 被替换为 `name` 中的字符数：

```bash
$ echo ${#SOURCEFILE}
21
```

## 运算符

`bash` 中的算术扩展和算术求值使用 C 语言相同的语法、优先级和结合性。表 27-8 按优先级递减顺序列出了运算符；每组运算符优先级相同。在表达式中，可以使用括号来改变求值顺序。

表 27-8 运算符

| 运算符类型/运算符 | 功能 |
| :--- | :--- |
| Post | `var++` 后增 |
| | `var--` 后减 |
| Pre | `++var` 前增 |
| | `--var` 前减 |

### 表 27-8 运算符（续）

| 运算符类型/运算符 | 功能 |
| :--- | :--- |
| Unary | `-` 一元负数<br>`+` 一元正数 |
| Negation | `!` 布尔非（逻辑取反）<br>`~` 补（位取反） |
| Exponentiation | `**` 幂 |
| Multiplication, division, remainder | `*` 乘法<br>`/` 除法<br>`%` 余数 |
| Addition, subtraction | `-` 减法<br>`+` 加法 |
| Bitwise shifts | `<<` 左移<br>`>>` 右移 |
| Comparison | `<=` 小于等于<br>`>` 大于等于 |
| Equality, inequality | `==` 等于<br>`!=` 不等于 |
| Bitwise | `^` 异或（或或） |

### 表 27-8 运算符（续）

| 运算符类型/运算符 | 功能 |
| :--- | :--- |
| Boolean | `&&` 与<br>`||` 或 |
| Assignment | `*=` 赋值<br>`/=` 赋值<br>`%=` 赋值<br>`-=` 赋值 |
| Comma | `,` 逗号 |
| Pipe | `|` 管道 |
| Ternary | `?` 三元运算符 |

余数运算符 `%` 在第一个操作数除以第二个操作数时产生余数。例如，表达式 `$((15%7))` 的值为 `1`。布尔操作的结果为 `0`（假）或 `1`（真）。`&&`（与）和 `||`（或）布尔运算符被称为短路运算符。如果这些运算符之一的结果仅通过左侧操作数决定，则右侧不会被求值。`&&` 运算符调用 shell 测试其先前的命令的退出状态。如果命令成功，`bash` 执行下一个命令；否则跳过该行的剩余命令。你可以使用这种结构条件条件执行命令。

```bash
$ mkdir bkup && cp -r src bkup
```

此命令创建目录 `bkup`。如果 `mkdir` 成功，目录 `src` 的内容递归复制到 `bkup`。`||` 运算符调用 `bash` 测试第一个命令的退出状态，但效果相反：只有当第一个命令失败（即状态非零）时，才会执行剩余命令。

```bash
$ mkdir bkup || echo "mkdir of bkup failed" >> /tmp/log
```

命令列表的退出状态是列表中最后一个命令的退出状态。你可以用括号对列表分组。例如，你可以结合这两个示例：

```bash
$ (mkdir bkup && cp -r src bkup) || echo "mkdir failed" >> /tmp/log
```

在没有括号的情况下，`&&` 和 `||` 优先级相等并从左到右分组。以下示例使用了 `true` 和 `false` 工具。这些工具不做操作，并分别返回真 `0` 和假 `1` 退出状态：

```bash
$ true; echo $
```

变量 `$` 保留上一个命令的退出状态。接下来两个命令产生的退出状态为 `1`（假）：

```bash
$ true || false && false
$ echo $$
1
```

同样，这两个命令产生的退出状态为 `0`（真）：

```bash
$ false && false || true
$ echo $$
0

$ (false && false) || true
$ echo $$
0
```

# 表达式 1039

由于 `||` 和 `&&` 的优先级相同，前两组示例中的括号并没有改变操作的顺序。

由于短路运算符右侧的表达式可能永远不会被执行，因此在在该位置放置赋值语句时必须小心。以下示例演示了可能发生的情况：

```bash
$ ((N=10,Z=0))
$ echo $((((N || ((Z+=1))))
1
$ echo $Z
0
```

因为 `N` 的值非零，所以 `||`（或）操作的结果为 `1`（真），无论右侧的值是什么。结果是 `((Z+=1))` 永远不会被评估，`Z` 也不会加增。

三元运算符 `?` 根据第三个表达式返回的值，决定应该评估两个表达式中的哪一个：

```
expression1 ? expression2 : expression3
```

如果 `expression1` 产生一个假 `0` 值，则评估 `expression3`；否则，评估 `expression2`。整个表达式的值是 `expression2` 或 `expression3` 的值，取决于评估了哪一个。如果 `expression1` 为真，则不评估 `expression3`；如果 `expression1` 为假，则不评估 `expression2`。

```bash
$ ((N=10,Z=0,COUNT=1))
$ ((T=N-COUNT++:Z:--Z))
$ echo $T
1
$ echo $Z
1
```

赋值运算符（如 `+=`）是简写符号。例如，`N+=3` 等同于 `((N=N+3))`。

以下命令使用语法 `base#n` 分配基 2（二进制）值。`v1` 被赋值为 `0101`（十进制 5），然后 `v2` 被赋值为 `0110`（十进制 6）。`echo` 工具验证了这些十进制值。

```bash
$ ((v1=#0101))
$ ((v2=#0110))
```
