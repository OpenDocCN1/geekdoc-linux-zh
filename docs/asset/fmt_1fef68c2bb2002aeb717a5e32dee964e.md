
声明一个或多个数据类型的联合。`fielddeclarations`必须是有效的数据定义。在嵌套的`UNION`定义中省略`ENDS`名称标签。

# `.UNTIL`

参见`REPEAT`。

# `.UNTILCXZ`

参见`REPEAT`

# `.WHILE condition`

语句

`.ENDW`

生成代码，在条件保持为真时执行语句块。

`WHILE expression`

语句

`ENDM`

只要`expression`保持为真，就重复汇编块语句。

`[[name |]] WORD initializer [[, initializer]], . .`

为每个初始化器分配并可选地初始化一个字（2字节）存储。也可以在任何类型的地方作为类型指定符使用。

`.XALL`, 参见`.LISTMACRO`。
`.XREF`参见`.NOCREF`。
`.XLIST`参见`.NOLIST`。

**`XMM`**

启用 Internet Streaming SIMD 指令的汇编。

## D.8 预定义符号

`$`

计数器的当前值。

`?`

在数据定义中，一个分配但不初始的值。

`@@`

定义`label1`和`label2`之间的代码，其中`label1`是代码的起始，`label2`是代码的结束。参见`@B`和`@F`。

`@B`

之前的代码。

`@CatStr string1 [[, string2 ]]`

函数连接一个或多个字符串。返回字符串。

`@Cpu`

处理器模式。

`@fata`

由`.F`定义的段名。

`@fata?`

由`.FATA?`定义的段名。

`@FileCur`

当前文件名。

`@FileName`正在汇编的主文件名。

`@Instr([ position |], string1, string2`

函数，在`string1`中从`position`开始查找`string2`的首次出现。如果未找到`string2`则返回正整数。

`@Interface`关于语言参数的信息（数值常量）。

`@Line`当前文件的行号（数值常量）。

`@Model1`代表 TINY，2 代表 SMALL，3 代表 COMPACT，4 代表 MEDIUM，5 代表 LARGE，6 代表 HUGE，7 代表 FLAT 模型（数值常量）。

`@SizeStr( string )`
函数，返回给定字符串的长度。返回整数。

`@stack`近栈使用 DGROUP，远栈使用 STACK（文本宏）。

`@SubStr( string, position || length )`
函数，返回`position`处的子字符串。

`@Date mm/dd/yy`格式的系统日期（文本宏）。

`@Time`24小时 hh:mm:ss 格式的系统时间（文本宏）。

`@Version`MASM 6.1 中的 610（文本宏）。

`@WordSize`16 位段为 2，32 位段为 4（数值常量）。

## D.8 预定义符号（注：此处原文标题与 D.8 重复，已翻译）

`$`

计数器的当前值。

`?`

在数据定义中，一个分配但不初始的值。

`@@`

定义`label1`和`label2`之间的代码，其中`label1`是代码的起始，`label2`是代码的结束。参见`@B`和`@F`。

`@B`之前的代码。

`@CatStr string1 [[, string2 ]]`

函数连接一个或多个字符串。返回字符串。

`@Cpu`处理器模式。

`@fata`由`.F`定义的段名。

`@fata?`由`.FATA?`定义的段名。

`@FileCur`当前文件名。

`@FileName`正在汇编的主文件名。

`@Instr([ position |], string1, string2`

函数，在`string1`中从`position`开始查找`string2`的首次出现。如果未找到`string2`则返回正整数。

`@Interface`关于语言参数的信息（数值常量）。

`@Line`当前文件的行号（数值常量）。

`@Model`1 代表 TINY，2 代表 SMALL，3 代表 COMPACT，4 代表 MEDIUM，5 代表 LARGE，6 代表 HUGE，7 代表 FLAT 模型（数值常量）。

`@SizeStr( string )`函数，返回给定字符串的长度。返回整数。

`@stack`近栈使用 DGROUP，远栈使用 STACK（文本宏）。

`@SubStr( string, position || length )`函数，返回`position`处的子字符串。

`@Time`24小时 hh:mm:ss 格式的系统时间（文本宏）。

`@Version`MASM 6.1 中的 610（文本宏）。

`@WordSize`16 位段为 2，32 位段为 4（数值常量）。

## D.9 运算符

```
expression1 + expression2
```

返回`expression1`加`expression2`。
```
expression1 - expression2
```
返回`expression1`减去`expression2`。
```
expression1 * expression2
```
返回`expression1`乘以`expression2`。
```
expression1 / expression2
```

返回`expression1`除以`expression2`。
```
-expression
```
反转`expression`的符号。
```
expression1 [expression2]
```
返回`expression1`加[`expression2`]。
```
nsegment: expression:
```
用`segment`覆盖`expression`的默认段。`segment`可以是段寄存器、组名、段名或段表达式。`expression`必须是常量。
```
expression,field ||.field ||...
```
返回`expression`加上其在结构或联合中的字段偏移量。
```
[register],field ||.field ||...
```
返回`register`指向的位置加上其在结构或联合中的字段偏移量。

