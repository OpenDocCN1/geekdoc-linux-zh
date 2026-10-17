
mary linda

castle$

```
以下示例打印包含 ed 和 mary 名字行中的第二个字段。
```

castle$ awk '/ed|mary/ {print $2}' file1

harry
```

## 92

## awk

linda
castle$

上述每个示例都假设字段由空格或制表符隔开。
如果字段由冒号 (`:`) 分隔，请使用 `-F`，如下例所示。
`castle$ awk -F: '/ed|mary/ {print $2}' file1`

以下示例打印长度超过 72 个字符的行。
`length > 72`

以下示例以相反顺序打印前两个字段。
`{ print $2, $1 }`

以下示例以相反顺序打印前两个字段，输入字段由逗号/或空格和制表符隔开。

```
BEGIN { FS = ",[\t]*[\t]+" }

{ print $2, $1 }
```

以下示例累加第一列，打印和和平均值。

```
{ s += $1 }

END { print "sum is", s, " average is", s/NR }
```

以下示例按反序打印字段。
`{ for (i = NF; i > 0; --i) print $i }`

以下示例打印起始/停止对之间的所有行。
`/start/, /stop/`

以下示例打印所有第一个字段与上一个字段不同的行。
`$1 != prev { print; prev = $1 }`

以下示例打印文件，页码从 5 开始填充。
`/Page/ { $2 = n++; } { print }`

假设此程序存储在一个名为 `prog` 的文件中，以下命令行打印文件输入，页码从 5 开始编号。
`castle$ awk -f prog n=5 input`

## 环境变量

查看 `environ(5)` 以获取影响 `awk` 执行的以下环境变量描述：`LC_CTYPE` 和 `LC_MESSAGES`。

`LC_NUMERIC` 确定在解释数值输入、执行数值与字符串值之间的转换、格式化数值输出时使用的进制字符。无论区域设置如何，句号字符（POSIX 区域的小数点字符）都是处理 `awk` 程序（包括命令行参数）时识别的。在 Solaris 8 中引入。

### 属性

查看 `attributes(5)` 以获取以下属性的描述：

- `/usr/bin/awk`

| 属性类型 | 属性值 |
| :--- | :--- |
| 可用性 |  |
| 执行 | 是 |

- `/usr/xpg4/bin/awk`

| 属性类型 | 属性值 |
| :--- | :--- |
| 可用性 |  |
| 执行 | 是 |

## 参见

`egrep(1)`, `grep(1)`, `nawk(1)`, `sed(1)`, `printf(3)`, `attributes(5)`, `environ(5)`, `large(5)`, `XPG(5)`

## B

## banner — 生成海报

### 概要

`/usr/bin/banner strings`

### 描述

`banner` 在标准输出上以大字母打印其参数，最多 10 个字符。

### 示例

以下示例打印 happy birthday。

```
castle% banner happy birthday
```

# 11

## bc — 二进制计算器

### 概要

```
/usr/bin/bc [-c] [-1] [file...]
```

### 描述

`bc` 既是一个计算器也是一种类似 C 的语言，你可以用它编写数值程序。`bc` 实际上是 `dc` 计算器的预处理器，并使用 `dc` 命令执行其工作。然而，`bc` 包含的函数比 `dc` 多，包括命名函数、逻辑运算符和如 `sqrt`（平方根）之类的数学函数。它使用中缀表示，即将操作符放在要操作的数字之间。例如，2 + 2 = 4。

你从命令行执行 `bc`。它可以从命令行获取输入，或直接从文件获取后再从命令行获取输入。当你使用文件名作为参数时，`bc` 读取文件，处理其命令，并切换到命令行获取输入。通过这种方式，你可以在文件中存储复杂的命令和函数，并直接从命令行使用它们。

`bc` 会自动显示每行的计算结果。单次计算的所有信息必须在一行内。要退出 `bc`，输入 `quit` 或按 Control-D 信号文件结束符。`bc` 命令语言类似于 C 语言。

### 注意

`bc` 命令不识别逻辑运算符 `&&` 和 `||`。对于语句必须包含三个表达式。

## 96

## basename, dirname — 提取路径部分

### 概要

```
/usr/bin/basename string [suffix]

/usr/xpg4/bin/basename string [suffix] string
```

### 描述

你可以使用 `basename` 命令从文件名中提取路径。例如，

# basename, dirname 97

你可以使用 `basename` 命令从文件名中提取路径。例如，如果你有一个路径名，可以使用 `basename` 提取路径的最后一个部分。`basename` 命令还接受一个可选后缀，该后缀将从文件名末尾移除。

以下示例显示如何使用 `basename` 从路径获取文件名：

```
castle$ basename /home/user/file.txt

file.txt
```

如果你提供了后缀，它将从文件名中移除。

以下示例显示如何使用带后缀的 `basename` 移除扩展名：

```
castle$ basename /home/user/file.txt .txt

file
```

### 示例

以下示例显示如何使用 `basename` 从路径获取文件名：

```
castle$ basename /home/user/file.txt

file.txt
```

以下示例显示如何使用带后缀的 `basename` 移除扩展名：

```
castle$ basename /home/user/file.txt .txt

file
```

`basename` 命令通常用于脚本中处理路径名。

## 环境变量

查看 `environ(5)` 以影响 `basename` 执行的以下环境变量描述：`LC_CTYPE` 和 `LC_MESSAGES`。

## 退出状态

- 0 成功完成。
- >0 发生错误。

### 属性

查看 `attributes(5)` 以获取以下属性的描述：

- `/usr/bin/basename`

| 属性类型 | 属性值 |
| :--- | :--- |
| 可用性 |  |
| 执行 | 是 |

- `/usr/xpg4/bin/basename`

| 属性类型 | 属性值 |
| :--- | :--- |
| 可用性 |  |
| 执行 | 是 |

## 参见

`expr(1)`, `attributes(5)`, `environ(5)`, `x4(5)`

## batch — 延迟执行命令

### 语法

```
usr/bin/batch
```

### 描述

查看 (1)。

### 用法

以下列表详细描述了 `bc` 程序的语法：

- 字母 (Letter): a 到 z 之间的单个字母。
- 表达式 (Expression): 一个表达式：一个数学或逻辑值、一个接受值的的操作数，或者一组可以求值的操作数和运算符的组合。
- 语句 (Statement): 一个语句。

### 注释

注释封装在 `/*` 和 `*/` 之间。

### 名称（操作数）

- 字母 (Letter): 简单的单字母变量。
- 字母 [Expression]（最多 `BC_DIM_MAX` 维）：数组元素。
- `ibase`：输入基数。
- `obase`（受限制为 `BC_BASE_MAX`）：输出基数。
- `scale`（限制为 `BC_SCALE_MAX`）：`bc` 计算中保留的小数点后位数。

### 其他操作数

- 带有可选符号和小数点的任意长度数字。
- 双引号（""）之间少于 `BC_STRING_MAX` 个字符的字符串。
- ( Expression )。
- `sqrt` ( Expression ): 平方根。
- `length` ( Expression ): （有效小数位数）。
- `scale` ( Expression ): （小数点后的位数）。
- 字母 (Expression, ..., Expression )。

### 运算符

- +-* / % ^: (% 是取余数；^ 是幂)。
- --（前缀和后缀；应用于名称）。
- <= >= != = <
- += -= *= = /= % = ^

### 语句

- Expression
- [Statement;...;Statement]
- if (Expression) Statement
- while (Expression) Statement
- for (Expression; Expression; Expression) Statement
- 空语句 (null statement)。
- break
- quit
- string

### 函数定义

```
bc
```
