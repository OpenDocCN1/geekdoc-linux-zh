
```
INSERT INTO tablename (column_list) VALUES (new_values);
```

首先，向 Makes 表添加一些初始数据：

```
INSERT INTO Makes (make_id, make_name) VALUES (1, 'Ford'), (2, 'Honda'), (3, 'Volkswagen'), (4, 'Toyota'), (5, 'Chevrolet');
```

这里使用了基本的 SQL INSERT 语法，但加了一点变化。在 MySQL 中，您可以指定一组以逗号分隔的列值，而不是仅一组，以一次填充多行。通常，在向 Makes 表插入数据时，您可能会省略 `make_id` 列——自动递增的 ID 会自动为它们分配数字。在这种情况下，指定 ID 是因为您稍后将添加到其他表的行将具有有效的外键。

## 第 4 章

使用以下内容向其余表添加数据（如果您想省去打字，请记住您可以从 www.wrox.com 下载此代码）：

```
INSERT INTO Models (model_id, model_name, make_id) VALUES (1, 'Explorer', 1), (2, 'Accord', 2), (3, 'Golf', 3), (4, 'Tacoma', 4), (5, 'Corvette', 5);
INSERT INTO New_Vehicles (model_id, modelyear, color, description) VALUES
(1, 2005, 'Dark Blue', 'Popular SUV; great for moving people or cargo across town, or wherever your adventures may take you.'),
(NULL, 2004, 'Graphite Pearl', 'Last of the 2004 stock! Must sell! Loaded, all options!'),
(4, 2005, 'Radiant Red', 'Come drive this terrific truck! 4WD, extended cab, many options.'),
(5, 2005, 'Daytona Sunset Orange Metallic', 'All the new C6 Corvette, the next generation of classic American sportscars. 400HP V8; very fast!'),
(1, 2005, 'Dark Blue', 'Popular SUV; great for moving people or cargo across town, or wherever your adventures may take you.');
INSERT INTO Used_Vehicles (model_id, modelyear, color, mileage, certified, warranty, description) VALUES
(1, 2000, 'White', 64800, 0, 0, 'Good condition; One owner; 4WD; V6'),
(2, 2003, 'Deep Green Pearl', 27300, 0, 1, 'Excellent condition, off-lease vehicle; Must see!'),
(3, 2004, 'Reflex Silver', 3800, 1, 1, 'R32 Limited edition; Low miles; Understated and surprisingly functional; Loaded.'),
(4, 1993, 'Red', 152000, 0, 0, 'Runs decent; 4WD; Tinted windows, aftermarket stereo; Needs a little TLC.');
```

请注意，您添加到 `New_Vehicles` 表的第二辆车的 `model_id` 有一个 `NULL` 值。您稍后会了解到原因。

## 检索信息

您花了很多时间创建数据库表并填充数据；现在是时候取回一些数据了。为此，您将使用 `SELECT` 语句。简化的 `SELECT` 形式看起来像这样：

```
SELECT [column_names] FROM [table] WHERE [criteria]
```

例如，如果您想获取二手车颜色列表，可以使用类似以下内容：

```
SELECT color FROM Used_Vehicles;
```

这将返回以下内容：

![](img/cacdd24f2926f10ee3219256ad732604_101_0.png)

或者，也许您想要列出 2001 年之前车型的所有里程数：

```
SELECT mileage, modelyear FROM Used_Vehicles WHERE modelyear < 2001;
```

运行此查询显示以下内容：

| mileage | modelyear |
|---------|-----------|
| 64800   | 2000      |
| 152000  | 1993      |

这很简单，但如果您发现错误，想要更改现有记录怎么办？

## 更新信息

要更新信息，您使用 `UPDATE` 语句。`UPDATE` 语句的通用形式如下：

```
UPDATE [table] SET [column] = [value] WHERE [criteria]
```

回到车辆库存示例，假设有一天，汽车经销商经理在浏览库存时，注意到其中一辆车的里程数记录错误。为了将其更改为正确值，您可以使用以下查询：

```
UPDATE Used_Vehicles SET mileage = 66000 WHERE vehicle_id = 1;
```

在这种情况下，车辆 ID 1 对应于您在之前 `INSERT` 语句中添加的二手福特探险者自动递增分配的 ID。

## 删除信息

假设汽车经销商的销售量开始增加，最近的一些销售要求从您的数据库中删除一些车辆。在这种情况下，您将使用 `DELETE` 语句：

```
DELETE FROM [table] WHERE [criteria];
```

之前示例中修复了错误里程数的那辆二手福特探险者今天卖掉了。要从 `Used_Vehicles` 表中删除它，您只需执行以下操作：

```
DELETE FROM Used_Vehicles WHERE vehicle_id = 1;
```

这应该涵盖了 MySQL 使用的基础知识，是时候转向更强大的查询了。

## 查询多个表

您已经设置好了车辆库存，可以使用基础知识对单个表执行简单查询。但您想看到更多——也许是一个将每辆车的品牌和型号与其单独记录关联起来的查询。为此，您将使用*连接*（joins）。

在 SQL 中，连接是一种在指定列或列上将两个或更多表链接起来的方法。在 MySQL 中，最常用的是两种连接类型：内连接（inner joins）和外连接（outer joins）。

### 内连接

内连接是一种将两个表基于每行共同共享的值组合其行的方法。当您在*SELECT*查询中执行内连接时，您只需在*FROM*子句中指定要连接的表，并提供关于它们有哪些共同列的提示。MySQL 内连接语法的通用抽象如下：

```
SELECT [column names] FROM [table1] INNER JOIN [table2] ON [table1.column] = [table2.column]
```

使用假设的汽车经销商库存，您希望每辆车的具体信息旁边返回该车的型号。为了实现这一点，您的查询看起来像这样：

```
SELECT Models.model_name, New_Vehicles.color, New_Vehicles.modelyear FROM Models
INNER JOIN New_Vehicles ON Models.model_id = New_Vehicles.model_id;
```

对您的数据库运行此查询产生以下结果：

| model_name | color                            | modelyear |
|------------|----------------------------------|-----------|
| Explorer   | Dark Blue                        | 2005      |
| Tacoma     | Radiant Red                      | 2005      |
| Corvette   | Daytona Sunset Orange Metallic   | 2005      |
