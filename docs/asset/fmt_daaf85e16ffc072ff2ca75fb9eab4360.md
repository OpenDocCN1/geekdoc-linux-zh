
在返回的输出中，`Field` 列包含每个列的名称，`Type` 显示列数据类型，`Null` 指定是否允许列中包含 `NULL` 值，`Key` 指示每个列属于什么键或索引类型，`Default` 显示指定的默认列值，`Extra` 显示给予每个列的任何特殊处理。请注意，此命令在功能上与 MySQL 的 `DESCRIBE [table]` 命令完全相同。

### SHOW CREATE TABLE

你可能希望了解可以使用什么命令来创建给定的表。为此，你可以使用 `SHOW CREATE TABLE` 命令：

```sql
SHOW CREATE TABLE [table name]
```

要获取用于创建你的 `New_Vehicles` 表的创建命令，请发送：

```sql
SHOW CREATE TABLE New_Vehicles \G
```

针对 `VehicleInventory` 数据库运行此命令将得到以下结果：

```
*************************** 1. row ***************************
Table: New_Vehicles
Create Table: CREATE TABLE `New_Vehicles` (
`vehicle_id` int(11) NOT NULL auto_increment,
`model_id` int(11) default NULL,
`price` decimal(10,2) default NULL,
`color` varchar(200) default NULL,
`description` text,
`modelyear` int(11) default NULL,
PRIMARY KEY (`vehicle_id`)
) ENGINE=MyISAM DEFAULT CHARSET=latin1
```

然后可以在新的数据库中进入整个 CREATE TABLE 命令，以创建 `New_Vehicles` 表结构的精确副本。

### SHOW DATABASES

`SHOW DATABASES` 命令做的正是它看起来做的事情——它显示系统中当前登录账户可访问的所有数据库。只需运行该命令：

```sql
SHOW DATABASES;
```

它将返回当前用户可访问的数据库列表：

```
+--------------------+
| Database           |
+--------------------+
| VehicleInventory |
| mysql              |
+--------------------+
```

### SHOW GRANTS

`SHOW GRANTS` 命令列出授予特定用户账户的所有访问权限。例如，要查看在 `VehicleInventory` 数据库中授予 `testuser1` 账户的所有访问权限，请使用以下内容：

```sql
SHOW GRANTS FOR `testuser1`@'localhost' \G
```

这将返回以下内容：

```
*************************** 1. row ***************************
Grants for testuser1@localhost: GRANT USAGE ON *.* TO `testuser1`@'localhost'
IDENTIFIED BY PASSWORD '*E69S70P2322D3DC1F956C48199FEB21FF2D7D984'
*************************** 2. row ***************************
Grants for testuser1@localhost: GRANT ALL PRIVILEGES ON `vehicleinventory`.* TO
`testuser1`@'localhost'
*************************** 3. row ***************************
Grants for testuser1@localhost: GRANT SELECT, SELECT (description), INSERT
description), UPDATE (description) ON `vehicleinventory`.`used_vehicles` TO
`testuser1`@'localhost'
```

## 数据库维护

您已创建好车辆库存数据库，并将其投入生产环境，配置了搜索功能，客户对结果表示满意。现在是时候放松一下了吗？

未必。您可能还需要考虑另一件事，以最小化生产数据库发生灾难性数据丢失时的成本。您需要的是备份。

### 创建备份

在 MySQL 中创建备份非常容易，这得益于系统附带的一套出色的客户端工具。要创建备份，您可以使用 `mysqldump` 实用程序。您需要做的第一件事是退出 MySQL 客户端（如果需要的话），并回到标准的 shell 提示符：

```
mysql> exit
```

回到命令提示符后，只需调用 `mysqldump` 命令行工具即可。对于大多数数据库备份，以下通用格式即可满足需求：

```
mysqldump --opt database name > backupfile.sql
```

这里您正在调用 `mysqldump` 命令，并告诉它将名为 `database name` 的数据库导出到名为 `backupfile.sql` 的文件中。此外还包含 `--opt` 选项，该选项告诉备份实用程序使用一组通用选项，以输出一种有助于 MySQL 更准确恢复文件格式。

> 如需了解更多的 `mysqldump` 选项，请在命令提示符下输入 `man mysqldump`。

要备份车辆库存数据库，请使用以下命令：

```
mysqldump --opt VehicleInventory > vi_backup.sql
```

> 与 `mysql` 命令行客户端一样，如果您需要提供用户名和密码，请确保在数据库名称之前相应地使用 `-u` 和 `-p` 参数。

现在，您已在 `vi_backup.sql` 文件中拥有一个完整的数据库创建脚本。您可以随时归档此文件，将其恢复到其他服务器，刻录到 CD 或 DVD 上，或执行其他您喜欢的操作。

### 从备份中恢复数据库

如果服务器崩溃、遭到黑客攻击，或者您只是想在生产数据库中获取一份副本用于开发环境测试，您需要知道如何恢复数据库备份。在 MySQL 中，这非常简单，您可以使用 MySQL 命令行客户端，如下所示：

```
mysql database name < backupfile.sql
```

因此，要恢复 `VehicleInventory` 数据库，请使用以下命令：

```
mysql VehicleInventory < vi_backup.sql
```

请注意，恢复目标数据库的名称必须是系统中已实际存在的数据库。如果您想要将备份恢复到新表中，只需登录 `mysql` 客户端，创建一个您所需名称的空数据库，退出客户端，然后按所需方式恢复备份即可。

#### 总结

希望本章中的信息能帮助您设置复杂的数据库模式，使用复杂的查询，并维护整个系统。掌握了这些基本工具，您将很少遇到无法克服的数据库障碍。作为开发人员，您可能会发现自己在命令行界面花费的时间更少，而更多地在诸如 PhpMyAdmin 或 MySQL AB 自己的 MySQL Administrator GUI 工具上工作。只要这些工具有输入原始命令的方式，您在本章中看到的原始命令和查询都可以应用于其中。您对执行管理和数据操作任务的具体 SQL 的理解，也将有助于您理解任何 GUI MySQL 应用程序中任何文本字段、单选按钮和复选框背后正在发生的事情——或者甚至是在您的 PHP 应用程序本身中。

# 第 5 章

## PHP 配置

当使用 LAMP 技术时，很少有事情比 PHP 的配置方式对编码决策产生更大的影响。任何 PHP 安装的核心都是配置文件 `php.ini`。该文件中的设置可以极大地影响您的应用程序编码方式、服务器性能以及安全性。本章告诉您需要查找和更改哪些设置，以改善您的 PHP 安装，并提供一组脚本来自动根据您的喜好准备 PHP 环境和配置设置。

## 修改 `php.ini`

如前所述，`php.ini` 文件是配置 PHP 安装的主要工具。本节介绍了许多您应该设置的配置指令，以及几个在 PHP 5 中新增的指令。

### 推荐的配置指令

配置 PHP 时，为了确保系统安全并以最快速度运行，需要牢记许多设置：
