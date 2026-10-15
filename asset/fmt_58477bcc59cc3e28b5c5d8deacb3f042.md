
`title_id_number` 列提供了标题的唯一标识。`AUTO_INCREMENT` 关键字用于 MySQL 在插入记录时自动为该列分配唯一值。

`title` 和 `author` 列提供了书籍标题和作者。

`isbn`、`loc_number` 和 `ddn_number` 提供书籍的 ISBN 号、美国国图书馆分类号和杜威分类号。大多数书籍没有这三个号码；旧书将没有 ISBN 号。由于这个原因，我们允许这些字段为 NULL。

`adult_flag` 标记该标题是否为成人。未成年人不能购买成人书籍。

`publisher`、`city`、`year` 和 `price` 列提供了书籍出版的信息。我们允许这些字段为 NULL，因为它们可能未知，而且它们对于识别标题至关重要。

此表有一个主键 `title_id_number`。它没有引用任何其他表，因此没有外键。

`copy` 表描述书籍的副本：

```sql
CREATE TABLE copy (
  title_id_number INTEGER NOT NULL,
  copy_number INTEGER NOT NULL,
  branch_code CHAR(5) NOT NULL,
  PRIMARY KEY (title_id_number, copy_number),
  FOREIGN KEY (title_id_number) REFERENCES title,
  FOREIGN KEY (branch_code) REFERENCES branch
);
```

`title_id_number` 列给出了 `title` 表设置的标题键。

`copy_number` 列提供了书籍副本的编号。

`branch_code` 列提供了“拥有”该副本的分馆名称。

`title_id_number` 和 `branch_name` 列被声明为外键，因为它们都引用了另一个表中的某个列。如你所见，一个列可以在多个表中使用——`title_id_number` 既是外键，也是此表主键的一部分。

## 所有者

两个实体可以拥有一本书：一个用户和一个图书馆分馆。

图书馆分馆在一个表中进行描述。用户在两个张表中描述：其中一张表描述用户本人，而其他表描述用户用于借阅书籍的借卡。

`branch` 表描述了我们图书馆的一个分馆：

```sql
CREATE TABLE branch (
    branch_code CHAR(5) NOT NULL,
    branch_name VARCHAR(64) NOT NULL,
    street VARCHAR(64) NOT NULL,
    city VARCHAR(32) NOT NULL,
    state CHAR(2) NOT NULL,
    zip CHAR(5) NOT NULL,
    area_code CHAR(3) NOT NULL,
    phone CHAR(7) NOT NULL,
    PRIMARY KEY (branch_code)
);
```

`branch_code` 列提供了一个简短的助记代码，用于唯一标识分馆图书馆。这是一个主键，其他表使用该字段作为外键将自身连接到此表。

`name` 列提供分馆名称。每个分馆必须有唯一的名称。由于分馆只有寥几个，这并不难实现。

`city`、`street`、`state` 和 `zip` 列提供了分馆的地址。

`area_code` 和 `phone` 列提供了分馆的电话号码。大多数分馆都有多个电话分机，但所有分馆都只有一个主号码。

在上一节中拆解“地址”概念时，我们讨论了地址本身就是一个实体，可以拆分到自己的表中。然而，地址与拥有该地址的实体（用户或分馆）之间存在一一一的关系；因此，我们认为将地址拆分到单独的表中——并建立它们的关联机制、维护两个表之间的完整性等——其投入的精力远大于其价值。因此，我们直接将分馆的地址嵌入到其表中。电话号码也是如此。

`branch_code` 列是主键。因为此表没有引用任何其他表，所以它没有外键。

`user` 表描述了图书馆的用户，即拥有借书权限的人。

