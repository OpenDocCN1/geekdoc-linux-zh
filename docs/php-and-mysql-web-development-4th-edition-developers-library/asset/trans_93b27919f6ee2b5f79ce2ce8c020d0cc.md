
## 字符集和排序规则属性

当你在列、表或数据库级别指定 **CHARACTER SET** 和 **COLLATE** 属性时，适用以下规则：

- 字符集必须是服务器支持的字符集。要显示可用的字符集，请使用 `SHOW CHARACTER SET`。
- 对于同时包含 **CHARACTER SET** 和 **COLLATE** 的定义，字符集和排序规则必须兼容。例如，如果使用字符集 `latin2`，可以使用排序规则 `latin2_croatian_ci`，但不能使用 `latin1_bin`。要显示每个字符集的排序规则，请使用 `SHOW COLLATION`。
- 对于包含 **CHARACTER SET** 但不包含 **COLLATE** 的定义，使用字符集的默认排序规则。
- 对于包含 **COLLATE** 但不包含 **CHARACTER SET** 的定义，字符集由排序规则名称的第一部分决定。

为了查看这些规则是如何应用的，请考虑以下语句。它创建一个使用多种字符集的表：

```sql
CREATE TABLE mytbl
(
  c1 CHAR(10),
  c2 CHAR(40) CHARACTER SET latin2,
  c3 CHAR(10) COLLATE latin1_german1_ci,
  c4 BINARY(40)
) CHARACTER SET utf8;
```

生成的表将 `utf8` 作为其默认字符集。由于未给出 **COLLATE** 表选项，因此默认表排序规则是默认的 `utf8` 排序规则（即 `utf8_general_ci`）。c1 列定义本身不包含 **CHARACTER SET** 或 **COLLATE** 属性，因此为其使用表默认值。表级字符集和排序规则不适用于 c2、c3 和 c4：c2 和 c3 拥有自己的字符集信息，而 c4 是二进制字符串类型，因此字符集属性不适用。对于 c2，排序规则为 `latin2_general_ci`，这是 `latin2` 的默认排序规则。对于 c3，字符集为 `latin1`，这是由排序规则名称 `latin1_german1_ci` 暗示的。

要查看现有表的字符集信息，请使用 **SHOW CREATE TABLE**：

```text
mysql> SHOW CREATE TABLE mytbl\G
*************************** 1. row ***************************
   Table: mytbl
Create Table: CREATE TABLE `mytbl` (
  `c1` char(10) default NULL,
  `c2` char(40) character set latin2 default NULL,
  `c3` char(10) character set latin1 collate latin1_german1_ci default NULL,
  `c4` binary(40) default NULL
) ENGINE=MyISAM DEFAULT CHARSET=utf8
```

如果 `SHOW CREATE TABLE` 未显示列字符集，则它与表默认字符集相同。如果未显示列排序规则，则是该字符集的默认排序规则。

你还可以在 `SHOW COLUMNS` 中添加 `FULL` 关键字，使其显示排序规则信息（从中可以推导出字符集）：

```text
mysql> SHOW FULL COLUMNS FROM mytbl;
```

| 字段 | 类型 | 排序规则 | 允许为空 | 键 | 默认值 |
|-------|------|-----------|------|-----|---------|
| c1    | char(10) | utf8_general_ci | 是 | | NULL |
| c2    | char(40) | latin2_general_ci | 是 | | NULL |
| c3    | char(10) | latin1_german1_ci | 是 | | NULL |
| c4    | binary(40) | NULL | 是 | | NULL |

上述讨论提到了列和表的字符集分配，但实际上字符集可以在列、表、数据库或服务器级别指定。当 MySQL 处理字符列定义时，它会通过按顺序尝试以下规则来确定使用哪个字符集：

1. 如果列定义包含字符集，则使用该字符集。（这也包括仅存在 `COLLATE` 属性的情况，因为这暗示了使用哪个字符集。）
2. 否则，如果表定义包含表字符集选项，则使用该字符集。
3. 否则，使用数据库字符集作为表默认字符集，这也成为列字符集。如果数据库从未明确分配过字符集（例如，它是在 MySQL 4.1 之前创建的），则数据库字符集取自服务器字符集。

换句话说，MySQL 会在可能指定字符集的各级别中向上搜索，直到找到已定义的字符集，然后将其用于该列。由于数据库始终具有默认字符集，因此即使在任何较低级别未明确指定字符集，搜索过程也保证会在数据库级别终止。

字符集名称 `binary` 是特殊的。如果你将 `binary` 字符集分配给非二进制字符串列，这等效于使用相应的二进制字符串类型定义该列。以下成对的列定义各显示了两个等效的定义：

```sql
c1 CHAR(10) CHARACTER SET binary
c1 BINARY(10)

c2 VARCHAR(10) CHARACTER SET binary
c2 VARBINARY(10)

c3 TEXT CHARACTER SET binary
c3 BLOB
```

如果你为二进制字符串列指定 **`CHARACTER SET`** *binary*，它将被忽略，因为类型已经是二进制的。如果你为 **ENUM** 或 **SET** 指定 **`CHARACTER SET`** *binary*，则按原样使用。

