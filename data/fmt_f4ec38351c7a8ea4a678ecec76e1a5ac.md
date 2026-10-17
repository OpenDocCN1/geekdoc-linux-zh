
为什么在 `student_id` 上建有索引？原因是，对于 `FOREIGN KEY` 定义中的任意列，都应当为其建立索引，或者它们应当是多列索引中列出的第一列。对于 `event_id` 上的 `FOREIGN KEY`，该列在 `PRIMARY KEY` 中排在第一位。而对于 `student_id` 上的 `FOREIGN KEY`，由于 `student_id` 并非排在主键的第一位，因此无法使用 `PRIMARY KEY` 作为索引。所以，我们改为单独在 `student_id` 上创建一个索引。

`InnoDB` 实际上会为外键定义中的列创建索引，但它可能不会使用与你相同定义的索引（关于此问题的进一步讨论见 2.14.1 节，“创建和使用外键”）。显式地定义索引可以避免这一问题。

用于记录缺勤情况的 `absence` 表如下所示：

```
CREATE TABLE absence (
student_id INT UNSIGNED NOT NULL,
date       DATE NOT NULL,
PRIMARY KEY (student_id, date),
FOREIGN KEY (student_id) REFERENCES student (student_id)
) ENGINE = InnoDB;
```

将该语句输入 `mysql`，或执行以下命令：

```
% mysql sampdb < create_absence.sql
```

`student_id` 和 `date` 列均被定义为 `NOT NULL`，以禁止出现缺失值。我们将这两列的组合设为主键，以防止意外创建重复的行。同一天将一名学生计算为缺勤两次显然不公平，对吧？

`absence` 表还包含一个外键关系，该关系定义为确保每个 `student_id` 值都与 `student` 表中的某个 `student_id` 值相匹配。

在成绩记录表中包含外键关系，旨在在数据录入时强制执行约束：我们只希望插入包含合法的事件 ID 和学生 ID 值的行。然而，外键关系还有另一个效果。它们建立了依赖性，限制了创建和删除表的顺序：

- `score` 表引用了 `grade_event` 和 `student` 表，因此在创建 `score` 表之前，必须先创建这两个表。同样，`absence` 表引用了 `student` 表，因此在创建 `absence` 表之前，`student` 表必须已经存在。
- 如果你要删除（移除）表，则情况相反。如果尚未先删除 `score` 表，你就无法删除 `grade_event` 表；除非先删除 `score` 和 `absence` 表，否则 `student` 表也无法被删除。

> **注意**
>
> 如果你的 `MySQL` 服务器由于某种原因不支持 `InnoDB`，你可以改为使用 `MyISAM` 表来创建这些成绩记录项目表。在每个 `CREATE TABLE` 语句中，将 `InnoDB` 替换为 `MyISAM`，或者直接省略 `ENGINE` 子句。但是，如果你使用 `MyISAM` 表，那么本书后续利用这些表来演示外键操作的那些示例将无法正常工作。

### 1.4.7 添加新行

至此，我们的数据库及其表已经创建完毕。现在我们需要往表中插入一些行。不过，在向表中放入数据后，知道如何检查表的内容是有用的。因此，尽管直到 1.4.9 节“检索信息”才会详细讲解检索操作，你至少应该知道，以下语句可以显示任意表 `tbl_name` 的完整内容：

```
SELECT * FROM tbl_name;
```

#### 示例：

```
mysql> SELECT * FROM student;
Empty set (0.00 sec)
```

目前，`mysql` 显示该表为空，但在尝试本节中的示例后，你会看到不同的结果。

向数据库添加数据有几种方法。你可以通过发出 `INSERT` 语句手动向表中插入行。你也可以通过从文件读取来添加行，形式可以是预写好的 `INSERT` 语句供 `mysql` 使用，或者是使用 `LOAD DATA` 语句或 `mysqlimport` 客户端程序加载的原始数据值。