```sql
CREATE TABLE user (
  first_name VARCHAR(32) NOT NULL,
  middle_init CHAR(1) NULL,
  last_name VARCHAR(32) NOT NULL,
  birthdate DATE NOT NULL,
  ssn CHAR(9) NOT NULL,
  street VARCHAR(32) NOT NULL,
  unit VARCHAR(32) NOT NULL,
  state CHAR(2) NOT NULL,
  zip CHAR(5) NOT NULL,
  area_code CHAR(3) NOT NULL,
  phone CHAR(7) NOT NULL,
  status CHAR(1) NOT NULL,
  PRIMARY KEY (ssn)
);
```

`first_name`、`middle_init` 和 `last_name` 分别提供用户的名、中间名字母和姓。注意 `middle_init` 可以为 `NULL`，因为有些人人没有中间名。

`birthdate` 列提供用户的出生日期。我们的系统将使用此日期来计算用户是否为成年人。

`ssn` 列提供用户的社会安全号码。

`street`、`unit`、`city`、`state` 和 `zip` 列提供用户的地址——分别是街道和名称（或公寓号）、城市、州和邮政编码。`unit` 列可以为 `NULL`，因为有些用户住在没有单元号的单独住宅中。

`area_code` 和 `phone` 列提供用户的电话号码。

`status` 列标记用户的状态——用户是活跃还是非活跃。用户可能因为各种原因变得非活跃：用户可能离开了我们的社区；用户可能去世了；或者用户可能有未付罚款或逾期已久的书籍。我们为此应用程序编写的“中间件”将涵盖设置和取消用户状态。

`ssn` 列是此表的唯一主键。因为美国每个年满一岁的人必须有社会安全号码，而且社会安全号码对每个人来说都是唯一的（至少在理论上如此）。

此表没有引用任何其他表，所以它没有外键。

## 第 4 节：数据库设计

从我们的地址和电话号码列可以看出，我们为所有存储相同类型信息的列赋予了相同的名称。例如，`user` 表和 `branch` 表都有一列提供邮政编码的列；在每个实例中，我们将该列命名为 `zip`。虽然这不是强制要求的，但给相同的列赋予相同的名称是一个经验法则，这将使你的数据库代码编写和查询变得简单得多。

`card` 表标识一张图书馆卡。一个用户在光顾我们图书馆的多年可能会拥有很多借卡；此后，卡会磨损、经过洗涤、丢失或被盗。我们在记录用户信息之外，还记录关于卡的信息，因为我们想确保假卡不在流通中，并确保每个用户在任何时候只有一张活跃卡。

```sql
CREATE TABLE card (
  card_id_number INTEGER NOT NULL AUTO_INCREMENT,
  sn CHAR(9) NOT NULL,
  date_issued DATE NOT NULL,
  status CHAR(1) NOT NULL,
  PRIMARY KEY (card_id_number),
  FOREIGN KEY (sn) REFERENCES user
);
```

`card_id_number` 列提供图书馆卡的唯一标识。此列是主键。

`sn` 列提供发放该卡的用户的社会安全号码。此列是引用 `user` 表的外键。

`date_issued` 列提供卡发放给用户的日期。此列将指示卡是否处于活跃状态。

`status` 列提供卡的状态：是否在使用中、丢失或被盗。非活跃的卡无法借书。

### 占有行为

占有行为发生在书籍离开一个实体（图书馆或用户）并进入另一个实体占有范围时。有此类行为：

- 用户从图书馆借书。
- 用户向图书馆还书。
- 书籍在图书馆之间转移。

借书和还书是同一事件的两个部分，因此我们用一个表记录两者：

```sql
CREATE TABLE borrow (
  card_id INTEGER NOT NULL,
  title_id INTEGER NOT NULL,
  copy_number INTEGER NOT NULL,
  borrow_date DATE NOT NULL,
  return_date DATE,
  PRIMARY KEY (card_id, title_id, copy_number, borrow_date),
  FOREIGN KEY (card_id) REFERENCES card,
  FOREIGN KEY (title_id, copy_number) REFERENCES copy
);
```

`card_id` 列提供借书用卡的唯一标识。此列是引用 `card` 表的外键。

`title_id` 和 `copy_number` 列标识被借的书籍。它们构成引用 `copy` 表中对应列的外键。
