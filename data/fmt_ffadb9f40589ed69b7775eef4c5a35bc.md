
正如预期的那样，外键检查发现该值不在 *Models* 表中，并拒绝允许插入该行。你设法阻止了带有不良数据的新行，但那些正在被修改的现有行呢？尝试此查询：

```sql
UPDATE New_Vehicles SET model_id=12345 WHERE vehicle_id=1;
```

正如你所见，外键也会阻止错误的更新：

```
ERROR 1216 (23000): Cannot add or update a child row: a foreign key constraint fails
```

因此，外键成功地保护了表免受有害的 INSERT 和 UPDATE 操作，但当 *Models* 表中的值发生变化时会发生什么？请查看以下查询，其中你尝试更改一个现有的 *model_id*：

```sql
UPDATE Models SET model_id=123 WHERE model_id=1;
```

当你运行此查询时，你应该会得到以下错误：

```
ERROR 1217 (23000): Cannot delete or update a parent row: a foreign key constraint fails
```

这个错误仅仅反映了简单 InnoDB 外键相关的另一种行为：如果被引用列的值存在于引用表中，则不能修改该被引用列。如果这不是你想要的行为怎么办？幸运的是，你可以将外键的更新和删除行为指定为五种不同选项之一：`RESTRICT`、`CASCADE`、`SET NULL`、`NO ACTION` 和 `SET DEFAULT`。以下是每种行为含义的简要说明：

-   `RESTRICT` 是默认行为。被引用的值不能被更改或删除。
-   `CASCADE` 允许任何更新向下传播到引用表。如果你更新了 `Models` 表中的 `model_id`，它将级联到 `New_Vehicles` 表并更新任何相应的行。请注意，这也适用于删除（如果指定了）——删除父表中的一行将自动删除子表中引用该值的所有行。
-   `SET NULL` 在更新父值时将子表中的值更改为 `NULL`。
-   `NO ACTION` 只是告诉数据库允许对父表的更改，并对子表不做任何操作。
-   `SET DEFAULT` 在父值被更改或删除时，将子表中的值更改为其 `DEFAULT` 值。

实现这些行为只需在外键定义的末尾添加所需的 `ON DELETE` 或 `ON UPDATE` 子句，如下所示：

```sql
ALTER TABLE [tablename] ADD CONSTRAINT [key_name] FOREIGN KEY ([indexed_column])
REFERENCES [foreign_table] ([id_column]) ON UPDATE [update behavior] ON DELETE
[delete behavior]
```

要将现有键更改为支持不同的更新和删除行为，你必须先删除旧键，然后使用新行为重新创建外键。要将 `New_Vehicles` 表的外键更改为级联任何更新，并在删除模型时设置为 `NULL`，请使用以下内容：

```sql
ALTER TABLE New_Vehicles DROP FOREIGN KEY refmdl;
ALTER TABLE New_Vehicles ADD CONSTRAINT refmdl FOREIGN KEY (model_id) REFERENCES
Models (model_id) ON UPDATE CASCADE ON DELETE SET NULL;
```

现在，每当 `Models` 表中的 `model_id` 发生变化时，新值就会传播到 `New_Vehicles` 中使用原始值的所有行。请亲自查看：

```sql
UPDATE Models SET model_id=123 WHERE model_id=1;
SELECT * FROM New_Vehicles \G
```

更新将成功，并返回类似以下内容：

```
*************************** 1. row ***************************
vehicle_id: 1
model_id: 123
price: NULL
color: Dark Blue
description: Poplar SUV; great for moving people or cargo across town, or wherever
your adventures may take you.
modelyear: 2005
*************************** 2. row ***************************
vehicle_id: 2
model_id: NULL
price: NULL
color: Graphite Pearl
description: Last of the 2004 stock! Must sell! Loaded, all options!
modelyear: 2004
*************************** 3. row ***************************
vehicle_id: 3
model_id: 4
price: NULL
color: Radiant Red
description: Come drive this popular truck! 4WD, extended cab, many options.
modelyear: 2005
*************************** 4. row ***************************
vehicle_id: 4
model_id: 5
price: NULL
color: Daytona Sunset Orange Metallic
description: The all new C6 Corvette, the next generation of classic American sports cars. 400HP V8; Very fast!
modelyear: 2005
```

### 从 InnoDB 转换回 MyISAM

你体验了 InnoDB 表和外键，但你决定更希望拥有全文搜索功能。转回 MyISAM 是一个相对无痛的过程。通常它只涉及两个步骤：移除任何 InnoDB 特有的功能，如外键，并使用 `ALTER TABLE` 将存储引擎类型改回 MyISAM。要将 `New_Vehicles` 表转回 MyISAM，请执行以下操作：

```sql
ALTER TABLE New_Vehicles DROP FOREIGN KEY refmid1;
ALTER TABLE New_Vehicles ENGINE=MyISAM;
```

此时，`New_Vehicles` 表已改回使用 MyISAM 存储引擎，你再次获得在该表上添加和使用全文索引的能力。

## 访问控制

作为 MySQL 数据库管理员，你将承担的最重要的任务之一是控制谁可以访问系统以及他们可以访问哪些资源。在大多数情况下，你每个数据库只需要少数几个用户帐户，而且你需要创建的帐户应该只授予执行其任务所需的最小访问权限。幸运的是，MySQL 提供了多种方式来控制谁有权访问你的系统以及具体哪些资源。

### 用户管理

为了帮助控制数据库中的用户帐户，MySQL 提供了几种维护用户帐户的方式。无论是协作开发者的帐户、精通技术的客户端帐户，还是系统的基于 Web 的前端，每个用户都需要专门授权以访问他们所需的资源。

# 第 4 章

为实际应用场景配置数据库时，你需要做的第一件事之一就是设置用户或系统本身可能需要的一些账户。为了在数据库中为用户设置专门的访问权限，你需要了解 MySQL 可以控制访问的不同层级。MySQL 4.1 在权限方面可以区分四种不同的访问级别：全局级别、数据库级别、表级别和列级别。

全局级别权限是最强大的权限，适用于运行在 MySQL 实例上的所有数据库。通常，这类权限保留给管理员账户，因为应用程序或最终用户极少需要访问数据库服务器操作的所有方面。

数据库级别权限如其名称所示，应用于数据库级别。数据库级别访问通常由特定数据库或应用程序的管理员使用，它赋予了用户对指定特定数据库的完全控制权。

表级别权限按表为基础进行应用。你可以为用户在特定表或一组表上创建或移除访问权限。这种访问控制级别通常在配置数据库以便应用程序直接访问时使用——应用程序只需对每个表拥有特定类型的访问权限，而不需要更多。

列级别权限是 MySQL 提供的最精细的控制级别。正如你所料，它控制对给定表中特定列或列组的访问。

#### 使用 GRANT

现在你理解了 MySQL 访问系统的不同范围，是时候看看如何实际控制权限了。

为了创建用户账户并添加权限，MySQL 提供了 `GRANT` 命令。`GRANT` 命令相对简单，只要你知道你授予的是什么访问权限以及授予给谁。`GRANT` 命令的通用语法如下：

```
GRANT [privileges] ON [resource] TO [identity]
```
