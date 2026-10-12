
若要添加访问权限，您只需在相应的表中插入一行，并将每个所需的权限列指定为 `Y`。若要为您新创建的用户赋予 `VehicleInventory` 数据库的数据库级 `SELECT`、`UPDATE`、`INSERT` 和 `DELETE` 权限，请使用以下语句：

```sql
INSERT INTO mysql.db (Host, Db, User, Select_priv, Insert_priv, Update_priv, Delete_priv) VALUES ('localhost', 'VehicleInventory', 'testuser6', 'Y', 'Y', 'Y', 'Y');
```

如果需要撤销用户权限，您只需对所需的表执行 `DELETE` 操作即可。若要移除 `testuser6` 的数据库级权限，请使用此查询：

```sql
DELETE FROM mysql.db WHERE Host='localhost' AND User='testuser6';
```

将用户完全从数据库中移除的操作稍微复杂一些。您必须首先移除授予该用户的所有权限，然后才能使用 `DELETE` 命令将其从用户表中移除。

为了使 MySQL 意识到您刚刚手动更改的权限，您必须重新加载权限表：

```sql
FLUSH PRIVILEGES;
```

如果在进行访问更改后没有刷新权限，这些更改在 MySQL 下次重启之前都不会生效。这适用于您手动进行的任何访问级别的权限更改——使用 `GRANT` 或 `REVOKE` 不需要重新加载权限表。

## 服务器限制

限制服务器访问的另一种方式是大幅限制整个服务器的远程访问。如果您的数据库仅服务于直接登录到该机器上的用户，则无需让服务器接受远程网络连接。若要阻止 MySQL 监听传入的网络连接，请确保您的 MySQL 配置文件（通常是 `my.cnf`）的 `[mysqld]` 部分中存在以下内容：

```ini
[mysqld]
skip-networking
```

将上述语句添加到配置文件，然后重启 MySQL 服务器进程，即可禁用任何传入 MySQL 的流量。如果您的网络和安全服务器安全至关重要，且只有本地账户需要访问时，采取此类措施非常重要。

## 分析数据库

虽然您使用数据库的大多数时间可能都花在了添加、更新、检索和删除数据上，但总会有您需要立即了解数据库结构本身信息的时候。幸运的是，MySQL 提供了一些易于使用的信息工具，以及分析和优化数据库的简单方法。

## 高级 MySQL

在 MySQL 命令 shell 中，您可以使用几个共享 `SHOW` 前缀的不同命令，以获取有关数据库当前状态的各种信息。以下部分介绍了一些常见的 `SHOW` 命令。

### SHOW COLUMNS

`SHOW COLUMNS` 命令返回表中所有列及其属性的列表。`SHOW COLUMNS` 的一般格式如下：

```sql
SHOW COLUMNS FROM [table] FROM [database]
```

如果您想获取 `New_Vehicles` 表中所有列的列表，可以使用以下命令：

```sql
SHOW COLUMNS FROM New_Vehicles FROM VehicleInventory;
```

返回结果如下：

![](img/cacdd24f2926f10ee3219256ad732604_126_0.png)

在返回的输出中，`Field` 列包含每列的名称，`Type` 显示列的数据类型，`Null` 指定该列是否允许 `NULL` 值，`Key` 指示每列属于哪种键或索引类型，`Default` 显示指定的列默认值，`Extra` 显示每列的特殊处理。请注意，该命令在功能上与 MySQL 的 `DESCRIBE [table]` 命令相同。

### SHOW CREATE TABLE

您可能希望了解创建给定表可以使用什么命令。为此，您可以使用 `SHOW CREATE TABLE` 命令：

```sql
SHOW CREATE TABLE [table name]
```

若要获取创建您的 `New_Vehicles` 表的命令，请发送：

```sql
SHOW CREATE TABLE New_Vehicles \G
```

对 `VehicleInventory` 数据库运行此命令将得到以下结果：

```text
*************************** 1. row ********************
Table: New_Vehicles
Create Table: CREATE TABLE `New_Vehicles` (
`vehicle_id` int(11) NOT NULL auto_increment,
`model_id` int(11) default NULL,
`price` decimal(10,2) default NULL,
`color` varchar(20) default NULL,
`description` text,
`modelyear` int(11) default NULL,
PRIMARY KEY (`vehicle_id`)
) ENGINE=MyISAM DEFAULT CHARSET=lain1
```

然后，可以将此完整的 `CREATE TABLE` 命令输入到一个新的数据库中，以创建 `New_Vehicles` 表结构的精确副本。

### SHOW DATABASES

`SHOW DATABASES` 命令执行其字面意思所指的操作——它显示当前登录账户可以访问的系统中的所有数据库。只需运行该命令：

```sql
SHOW DATABASES;
```

它将返回当前用户可以访问的数据库列表：

![](img/cacdd24f2926f10ee3219256ad732604_127_0.png)

### SHOW GRANTS

`SHOW GRANTS` 命令列出授予特定用户账户的所有访问权限。例如，若要查看 `VehicleInventory` 数据库中授予 `testuser1` 账户的所有访问权限，请使用以下命令：

```sql
SHOW GRANTS FOR 'testuser1'@'localhost';
```

返回结果如下：

```text
*************************** 1. row
Grants for testuser1@localhost: GRANT USAGE ON *.* TO 'testuser1'@'localhost'
IDENTIFIED BY PASSWORD '*E69570F2322D3DC1F956C48199FEB21FF2D7D984'
*************************** 2. row
Grants for testuser1@localhost: GRANT ALL PRIVILEGES ON `vehicleinventory`.* TO 'testuser1'@'localhost'
*************************** 3. row
Grants for testuser1@localhost: GRANT SELECT, SELECT (description), INSERT (description), UPDATE (description) ON `vehicleinventory`.`used_vehicles` TO 'testuser1'@'localhost'
```

## 数据库维护

您创建了车辆库存数据库，将其投入生产，设置了搜索功能，并且客户对结果感到满意。现在可以坐下来放松一下，对吗？

不完全是。您可能还想考虑另一件事，以帮助将生产数据库灾难性丢失的成本降至最低。您需要的是备份。

### 创建备份

在 MySQL 中创建备份非常容易，这要归功于随系统附带的一套出色的客户端工具。要创建备份，您可以使用 `mysqldump` 实用程序。您需要做的第一件事是（如果需要）退出 MySQL 客户端，回到您的标准 shell 提示符：

```sql
mysql> exit
```

一旦您回到命令提示符，调用 `mysqldump` 命令行工具就变得很简单。对于大多数数据库备份，以下通用格式都可以工作：

```bash
mysqldump --opt database > backupfile.sql
```

这里您正在调用 `mysqldump` 命令，并告诉它将名为 `database` 的数据库转储到名为 `backupfile.sql` 的文件中。同时存在的是 `--opt` 选项，它告诉备份实用程序使用一组常用选项，以输出有助于 MySQL 更准确地恢复该文件的格式。

要了解更多的 `mysqldump` 选项，请在命令提示符处输入 `man mysqldump`。

若要备份车辆库存数据库，请使用以下命令：

```bash
mysqldump --opt VehicleInventory > vi_backup.sql
```

与 `mysql` 命令行客户端一样，如果需要提供用户名和密码，请确保在数据库名称之前正确使用 `-u` 和 `-p`。
