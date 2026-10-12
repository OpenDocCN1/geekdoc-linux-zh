
- `RAND()` $\rightarrow$ .1036697114852
- `RAND(1)` $\rightarrow$ .5725383884949
- `RAND(10)` $\rightarrow$ .65705152196535
- `RAND(10)` $\rightarrow$ .65705152196535

种子操作是特定于客户端的。如果一个客户端调用 `RAND(n)` 为随机数生成器设置种子，这不会影响其他客户端返回的数字。

如果 `RAND()` 出现在 `WHERE` 子句中，它将在每次执行该子句时被调用一次。

### ROUND(x)

- `ROUND(x)`
- `ROUND(x, d)`

`ROUND()` 返回 `x` 的值，四舍五入到 `d` 位小数。如果 `d` 为 0 或缺失，结果没有小数点或小数部分。返回值具有与第一个参数相同的数值类型，因此如果该参数是整数，结果就没有小数。指定为字符串的数字会 undergo 常规转换为双精度浮点数，并按此处理。

- `ROUND(15.3)` $\rightarrow$ 15
- `ROUND(15.5)` $\rightarrow$ 16
- `ROUND(-33.27834,2)` $\rightarrow$ -33.28
- `ROUND(1,4)` $\rightarrow$ 1
- `ROUND('1',4)` $\rightarrow$ 1.0000

如果 `d` 为负数，`ROUND()` 将截断任何小数部分，并将小数点左侧的 `ABS(d)` 位数字清零。

- `ROUND(123456,-2)` $\rightarrow$ 123500

在 MySQL 5.0.3 之前，`ROUND()` 的精确行为取决于底层数学库的四舍五入行为。这意味着 `ROUND()` 的结果可能因系统而异。自 MySQL 5.0.3 起，`ROUND()` 对 `x` 的四舍五入处理如下：

- 对于近似值数字，四舍五入仍取决于底层数学库。
- 具有 .5 或更大小数部分的精确值数字将远离零四舍五入。具有小于 .5 小数部分的精确值数字将向零四舍五入。例如，`1.5` 和 `−1.5` 四舍五入为 `2` 和 `−2`，而 `1.49` 和 `−1.49` 四舍五入为 `1` 和 `−1`。

有关哪些构成精确或近似数字的信息，请参阅 3.1.1.1 节，“精确值和近似值数字”。

### SIGN(x)

根据 `x` 的值为负、零或正，返回 −1、0 或 1。

- `SIGN(15.803)` $\rightarrow$ 1
- `SIGN(0)` $\rightarrow$ 0
- `SIGN(-99)` $\rightarrow$ -1

### SIN(x)

返回 `x` 的正弦值，其中 `x` 以弧度为单位。

- `SIN(0)` $\rightarrow$ 0
- `SIN(PI()/2)` $\rightarrow$ 1

### SQRT(x)

返回 `x` 的非负平方根。

- `SQRT(625)` $\rightarrow$ 25
- `SQRT(2.25)` $\rightarrow$ 1.5
- `SQRT(-1)` $\rightarrow$ NULL

### TAN(x)

返回 `x` 的正切值，其中 `x` 以弧度为单位。

- `TAN(0)` $\rightarrow$ 0
- `TAN(PI()/4)` $\rightarrow$ 1

### TRUNCATE(x, d)

返回值 `x`，小数部分截断为 `d` 位小数。如果 `d` 为 0，结果没有小数点或小数部分。如果 `d` 大于 `x` 的小数位数，小数部分将在右侧填充尾随零以达到所需宽度。

- `TRUNCATE(1.23, 1)` $\rightarrow$ 1.2
- `TRUNCATE(1.23, 0)` $\rightarrow$ 1
- `TRUNCATE(1.23, 4)` $\rightarrow$ 1.2300

如果 `d` 为负数，`TRUNCATE()` 将截断任何小数部分，并将小数点左侧的 `ABS(d)` 位数字清零。

- `TRUNCATE(123456.789, -3)` $\rightarrow$ 123000

## C.2.4 字符串函数

