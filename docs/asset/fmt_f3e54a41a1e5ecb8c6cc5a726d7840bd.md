
当某些数据被输入到表中后，你在命令行执行的任何查询的输出将以表格格式返回，并附带处理查询所花费的时间。如果列对于你的屏幕来说太宽，它们会换行而不是截断；这可能导致显示混乱。有选择性地查询字段有助于保持输出的可读性。

以下示例显示几个多行 `INSERT` 查询，用于填充 `Users` 表，随后是一个经过精心限制的 `SELECT` 查询的表格输出：

```
mysql> INSERT INTO Users (ID,FullName,Email,Age)
   -> VALUES (1,"Joe Smith","jsmith@somewhere.com",22);
mysql> INSERT INTO Users (ID,FullName,Email,Age)
   -> VALUES (2,"Alice Walker","awalker@elsewhere.com",31);
mysql> SELECT ID,FullName,Email,Age FROM Users;
+----+----------+-----------------------+----+
| ID | FullName | Email                 | Age |
+----+----------+-----------------------+----+
|  1 | Joe Smith  | jsmith@somewhere.com | 22 |
|  2 | Alice Walker | awalker@elsewhere.com | 31 |
+----+----------+-----------------------+----+
2 rows in set (0.00 sec)
```

## 索引和键

你现在已经有了可用于活动查询的工作表。但是，设置一个完整的数据库并不像那样简单。在设计你的表时需要考虑的另一个事项是如何索引。索引决定了数据库内数据的排序，这就是数据库能如此快速的原因。想想在字典中查找单词；如果你在找单词 `sleep`，但不知道什么是“字母顺序”，你实际上可能花几周时间线性地搜索字典才能找到它。但既然你知道字母 `S` 在字母表中的位置，你就知道如何直接锁定该单词并快速找到它。

计算机也是如此。如果没有索引方案来查找某项数据，它们只能对数据存储进行线性搜索——虽然它们可以做得比我们快，但在大多数高性能数据库场景中，仍然是一个不可接受的缓慢解决方案。因此，我们必须创建适当的索引（对于计算机而言，类似于我们的字母顺序概念）和键（例如 `sleep` 的首字母），以帮助数据库在数据中找到路径。

所有实体数据表（那些在 E-R 图中用矩形表示的表）都应该有一个主键。这是一个专门指定为表中数据应自动索引其值的列。该列中的值应指定为 `NOT NULL`（换句话说，它们不能具有 `NULL` 值——对于数值数据类型，空白输入值将变为 `0`，对于文本类型，则变为空字符串）。主键列中的所有值还必须是唯一的。

这听起来就像是为我们表中的整数 `ID` 列量身定制的角色。实际上，创建表的最佳实践通常要求每个表的第一个列是一个数值 `ID`，它是主键，并且指定了 `AUTO_INCREMENT` 属性。这使得该列以一种特殊的方式工作：如果你向具有 `AUTO_INCREMENT` 列（这也必须是主键）的表中插入行，你可以简单地将该列的值留空或设为 `NULL`，数据库将自动为每个新行填入下一个未使用的整数（列中的最高数值加一）。这对本章的目的是完美的：你将为放入表中的每个条目获得一个新的唯一 `ID` 号，甚至不需要自己计算它。

通常，你会在创建表时指定这些属性：

```sql
CREATE TABLE Users (ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
  Fullname VARCHAR(64), Email VARCHAR(32), Age INT);
```

然而，由于在这种情况下你的表已经创建，你可以使用 `ALTER TABLE` 命令将 `ID` 列更改为你想要的样子：

```sql
ALTER TABLE Users CHANGE ID ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT;
```

### 注意

`PostgreSQL` 没有 `AUTO_INCREMENT`；相反，它有一种称为 `SERIAL` 的特殊数据类型。`SERIAL` 数据类型不受与 `AUTO_INCREMENT` 相同的键限制，但行为非常相似。使用 `SERIAL` 代替 `INT` 来创建自动递增的 `ID` 字段。

请注意，在 `PostgreSQL` 中，如果你在 `INSERT` 操作中为 `ID` 字段指定 `NULL`（而不是 `0`），将输入 `NULL` 而不是下一个可用的整数（后者是你如果不提供该字段值时会得到的）。在 `PostgreSQL` 中，`NULL` 优先于 `SERIAL` 属性。相比之下，`MySQL` 的 `AUTO_INCREMENT` 在对这种字段的任何 `NULL` 或 `0` 条目时都会被调用。

你可以在创建表时，通过在变量名后使用 `KEY` 属性来指定表中其他列的其他键，或使用 `ALTER TABLE` 命令。发出此命令会在你指定的每个键上创建索引。你还可以基于多个列创建索引。当两个列的组合在一起是有用唯一时，这种方法很有用。你可以像这样基于多个列创建索引：

```sql
ALTER TABLE Users ADD INDEX (Email,FullName);
```

这段代码将导致在 `describe Users` 输出的 `Key` 列中出现一个 `MUL` 标记（代表“multiple”，意味着表有多个索引）。

尝试预测哪些表会被频繁访问以及哪些表将包含大量数据非常重要。正确地索引这些表，键设置为那些表最常搜索的列，可能会带来令人难以置信的性能提升。

## 维护安全性

以 `root` 身份访问你的数据库并不是特别好的主意。你很可能会希望启用其他用户——普通用户——来访问你系统上的某些数据库；当将数据库连接到 Web 时尤其如此。每个数据库都有访问权限，可以分配给不同主机上的个人用户，而正确配置的数据库系统会谨慎但完全地分配这些权限。

假设你的 `PictureArchive` 数据库需要允许本地系统的用户 `frank` 访问。`frank` 需要能够创建表、向表中添加数据、从表中选择和删除数据、更新表以及删除表。（创建和删除表的能力对于他处理临时表是必需的。）你可以使用 `MySQL` 中的 `GRANT` 命令授予 `frank` 这些权限：

```sql
GRANT CREATE, SELECT, INSERT, UPDATE, DELETE, DROP ON PictureArchive.*
TO frank@localhost IDENTIFIED BY '<password>' WITH GRANT OPTION;
```

如果你想更宽松一些，可以使用 `GRANT ALL PRIVILEGES` 代替明确列出的权限。你也可以授予 `PictureArchive` 内特定表的权限（输入这些表的名称而不是星号，星号意味着“所有表”），或者你可以通过在 `PictureArchive.*` 的位置输入 `*.*` 来授予所有数据库中所有表的权限。将 `<password>` 替换为 `frank` 希望使用的密码；将其作为 `IDENTIFIED BY` 的参数放入单引号中会哈希密码并以加密格式放入系统。最后，可选的 `WITH GRANT OPTION` 赋予 `frank` 自己向其他用户授予权限的能力。

`PostgreSQL` 中类似的功能是 `createuser` 工具，它在常规系统命令行中以交互方式提供相同的选项，如下所示：

```bash
# su -l psql
$ createuser -P
Enter name of user to add: frank
Enter password for user 'frank':
Enter it again:
Shall the new user be allowed to create databases? (y/n) y
Shall the new user be allowed to create more new users? (y/n) y
CREATE USER
```

为了提供数据库的用户级安全性，你可能需要编辑 `/usr/local/pgsql/pg_hba.conf` 并取消注释以下示例行（并注释掉当前活动的配置行）：

```
# TYPE      DATABASE   IP_ADDRESS     MASK     AUTH_TYPE  AUTH_ARGUMENT
local       sameuser                  md5
local       all                       md5    admins
```
