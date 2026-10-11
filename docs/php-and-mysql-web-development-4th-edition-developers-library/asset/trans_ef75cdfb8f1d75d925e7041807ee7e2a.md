

POSIX 构造函数用于字符类中：

- 'abc' REGEXP '[[:space:]]' → 0
- 'a c' REGEXP '[[:space:]]' → 1
- 'abc' REGEXP '[[:digit:]][[:punct:]]' → 0
- 'a@c' REGEXP '[[:digit:]][[:punct:]]' → 1
- 'a,c' REGEXP '[[:digit:]][[:punct:]]' → 1

在字符类中，特殊标记 `[.:<]` 和 `[.:>]` 分别匹配单词边界和结尾。单词字符被视为 alnum 类中的任何字符或下划线。单词由一个或多个单词字符组成，且前后均未出现单词字符。

- 'a few words' REGEXP '[.:<:]]few[.:>:]]' → 1
- 'a few words' REGEXP '[.:<:]]fe[.:>:]]' → 0

MySQL 在正则表达式字符串中使用类似于 C 的转义序列语法。例如，`'\n', '\t',` 和 `'\\'` 被解释为换行符、制表符和反斜杠。要在模式中指定这些字符，请将反斜杠加倍，即 `'\n', '\t',` 和 `'\\\\'`。在查询解析过程中会去除一个反斜杠；对剩余转义序列的解释发生在模式匹配操作期间。

- `str LIKE pattern`
- `str NOT LIKE pattern`

`LIKE` 和 `NOT LIKE` 是 `REGEXP` 和 `NOT REGEXP` 的同义词。

## C.2 函数

调用函数以执行计算并返回值。默认情况下，调用函数时，函数名及其后的括号之间不能有空格，否则可能会发生错误：

```
mysql> SELECT NOW();
+---------------------+
| NOW()               |
+---------------------+
| 2008-04-30 22:39:26 |
+---------------------+
1 row in set (0.00 sec)

mysql> SELECT NOW ();
ERROR 1305 (42000): FUNCTION NOW does not exist
```

如果启用了 `IGNORE_SPACE` SQL 模式，服务器允许在内置函数名称后包含空格，但副作用是所有函数名称都变成了保留字。根据客户端程序的不同，您也许能够针对特定连接选择此行为。例如，您可以使用 ignore-space 选项启动 `mysql`；在 C 程序中，您可以使用 `CLIENT_IGNORE_SPACE` 选项调用 `mysql_real_connect()`。

在大多数情况下，函数的多个参数由逗号分隔。函数参数前后允许有空格。以下两行均合法：

```
CONCAT( 'abc' ,'def')
CONCAT( 'abc' , 'def' )
```

此语法有少数例外，例如 `TRIM()` 或 `EXTRACT()`：

```
TRIM( ' ' FROM 'x' )      → 'x'
EXTRACT(YEAR FROM '2003-01-01')  → 2003
```

每个函数条目都描述其允许的语法。

### C.2.1 比较函数

这些函数用于执行值的比较。

- **ELT(n, str1, str2, ...)**
  - 从字符串列表 str1, str2, ... 中返回第 n 个字符串。如果 n 为 NULL、第 n 个字符串为 NULL 或没有第 n 个字符串，则返回 NULL。第一个字符串的索引为 1。ELT() 与 FIELD() 互为补充。
  ```
  ELT(3, 'a','b','c','d','e')         → 'c'
  ELT(0, 'a','b','c','d','e')         → NULL
  ELT(6, 'a','b','c','d','e')         → NULL
  ELT(FIELD('b','a','b','c'),'a','b','c') → 'b'
  ```

- **FIELD(arg0, arg1, arg2, ...)**
  - 在参数列表 arg1, arg2, ... 中查找 arg0，并返回匹配参数的索引（从 1 开始）。如果没有匹配项或 arg0 为 NULL，则返回 0。如果所有参数均为字符串，则使用字符串比较；如果所有参数均为数字，则使用数字比较；否则使用双精度比较。FIELD() 与 ELT() 互为补充。
  ```
  FIELD('b','a','b','c')              → 2
  FIELD('d','a','b','c')              → 0
  FIELD(NULL,'a','b','c')            → 0
  FIELD(ELT(2,'a','b','c'),'a','b','c') → 2
  ```

- **GREATEST(expr1, expr2, ...)**
  - 返回最大参数，其中“最大”的定义遵循以下规则：
    - 如果函数在整数上下文中调用，或者其所有参数均为整数，则按整数比较参数。
    - 如果函数在浮点上下文中调用，或者其所有参数均为浮点值，则按浮点值比较参数。
    - 如果上述两条规则均不适用，则按字符串比较参数。字符串比较规则如 C.1.4 节“比较运算符”开头所述。

  ```
  GREATEST(2,3,1) → 3
  GREATEST(38.5,94.2,-1) → 94.2
  GREATEST('a','ab','abc') → 'abc'
  GREATEST(1,3,5) → 5
  GREATEST('A','b','C') → 'C'
  GREATEST(BINARY 'A','b','C') → 'b'
  ```

- **IF(expr1, expr2, expr3)**
  - 如果 `expr1` 为真（非零、非 NULL），则返回 `expr2`；否则，返回 `expr3`。
  - `IF()` 的返回类型按以下顺序通过测试确定：如果 `expr2` 或 `expr3` 是字符串，则为字符串；如果其中任一为浮点值，则为浮点值；如果其中任一为整数，则为整数。

  ```
  IF(1, 'true', 'false') → 'true'
  IF(0, 'true', 'false') → 'false'
  IF(NULL, 'true', 'false') → 'false'
  IF(1,3, 'non-zero', 'zero') → 'non-zero'
  IF(0.3 <> 0, 'non-zero', 'zero') → 'non-zero'
  ```

  请注意，`IF()` 函数与 E.2.1 节“控制结构语句”中描述的 `IF` 语句不同。

