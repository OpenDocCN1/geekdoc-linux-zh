
| Grant_priv | enum('N','Y') |

| References_priv | enum('N','Y') |

| Index_priv | enum('N','Y') |

| Alter_priv | enum('N','Y') |

| Show_db_priv | enum('N','Y') |

| Super_priv | enum('N','Y') |

| Create_tmp_table_priv | enum('N','Y') |

| Lock_tables_priv | enum('N','Y') |

| Execute_priv | enum('N','Y') |

| Repl_slave_priv | enum('N','Y') |

| Repl_client_priv | enum('N','Y') |

| ssl_type | enum('ANY','X509','SPECIFIED') |

| ssl_cipher | Blob |

| x509_issuer | Blob |

| x509_subject | Blob |

| max_questions | int(11) unsigned |

| max_updates | int(11) unsigned |

| max_connections | int(11) unsigned |

`user` 表包含系统中所有用户的列表，以及该用户可能拥有的任何全局权限。与访问权限相关的关键字段是所有后缀为 `_priv` 的列。请注意，所有权限列的默认值均为 `no`。

`db` 表保存数据库级别访问权限的记录。`db` 的结构如下：

| 字段 | 类型 |
| --- | --- |
| Host | varchar(60) |
| Db | varchar(64) |
| User | varchar(16) |
| Select_priv | enum('N','Y') |
| Insert_priv | enum('N','Y') |
| Update_priv | enum('N','Y') |
| Delete_priv | enum('N','Y') |
| Create_priv | enum('N','Y') |
| Drop_priv | enum('N','Y') |
| Grant_priv | enum('N','Y') |
| References_priv | enum('N','Y') |
| Index_priv | enum('N','Y') |
| Alter_priv | enum('N','Y') |
| Create_tmp_table_priv | enum('N','Y') |
| Lock_tables_priv | enum('N','Y') |

只有当用户需要显式的数据库级别权限时，才会出现在此表中。

另一个表，`tables_priv`，保存表级别操作的权限：

| 字段 | 类型 |
| --- | --- |
| Host | char(60) |
| Db | char(64) |
| User | char(16) |
| Table_name | char(64) |
| Granter | char(77) |
| Timestamp | timestamp |
| Table_priv | set('Select', 'Insert', 'Update', 'Delete', 'Create', 'Drop', 'Grant', 'References', 'Index', 'Alter') |
| Column_priv | set('Select', 'Insert', 'Update', 'References') |

与 `db` 表类似，只有当用户需要表级别权限时，用户才会出现在此表中。

最后一个表，`columns_priv`，包含列级别的访问定义，其结构如下：

| 字段 | 类型 |
| --- | --- |
| Host | char(60) |
| Db | char(64) |
| User | char(16) |
| Table_name | char(64) |
| Column_name | char(64) |
| Timestamp | timestamp |
| Column_priv | set('Select', 'Insert', 'Update', 'References') |

为什么你需要知道这些每个表的内部细节？如果你想在不使用 `GRANT` 或 `REVOKE` 的情况下添加或移除访问权限，你必须针对这些核心表使用标准的 `INSERT`、`UPDATE` 和 `DELETE` 命令。

首先要在数据库中创建一个用户，无论访问级别如何，该用户必须存在于 `user` 表中：

```sql
INSERT INTO mysql.user (Host, User, Password) VALUES ('localhost', 'testuser6', PASSWORD('testpass6'));
```

请注意，这里使用了 `PASSWORD()` 函数，而在 `GRANT` 语法中不使用。`GRANT` 命令会自动使用 `PASSWORD()` 函数对密码进行加密；像这样的手动插入不会这样做，因此你必须自己加密它。

要添加访问权限，只需向相应的表插入一行，将每个所需的权限列指定为 Y。要为新建用户授予 VehicleInventory 数据库的数据库级别 SELECT、UPDATE、INSERT 和 DELETE 权限，请使用以下命令：

```sql
INSERT INTO mysql.db (Host, Db, User, Select_priv, Insert_priv, Update_priv, Delete_priv) VALUES ('localhost', 'VehicleInventory', 'testuser6', 'Y', 'Y', 'Y', 'Y');
```

如果你需要撤销用户权限，只需在所需的表上执行 DELETE。要移除 testuser6 的数据库级别权限，请使用此查询：

```sql
DELETE FROM mysql.db WHERE Host='localhost' AND User='testuser6';
```

完全从数据库中移除用户稍微复杂一点。你必须先移除授予该用户的所有权限，然后可以使用 DELETE 命令将其从用户表中移除。

为了让 MySQL 意识到你刚刚手动更改的权限，你必须重新加载权限表：

```sql
FLUSH PRIVILEGES;
```

如果在更改访问权限后没有刷新权限，直到下次重启时 MySQL 才会反映这些更改。这适用于你对任何访问级别手动进行的任何权限更改——使用 `GRANT` 或 `REVOKE` 不需要重新加载权限表。

## 服务器限制

限制服务器访问的另一种方式，在更大规模上，实际上是限制服务器整体的远程访问。如果你的数据库仅服务于直接登录机器的用户，那么让服务器接受远程网络连接的需求很小。要停止 MySQL 监听传入的网络连接，请确保以下内容存在于 MySQL 配置文件（通常是 `my.cnf`）的 `[mysqld]` 部分中：

```ini
[mysqld]
skip-networking
```

将该语句添加到配置文件中，然后重新启动 MySQL 服务器进程，将禁用任何传入 MySQL 的流量。如果你的网络和服务安全性很重要，并且只有本地账户需要访问，那么这种措施非常重要。

## 分析数据库

尽管你使用数据库的时间大部分将花费在添加、更新、检索和删除数据上，但偶尔你需要立即了解数据库结构本身的信息。幸运的是，MySQL 提供一些易于使用的信息工具，以及分析和优化数据库的简单方法。

在 MySQL 命令 shell 内部，你可以使用几个共享前缀 `SHOW` 的常见命令，以获取关于数据库当前状态的各种信息。以下部分描述了一些更常见的 `SHOW` 命令。

### SHOW COLUMNS

`SHOW COLUMNS` 命令返回表中所有列及其属性的列表。`SHOW COLUMNS` 的一般格式如下：

```sql
SHOW COLUMNS FROM {table} FROM {database}
```

如果你想获取 `New_Vehicle` 表中所有列的列表，你可以使用以下命令：

```sql
SHOW COLUMNS FROM New_Vehicles FROM VehicleInventory;
```

这将返回以下内容：

| 字段 | 类型 | Null | 键 | 默认 | 额外 |
| --- | --- | --- | --- | --- | --- |
| `vehicle_id` | `int(11)` |  | PRI | `NULL` | `auto_increment` |
| `model_id` | `int(11)` | YES |  | `NULL` |  |
| `price` | `decimal(10,2)` | YES |  | `NULL` |  |
