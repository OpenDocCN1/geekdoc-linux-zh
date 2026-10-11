

## C.2.6 汇总函数

汇总函数也称为“聚合”函数。它们基于一组值计算出一个单一的值。但是，该结果值仅基于所选行中的非 NULL 值（`COUNT(*)` 除外，它统计所有行）。汇总函数可用于汇总整个值集，或者在查询包含 `GROUP BY` 子句时，为值集的每个子组生成汇总。请参阅第 1.4.9.9 节，“生成汇总”。

本节中的示例假设存在一个表 `mytbl`，其中包含一个整型列 `mycol`，该列有八行，值为 1, 3, 5, 5, 7, 9, 9 和 `NULL`。

```sql
mysql> SELECT mycol FROM mytbl;
+--------+
| mycol  |
+--------+
|      1 |
|      3 |
|      5 |
|      5 |
|      7 |
|      9 |
|      9 |
|   NULL |
+--------+
```

### `AVG` ([DISTINCT] *expr*)

返回所选行中所有非 NULL 值中 *expr* 的平均值。如果没有非 NULL 值，则返回 `NULL`。

```sql
SELECT AVG(mycol) FROM mytbl           -> 5.5714
SELECT AVG(mycol)*2 FROM mytbl         -> 11.1429
SELECT AVG(mycol*2) FROM mytbl         -> 11.1429
```

从 MySQL 5.0.3 开始允许使用 `DISTINCT`。它使 `AVG()` 返回不同 *expr* 值的平均值。

### `BIT_AND` (*expr*)

返回所选行中所有非 NULL 值中 *expr* 的按位 AND 值。如果没有非 NULL 值，则返回 ~0。

```sql
SELECT BIT_AND(mycol) FROM mytbl       -> 1
```

### `BIT_OR` (*expr*)

返回所选行中所有非 NULL 值中 *expr* 的按位 OR 值。如果没有非 NULL 值，则返回 0。

```sql
SELECT BIT_OR(mycol) FROM mytbl        -> 15
```

### `BIT_XOR` (*expr*)

返回所选行中所有非 NULL 值中 *expr* 的按位异或值。如果没有非 NULL 值，则返回 0。

```sql
SELECT BIT_XOR(mycol) FROM mytbl       -> 5
```

### `COUNT`

- `COUNT(*expr*)`
- `COUNT(*)`
- `COUNT(DISTINCT expr1, expr2, ...)`

如果提供表达式参数，则返回结果集中非 NULL 值的数量。如果没有非 NULL 值，则返回 0。如果参数为 '*'，则返回结果集中所有行的数量，无论其内容如何。

```sql
SELECT COUNT(mycol) FROM mytbl         -> 7
SELECT COUNT(*) FROM mytbl             -> 8
```

对于 MySQL 表，没有 WHERE 子句的 `COUNT(*)` 会被优化，以非常快速地从 FROM 子句中指定的表名返回表中的行数。当命名了多个表时，`COUNT(*)` 返回各个表中行数的乘积。

```sql
SELECT COUNT(*) FROM mytbl AS m1 INNER JOIN mytbl AS m2 -> 64
```

`COUNT(DISTINCT)` 可用于统计不同的非 NULL 值的数量。

```sql
SELECT COUNT(DISTINCT mycol) FROM mytbl                -> 5
SELECT COUNT(DISTINCT MOD(mycol,3)) FROM mytbl          -> 3
```

如果给出多个表达式，`COUNT(DISTINCT)` 将统计不同的非 NULL 值组合的数量。

### `GROUP_CONCAT`

`GROUP_CONCAT([DISTINCT] var_list [ORDER BY ...] [SEPARATOR str])`

此函数连接一组字符串中的非 NULL 值并返回结果。如果没有非 NULL 值，则返回 NULL。您可以使用 DISTINCT 去除重复项，使用 ORDER BY 对结果进行排序，并使用 SEPARATOR 指定字符串之间的分隔符。默认情况下，GROUP_CONCAT() 不执行去重或排序，并使用逗号分隔值。

