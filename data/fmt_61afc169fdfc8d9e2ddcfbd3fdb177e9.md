
在使用 `GRANT` 命令时，你不需要预先加密密码作为密码——`MySQL` 会在将其存储在系统中之前自动加密密码。

现在你将看到一些如何使用 `USE` `GRANT` 的通用示例，你可以在实际数据库上尝试。你将向车辆库存数据库添加三个用户。一个用户将获得整个数据库的完全访问权限。第二个将获得对 `New_Vehicles` 表的 `SELECT`、`UPDATE`、`INSERT` 和 `DELETE` 访问权限。第三个也是最后一个用户将获得对 `New_Vehicles` 表中颜色列的仅 `SELECT` 访问权限。首先，创建拥有数据库中所有权限的用户：

```sql
GRANT ALL PRIVILEGES ON VehicleInventory.* TO testuser1@localhost IDENTIFIED BY ‘testpass1’;
```

接下来，创建具有有限表级权限的用户：

```sql
GRANT SELECT, INSERT, UPDATE, DELETE ON VehicleInventory.New_Vehicles TO testuser2@localhost IDENTIFIED BY ‘testpass2’;
```

最后，创建具有极其有限访问权限的第三个用户：

```sql
GRANT SELECT (color) ON VehicleInventory.New_Vehicles TO testuser3@localhost IDENTIFIED BY ‘testpass3’;
```

## 使用 `REVOKE`

现在你可以使用 `GRANT` 命令创建用户和权限，但你仍然需要一种方式来撤销权限。为此，你使用 `REVOKE`。`REVOKE` 命令看起来与 `GRANT` 命令几乎完全一样：

```sql
REVOKE [权限] ON [资源] FROM [身份]
```

注意 `REVOKE` 和 `GRANT` 语法之间唯一的真正区别：使用单词 `FROM` 代替 `TO`，并且不需要添加 `IDENTIFIED BY` 短语。

为了快速查看 `REVOKE` 在实时数据库上的运行情况，请尝试以下查询：

```sql
REVOKE ALL PRIVILEGES ON VehicleInventory.New_Vehicles FROM testuser2@localhost;
```

用这一快速操作，你就撤销了 testuser2 账户拥有的任何权限。在撤销权限时，你通常必须列出用户拥有明确权利的具体表、数据库和列。如果你使用的是 `MySQL` 4.1.2 或更高版本，你可以用一个快速命令在任何权限级别快速清除用户的所有权限：

```sql
REVOKE ALL PRIVILEGES, GRANT OPTION FROM [身份]
```

如果你想要从系统中彻底删除 testuser3，你会发送以下内容：

```sql
REVOKE ALL PRIVILEGES, GRANT OPTION FROM testuser3@localhost;
```

### `GRANT` 和 `REVOKE` 的替代方案

如果由于某种原因，你不想使用 `GRANT` 或 `REVOKE` 命令，你可以手动创建用户并直接将权限应用于 `MySQL` 访问表。

`MySQL` 在内置的 `mysql` 数据库内的四个主要表中存储不同级别的用户权限。这四个主要访问表中的每一个都对应于四个不同的访问级别。

在全局级别，有 `user` 表，其结构如下：

| 字段 | 类型 |
| :--- | :--- |
| 主机 | varchar(60) |
| 用户 | varchar(16) |
| 密码 | varchar(41) |
| 选择权限 | enum('N','Y') |
| 插入权限 | enum('N','Y') |
| 更新权限 | enum('N','Y') |
| 删除权限 | enum('N','Y') |
| 创建权限 | enum('N','Y') |
| 丢弃权限 | enum('N','Y') |
| 重新加载权限 | enum('N','Y') |
| 关闭权限 | enum('N','Y') |
| 进程权限 | enum('N','Y') |
| 文件权限 | enum('N','Y') |
| 授予权限 | enum('N','Y') |
| 引用权限 | enum('N','Y') |
| 索引权限 | enum('N','Y') |
| 修改权限 | enum('N','Y') |
| 显示数据库权限 | enum('N','Y') |
| 超级权限 | enum('N','Y') |
| 创建临时表权限 | enum('N','Y') |
| 锁定表权限 | enum('N','Y') |
| 执行权限 | enum('N','Y') |
| 复制从属权限 | enum('N','Y') |
| 复制客户端权限 | enum('N','Y') |
| ssl类型 | enum('','ANY','X509','SPECIFIED') |
| ssl密码 | Blob |
| x509颁发者 | Blob |
| x509主题 | Blob |
| 最大查询数 | int(11) 无符号 |
| 最大更新数 | int(11) 无符号 |
| 最大连接数 | int(11) 无符号 |

`user` 表包含系统中所有用户的列表，以及该用户可能拥有的任何全局权限。与访问权限相关的关键字段是所有带有后缀 _priv 的列。请注意，所有权限列的默认值均为 `no`。

`db` 表保存任何数据库级别访问权限的记录。`db` 的结构如下：

| 字段 | 类型 |
| --- | --- |
| 主机 | varchar(60) |
| 数据库 | varchar(64) |
| 用户 | varchar(16) |
| 选择权限 | enum('N','Y') |
| 插入权限 | enum('N','Y') |
| 更新权限 | enum('N','Y') |
| 删除权限 | enum('N','Y') |
| 创建权限 | enum('N','Y') |
| 丢弃权限 | enum('N','Y') |
| 授予权限 | enum('N','Y') |
| 引用权限 | enum('N','Y') |
| 索引权限 | enum('N','Y') |
| 修改权限 | enum('N','Y') |
| 创建临时表权限 | enum('N','Y') |
| 锁定表权限 | enum('N','Y') |

只有当用户需要显式的数据库级别权限时，才会显示在此表中。

另一个表 `tables_priv` 保存表级别操作的权限：

| 字段 | 类型 |
| :--- | :--- |
| 主机 | char(60) |
| 数据库 | char(64) |
| 用户 | char(16) |
| 表名 | char(64) |
| 授予者 | char(77) |
| 时间戳 | timestamp |
| 表权限 | set('Select', 'Insert', 'Update', 'Delete', 'Create', 'Drop', 'Grant', 'References', 'Index', 'Alter') |
| 列权限 | set('Select', 'Insert', 'Update', 'References') |

与 `db` 表一样，只有当用户需要表级别权限时，才需要出现在此表中。

最后一个表 `columns_priv` 包含列级别的访问定义，看起来像这样：

| 字段 | 类型 |
| :--- | :--- |
| 主机 | char(60) |
| 数据库 | char(64) |
| 用户 | char(16) |
| 表名 | char(64) |
| 列名 | char(64) |
| 时间戳 | timestamp |
| 列权限 | set('Select', 'Insert', 'Update', 'References') |

你为什么要知道这些每个表的详细情况？如果你想在不使用 `GRANT` 或 `REVOKE` 的情况下添加或移除访问权限，你必须对这些核心表使用标准的 `INSERT`、`UPDATE` 和 `DELETE` 命令。

首先，要在数据库中创建用户，无论访问级别如何，他们都必须存在于 `user` 表中：

```sql
INSERT INTO mysql.user (Host, User, Password) VALUES ('localhost', 'testuser6',
PASSWORD('testpass6'));
```

注意这里使用了 `PASSWORD()` 函数，而在 `GRANT` 语法中不使用。`GRANT` 命令自动使用 `PASSWORD()` 函数对密码进行加密；像这样的手动插入则不会，因此你必须自己对其进行加密。

## 高级 MySQL

## 第 4 章