如果你将 **`binary`** 字符集作为表选项分配，则它应用于其自身定义中未指定任何字符集信息的每个字符串列。MySQL 提供了一些更短的属性来定义字符列：

- **`ASCII`** 属性是 **`CHARACTER SET`** *latin1* 的简写。
- **`UCS2`** 属性是 **`CHARACTER SET`** *ucs2* 的简写。
- 如果你为非二进制字符串列、**ENUM** 或 **SET** 使用 **`BINARY`** 属性，它是指定列字符集的二进制排序规则的简写。例如，假设表默认字符集为 *latin1*，这些定义是等效的：

```sql
c1 CHAR(10) BINARY
c2 CHAR(10) CHARACTER SET latin1 BINARY
c3 CHAR(10) CHARACTER SET latin1 COLLATE latin1_bin
```

如果你为二进制字符串列指定 **`BINARY`** 属性，它将被忽略，因为类型已经是二进制的。

通用属性 **`NULL`** 或 **`NOT NULL`** 可以为任何字符串类型指定。如果你未指定其中任何一个，**`NULL`** 是默认值。然而，将字符串列定义为 **`NOT NULL`** 并不能阻止你在列中存储空字符串（即 *''*）。在 MySQL 中，空值与缺失值不同，因此不要犯错误认为通过将其定义为 **`NOT NULL`** 就可以强制字符串列包含非空值。如果你要求字符串值非空，那是你必须在自己的应用程序中执行的约束。

除了 **`BLOB`** 和 **`TEXT`** 类型外，你还可以使用 **`DEFAULT`** 子句为所有字符串数据类型指定默认值。本章前面 3.2.3 节“指定列默认值”描述了当列定义不包含 **`DEFAULT`** 子句时，MySQL 用于分配默认值的规则。

## 3.2.5.6 选择字符串数据类型

当你为字符串列选择数据类型时，请考虑以下问题：

**值是以字符数据还是二进制数据表示？** 对于字符数据，非二进制字符串类型最为合适。对于二进制数据，请使用二进制字符串类型。

**你希望比较是否*区分大小写*？** 如果是，请使用非二进制字符串类型之一，因为它们存储字符并关联字符集和排序规则。

非二进制字符串值在比较和排序目的上的大小写敏感性由分配给它们的排序规则控制。如果你希望字符串值在比较时被视为相等而不考虑大小写，请使用不区分大小写的排序规则。否则，使用二进制或区分大小写的排序规则。二进制排序规则使用数值字符代码比较字符单元。区分大小写的排序规则使用特定的排序顺序比较字符单元，这与字符代码顺序不一定对应。在这两种情况下，给定字符的小写和大写版本在比较中被视为不同。假设 'mysql'、'MYSQL' 和 '?MySQL' 是 latin1 字符集中的字符串。如果使用 latin1_swedish_ci 等不区分大小写的排序规则进行比较，它们都被视为相同；但如果使用二进制 latin1_bin 排序规则或区分大小写的 latin1_general_cs 排序规则进行比较，则被视为三个不同的字符串。

如果你希望字符串列既用于区分大小写的比较，也用于不区分大小写的比较，请使用与你最常执行的比较类型相对应的排序规则。对于其他类型的比较，应用 COLLATE 运算符来更改排序规则。例如，如果 mysql 是使用 latin1 字符集的 CHAR 列，你可以为其分配 latin1_swedish_ci 排序规则以默认执行不区分大小写的比较。以下比较是不区分大小写的：

```sql
mysql = ‘ABC’
```

在需要区分大小写的比较时，使用 latin1_general_cs 或 latin1_bin 排序规则。以下比较是区分大小写的（将 COLLATE 运算符应用于左侧字符串还是右侧字符串无关紧要）：

```sql
mysql COLLATE latin1_general_cs = ‘ABC’
mysql COLLATE latin1_bin = ‘ABC’
mysql = ‘ABC’ COLLATE latin1_general_cs
mysql = ‘ABC’ COLLATE latin1_bin
```

你想最小化存储需求吗？如果是，请使用变长类型，而不是定长类型。

允许的列值是否始终从固定的合法值集中选择？如果是，ENUM 或 SET 可能是一个很好的选择。

如果你有一组有限的字符串值，并希望以某种非字典顺序进行排序，ENUM 也很有用。ENUM 值的排序是根据你在列定义中列出枚举值的顺序进行的，因此你可以使值按任意顺序排序。

尾部填充值是否重要？如果值必须按存储的方式准确检索，而在存储或检索期间不添加或删除尾部空格（或对于二进制数据类型为 0x00 字节），请使用 TEXT 或 VARCHAR 列用于非二进制字符串，使用 BLOB 或 VARBINARY 列用于二进制字符串。如果你存储压缩、哈希或加密值，并且编码方式可能导致尾部空格，那么这一因素也很重要。表 3.12 显示了各种字符串数据类型的存储和检索操作如何处理尾部填充。

从 MySQL 5.1.20 开始，你可以启用 PAD_CHAR_TO_FULL_LENGTH SQL 模式，使检索到的 CHAR 列值保留尾部空格。对于 MySQL 5.0.15 之前的 BINARY 列，较短的值在存储时用空格填充，在检索时去除尾部空格。

