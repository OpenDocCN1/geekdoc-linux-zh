

## 4 高级 MySQL

大多数动态网站的关键要素之一是为其提供数据的数据库。无论是简单的新闻页面，还是复杂的发布系统或 CMS，数据库在站点内容管理中都发挥着核心作用。为了让站点平稳运行，了解一些数据库系统的技巧和窍门非常有帮助。在本章中，你将学习如何创建数据库，管理访问系统的各种用户账户，以及如何组合和优化 SQL 代码以执行复杂和精细的查询。

### 基础知识回顾

在深入研究高级功能之前，我们先快速回顾一下 MySQL 的用法。假设你刚接到一个新客户，一家汽车经销商。经销商的经理希望你创建一个网站，帮助他们跟踪汽车库存。没问题，你说着便坐下来开始规划他们的 Web 应用程序。

在规划过程中，你设计了一个简单的多表数据库方案，用于存储他们的汽车场地数据。为了便于练习，你决定创建类似图 4.1 的数据库表。

你创建了一个非常简单的数据库结构，涉及两个表。在 `New_Vehicles` 表中，显然存储的是新车的数据。可以为库存中的每辆车指定里程、价格、颜色和描述等属性。`Used_Vehicles` 表的结构与 `New_Vehicles` 几乎相同，但旨在存储二手车（正如你可能猜到的那样）的记录。`Used_Vehicles` 表还有几个额外的列，用于指示车辆是否经过认证或拥有保修，以及一个里程列。最后两个表，`Make` 和 `Model`，存储经销商销售的各种品牌的通用制造商和型号名称。

![](img/fd2e7361878181c2b12e30301ff3e182_99_0.png)

### 创建数据库

你需要做的第一件事是在 MySQL 中创建数据库和表。首先启动命令行中的 MySQL 客户端，或者如果你有其他更熟悉的程序，可以直接输入 MySQL 命令，不妨使用那个。

```
shell$ **mysql**
```

这将打开 MySQL 监视器，其外观应类似于以下内容（如果你使用的是命令行客户端）：

> 欢迎使用 MySQL 监视器。命令以 ; 或 \g 结尾。
> 你的 MySQL 连接 id 为 2，服务器版本：4.1.11-log
> 
> 输入 'help;' 或 '\h' 获取帮助。输入 '\c' 清除当前缓冲区。
> mysql>

在许多情况下，你需要使用登录名和密码来访问 MySQL 客户端。为此，只需在 *mysql* 命令末尾添加 -u username -p，MySQL 就会提示你输入密码，如下所示：

```
shell$ mysql -u username -p
```

使用 MySQL 命令行客户端是熟悉 MySQL 大多数命令和功能的好方法，这些功能在图形界面客户端中通常会被自动化处理。

输入以下命令来创建数据库，并将其命名为“VehicleInventory”：

```
mysql> CREATE DATABASE VehicleInventory;
```

既然你已经创建了数据库，就需要将其设置为后续查询的活动数据库：

```
mysql> USE VehicleInventory;
```

接下来，为你的数据库创建表。在 MySQL 中创建表的基本 SQL 语句如下：

```
CREATE TABLE tablename (column_definitions);
```

要创建四个车辆信息表，可以使用以下内容：

```
mysql> CREATE TABLE Makes (make_id int PRIMARY KEY AUTO_INCREMENT, make_name varchar(100) );
mysql> CREATE TABLE Models (model_id int PRIMARY KEY AUTO_INCREMENT, model_name varchar(200), make_id int );
mysql> CREATE TABLE New_Vehicles (vehicle_id int PRIMARY KEY AUTO_INCREMENT, model_id int, modelyear int, price decimal(10,2), color varchar(200), description text );
mysql> CREATE TABLE Used_Vehicles (vehicle_id int PRIMARY KEY AUTO_INCREMENT, model_id int, modelyear int, mileage int, price decimal(10,2), color varchar(200), certified tinyint, warranty tinyint, description text );
```

简而言之，我们只需使用 MySQL 的 CREATE TABLE 命令，后面跟着表名，然后在括号中列出列名和类型。你还会注意到每个表都添加了一个自动递增的主键，以便在添加行后帮助你唯一地标识这些行。

### 添加信息

既然你已经创建了表，就需要向其中添加一些数据。为此，你将使用 INSERT 语句。MySQL 的 INSERT 命令通常遵循以下格式：

```
INSERT INTO tablename (column_list) VALUES (new_values);
```

首先，向 Makes 表添加一些初始数据：

```
INSERT INTO Makes (make_id, make_name) VALUES (1, 'Ford'), (2, 'Honda'), (3, 'Volkswagen'), (4, 'Toyota'), (5, 'Chevrolet');
```

这里使用了基本的 SQL INSERT 语法，但增加了一点变化。在 MySQL 中，你可以指定一组以逗号分隔的列值，而不是仅一组值，以便一次填充多行。通常，在向 Makes 表插入数据时，你可能会省略 make_id 列——自动递增的 ID 会自动为它们分配数字。在这种情况下，你指定了 ID，以便稍后添加到其他表的行具有有效的外键。

使用以下内容向其余表添加数据（记住，你可以从 **www.wrox.com** 下载此代码，如果你想节省打字功夫的话）：

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

请注意，你添加到 New_Vehicles 表中的第二辆车的 model_id 值为 NULL。稍后你会明白原因。

### 检索信息

你花了那么多时间创建数据库表并填充数据；现在是时候把一些数据取回来了。为此，你将使用 SELECT 语句。SELECT 的简化形式看起来像这样：

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

你已经建立了车辆库存，可以使用基础知识对单个表执行简单查询。但你希望看到更多——甚至是一个将每辆车的制造商和型号与其单独记录关联起来的查询。为此，你将使用*连接*（joins）。

