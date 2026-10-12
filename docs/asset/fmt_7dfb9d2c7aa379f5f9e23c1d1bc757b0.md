
- `ON UPDATE` 允许您指定当父表行被更新时子表会发生什么。如果没有 `ON UPDATE` 子句，默认行为是拒绝子表中与父表索引中没有匹配项的任何插入或更新，并防止更新子行指向的父表索引值。可能的操作值与 `ON DELETE` 相同，并且具有相似的效果。

要建立外键关系，请遵循以下准则：

- 子表必须有一个索引，其中外键列作为其第一列列出。父表也必须有一个索引，其中 `REFERENCES` 子句中的列作为其第一列列出。（换句话说，外键关系两端的表中的键中的列必须被索引。）在定义外键关系之前，必须显式创建父表索引。如果 `CREATE TABLE` 语句不包含这样的索引，`InnoDB` 会自动在子表的外键列（引用列）上创建索引。这使得在某些情况下编写 `CREATE TABLE` 语句变得更加容易。但是，自动创建的索引将是非唯一索引，并且只包含外键列。如果您希望它是主键或唯一索引，或者除了外键中的列之外还应包含其他列，您应该显式地在子表中定义索引。

- 父表和子表索引中的相应列必须具有兼容的类型。例如，您不能用 `INT` 列与 `CHAR` 列匹配。相应的字符列必须具有相同的长度。相应的整数列必须具有相同的大小，并且都必须是有符号或无符号。

- 在外键关系中，您不能对字符串列的前缀建立索引。（也就是说，对于字符串列，您必须索引整个列，而不仅仅是其前缀。）

在第 1 章中，我们为成绩记录项目创建了具有简单外键关系的表。现在让我们通过一个更复杂的例子来演练。首先创建名为 `parent` 和 `child` 的表，使得 `child` 表包含一个引用 `parent` 表中 `par_id` 列的外键：

```sql
CREATE TABLE parent
(
  par_id   INT NOT NULL,
  PRIMARY KEY (par_id)
) ENGINE = INNODB;

CREATE TABLE child
(
  par_id    INT NOT NULL,
  child_id  INT NOT NULL,
  PRIMARY KEY (par_id, child_id),
  FOREIGN KEY (par_id) REFERENCES parent (par_id)
      ON DELETE CASCADE
      ON UPDATE CASCADE
) ENGINE = InnoDB;
```

在这种情况下，外键使用 `ON DELETE CASCADE` 来指定当从 `parent` 表中删除一行时，MySQL 还应自动移除具有匹配 `par_id` 值的 `child` 行。`ON UPDATE CASCADE` 表示如果父行 `par_id` 值更改，MySQL 还应将 `child` 表中任何匹配的 `par_id` 值更改为新值。

现在向 `parent` 表中插入几行，然后向 `child` 表中添加一些具有相关键值的行：

```sql
mysql> INSERT INTO parent (par_id) VALUES(1),(2),(3);
mysql> INSERT INTO child (par_id,child_id) VALUES(1,1),(1,2);
mysql> INSERT INTO child (par_id,child_id) VALUES(2,1),(2,2),(2,3);
mysql> INSERT INTO child (par_id,child_id) VALUES(3,1);
```

这些语句导致以下内容表格，其中 `child` 表中的每个 `par_id` 值都匹配 `parent` 表中的 `par_id` 值：

| par_id |

|:-------:|

|   1    |

|   2    |

|   3    |

| par_id | child_id |

|:------:|:--------:|

|   1    |    1     |

|   1    |    2     |

|   2    |    1     |

|   2    |    2     |

|   2    |    3     |

|   3    |    1     |

要验证 `InnoDB` 是否强制执行插入时的键关系，请尝试向 `child` 表中添加一行，其 `par_id` 值在 `parent` 表中不存在：

```sql
mysql> INSERT INTO child (par_id,child_id) VALUES(4,1);
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`sampdb`.`child`, CONSTRAINT `child_ibfk_1` FOREIGN KEY (`par_id`) REFERENCES `parent` (`par_id`) ON DELETE CASCADE ON UPDATE CASCADE)
```

要测试级联删除，看看当你删除一个父行时发生什么：

```sql
mysql> DELETE FROM parent WHERE par_id = 1;
```

MySQL 从父表中删除该行：

| par_id |

|:------:|

|   2    |

|   3    |

此外，它将 `DELETE` 语句的影响级联到子表：

| par_id | child_id |

|:------:|:--------:|

|   2    |    1     |

|   2    |    2     |

|   2    |    3     |

|   3    |    1     |

要测试级联更新，看看当你更新一个父行时发生什么：

```sql
mysql> UPDATE parent SET par_id = 100 WHERE par_id =2;
mysql> SELECT * FROM parent;
```

| par_id |

|:------:|

|   3    |

|  100   |

```sql
mysql> SELECT * FROM child;
```

| par_id | child_id |

|:------:|:--------:|

|   3    |    1     |

|  100   |    1     |

|  100   |    2     |

|  100   |    3     |

## 2.14 外键与引用完整性

前面的示例展示了如何安排父行的删除或更新操作，以便级联删除或更新相应的子行。`ON DELETE` 和 `ON UPDATE` 子句允许执行其他操作。例如，一种可能的做法是让子行保留在表中，但将其外键列设置为 `NULL`。为了做到这一点，需要对子表的定义进行几处修改：

- 使用 `ON DELETE SET NULL` 而不是 `ON DELETE CASCADE`。这指示 `InnoDB` 将外键列（`par_id`）设置为 `NULL`，而不是删除行。

- 使用 `ON UPDATE SET NULL` 而不是 `ON UPDATE CASCADE`。这指示 `InnoDB` 在匹配的父行被更新时，将外键列（`par_id`）设置为 `NULL`。

- `child` 表的原定义将 `par_id` 定义为 `NOT NULL`。这与 `ON DELETE SET NULL` 或 `ON UPDATE SET NULL` 不兼容，因此必须修改列定义以允许 `NULL`。

- `child` 表的原定义还将 `par_id` 定义为 `PRIMARY KEY` 的一部分。然而，主键不能包含 `NULL` 值。因此，将 `par_id` 改为允许 `NULL` 还要求将 `PRIMARY KEY` 更改为 `UNIQUE` 索引。`UNIQUE` 索引强制执行唯一性，但 `NULL` 值除外，`NULL` 值可以在索引中出现多次。

要查看这些更改的效果，请使用原始定义重新创建父表，并加载相同的初始行。然后使用此处所示的新定义创建子表：

```sql
CREATE TABLE child
(
  par_id INT NULL,
  child_id INT NOT NULL,
  UNIQUE (par_id, child_id),
  FOREIGN KEY (par_id) REFERENCES parent (par_id)
  ON DELETE SET NULL
  ON UPDATE SET NULL
) ENGINE = InnoDB;
```

就插入新行而言，子表的行为与原始定义相似。也就是说，它允许插入在父表中找到的 `par_id` 值的行，但不允许输入未在该表中列出的值：
