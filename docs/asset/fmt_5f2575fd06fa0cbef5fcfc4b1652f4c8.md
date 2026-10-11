
第 12 行调用 `format()` 方法来格式化输出。像 `printf` 一样，`format()` 方法接收一个字符串和一个参数列表。区别在于，`printf` 直接将格式化输出发送到标准输出流，而 `formatter` 则将格式化输出发送到其构造函数指定的目标（在本程序中为内存中的一个字符串）。第 15 行调用 `toString()` 方法获取字符串形式的格式化数据，然后在消息对话框中显示。

注意，`String` 类也提供了一个名为 `format` 的静态便利方法，允许你无需先创建 `Formatter` 对象即可在内存中创建字符串。在图 29.24 的第 11–12 行中，第 15 行可以被替换。

![](img/1df0d1e8ac6007b95647eb8ea38390af_1485_0.png)

图 29.24 | 使用 `Formatter` 类进行格式化输出。

## 29.14 总结

本章总结了如何使用各种格式字符 `d`、`o`、`x` 和 `X` 显示格式化输出。我们使用格式字符 `e`、`f`、`g` 和 `G` 显示了浮点数。我们使用格式字符 `t` 和 `T` 及其转换后缀字符以各种格式显示了日期时间。你学习了如何使用字段宽度和精度显示输出。我们引入了标志 `+`、`-`、空格、`#`、`0`、逗号和 `(`，这些标志与格式字符一起使用产生输出。我们还演示了如何使用 `Formatter` 类输出。在下一章中，我们将讨论 `String` 类用于处理字符串的方法。我们还将引入正则表达式，并演示如何使用正则表达式验证用户输入。

## 总结

- 29.2 节 流

  - 输入和输出通常通过流进行，流是字节序列。在输入操作中，字节从设备流向主内存。在输出操作中，字节从主内存流向设备。
  - 通常情况下，标准输入流连接到键盘，标准输出流连接到计算机屏幕。

- 29.3 节 使用 `printf` 格式化输出

  - `printf` 字符串描述了输出值出现的格式。格式说明符由参数索引、标志、字段宽度和转换字符组成。

- 29.4 节 打印整数

  - 整数使用 `d` 打印十进制，`o` 打印八进制，`x` 或 `X` 打印十六进制。

- 29.5 节 打印浮点数

  - 浮点数使用 `e` 或 `E` 打印指数计数法，`f` 打印普通形式，`g` 或 `G` 打印科学计数法。

- 29.6 节 打印字符串和字符

  - 字符 `c` 打印字符。字符 `s` 或 `S` 打印字符串。

- 29.7 节 打印日期和时间

  - 字符 `t` 或 `T` 打印日期时间。

# 1487 第29章 格式化输出

### 29.8 节 其他转换字符

- 字符 `b` 或 `B` 输出布尔值的字符串表示。这些转换字符对非空输出 `"true"`，对空引用输出 `"false"`。使用转换字符 `B` 时输出为大写。
- 字符 `h` 或 `H` 返回对象的哈希值。哈希值用于 `Hashtable` 和 `HashMap`。使用转换字符 `H` 时输出为大写。
- 字符 `n` 打印平台换行符。
- 字符 `x` 用于显示字面量。

### 29.9 节 使用字段宽度和精度打印

- 如果字段宽度大于要打印的对象，则输出在字段中右对齐。
- 字段宽度可以用于换行符以外的所有转换字符。
- 浮点型转换字符 `e` 和 `f` 的精度表示小数点后的数字位数。
- 浮点型字符 `g` 的精度表示有效位数。
- 转换字符 `s` 的精度表示要打印的字符数。
- 通过在百分号和转换字符之间放置字段宽度、小数点和精度可以结合字段宽度和精度。

### 29.10 节 在格式字符串中使用标志

