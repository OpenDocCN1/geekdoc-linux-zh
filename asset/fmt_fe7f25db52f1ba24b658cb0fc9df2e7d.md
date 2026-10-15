
### 插入示例

```
1 mysql> INSERT INTO teams
      -> SET name='Fremont Tigers',
      -> wins=24,
      -> losses=26;
  Query OK, 1 row affected (0.00 sec)

2 mysql> INSERT INTO teams
      -> SET name='Chico Hardhats',
      -> wins=19,
      -> losses=25;
  Query OK, 1 row affected (0.00 sec)

3 mysql> INSERT INTO teams VALUES
      -> ('Bath Warships',32,3);
  Query OK, 1 row affected (0.00 sec)

4 mysql> INSERT INTO teams VALUES
      -> ('Bangor Rams', 22, 24);
  Query OK, 1 row affected (0.00 sec)

5 mysql> SELECT name FROM teams;
  +---------------------+
  | name                |
  +---------------------+
  | Fremont Tigers      |
  | Chico Hardhats      |
  | Bath Warships       |
  | Bangor Rams         |
  +---------------------+
  4 rows in set (0.00 sec)

mysql> INSERT INTO coaches VALUES
      -> ('', 'John Doe', 'Chico Hardhats', 'Head Coach', 20021210);
  Query OK, 1 row affected, 1 warning (0.05 sec)

6 mysql> INSERT INTO coaches VALUES
      -> ('', 'Jack Mattson', 'Chico Hardhats', 'Offensive Coach',
      '20041005');
  Query OK, 1 row affected, 1 warning (0.00 sec)

7 mysql> INSERT INTO coaches(name, team, title, start_date)
      -> VALUES ('Bud Wilkins','Fremont Tigers', 'Head Coach',
      '19990906');
  Query OK, 1 row affected (0.03 sec)

8 mysql> INSERT INTO coaches(name, team, title, start_date)
      -> VALUES ('Joe Hayes', 'Fremont Tigers', 'Defensive Coach',
      '19980616');
  Query OK, 1 row affected (0.02 sec)
```

### 解释

- 1. 使用 `INSERT` 语句中的 `SET` 子句为字段和值进行赋值。对于 `SET` 子句中未指定的任何字段，MySQL 会将其赋值为默认值。
- 2. 再次使用 `SET` 子句插入字段和值。
- 3. 在这个示例中，`INSERT` 语句包含一个 `VALUES` 列表，其中每个字段的值按照创建表时指定的顺序进行赋值。如果不确定顺序，请使用前一个示例中所示的 `DESCRIBE` 语句来查看顺序。
- 4. 在本示例中，为新的记录重复使用了 `VALUES` 列表。注意，日期是以 `yyyy-mm-dd` 格式插入的。
- 5. `SELECT` 语句显示了已插入到表中的所有团队名称。
- 6-9. 使用 `VALUES` 列表插入了更多记录。

## 从表中选择数据——`SELECT` 命令

`SELECT` 是最常用的 SQL 命令之一，执行查询时必不可少。`SELECT` 命令用于根据某些条件从表中检索数据。它指定了要检索的逗号分隔的字段列表，`FROM` 子句则指定要访问的表。结果存储在一个称为结果集的结果表中，这本身也是一个小型表格。`*` 符号可用于表示所有字段。

### 按列选择

在以下示例中，检索特定列的数据，每列（字段）由逗号分隔。

### 示例 15.10

```sql
1 mysql> SELECT name FROM teams;

| name |
| Fremont Tigers |
| Chico Hardhats |
| Bath Warships |
| Bangor Rams |
4 rows in set (0.00 sec)

2 mysql> SELECT name, wins FROM teams;

| name | wins |
| Bangor Rams | 22 |
| Bath Warships | 32 |
| Fremont Tigers | 24 |
| Chico Hardhats | 19 |
4 rows in set (0.00 sec)
```

![](img/8556abcb353c0991f12099420ec28735_576_0.png)

```sql
3 mysql> SELECT id, name, title FROM coaches;

| id | name            | title          |
+----+-----------------+------------------+
|  1 | John Doe        | Head Coach       |
|  2 | Jack Mattison   | Offensive Coach  |
|  3 | Bud Wilkins     | Head Coach       |
|  4 | Joe Haynes      | Defensive Coach  |
+----+-----------------+------------------+
4 rows in set (0.00 sec)
```

![](img/8556abcb353c0991f12099420ec28735_576_1.png)

- 1. `SELECT` 语句从 `teams` 表中检索 `name` 字段中的所有值。
- 2. `SELECT` 语句从名为 `teams` 的表中检索 `name` 字段和 `wins` 字段中的所有值。字段名称列表用逗号分隔。
- 3. `SELECT` 语句从 `coaches` 表中检索 `id` 字段、`name` 字段和 `title` 字段中的所有值。

**选择所有列。** `*` 是一个通配符，用于表示表中的所有列。

![](img/8556abcb353c0991f12099420ec28735_576_2.png)

```sql
1 mysql> SELECT * FROM teams;

| name            | wins | losses |
+-----------------+------+--------+
| Fremont Tigers  |  24  |   26   |
| Chico Hardhats  |  19  |   25   |
| Bath Warships   |  32  |    3   |
| Bangor Rams     |  22  |   24   |
+-----------------+------+--------+

2 mysql> SELECT * FROM coaches;

| id | name        | team          | title            | start_date |
+----+-------------+---------------+------------------+------------+
|  1 | John Doe    | Chico Hardhats| Head Coach       | 2002-12-10 |
|  2 | Jack Mattison| Chico Hardhats| Off. Coach      | 2004-10-05 |
|  3 | Bud Wilkins | Fremont Tigers| Head Coach       | 1999-09-06 |
|  4 | Joe Haynes  | Fremont Tigers| Def. Coach      | 1998-06-16 |
+----+-------------+---------------+------------------+------------+
4 rows in set (0.00 sec)
```