本节中的大多数函数返回字符串结果。其中一些，如 `LENGTH()`，以字符串为参数并返回数字。对于基于字符串位置操作的字符串函数，第一个（最左侧）字符的位置是 1，而不是 0。有几个字符串函数是支持多字节的：`CHAR_LENGTH()`、`INSERT()`、`INSTR()`、`LOCATE()`、`LEFT()`、`LOCATE()`、`LOWER()`、`LTRIM()`、`MID()`、`POSITION()`、`REPLACE()`、`REVERSE()`、`RIGHT()`、`RPAD()`、`RTRIM()`、`SUBSTRING()`、`SUBSTRING_INDEX()`、`TRIM()`、`UCASE()` 和 `UPPER()`。

### ASCII(str)

返回字符串 `str` 最左侧字节的整数值，范围从 0 到 255。如果 `str` 为空，则返回 0；如果 `str` 应仅包含 8 位字符，则返回 NULL。

- `ASCII('abc')` $\rightarrow$ 97
- `ASCII('')` $\rightarrow$ 0
- `ASCII(NULL)` $\rightarrow$ NULL

### BIN(n)

返回包含参数 `n` 的二进制位表示的字符串。以下两个表达式是等价的：

- `BIN(65)` $\rightarrow$ '1000001'
- `CONV(65,10,2)` $\rightarrow$ '1000001'

有关更多信息，请参阅 `CONV()` 的描述。

### CHAR(n1, n2, ... [USING charset])

在 MySQL 5.0.15 之前，将 `n1, n2, ...` 参数解释为数字字符代码，并返回由相应字符值的连接组成的连接字符集中的字符串。代码按模 256 解释（仅使用低 8 位）。自 MySQL 5.0.15 起，大于 255 的字符代码会产生多个结果字节，并且可以给出 `USING` 选项。如果没有 `USING`，返回值是二进制字符串。如果有 `USING`，返回值具有指定的字符集。如果结果对于字符集不合法，则会发出警告（并且在严格 SQL 模式下，结果为 NULL）。忽略 NULL 参数。

- `CHAR(65)` $\rightarrow$ 'A'
- `CHAR(97)` $\rightarrow$ 'a'
- `CHAR(89,105,107,101,115,33)` $\rightarrow$ 'Yikes!'

### CHAR_LENGTH(str)

- `CHARACTER_LENGTH(str)`

这些函数与 `LENGTH()` 类似，不同之处在于参数长度是按字符而非字节计算的。（多字节字符每个都计为长度 1。）

### CHARSET(str)

返回给定字符串的字符集名称，如果参数为 NULL，则返回 NULL。

```
CHARSET('abc')               → 'latin1'
CHARSET(CONVERT('abc' USING utf8))          → 'utf8'
CHARSET(123)                   → 'binary'
```

### COALESCE(expr1, expr2, . . . )

返回列表中第一个非 NULL 元素，如果所有参数均为 NULL，则返回 NULL。

```
COALESCE(NULL, 1/0, 2, 'a', 45+97)         → '2'
COALESCE(NULL, 1/0)                  → NULL
```

### COERCIBILITY(str)

返回字符串的比较排序强制性，如果参数非法，则返回 NULL。比较排序强制性是指字符串在包含其他字符串的表达式中其比较排序规则被改变的程度。下表列出了从低到高比较排序强制性的返回值。

| 比较排序强制性 | 含义 |
| :----------- | :----------- |
| 0 | 显式指定比较排序，不可强制转换 |
| 1 | 未指定比较排序 |
| 2 | 隐式比较排序 |
| 3 | 系统值（如 `USER()`）的比较排序 |
| 4 | 可强制转换比较排序 |
| 5 | 可忽略比较排序（类似于 NULL） |

```
COERCIBILITY(_utf8 'abc' COLLATE utf8_bin)  → 0
COERCIBILITY('abc')                          → 4
```

### COLLATION(str)

返回给定字符串的比较排序名称，如果参数非法，则返回 NULL。

```
COLLATION(_latin2 'abc')              → 'latin2_general_ci'
COLLATION(CONVERT('abc' USING utf8) COLLATE utf8_bin)  → 'utf8_bin'
```

### CONCAT(str1, str2, . . . )