GROUP_CONCAT() 返回的值长度受系统变量 group_concat_max_len 的值限制。您可以更改此变量的值以启用更长的值。

```sql
mysql> CREATE TABLE t (name CHAR(10));
mysql> INSERT INTO t VALUES('dog'),('cat'),('rat'),('dog'),('rat');
mysql> SELECT GROUP_CONCAT(name) FROM t;
+-------------------+
| GROUP_CONCAT(name)|
+-------------------+
| dog,cat,rat,dog,rat |
+-------------------+

mysql> SELECT GROUP_CONCAT(name SEPARATOR ':') FROM t;
+------------------+
| GROUP_CONCAT(name SEPARATOR ':') |
+------------------+
| dog:cat:rat:dog:rat |
+------------------+

mysql> SELECT GROUP_CONCAT(name ORDER BY name DESC) FROM t;
+-------------------------------+
| GROUP_CONCAT(name ORDER BY name DESC) |
+-------------------------------+
| rat,rat,dog,dog,cat        |
+-------------------------------+

mysql> SELECT GROUP_CONCAT(DISTINCT name ORDER BY name) FROM t;
+-------------------------------+
| GROUP_CONCAT(DISTINCT name ORDER BY name) |
+-------------------------------+
| cat,dog,rat                 |
+-------------------------------+
```

### `MAX`

`MAX([DISTINCT] expr)`

返回所选行中所有非 `NULL` 值中 *expr* 的最大值。如果没有非 `NULL` 值，则返回 `NULL`。MAX() 也可用于字符串或时间值，在这种情况下，它返回词典序或时间上最大的值。

```sql
SELECT MAX(mycol) FROM mytbl            → 9
```

DISTINCT 使 MAX() 返回不同 *expr* 值的最大值（这不会改变结果）。

### `MIN`

`MIN([DISTINCT] expr)`

返回所选行中所有非 `NULL` 值中 *expr* 的最小值。如果没有非 `NULL` 值，则返回 `NULL`。MIN() 也可用于字符串或时间值，在这种情况下，它返回词典序或时间上最小的值。

```sql
SELECT MIN(mycol) FROM mytbl            → 1
```

DISTINCT 使 MIN() 返回不同 *expr* 值的最小值（这不会改变结果）。

### `STD`, `STDDEV`, `STDDEV_POP`

- `STD(*expr*)`
- `STDDEV(*expr*)`
- `STDDEV_POP(*expr*)`

返回所选行中所有非 `NULL` 值中 *expr* 的总体标准差。如果没有非 `NULL` 值，则返回 `NULL`。

```sql
SELECT STDDEV_POP(mycol) FROM mytbl      → 2.7701
```

STDDEV_POP() 在 MySQL 5.0.3 中引入。

### `STDDEV_SAMP`

`STDDEV_SAMP(expr)`

返回所选行中所有非 NULL 值中 *expr* 的样本标准差。如果没有非 NULL 值，则返回 *NULL*。

```sql
SELECT STDDEV_SAMP(mycol) FROM mytbl → 2.9921
```

STDDEV_SAMP() 在 MySQL 5.0.3 中引入。

### `SUM`

`SUM([DISTINCT] expr)`

返回所选行中所有非 NULL 值中 *expr* 的总和。如果没有非 NULL 值，则返回 *NULL*。

```sql
SELECT SUM(mycol) FROM mytbl → 39
```

DISTINCT 使 SUM() 返回不同 *expr* 值的总和。

### `VARIANCE`, `VAR_POP`

- `VARIANCE(expr)`
- `VAR_POP(expr)`

返回所选行中所有非 NULL 值中 *expr* 的总体方差。如果没有非 NULL 值，则返回 *NULL*。

```sql
SELECT VAR_POP(mycol) FROM mytbl → 7.6735
```

VAR_POP() 在 MySQL 5.0.3 中引入。

### `VAR_SAMP`

