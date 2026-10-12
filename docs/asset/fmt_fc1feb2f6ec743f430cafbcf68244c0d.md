
```
mysql> CREATE TABLE Makes (make_id int PRIMARY KEY AUTO_INCREMENT, make_name varchar(100) );
mysql> CREATE TABLE Models (model_id int PRIMARY KEY AUTO_INCREMENT, model_name varchar(200), make_id int );
mysql> CREATE TABLE New_Vehicles (vehicle_id int PRIMARY KEY AUTO_INCREMENT, model_id int, modelyear int, price decimal(10,2), color varchar(200), description text );
mysql> CREATE TABLE Used_Vehicles (vehicle_id int PRIMARY KEY AUTO_INCREMENT, model_id int, modelyear int, mileage int, price decimal(10,2), color varchar(200), certified tinyint, warranty tinyint, description text );
```

简而言之，我们只需使用 MySQL 的 `CREATE TABLE` 命令，后面跟着表名，然后在括号中列出列名和类型。你还会注意到每个表都添加了一个自动递增的主键，以便在添加行后帮助你唯一地标识这些行。

### 添加信息

既然你已经创建了表，就需要向其中添加一些数据。为此，你将使用 `INSERT` 语句。MySQL 的 `INSERT` 命令通常遵循以下格式：

```
INSERT INTO tablename (column_list) VALUES (new_values);
```

首先，向 `Makes` 表添加一些初始数据：

```
INSERT INTO Makes (make_id, make_name) VALUES (1, 'Ford'), (2, 'Honda'), (3, 'Volkswagen'), (4, 'Toyota'), (5, 'Chevrolet');
```

这里使用了基本的 SQL `INSERT` 语法，但增加了一点变化。在 MySQL 中，你可以指定一组以逗号分隔的列值，而不是仅一组值，以便一次填充多行。通常，在向 `Makes` 表插入数据时，你可能会省略 `make_id` 列——自动递增的 ID 会自动为它们分配数字。在这种情况下，你指定了 ID，以便稍后添加到其他表的行具有有效的外键。

使用以下内容向其余表添加数据（记住，你可以从 `www.wrox.com` 下载此代码，如果你想节省打字功夫的话）：

```
INSERT INTO Models (model_id, model_name, make_id) VALUES (1, 'Explorer', 1), (2, 'Accord', 2), (3, 'Golf', 3), (4, 'Tacoma', 4), (5, 'Corvette', 5);
INSERT INTO New_Vehicles (model_id, modelyear, color, description) VALUES
(1, 2005, 'Dark Blue', 'Popular SUV; great for moving people or cargo across town, or wherever your adventures may take you.'),
(NULL, 2004, 'Graphite Pearl', 'Last of the 2004 stock! Must sell! Loaded, all options!'),
(4, 2005, 'Radiant Red', 'Come drive this terrific truck! 4WD, extended cab, many options.'),
(5, 2005, 'Daytona Sunset Orange Metallic', 'The all new C6 Corvette, the next generation of classic American sports cars. 400HP V8; Very fast!'),
(1, 2005, 'Dark Blue', 'Popular SUV; great for moving people or cargo across town, or wherever your adventures may take you.');
INSERT INTO Used_Vehicles (model_id, modelyear, color, mileage, certified, warranty, description) VALUES
(1, 2000, 'White', 64800, 0, 0, 'Good condition; One owner; 4WD, V6'),
(2, 2003, 'Deep Green Pearl', 27300, 0, 1, 'Excellent condition, off-lease vehicle; Must see!'),
(3, 2004, 'Reflex Silver', 3800, 1, 1, 'R32 Limited edition; Low miles; Understated and surprisingly functional; Loaded.'),
(4, 1993, 'Red', 152000, 0, 0, 'Runs decent; 4WD; Tinted windows, aftermarket stereo; Needs a little TLC.'
)
```

请注意，你添加到 `New_Vehicles` 表中的第二辆车的 `model_id` 值为 `NULL`。稍后你会明白原因。

### 检索信息

你花了那么多时间创建数据库表并填充数据；现在是时候把一些数据取回来了。为此，你将使用 `SELECT` 语句。`SELECT` 的简化形式看起来像这样：

```
SELECT [column_names] FROM [table] WHERE [criteria]
```

例如，如果你想检索二手车颜色的列表，可以使用类似以下内容：

```
SELECT color FROM Used_Vehicles
```

这将返回以下内容：

| color        |

|--------------|

| White        |

| Deep Green Pearl |

| Reflex Silver |

| Red          |

或者，也许你想要列出 2001 年款之前所有汽车的里程数：

```
SELECT mileage, modelyear FROM Used_Vehicles WHERE modelyear < 2001;
```

运行此查询显示以下内容：

| mileage | modelyear |

| :--- | :--- |

| 64800 | 2000 |

| 152000 | 1993 |

很简单，但如果你发现错误，并想要更改现有记录怎么办？

### 更新信息

要更新信息，你使用 `UPDATE` 语句。`UPDATE` 语句的通用形式如下：

```
UPDATE [table] SET [column]=[value] WHERE [criteria]
```

回到车辆库存示例，假设有一天，汽车场地的经理在查看库存时，发现其中一辆车的里程记录有误。为了将其更改为正确值，你可能会使用以下查询：

```
UPDATE Used_Vehicles SET mileage=66000 WHERE vehicle_id=1;
```

在这种情况下，车辆 ID 1 对应于之前 `INSERT` 语句中添加的二手福特探险者（Ford Explorer）自动递增分配的 ID。

### 删除信息

假设的汽车场地销售开始增长，一些最近的销售额需要从数据库中移除一些车辆。在这种情况下，你将使用 `DELETE` 语句：

```
DELETE FROM [table] WHERE [criteria];
```

那辆里程记录有误的二手福特探险者今天卖掉了。要将其从 `Used_Vehicles` 表中移除，你只需执行以下操作：

```
DELETE FROM Used_Vehicles WHERE vehicle_id=1;
```

这应该涵盖了 MySQL 使用的基础知识，是时候进入更强大的查询了。

### 多表查询

你已经建立了车辆库存，可以使用基础知识对单个表执行简单查询。但你希望看到更多——甚至是一个将每辆车的制造商和型号与其单独记录关联起来的查询。为此，你将使用 `连接`（joins）。

#### 内连接

在 SQL 中，连接（join）是通过指定的一列或多列将两个或更多表关联起来的方式。在 MySQL 中，最常使用的两种连接类型是内连接和外连接。