- **IFNULL(expr1, expr2)**
  - 如果表达式 `expr1` 的值为 NULL，则返回 `expr2`；否则，返回 `expr1`。`IFNULL()` 根据使用上下文返回数字或字符串。

  ```
  IFNULL(NULL, 'null') → 'null'
  IFNULL('not null', 'null') → 'not null'
  ```

- **INTERVAL(n, n1, n2, ...)**
  - 如果 `n` < `n1` 返回 `0`，如果 `n` < `n2` 返回 `1`，依此类推；如果 `n` 为 NULL 则返回 -1。也就是说，`INTERVAL()` 查找第一个参数在由剩余参数定义的区间内的位置。所有参数必须是整数。值 `n1`, `n2`, ... 必须严格递增（`n1` < `n2` < ...），因为使用的是快速二分查找。否则 `INTERVAL()` 的行为将不可预测。

  ```
  INTERVAL(2,0,1,3) → 2
  INTERVAL(7,1,3,5,7,9) → 4
  ```

- **ISNULL(expr)**
  - 如果表达式 expr 的值为 NULL，则返回 1；否则，返回 0。

  ```
  ISNULL(NULL)            → 1
  ISNULL(0)              → 0
  ISNULL(1)              → 0
  ```

- **LEAST(expr1, expr2, ...)**
  - 返回最小参数，其中“最小”的定义使用与 GREATEST() 函数相同的比较规则。

  ```
  LEAST(2,3,1)            → 1
  LEAST(38.5,94.2,-1)     → -1
  LEAST('a','ab','abc')   → 'a'
  ```

- **NULLIF(expr1, expr2)**
  - 如果两个表达式的值不同，则返回 expr1；如果它们相同，则返回 NULL。

  ```
  NULLIF(3,4)             → 3
  NULLIF(3,3)             → NULL
  ```

- **STRCMP(str1, str2)**
  - 此函数根据第一个参数在字典序上是否大于、等于或小于第二个参数，分别返回 1、0 或 -1。如果任一参数为 NULL，则函数返回 NULL。如果任一操作数是二进制字符串，则 STRCMP() 将字符串作为二进制字符串进行比较；如果操作数是非二进制字符串，则使用操作数的排序规则。

  ```
  STRCMP('a','a')             → 0
  STRCMP('a','A')             → 1
  STRCMP(BINARY 'a','A')      → -1
  STRCMP('A' COLLATE latin1_general_ci, 'a')    → 0
  STRCMP('A' COLLATE latin1_general_cs, 'a')    → -1
  ```

### C.2.2 转换函数

这些函数将值从一种类型转换为另一种类型。

- **CAST(expr AS type)**
  - 将表达式值 expr 转换为给定类型。类型值可以是 BINARY(n)（二进制字符串）、CHAR(n)（非二进制字符串）、DATE、DATETIME、TIME、SIGNED [INTEGER]、UNSIGNED [INTEGER]，或者（从 MySQL 5.0.8 开始）DECIMAL(M,D)。

  ```
  CAST(304 AS BINARY)         → '304'
  CAST(-1 AS UNSIGNED)        → 18446744073709551615
  CAST(13 AS DECIMAL(5,2))    → 13.00
  ```

  可以为 BINARY 和 CHAR 指定可选长度 $n$，这使得结果分别不超过 $n$ 字节或字符。对于 BINARY，从 MySQL 5.0.17 开始，少于 $n$ 字节的值会被 `0x00` 字节填充至长度 $n$。在使用 `CREATE TABLE ... SELECT` 创建新表时，CAST() 可用于强制列具有特定类型，这非常有用。

```
mysql> CREATE TABLE t SELECT CAST(20080101 AS DATE) AS date_val;
mysql> SHOW COLUMNS FROM t;
+---------+------+-----+------+-------+-------+
| Field   | Type | Null | Key | Default | Extra |
+---------+------+-----+------+-------+-------+
| date_val | date | YES  |      | NULL    |       |
+---------+------+-----+------+-------+-------+
mysql> SELECT * FROM t;
+---------+
| date_val |
+---------+
| 2008-01-01 |
+---------+
```

CONVERT() 类似于 CAST()，但 CONVERT() 使用 ODBC 语法，而 CAST() 使用标准 SQL 语法。

- `CONVERT ( expr, type )`
- `CONVERT ( expr USING charset )`

CONVERT() 的第一种形式与 CAST() 的目的相同，但语法略有不同。`expr` 和 `type` 参数的含义相同。第二种（USING）形式将值转换为具有给定字符集的字符串。

```
CONVERT(304, BINARY) → '304'
CONVERT(-1, UNSIGNED) → 18446744073709551615
CONVERT('abc' USING utf8); → 'abc'
```

### C.2.3 数值函数

如果您传递超出范围或其他无效的参数，数值函数将返回 `NULL`。

- **ABS ( x )**
  - 返回 $x$ 的绝对值。
  ```
  ABS(13.5)      → 13.5
  ABS(-13.5)     → 13.5
  ```

- **ACOS ( x )**
  - 返回 $x$ 的反余弦，如果 $x$ 不在 -1 到 1 的范围内，则返回 `NULL`。
  ```
  ACOS(1)        → 0
  ```