- `-` 标志使其在字段中左对齐。
- `+` 标志为正值打印加号，为负值打印减号。
- 空格标志在正值前打印一个空格。空格标志和 `+` 不能在转换字符中一起使用。
- `#` 标志在八进制值前加 `0`，十六进制值前加 `0x`。
- `0` 标志为未占据整个字段的值打印前零。
- 逗号 `,` 标志使用特定区域的千位分隔符（例如美国区域为 `','`）来显示整数和浮点数。
- `(` 标志将数字括在括号中。

### 29.11 节 使用参数索引打印

- 参数索引是跟随 `$` 符号的可选数字，指示参数在参数列表中的位置。
- 参数索引允许程序员重新排序输出，使得参数列表中的参数不一定与其对应的格式说明符顺序一致。参数索引还有助于避免重复使用参数。

## 术语

## 1443

## 术语

- 标记 `flag`
- 转换字符 `conversion character`
- C 标记
- `(正号)标记 ((plus) flag)`
- `(负号)标记 ((minus) flag)`
- `,` (逗号)标记 `,comma flag`
- `0` (零)标记 `0 (zero) flag`
- A 转换后缀 `A conversion suffix`
- a 转换后缀字符 `a conversion suffix character`
- 对齐 `alignment`
- 参数索引 `argument index`
- b 转换字符
- B 转换字符
- B 后缀字符 `B suffix character`
- c 转换字符
- C 后缀字符 `C suffix character`
- 转换字符 `conversion character`
- d 转换字符
- D 转换后缀字符 `D conversion suffix character`
- e 转换字符
- E 转换字符
- e 转换后缀字符 `e conversion suffix character`
- 指指数计数法 `exponential floating-point format`
- f 转换字符
- 字段宽度 `field width`
- 标记 `flag`
- 浮点 `floating-point`
- 浮点数转换 `floating-point number conversion`
- `Formatter` 的 `format` 方法 `format method of Formatter`
- `String` 的 `format` 方法 `format method of String`
- 格式说明符 `format specifier`
- 格式字符串 `format string`
- `Formatter` 类
- g 转换字符
- G 转换字符
- h 转换字符
- H 转换字符
- H 后缀字符 `H suffix character`
- 十进制格式 `hexadecimal format`
- I 转换后缀 `I conversion suffix character`
- 整数转换 `integer conversion`
- j 转换后缀 `j conversion suffix character`
- K 转换后缀 `K conversion suffix character`
- 左对齐 `left justification`
- m 转换后缀 `m conversion suffix character`
- M 转换后缀 `M conversion suffix character`
- n 转换字符
- o 转换字符
- 进制格式 `octal format`
- P 转换后缀 `P conversion suffix character`
- p 转换后缀 `p conversion suffix character`
- 精度 `precision`
- `printf` 方法
- r 转换后缀 `r conversion suffix character`
- 重定向流 `redirect a stream`
- 右对齐 `right justification`
- 舍入 `rounding`
- s 转换字符
- S 转换字符
- S 后缀字符 `S suffix character`
- 科学计数法 `scientific notation`
- 空格标记 `space flag`
- 标准错误流 `standard error stream`
- 标准输入流 `standard input stream`
- 标准输出流 `standard output stream`
- 流 `stream`
- t 转换字符
- T 转换字符
- T 转换后缀 `T conversion suffix character`
- `Formatter` 的 `toString` 方法 `toString method of Formatter`
- x 转换字符
- Y 转换后缀 `Y conversion suffix character`
- y 转换后缀 `y conversion suffix character`
- Z 转换后缀 `Z conversion suffix character`

## 自测练习

- 29.1 为下列每项填空：

  a) 所有的输入和输出都以 ______ 的形式进行处理。
  b) ______ 流通常连接到键盘。
  c) ______ 流通常连接到计算机屏幕。
  d) `System.out` 的 ______ 方法可以用于格式化显示在标准输出上的文本。
  e) 转换字符 ______ 可用于输出十进制整数。

## 1444 第29章 格式化输出
