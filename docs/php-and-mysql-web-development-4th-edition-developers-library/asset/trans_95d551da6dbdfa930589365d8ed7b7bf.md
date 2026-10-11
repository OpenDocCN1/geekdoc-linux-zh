

## ACOS(x)

返回 $x$ 的反正切值，如果 $x$ 不在 -1 到 1 的范围内，则返回 NULL。

- ACOS(0) $\rightarrow$ 1.5707963267949
- ACOS(-1) $\rightarrow$ 3.1415926535898

## ASIN(x)

返回 $x$ 的反正弦值，如果 $x$ 不在 -1 到 1 的范围内，则返回 NULL。

- ASIN(1) $\rightarrow$ 1.5707963267949
- ASIN(0) $\rightarrow$ 0
- ASIN(-1) $\rightarrow$ -1.5707963267949

## ATAN(x)

- ATAN(x)
- ATAN(x, y)

atan() 的单参数形式返回 $x$ 的反正切值。双参数形式是 ATAN2() 的同义词。

- ATAN(1) $\rightarrow$ 0.78539816339745
- ATAN(0) $\rightarrow$ 0
- ATAN(-1) $\rightarrow$ -0.78539816339745

## ATAN2(y, x)

这类似于 ATAN(y/x)，但它使用两个参数的符号来确定返回值所在的象限。

- ATAN2(1, 1) $\rightarrow$ 0.78539816339745
- ATAN2(1, -1) $\rightarrow$ 2.3561944901923
- ATAN2(-1, 1) $\rightarrow$ -0.78539816339745
- ATAN2(-1, -1) $\rightarrow$ -2.3561944901923

## CEILING(x)

- CEILING(x)
- CEIL(x)

返回不小于 $x$ 的最小整数。如果参数具有精确值数值类型，则返回值也是如此。否则，返回值的类型为浮点（近似值）类型。即使数值没有小数部分，这一情况也成立。

- CEILING(3.8) $\rightarrow$ 4
- CEILING(-3.8) $\rightarrow$ -3

## COS(x)

返回 $x$ 的余弦值，其中 $x$ 以弧度为单位。

- COS(0) $\rightarrow$ 1
- COS(PI()) $\rightarrow$ -1

## COT(x)

返回 $x$ 的余切值，其中 $x$ 以弧度为单位。

- COT(PI()/4) $\rightarrow$ 1

## CRC32(str)

计算参数的循环冗余校验值，该参数被视为字符串。返回值是一个 32 位无符号值，范围从 0 到 $2^{32}-1$，如果参数为 `NULL`，则返回 `NULL`。

- CRC32('xyz') $\rightarrow$ 3951999591
- CRC32('0') $\rightarrow$ 4108050209
- CRC32(0) $\rightarrow$ 4108050209
- CRC32(NULL) $\rightarrow$ NULL

## DEGREES(x)

返回 $x$ 的值，将弧度转换为度。

- DEGREES(PI()) $\rightarrow$ 180
- DEGREES(PI()*2) $\rightarrow$ 360
- DEGREES(PI()/2) $\rightarrow$ 90
- DEGREES(-PI()) $\rightarrow$ -180

## EXP(x)

返回 $e^x$，其中 $e$ 是自然对数的底。

- EXP(1) $\rightarrow$ 2.718281828459
- EXP(2) $\rightarrow$ 7.3890560989307
- EXP(-1) $\rightarrow$ 0.36787944117144
- 1/EXP(1) $\rightarrow$ 0.36787944117144

## FLOOR(x)

返回不大于 $x$ 的最大整数。如果参数具有精确值数值类型，则返回值也是如此。否则，返回值的类型为浮点（近似值）类型。即使数值没有小数部分，这一情况也成立。

- FLOOR(3.8) $\rightarrow$ 3
- FLOOR(-3.8) $\rightarrow$ -4

## LN(x)

这是 LOG() 的同义词。

## LOG(x)

- LOG(x)
- LOG(b, x)

LOG() 的单参数形式返回 $x$ 的自然对数（以 $e$ 为底）。

- LOG(0) $\rightarrow$ NULL
- LOG(1) $\rightarrow$ 0
- LOG(2) $\rightarrow$ 0.69314718055995
- LOG(EXP(1)) $\rightarrow$ 1