本节将演示每种向表中插入行的方法。你应该做的是尝试所有这些方法，以熟悉它们并了解它们的工作原理。在尝试了每种方法之后，请前往 1.4.8 节“将示例数据库重置为已知状态”，并执行那里提供的命令。这些命令会删除表、重新创建表，并加载一组已知数据。通过执行它们，你将确保表中包含的行的内容与我撰写后续章节时所使用的一致，从而获得那些章节中展示的相同结果。（如果你已经知道如何插入行，并且只想填充表，你可以直接跳到那一节。）

#### 1.4.7.1 使用 INSERT 添加行

让我们从使用 `INSERT` 开始添加行。`INSERT` 是一种 SQL 语句，你通过它指定要插入数据行的目标表以及要放入该行的值。`INSERT` 语句有几种形式。

**你可以为所有列指定值。** 语法如下：

```
INSERT INTO tbl_name VALUES(value1,value2,...);
```

示例：

```
mysql> INSERT INTO student VALUES('Kyle','W',NULL);
mysql> INSERT INTO grade_event VALUES('2008-09-03','Q',NULL);
```

使用此语法，`VALUES` 列表必须包含表中每一列的一个值，且顺序需与列在表中存储的顺序一致。（通常，这与 `CREATE TABLE` 语句中指定列的顺序一致。）如果你不确定列的顺序，请发出 `DESCRIBE tbl_name` 语句以查明。

在 `MySQL` 中，可以使用单引号或双引号来引用字符串和日期值，但单引号更为标准。`NULL` 值用于 `student` 和 `grade_event` 表中的 `AUTO_INCREMENT` 列。向 `AUTO_INCREMENT` 列插入“缺失值”会促使 `MySQL` 为该列生成下一个序列号。

`MySQL` 允许通过指定多个值列表，在单个 `INSERT` 语句中向表插入多行：

```
INSERT INTO tbl_name VALUES(...), (...), ... ;
```

## 1.4 MySQL 教程

示例：

```
mysql> INSERT INTO student VALUES('Avery','F',NULL),('Nathan','M',NULL);
```

这与多条 `INSERT` 语句相比，需要更少的输入，并且对服务器执行来说效率更高。请注意，括号包围了*每一*行的列值集合。以下语句是不合法的，因为它在括号内没有包含正确数量的值：

```
mysql> INSERT INTO student VALUES('Avery','F',NULL,'Nathan','M',NULL);
ERROR 1136 (21S01): Column count doesn't match value count at row 1
```

你可以指定想要赋值的列名，然后列出这些值。这在你想要创建一条记录，而该记录中只有少数列需要初始设置时非常有用。

```
INSERT INTO tbl_name (col_name1,col_name2,...) VALUES(value1,value2,...);
```

示例：

```
mysql> INSERT INTO member (last_name,first_name) VALUES('Stein','Waldo');
```

这种 `INSERT` 形式也允许多个值列表：

```
mysql> INSERT INTO student (name,sex) VALUES('Abby','F'),('Joseph','M');
```

对于未在列列表中指定的任何列，`MySQL` 都会为其分配默认值。例如，前面的语句中都没有包含 `member_id` 或 `student_id` 列的值，因此 `MySQL` 会为它们分配默认值 `NULL`。由于 `member_id` 和 `student_id` 是 `AUTO_INCREMENT` 列，所以在每种情况下的净效果都是生成并分配下一个序列号，就好像你显式分配了 `NULL` 一样。

你可以提供一系列 `列=值` 赋值。这种语法使用包含 `col_name=value` 赋值的 `SET` 子句，而不是 `VALUES` () 列表：

```
INSERT INTO tbl_name SET col_name1=value1, col_name2=value2, ...;
```

示例：

```
mysql> INSERT INTO member SET last_name='Stein',first_name='Waldo';
```

对于未在 `SET` 子句中指定的任何列，`MySQL` 都会为其分配默认值。这种形式的 `INSERT` 无法用于通过单条语句插入多行。
