
# 第 4 章

make_name: 丰田
model_name: R32
color: 反射银
modelyear: 2004
price: NULL
description: R32 限量版；低里程；低调且 surprisingly 实用；配置丰富。
NULL: 1
1: 1

make_name: 丰田
model_name: Tacoma
color: 红色
modelyear: 1993
price: NULL
description: 运行尚可；四驱；深色车窗，售后音响；需要稍加维护。
NULL: 0
1: 0

你首先会注意到，结果看起来与你之前的结果略有不同。这是因为查询末尾使用了 `\G` 终止符，它使 MySQL 以垂直方式显示结果（否则表格对于本书来说会太宽）。除此之外，所有信息都完整无缺。在 *New_Vehicles* 表中，针对缺失的“certified”列指定的 **NULL** 值存在，由于所有新车都有保修，你指定的占位符值 1 也存在。你将更改发送给客户端，他们对此感到满意（至少暂时如此）。

## 全文搜索

到目前为止，车场老板们已经对你能够精确查询他们所需信息、提供各种列表以提高销售人员生产力的能力印象深刻——但他们仍然想要更多。他们现在想要一种通过关键字搜索汽车库存的方法。他们的搜索需求并不复杂，但在 **WHERE** 子句中进行简单的 **LIKE** 比较是无法完成这项任务的。

你需要的功能恰好内置于 **MySQL** 中——全文搜索。全文搜索在 **MySQL** 中默认启用，允许你对指定的任何文本列执行自然语言搜索。不过，你不能随意开始进行全文搜索——你必须先做一些准备工作。

### 启用全文搜索

在 **MySQL** 中启用全文搜索只需简单地创建表列上的索引。你可以用两种方式做到这一点：在创建表时，作为 **CREATE TABLE** 命令的一部分；或者在表的生命周期后期。

#### 创建启用全文搜索的新表

你要创建的第一个全文索引将成为一个全新表的一部分。要在创建表时指定全文索引，你只需在列定义的末尾指定全文索引和要索引的列列表：

```
CREATE TABLE tablename (column\_specs, FULLTEXT (columns\_to\_index) )
```

你可以在 **FULLTEXT** 列列表中指定单列，或以逗号分隔的列表指定多列。现在是时候在 `VehicleInventory` 数据库中实际创建一个启用全文搜索的表了：

```
CREATE TABLE testft (testint int, testvc varchar(50), testtxt text, FULLTEXT (testvc, testtxt) );
```

你刚刚创建了一个新表，在 **testvc** 和 **testtxt** 列上建立了全文索引。

### 修改现有表以支持全文搜索

修改现有表以支持全文搜索稍微麻烦一些，但也不算太复杂。要为现有表添加全文搜索功能，你使用 MySQL 的 **ALTER TABLE** 命令，如下所示：

```
ALTER TABLE tablename ADD FULLTEXT (columns)
```

现在为 `New_Vehicles` 表添加全文索引：

```
ALTER TABLE New_Vehicles ADD FULLTEXT (description);
```

完成后，是时候充分利用这些索引了。

### 使用全文搜索进行查询

在启用了全文索引的 MySQL 表中进行搜索是一个相对轻松的过程。你只需在 **WHERE** 子句中使用 **MATCH()** 函数，如下所示：

```
SELECT [columns] FROM [table] WHERE MATCH ([indexed_columns]) AGAINST ('keyword')
```

在 **MATCH** 的参数列表中，你可以指定任意数量的列，只要它们是全文索引的一部分即可。

回到车辆库存数据库，是时候对新车辆列表执行搜索了。要搜索单词“options”（选项），你可以使用以下内容：

```
SELECT vehicle_id, description FROM New_Vehicles WHERE MATCH (description) AGAINST ('options');
```

应该返回以下内容：

| vehicle_id | description |
|:---:|:---|
| 2 | Last of the 2004 stock! Must sell!! Loaded, all options! |
| 3 | Come drive this popular truck! 4WD, extended cab, many options. |

全文搜索的另一个巧妙之处在于它可以按相关性对条目进行排序，并返回相关性分数。要利用相关性数据，你可以在 **SELECT** 列表和 **ORDER BY** 子句中使用 **MATCH() . . . AGAINST()** 函数，如下所示：

```
SELECT MATCH (description) AGAINST('options') AS relevance, description FROM
New_Vehicles WHERE MATCH (description) AGAINST('options') ORDER BY MATCH
(description) AGAINST('options') \G
```