双参数形式返回 $x$ 以 $b$ 为底的对数。

- LOG(10,100) $\rightarrow$ 2
- LOG(2,256) $\rightarrow$ 8

您也可以使用 LOG($x$)/LOG($b$) 计算 $x$ 以 $b$ 为底的对数。

- LOG(100)/LOG(10) $\rightarrow$ 2
- LOG10(100) $\rightarrow$ 2

## LOG10(x)

返回 $x$ 以 10 为底的对数。

- LOG10(0) $\rightarrow$ NULL
- LOG10(10) $\rightarrow$ 1
- LOG10(100) $\rightarrow$ 2

## LOG2(x)

返回 $x$ 以 2 为底的对数。

- LOG2(0) $\rightarrow$ NULL
- LOG2(255) $\rightarrow$ 7.99435434368589
- LOG2(32767) $\rightarrow$ 14.999955597177

LOG2() 告诉您数值的“宽度”（以位为单位）。其用途之一是评估该值所需的存储空间。

## MOD(m, n)

MOD() 执行取模运算。MOD(m, n) 函数语法与 $m \% n$ 或 $m \text{ MOD } n$ 运算符语法相同（见 C.1.3 节，“算术运算符”）。

## PI()

返回 $\pi$ 的值。

- PI() $\rightarrow$ 3.141593

## POW(x, y)

返回 $x^y$，即 $x$ 的 $y$ 次幂。

- POW(2,3) $\rightarrow$ 8
- POW(2,-3) $\rightarrow$ 0.125
- POW(4,-5) $\rightarrow$ 2
- POW(16, 25) $\rightarrow$ 2

*注：原文 "POW (16, ,25)" 中多出一个逗号，已更正为 "POW(16, 25)"。*

## RADIANS(x)

返回 $x$ 的值，将度转换为弧度。

- RADIANS(0) $\rightarrow$ 0
- RADIANS(360) $\rightarrow$ 6.2831853071796
- RADIANS(-360) $\rightarrow$ -6.2831853071796

## RAND()

- RAND()
- RAND(n)

RAND() 返回 0.0 到 1.0 范围内的随机浮点值。对于常量整数参数 n，RAND(n) 执行相同操作，使用 n 作为随机化器的种子值。当您需要结果集中某列的可重复数字序列时，可以使用种子值。（自 MySQL 5.0.13 起，不允许非常量参数；在此之前的版本中，其影响是未定义的。）

- RAND() $\rightarrow$ .1036697114852
- RAND(1) $\rightarrow$ .5725383884949
- RAND(10) $\rightarrow$ .65705152196535
- RAND(10) $\rightarrow$ .65705152196535

种子操作是特定于客户端的。如果一个客户端调用 RAND(n) 为随机数生成器设置种子，这不会影响其他客户端返回的数字。

如果 RAND() 出现在 WHERE 子句中，它将在每次执行该子句时被调用一次。

## ROUND(x)

- ROUND(x)
- ROUND(x, d)

ROUND() 返回 x 的值，四舍五入到 d 位小数。如果 d 为 0 或缺失，结果没有小数点或小数部分。返回值具有与第一个参数相同的数值类型，因此如果该参数是整数，结果就没有小数。指定为字符串的数字会 undergo 常规转换为双精度浮点数，并按此处理。

- ROUND(15.3) $\rightarrow$ 15
- ROUND(15.5) $\rightarrow$ 16
- ROUND(-33.27834,2) $\rightarrow$ -33.28
- ROUND(1,4) $\rightarrow$ 1
- ROUND('1',4) $\rightarrow$ 1.0000

如果 d 为负数，ROUND() 将截断任何小数部分，并将小数点左侧的 ABS(d) 位数字清零。

- ROUND(123456,-2) $\rightarrow$ 123500

在 MySQL 5.0.3 之前，ROUND() 的精确行为取决于底层数学库的四舍五入行为。这意味着 ROUND() 的结果可能因系统而异。自 MySQL 5.0.3 起，ROUND() 对 x 的四舍五入处理如下：