`VAR_SAMP(expr)`

返回所选行中所有非 NULL 值中 *expr* 的样本方差。如果没有非 NULL 值，则返回 *NULL*。

```sql
SELECT VAR_SAMP(mycol) FROM mytbl → 8.9524
```

VAR_SAMP() 在 MySQL 5.0.3 中引入。

## C.2.7 安全和压缩函数

这些函数执行各种与安全相关的操作，例如加密或压缩字符串。其中一些函数成对出现，一个函数生成加密值，另一个执行解密。这类函数对通常使用字符串作为密钥或密码值。如果您想恢复原始值，必须使用加密时使用的相同密钥来解密该值。否则，解密结果将毫无意义。

如果使用返回二进制字符串的加密函数，并希望将结果存储在数据库中，通常使用 BLOB 类型之一的列。

### `AES_DECRYPT`

`AES_DECRYPT(str, key_str)`

给定作为调用 `AES_ENCRYPT()` 结果获得的加密字符串 *str*，使用密钥字符串 *key_str* 对其进行解密，并返回结果字符串。如果任一参数为 *NULL*，则返回 *NULL*。

```sql
AES_DECRYPT(AES_ENCRYPT('secret','scramble'),'scramble')
→ 'secret'
```

### `AES_ENCRYPT`

`AES_ENCRYPT(str, key_str)`

使用高级加密标准 (AES) 和 128 位密钥长度，使用密钥字符串 *key_str* 对字符串 *str* 进行加密。结果作为二进制字符串返回，如果任一参数为 NULL，则返回 NULL。可以使用 `AES_DECRYPT()` 和相同的密钥字符串来解码该字符串。

### `COMPRESS`

`COMPRESS(str)`

以二进制字符串形式返回参数字符串的压缩版本，如果服务器未使用压缩库编译，则返回 NULL。

### `DECODE`

`DECODE(str, key_str)`

给定作为调用 `ENCODE()` 结果获得的加密字符串 *str*，使用密钥字符串 *key_str* 对其进行解密。返回结果字符串，如果 *str* 为 NULL，则返回 NULL。

```sql
DECODE(ENCODE('secret','scramble'),'scramble')
→ 'secret'
```

### `DES_DECRYPT`

`DES_DECRYPT(str [, key_str])`

解密字符串 *str*，该字符串应为 `DES_ENCRYPT()` 生成的加密值。如果未启用 SSL 支持或解密失败，`DES_DECRYPT()` 将返回 NULL。

如果提供了 *key_str* 参数，则将其用作解密密钥。如果未提供 *key_str* 参数，`DES_DECRYPT()` 将使用服务器 DES 密钥文件中的密钥来解密字符串。密钥编号由加密字符串第一字节的 0-6 位确定。密钥文件的位置在服务器启动时通过 `--des-key-file` 选项指定。如果使用不同的密钥来加密和解密字符串，结果将没有意义。

如果 *str* 看起来不像加密字符串，`DES_DECRYPT()` 将原样返回该字符串。（例如，如果第一字节未设置第 7 位，就会发生这种情况。）

使用 `DES_DECRYPT()` 的单参数形式需要 `SUPER` 权限。

### `DES_ENCRYPT`

`DES_ENCRYPT(str [, (key_num|key_str)])`

对字符串 *str* 执行 DES 加密，并以二进制字符串形式返回加密结果。可以使用 `DES_DECRYPT()` 对加密字符串进行解密。如果未启用 SSL 支持或加密失败，`DES_ENCRYPT()` 将返回 NULL。

如果提供了 *key_str* 参数，则将其用作加密密钥。如果提供了 *key_num* 参数，其值应为 0 到 9 之间的一个数字，表示服务器 DES 密钥文件中条目的密钥编号。在这种情况下，加密密钥取自该条目。如果未提供 *key_str* 或 *key_num* 参数，则使用 DES 密钥文件中的第一个密钥进行加密。（这不等同于指定 *key_num* 值为 0。）

