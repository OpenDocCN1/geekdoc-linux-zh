
你首先会注意到的是，结果看起来与之前的结果略有不同。这是因为查询末尾使用了 `\G` 终止符，它使 MySQL 以垂直方式显示结果（否则，表格对这本书来说太宽了）。除此之外，所有信息都存在且准确无误。在 `New_Vehicles` 表中为缺失的 `certified` 列指定的 `NULL` 值存在，以及你指定的占位值 `1` 也存在，因为所有新车都有保修。你将这些更改发送回客户端，他们对此感到满意（至少暂时是这样）。

```
*************************** 1. 行 ***************************
make_name: Ford
model_name: Explorer
color: Dark Blue
modelyear: 2005
price: NULL
description: Popular SUV; great for moving people or cargo across town, or wherever your adventures may take you.
NULL: NULL
1: 1
*************************** 2. 行 ***************************
make_name: NULL
model_name: NULL
color: Graphite Pearl
modelyear: 2004
price: NULL
description: Last of the 2004 stock! Must sell! Loaded, all options!
NULL: NULL
1: 1
*************************** 3. 行 ***************************
make_name: Toyota
model_name: Tacoma
color: Radiant Red
modelyear: 2005
price: NULL
description: Come drive this terrific truck! 4WD, extended cab, many options.
NULL: NULL
1: 1
*************************** 4. 行 ***************************
make_name: Chevrolet
model_name: Corvette
color: Daytona Sunset Orange Metallic
modelyear: 2005
price: NULL
description: The all new C6 Corvette, the next generation of classic American sportscars. 400HP V8; Very fast!
NULL: NULL
1: 1
*************************** 5. 行 ***************************
make_name: Honda
model_name: Accord
color: Deep Green Pearl
modelyear: 2003
price: NULL
description: Excellent condition, off-lease vehicle; Must see!
NULL: 0
1: 1
*************************** 6. 行 ***************************
make_name: Volkswagen
model_name: Golf
color: Reflex Silver
modelyear: 2004
price: NULL
description: R32 Limited edition; Low miles; Understated and suprisingly functional; Loaded.
    NULL: 1
    1: 1
******************* 7. 行 *********************
make_name: Toyota
model_name: Tacoma
color: Red
modelyear: 1993
price: NULL
description: Runs decent; 4WD; Tinted windows, aftermarket stereo; Needs a little TLC.
    NULL: 0
    1: 0
```

# 全文搜索

到目前为止，汽车经销商对这些精确查询所需能力印象深刻，并提供各种列表来帮助提高销售人员的生产力——但他们仍然想要更多。他们现在希望有一种按关键字搜索汽车库存的方式。他们的搜索需求并不复杂，但简单的 `LIKE` 比较在 `WHERE` 子句中根本无法完成任务。

你需要做的事情恰好内置于 MySQL 中——全文搜索。全文搜索在 MySQL 中默认启用，允许你对指定的任何文本列执行自然语言搜索。不过，你不能随意在数据库中开始全文搜索——你必须先做一些准备工作。

## 启用全文搜索

在 MySQL 中启用全文搜索只是简单地在一个表的列上创建索引。你可以用两种方法之一来完成：在创建表时，作为 `CREATE TABLE` 命令的一部分，或者在表的生命周期中稍后添加。

### 创建启用全文搜索的新表

你要创建的第一个全文索引将是一个全新表的一部分。要在建表时指定全文索引，你只需在列定义末尾指定全文索引和索引列列表即可：

```
CREATE TABLE 表名 (列定义, FULLTEXT (要索引的列))
```

你可以在 `FULLTEXT` 列列表中指定单个列，或指定逗号分隔的多个列。是时候在 `VehicleInventory` 数据库中实际创建一个具有全文搜索功能的表了：

```
CREATE TABLE testft (testint int, testvc varchar(50), testtxt text, FULLTEXT (testvc, testxt));
```

你刚刚创建了一个新表，并在 `testvc` 和 `testtxt` 列上建立了全文索引。

### 修改现有表以支持全文搜索

修改现有表以支持全文搜索稍微复杂一点，但也没多难。要为现有表添加全文搜索功能，你使用 MySQL 的 `ALTER TABLE` 命令，如下所示：

```
ALTER TABLE 表名 ADD FULLTEXT (列)
```

现在为 `New_Vehicles` 表添加全文索引：

```
ALTER TABLE New_Vehicles ADD FULLTEXT (description);
```

完成后，是时候好好利用这些索引了。

## 使用全文搜索进行查询

在启用了全文索引的 MySQL 表中进行搜索是一个相对轻松的过程。你只需在 `WHERE` 子句中使用 `MATCH()` 函数，如下所示：

```
SELECT [列] FROM [表] WHERE MATCH ([索引列]) AGAINST ('关键字')
```

在 `MATCH` 的参数列表中，你可以指定任意数量的列，只要它们是全文索引的一部分即可。

回到车辆库存数据库，是时候对新车列表进行搜索了。要搜索单词 `options`，你可以使用以下内容：

```
SELECT vehicle_id, description FROM New_Vehicles WHERE MATCH (description) AGAINST ('options');
```

这应该返回以下内容：

| vehicle_id | description |
| :--- | :--- |
| 2 | Last of the 2004 stock! Must sell! Loaded, all options! |
| 3 | Come drive this popular truck! 4WD, extended cab, many options. |

全文搜索的另一个巧妙技巧是可以按相关性对结果排序，并返回相关性得分。为了利用相关性数据，你可以在 `SELECT` 列表和 `ORDER BY` 子句中都使用 `MATCH()...AGAINST()` 函数，如下所示：

```
SELECT MATCH (description) AGAINST('options') AS relevance, description FROM
New_Vehicles WHERE MATCH (description) AGAINST ('options') ORDER BY MATCH
(description) AGAINST('options') \G
```

返回以下内容：
