

# printf 1105

## 描述

使用 printfenv 命令打印环境变量中的变量值。如果指定了变量，则只打印其值。

## 示例

以下示例显示了 EDITOR 环境变量的值。

```
castle% printfenv EDITOR
/usr/bin/dtpad
castle%
```

## 属性

请参见 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可可用 | SUM/scpu |

## 参见

csh(1), echo(1), sh(1), stty(1), tset(1B), attributes(5), environ

## 诊断

如果指定了变量但在环境变量中未定义，printfenv 返回退出状态为 1。

# printf — 写入格式化输出

## 概要

```
/usr/bin/printf format [argument...]
```

## 描述

printf 命令将格式化后的操作数写入标准输出。参数操作数在格式操作数的控制下进行格式化。

## 操作数

```
format
```

一个描述用于写入后续操作数的格式的字符串。将格式操作数作为 formats(5) 手页中描述的格式字符串使用，但有例外：

- 在转换规范标志之外的任何上下文中，将格式字符串中的空格字符视为普通字符并复制到输出中。
- 将格式字符串中的增量字符（delta）视为增量字符，视为空格字符。

# 1106

## printf

- 除了 formats(5) 手页中描述的转义序列（\, \a, \b, \f, \n, \r, \t, \v）外，写入 \o 其中 o 是一、二或三位八进制数，作为由该八进制数指定的数值的字节。

- 不要在 d 或 u 转换规范的输出前后紧跟格式操作数未指定的空白字符。

- 不要在 o 转换规范的输出前紧跟格式操作数未指定的 os。

- 支持如下的额外转换字符 b。将参数视为可以包含反斜杠转义序列（backslash-escape sequences）的字符串。支持以下反斜杠转义序列：

- 将 formats(5) 手页中的转义序列（\, \a, \b, \f, \n, \r, \t, \v）转换为它们代表的字符。

- 将 \ddd（其中 ddd 是零、一或三位八进制数）转换为由该数字指定的数值的字节。

- 写入 \c 并忽略包含它的字符串操作数中的任何剩余字符、任何剩余的字符串操作数以及格式操作数中的额外字符。

反斜杠后跟任何其他字符序列的解释未定义。

从转换后的字符串开始写入字节，直到到达字符串末尾或精度规范指定的字节数。如果省略了精度，则为无限，写入到转换字符串末尾的所有字节。对于每个消耗参数的规范，评估下一个参数操作数并按照下文所述将其转换为转换所需的适当类型。根据需要重复复用格式操作数以满足参数操作数。评估任何 c 或 s 转换规范时，假设提供了空参数；评估额外的转换规范时，假设提供了参数。如果格式操作数不包含转换规范且存在参数操作数，则结果未定义。如果格式操作数中的字符序列以 % 字符开头但没有构成有效的转换规范，则其行为未定义。

在格式的控制下指定要写入标准输出的字符串。如果相应的转换字符是 b、c 或 s，则将参数操作数视为字符串；否则，按照 ISO C 标准将其评估为 c 常量，并具有以下扩展：

- 允许前导 + 或 - 号。

如果前导字符是单引号或双引号，则该值为紧随单引号或双引号字符的底层编码中的数值。

如果参数操作数无法完全转换为适用于相应转换规范的内部值，则向标准错误写入诊断信息，不要以 0 退出状态退出，继续处理剩余的操作数，并向输出写入检测到错误时累积的值。

## 用法

注意，printf 命令与其基于的 printf() 函数一样，在运行 %c 转换规范或在 %b 或 %s 转换规范中指定精度时，没有对处理多字节字符做出特殊规定。应用程序开发人员在字符集中存在多字节字符时，应在使用上述这些功能中的任一项时极其小心。

你不能使用 * 指定字段宽度和精度。

为了与之前的版本 SunOS 5.x 兼容，对于仅包含 % 符号的格式，支持 $ 格式指定符。

%b 转换不是 ISO 标准的一部分；它被添加为一种可移植的方法，用于处理 echo 命令提供的字符串操作数中扩展的反斜杠转义。参见 echo(1) 手页了解如何使用 printf 替换所有传统版本的 echo 命令。

如果参数无法为相应的转换规范正确解析，printf 命令将报告错误；用于数值转换的参数末尾的溢出和多余字符将报告为错误。

如果参数操作数未被完全用于 %c 转换，或者字符串操作数的第一个或第二个字符用于获取字符的数值，则不被视为错误。

## 示例

以下示例提醒用户，然后打印并读取一系列提示。

```
printf("Please fill in the following: %sName: %s"
read name
printf("Phone number: %s"
read phone
```

以下示例从文件读取一组正确和错误的答案，正确计算百分比并打印它们。数字是右对齐的，并用制表符分隔。百分比保留一位小数。

```
while read right wrong; do
percent=$(echo "%scale=1;($right*100)/($right+$wrong)" | bc)
printf("%2d right\t%2d wrong\t(%%s)\n", $right, $wrong, $percent)
done < database_file
```

1108

printf

命令

```
printf "%5d%4d\n" 1 21 321 4321 54321
```

产生

```
1 21
3214321
54321 0
```

注意格式操作数使用了三次打印所有给定的字符串，并且 printf 提供了 0 来满足最后一个 %4d 转换规范。
printf 命令在产生数值输出时检测到转换错误，因此在 32 位补码整数实现上会预期以下结果：

标准输出 | 诊断输出
---|---
5a | 5 printf: 5a not completely converted
999999999 | 2147483647 printf: 9999999999: Results too large
-999999999 | -2147483648 printf: -9999999999: Results too large
ABC | 0 printf: ABC expected numeric value

注意标准输出上显示的值将是函数 strtol(3C) 的返回值。%u 与 strtol(3C) 之间存在类似的对应关系，%e, %f, %g 与 strtod(3C) 之间也是。
在使用 ISO/IEC 646:1991 标准作为底层编码的 locale 中，命令

```
printf "%d\n" 3 -3 \\'+3 "'-3"
```

产生

```
3 Numeric of constant 3.
3 Numeric value of constant 3.
-3 Numeric value of constant -3.
51 Numeric value of the character 3 in the ISO/IEC 646:1991 standard codyset.
43 Numeric value of the character + in the ISO/IEC 646:1991 standard codyset.
45 Numeric value of the character - in the SO/IEC 646:1991 standard multibyte.
```

> 注意 — 在具有多字节字符的 locale 中，字符的值旨在是其等效的 wchar_t 表示的值。