返回以下内容：

```
*************************** 1. row **************************
relevance: 0.38341856002808
description: Last of the 2004 stock! Must sell! Loaded, all options!
*************************** 2. row **************************
relevance: 0.38341856002808
description: Come drive this popular truck! 4WD, extended cab, many options.
```

## 局限性

在使用全文搜索时，必须牢记几个局限性。首先，MySQL 仅支持 MyISAM 表类型的全文索引（将在下一节中介绍）。其次，在大多数情况下，如果你在一个以上的列上创建全文索引，则提供给 `MATCH()` 的列列表必须与你创建全文索引时指定的列表完全相同。最后，MySQL 默认的最低单词/标记长度为四个字符。如果你尝试对少于四个字母的关键字进行全文搜索匹配，将不会返回任何结果。

要更改默认的最低全文单词长度，请确保你的 MySQL 配置文件（*my.cnf*）中存在以下内容：

```
[mysqld]
ft_min_word_len=3
```

你可以使用任何整数作为最小长度（本例中设置为 3）。

## InnoDB 表

使用 MySQL 的优势之一是你不必局限于特定的数据存储引擎。什么是存储引擎？作为服务器，MySQL 为用户提供了一致的接口和查询语言，但它实际上如何存储数据的方式与其解耦紧密程度较低。MySQL 中的不同存储引擎提供了存储和访问数据的不同方式，从可靠的默认 MyISAM，到内存 Heap 表的极速性能，以及介于两者之间的所有中间状态。你可以使用的最灵活、功能最强大的表类型之一是 InnoDB。由芬兰赫尔辛基的 InnoBase Oy 创建的 InnoDB 存储引擎，为 MySQL 提供了安全且高效的数据存储和处理方式，并赋予了 MySQL 一些 MyISAM 或大多数其他表类型所不具备的额外功能。

## InnoDB 优势

虽然默认的 MyISAM 表类型提供了存储简单数据结构的成熟且快速的方式，但它缺乏许多开发者希望具备的一些功能——而 InnoDB 可以提供。自 MySQL 4.0 以来默认可用，InnoDB 表允许你使用事务、行级锁定，以及最重要的，外键约束。

外键约束提供了一种在关联表之间维护引用完整性的方法。在 `VehicleInventory` 数据库中，`New_Vehicles` 和 `Used_Vehicles` 表包含一个用于指定车辆型号（进而指定制造商）的 `model_id` 列。可以对外键约束应用于 `model_id` 列，以确保不能向该列插入任何不存在于 `ModelList` 表中的值。在默认的 MyISAM 表类型中，MySQL 无法自动执行此类规则，而在较大的数据库中，这可能导致表中出现大量无效值。InnoDB 为 MySQL 提供了一种执行此类规则的方法，从而确保数据始终保持相关性。

> *受外键约束的列仅允许引用表中存在的值，有一个例外：NULL。在其他受外键控制的列中，允许使用 NULL 值。*

## InnoDB 劣势

不幸的是，InnoDB 的优势伴随着一些特别令人烦恼的问题。首先，InnoDB 表不支持全文搜索。当你决定是否使用 InnoDB 时，你必须始终考虑未来对全文索引的需求，以及对于特定表而言，这与引用完整性相比哪个更重要。

其次，InnoDB 存储引擎在 `AUTO_INCREMENT` 列方面受到轻微限制。创建表时，InnoDB 表不允许你指定自增序列的初始值。这未必是决定性的障碍，但在设计数据库架构时需要考虑这一点。

## 使用 InnoDB

了解 InnoDB 存储引擎的最佳方法是让它发挥实际作用。现在，你将通过从头创建新表以及修改另一个表来启用 InnoDB 引擎。之后，你将尝试外键的不同方面。

### 从头创建 InnoDB 表

使用 InnoDB 存储引擎创建新表与创建标准 MyISAM 表几乎没有区别。唯一的關鍵区别是你必须在创建表命令的末尾指定 `ENGINE`：

```
CREATE TABLE tablename (column_definitions) ENGINE=InnoDB;
```

很简单，对吧？在你的 MySQL 数据库中实际试一试：

```
CREATE TABLE innodtest (innocol int) ENGINE=InnoDB;
```

如果一切顺利，你应该看到以下内容：

```
Query OK, 0 rows affected
```

至此，你便创建了一个简单的 InnoDB 表。

