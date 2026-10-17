
### INSERT 语句

```sql
INSERT INTO tableName (columnName, columnName2, ..., columnNameN)
VALUES (value1, value2, ..., valueN)
```

其中 `tableName` 是要插入行的表。`tableName` 后面跟着逗号分隔的列名列表，后面跟着关键字 `VALUES` 和逗号分隔的值列表。

- SQL 使用单引号 (`''`) 作为字符串的分隔符。要在 SQL 中指定包含单引号的字符串，必须用另一个单引号对其进行转义。

## 25.4.6 UPDATE 语句

- `UPDATE` 语句修改表中的数据。`UPDATE` 语句的基本形式是：

```sql
UPDATE tableName
SET columnName1 = value1, columnName2 = value2, ..., columnName = valueN
WHERE
```

其中 `tableName` 是更新数据的表。`tableName` 后面跟着关键字 `SET` 和逗号分隔的键值对（格式为 `columnName = value`）。可选的 `WHERE` 决定更新哪些行。

## 25.4.7 DELETE 语句

- `DELETE` 语句从表中删除行。`DELETE` 语句简单的形式是：

```sql
DELETE FROM tableName criteria
```