将文本视为单个字面量元素。

`"text"`

将`"text"`视为字符串。

`'text'`

将`'text'`视为字符串。

`!character`

将字符视为字面字符，而不是运算符或符号。

`;text`

将文本视为注释。

`;;text`

将文本视为宏中的注释，仅在宏定义中出现。列表不会显示宏展开后的文本。

`%expression`

将宏参数中表达式的值视为文本。

`&parameter&`

将参数替换为相应的参数值。

`ABS`

参见`EXTNDEF`指令。

`ADDR`

参见`INVOKE`指令。

```
expression1 AND expression2
```
返回`expression1`和`expression2`的按位 AND 运算结果。

```
count DUP (initialvalue [, initialvalue]...)
```
指定`initialvalue`声明的`count`次。

```
expression1 EQ expression2
```
如果`expression1`等于`expression2`，则返回真 (-1)，否则返回假 (0)。

```
expression1 GE expression2
```
如果`expression1`大于或等于`expression2`，则返回真 (-1)，否则返回假 (0)。

```
expression1 GT expression2
```
如果`expression1`大于`expression2`，则返回真 (-1)，否则返回假 (0)。

`HIGH expression`

返回`expression`的高字节。

`HIGHWORD expression`

返回`expression`的高字。

# `expression1 LE expression2`

如果`expression1`小于或等于`expression2`，则返回真 (-1)，否则返回假 (0)。

# `LENGTH variable`

返回由第一个初始化器创建的变量中的数据个数。

# `LENGTHOF variable`

返回变量中数据对象的个数。

# `LOW expression`

返回`expression`的低字节。

# `LOWWORD expression`

返回`expression`的低字。

# `LFFSET expression`

返回`expression`的偏移量。与`OFFSET`相同，但它生成加载器解析的偏移，允许 Windows 重定位代码段。

# `expression1 LT expression2`

如果`expression1`小于`expression2`，则返回真 (-1)，否则返回假 (0)。

# `MASK { recordname record }`

返回一个位掩码，其中`recordfieldname`或`record`的位设置为，所有其他位清零。

# `expression1 MOD expression2`

返回`expression1`除以`expression2`的余数（模）的整数值。

# `expression1 NE expression2`

如果`expression1`不等于`expression2`，则返回真 (-1)，如果相等则返回假 (0)。

# `NOT expression`

返回所有位反转的表达式。

# `OFFSET expression`

返回`expression`的偏移量。

# `OPATTR expression`

返回定义表达式模式和范围的字。低字节与`.TYPE`返回的字节相同。高字节包含额外信息。

# `expression1 OR expression2`

返回`expression1`和`expression2`的按位 OR 运算结果。

# `type PTR expression`

强制将表达式视为具有指定的类型。

## D.10 运算符

`||distance || PTR type`

指定指向类型的指针。

# `SEG expression`

返回`expression`的段。

# `expression SHL count`

返回`expression`的位左移`count`位的结果。

# `SHORT label`

将标签的类型设置为 short。所有到`label`的跳转必须是短跳转（在跳转指令到标签的 -128 到 +127 字节范围内）。

# `expression SHR count`

返回`expression`的位右移`count`位的结果。

# `SIZE variable`

返回由第一个初始化器分配的变量的字节数。

# `SIZEOF {variable | type}`

返回变量或类型的字节数。

# `THIS type`

返回指定类型的操作数，其偏移量和段值等于当前位置计数器的值。

# `.TYPE expression`

参见`OPATTR`。

# `TYPE expression`

返回表达式的类型。

# `WIDTH {recordfieldname | record}`

返回当前`recordfieldname`或`record`的位宽。

# `expression1 XOR expression2`

返回`expression1`和`expression2`的按位 XOR 运算结果。

## D.10 运行时运算符

以下运算符仅用在`.IF`、`.WHILE`或`.REPEAT`块内，并在运行时评估，而不是在汇编时评估：

```
expression1 = expression2
```
等于。

```
expression1 != expression2
```
不等于。

```
expression1 > expression2
```
大于。

```
expression1 >= expression2
```
大于或等于。

```
expression1 < expression2
```
小于。

```
expression1 <= expression2
```
小于或等于。

```
expression1 || expression2
```
逻辑或 (OR)。

```
expression1 && expression2
```
逻辑与 (AND)。

```
expression1 & expression2
```
按位与。

```
!expression
```
逻辑非。

```
CARRY?
```
进位标志状态。

```
OVERFLOW?
```
溢出标志状态。

```
PARITY?
```
奇偶标志状态。

```
SIGN?
```
符号标志状态。

```
ZERO?
```