- 对于近似值数字，四舍五入仍取决于底层数学库。
- 具有 .5 或更大小数部分的精确值数字将远离零四舍五入。具有小于 .5 小数部分的精确值数字将向零四舍五入。例如，1.5 和 −1.5 四舍五入为 2 和 −2，而 1.49 和 −1.49 四舍五入为 1 和 −1。

有关哪些构成精确或近似数字的信息，请参阅 3.1.1.1 节，“精确值和近似值数字”。

## SIGN(x)

根据 x 的值为负、零或正，返回 −1、0 或 1。

- SIGN(15.803) $\rightarrow$ 1
- SIGN(0) $\rightarrow$ 0
- SIGN(-99) $\rightarrow$ -1

## SIN(x)

返回 x 的正弦值，其中 x 以弧度为单位。

- SIN(0) $\rightarrow$ 0
- SIN(PI()/2) $\rightarrow$ 1

## SQRT(x)

返回 x 的非负平方根。

- SQRT(625) $\rightarrow$ 25
- SQRT(2.25) $\rightarrow$ 1.5
- SQRT(-1) $\rightarrow$ NULL

## TAN(x)

返回 x 的正切值，其中 x 以弧度为单位。

- TAN(0) $\rightarrow$ 0
- TAN(PI()/4) $\rightarrow$ 1

## TRUNCATE(x, d)

返回值 x，小数部分截断为 d 位小数。如果 d 为 0，结果没有小数点或小数部分。如果 d 大于 x 的小数位数，小数部分将在右侧填充尾随零以达到所需宽度。

- TRUNCATE(1.23, 1) $\rightarrow$ 1.2
- TRUNCATE(1.23, 0) $\rightarrow$ 1
- TRUNCATE(1.23, 4) $\rightarrow$ 1.2300

如果 d 为负数，TRUNCATE() 将截断任何小数部分，并将小数点左侧的 ABS(d) 位数字清零。

- TRUNCATE(123456.789, -3) $\rightarrow$ 123000

## C.2.4 字符串函数

本节中的大多数函数返回字符串结果。其中一些，如 LENGTH()，以字符串为参数并返回数字。对于基于字符串位置操作的字符串函数，第一个（最左侧）字符的位置是 1，而不是 0。有几个字符串函数是支持多字节的：CHAR_LENGTH()、INSERT()、INSTR()、LOCATE()、LEFT()、LOCATE()、LOWER()、LTRIM()、MID()、POSITION()、REPLACE()、REVERSE()、RIGHT()、RPAD()、RTRIM()、SUBSTRING()、SUBSTRING_INDEX()、TRIM()、UCASE() 和 UPPER()。

## ASCII(str)

返回字符串 str 最左侧字节的整数值，范围从 0 到 255。如果 str 为空，则返回 0；如果 str 应仅包含 8 位字符，则返回 NULL。

- ASCII('abc') $\rightarrow$ 97
- ASCII('') $\rightarrow$ 0
- ASCII(NULL) $\rightarrow$ NULL

## BIN(n)

返回包含参数 n 的二进制位表示的字符串。以下两个表达式是等价的：

- BIN(65) $\rightarrow$ '1000001'
- CONV(65,10,2) $\rightarrow$ '1000001'

有关更多信息，请参阅 CONV() 的描述。

## CHAR(n1, n2, ... [USING charset])

在 MySQL 5.0.15 之前，将 n1, n2, ... 参数解释为数字字符代码，并返回由相应字符值的连接组成的连接字符集中的字符串。代码按模 256 解释（仅使用低 8 位）。自 MySQL 5.0.15 起，大于 255 的字符代码会产生多个结果字节，并且可以给出 USING 选项。如果没有 USING，返回值是二进制字符串。如果有 USING，返回值具有指定的字符集。如果结果对于字符集不合法，则会发出警告（并且在严格 SQL 模式下，结果为 NULL）。忽略 NULL 参数。

- CHAR(65) $\rightarrow$ 'A'
- CHAR(97) $\rightarrow$ 'a'
- CHAR(89,105,107,101,115,33) $\rightarrow$ 'Yikes!'

## CHAR_LENGTH(str)

- CHARACTER_LENGTH(str)

