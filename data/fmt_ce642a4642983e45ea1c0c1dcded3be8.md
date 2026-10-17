
```sql
(SELECT ma.make_name, mo.model_name, n.color, n.modelyear FROM New_Vehicles n LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id)) UNION (SELECT ma.make_name, mo.model_name, u.color, u.modelyear FROM Used_Vehicles u LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id));
```

在 MySQL 中运行这个庞大的查询，你将看到以下内容：

| make_name   | model_name | color                    | modelyear |
| :---------- | :--------- | :----------------------- | :-------- |
| Ford        | Explorer   | Dark Blue                | 2005      |
| NULL        | NULL       | Graphite Pearl           | 2004      |
| Toyota      | Tacoma     | Radiant Red              | 2005      |
| Chevrolet   | Corvette   | Daytona Sunset Orange Metallic | 2005  |
| Honda       | Accord     | Deep Green Pearl         | 2003      |
| Volkswagen  | Golf       | Reflex Silver            | 2004      |
| Toyota      | Tacoma     | Red                      | 1993      |

最终得到的是一个简洁的列表中所有车辆及其品牌、型号、颜色和年份。你在库存应用程序中实现这一点并将其发送给经销商批准，但你还没有完成。像许多客户一样，经销商老板很善变，再次改变了关于车辆列表中需要哪些字段的想法。这一次，你需要为所有车辆返回数据库中的所有信息。你已经知道 `New_Vehicles` 表和 `Used_Vehicles` 表具有不同数量的列，那么 `UNION` 如何奏效？答案其实很简单。你所需要做的就是在各自对应的表中缺失的列指定 `NULL`（或你喜欢的任何其他值），如下所示：

```sql
(SELECT ma.make_name, mo.model_name, n.color, n.modelyear, n.price, n.description, NULL, 1 FROM New_Vehicles n LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id)) UNION (SELECT ma.make_name, mo.model_name, u.color, u.modelyear, u.price, u.description, u.certified, u.warranty FROM Used_Vehicles u LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id));
```

运行此查询，你将看到以下内容：

```text
************************* 1. row **************************
make_name: Ford
model_name: Explorer
color: Dark Blue
modelyear: 2005
price: NULL
description: Popular SUV; great for moving people or cargo across town, or wherever your adventures may take you.
NULL: NULL
1: 1

************************* 2. row **************************
make_name: NULL
model_name: NULL
color: Graphite Pearl
modelyear: 2004
price: NULL
description: Last of the 2004 stock! Must sell! Loaded, all options!
NULL: NULL
1: 1

************************* 3. row **************************
make_name: Toyota
model_name: Tacoma
color: Radiant Red
modelyear: 2005
price: NULL
description: Come drive this terrific truck! 4WD, extended cab, many options.
NULL: NULL
1: 1

************************* 4. row **************************
make_name: Chevrolet
model_name: Corvette
color: Daytona Sunset Orange Metallic
modelyear: 2005
price: NULL
description: The all new C6 Corvette, the next generation of classic American sports-cars. 400HP V8; Very fast!
NULL: NULL
1: 1

************************* 5. row **************************
make_name: Honda
model_name: Accord
color: Deep Green Pearl
modelyear: 2003
price: NULL
description: Excellent condition, off-lease vehicle; Must see!
NULL: 0
1: 1

************************* 6. row **************************
make_name: Volkswagen
model_name: Golf
color: Reflex Silver
modelyear: 2004
price: NULL
description: R32 Limited edition; Low miles; Understated and surprisingly functional; Loaded.
NULL: 1
1: 1

************************* 7. row **************************
make_name: Toyota
model_name: Tacoma
color: Red
modelyear: 1993
price: NULL
description: Runs decent; 4WD; Tinted windows, aftermarket stereo; Needs a little TLC.
NULL: 0
1: 0
```

你首先会注意到的是，它看起来与之前的结果略有不同。这是因为查询末尾的 `\G` 终止符，它导致 MySQL 垂直显示结果（否则，表格对于本书来说太宽了）。除此之外，所有信息都存在并得到解释。在 `New Vehicles` 表中缺失的 `certified` 列指定的 `NULL` 值存在，以及你指定为 `1` 的占位符值，因为所有新车都有保修。你将更改发回给客户端，他们很高兴（至少暂时是这样）。

## 全文搜索

到目前为止，车场老板们对你精确查询所需内容的能力印象深刻，提供各种列表以提高销售人员的生产力——但他们仍想要更多。他们现在希望的是通过关键词搜索汽车库存的方法。他们的搜索需求不太复杂，但 `WHERE` 子句中的简单 `LIKE` 比较无法完成任务。

你所需的恰好是 MySQL 内置的功能——全文搜索。全文搜索在 MySQL 中默认启用，允许你对指定的任何文本列执行自然语言搜索。然而，你不能随意在数据库中进行全文搜索——你必须先进行一些准备工作。

### 启用全文搜索

在 MySQL 中启用全文搜索只需在表的一个或多个列上创建索引。你可以用两种方法之一完成此操作：在表创建时，作为 `CREATE TABLE` 命令的一部分，或在表生命周期的稍后阶段。
