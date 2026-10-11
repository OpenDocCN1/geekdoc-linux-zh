
## EXECUTE

```
EXECUTE stmt_name [USING @var_name [, @var_name] ...]
```

执行名为*stmt_name*的预编译语句，该语句先前已通过**PREPARE**进行准备。如果预编译语句包含任何占位符标记，则必须提供**USING**子句。该子句应提供一个逗号分隔的用户变量列表，为语句中的每个连续占位符提供值。

## EXPLAIN

```
EXPLAIN tbl_name [col_name | 'pattern']
```

```
EXPLAIN [EXTENDED | PARTITIONS] select_stmt
```

此语句的第一种形式等同于**DESCRIBE** *tbl_name*。有关更多信息，请参阅**DESCRIBE**语句的描述。

**EXPLAIN**语句的第二种形式提供了有关 MySQL 优化器将为处理紧随**EXPLAIN**关键字之后的**SELECT**语句而生成的查询执行计划的信息。

```
EXPLAIN SELECT score.* FROM score INNER JOIN grade_event
ON score.event_id = grade_event.event_id AND grade_event.event_id = 14;
```

**EXTENDED**选项使**EXPLAIN**产生额外的执行计划信息；请在使用**EXPLAIN**后立即使用**SHOW WARNINGS**来查看此信息。**PARTITIONS**选项（在 MySQL 5.1.5 中引入）生成一个包含分区信息的额外输出列。

如果*select_stmt*在**FROM**子句中包含子查询，**EXPLAIN**必须执行该子查询。这是因为优化器必须知道子查询返回什么，以便确定外部查询的执行计划。

**EXPLAIN**的输出包含一行或多行，具有下列列：

- **id**
  该输出行适用的**SELECT**的 ID 编号。如果语句包含子查询或为**UNION**，则可能存在多个**SELECT**。
- **select_type**
  该输出行适用的**SELECT**类型，如下表所示。

| 类型 | 含义 |
| --- | --- |
| SIMPLE | 没有**UNION**或**子查询部分**的**SELECT** |
| PRIMARY | 最外层或最左侧的**SELECT** |
| UNION | **UNION**中第二个或后续的**SELECT** |
| DEPENDENT UNION | 类似于**UNION**，但**依赖于**外部**查询** |
| UNION RESULT | **UNION**的结果 |
| SUBQUERY | 子查询中的第一个**SELECT** |
| DEPENDENT SUBQUERY | 类似于**SUBQUERY**，但依赖于外部查询 |
| DERIVED | **FROM**子句中的子查询 |

- **table**
  输出行所指的表。
- **partitions**
  将使用的分区。只有当存在**PARTITIONS**选项时，才显示此列。对于非分区表，值为 NULL。
- **type**
  MySQL 将执行的连接类型。可能的类型从最佳到最差依次为：system, const, eq_ref, ref, ref_or_null, index_merge, unique_subquery, index_subquery, range, index, 和 ALL。越好的类型限制越严格，意味着 MySQL 在执行检索时需要检查表中的行数更少。
- **possible_keys**
  MySQL 认为可用于查找**table**列中指定表中的行索引的候选项。值为 NULL 表示未找到索引。
- **key**
  MySQL 实际用于在表中查找行的索引。（如果 MySQL 使用 index_merge 连接类型，这里可能会列出几个键，因为该优化使用多个索引来处理查询。）值为 NULL 表示将不使用索引。
- **key_len**
  将使用多少索引长度。如果 MySQL 将使用索引的最左侧前缀，这将小于完整的索引行长度。
- **ref**
  MySQL 将与其比较索引值的值。单词 const 或 '???' 表示与常量进行比较；列名表示列对列的比较。
- **rows**
  为了执行查询，MySQL 必须检查的表中行的估计数量。此列中值的乘积是必须从所有表检查的行组合总数的估计值。
- **Extra**
  关于执行计划的其他信息。值可以为空，或包含一个或多个值，例如以下值：
  - *Using filesort*：索引值需要写入文件并排序，以便以排序顺序检索关联的行。
  - *Using index*：MySQL 可以使用仅索引中的信息而无需检查数据文件即可检索表的信息。
  - *Using temporary*：必须创建临时表。
  - *Using where*：SELECT 语句 WHERE 子句中的信息用于索引处理。

  此字段中可能会出现此处未列出的其他值；请参阅 MySQL 参考手册了解当前的额外值集合。

## FLUSH

```
FLUSH [LOCAL | NO_WRITE_TO_BINLOG] option [, option] . . .
```

刷新服务器使用的各种内部缓存。每个选项值应为以下各项之一：

- **DES_KEY_FILE**
  重新加载由 DES_ENCRYPT() 和 DES_DECRYPT() 函数用于加密和解密的 DES 密钥文件。
- **HOSTS**
  刷新主机缓存。
- **LOGS**
  通过关闭并重新打开日志文件来刷新日志文件。如果启用了二进制日志或中继日志，这会导致打开序列中的下一个文件。对于到文件的错误日志记录，旧文件将被重命名并添加 .old 后缀。
- **MASTER**
  此选项已重命名为 RESET MASTER，应改用该选项。
- **PRIVILEGES**
  重新加载权限表。如果您使用 GRANT 或 REVOKE 修改表，服务器会自动重新加载表的内存副本。如果您使用 INSERT 或 UPDATE 等语句直接修改表，则需要明确告知服务器重新加载它们。此外，此选项对账户资源管理限制具有与 USER_RESOURCES 选项相同的效果。
- **QUERY CACHE**
  刷新查询缓存以进行碎片整理，而不从缓存中移除语句。（若要完全清除缓存，请使用 RESET QUERY CACHE。）
- **SLAVE**
  此选项已重命名为 RESET SLAVE，应改用该选项。
- **STATUS**
  重新初始化服务器状态变量。
- **(TABLE | TABLES) [tbl_name [, tbl_name] ...]**
  如果不指定任何表名，将关闭表缓存中所有打开的表。您可以指定一个可选的逗号分隔的一个或多个表名列表，以刷新特定的表而不是整个表缓存。
  
  如果查询缓存正在运行，FLUSH TABLES 也会刷新查询缓存。
- **TABLES WITH READ LOCK**
  刷新所有数据库中的所有表，然后对它们施加全局读锁，该锁将一直持续到您发出 UNLOCK TABLES 语句。此语句允许客户端读取表，但禁止进行任何更改，这对于获取整个服务器的备份且保证在备份期间没有表发生变化非常有用。从客户端角度来看，这样做的缺点是更新被禁止的时间段更长。
- **USER_RESOURCES**
  重置账户资源管理限制（如 MAX_QUERIES_PER_HOUR）的小时计数器。已达到其限制的账户可以再次进行其活动。此选项不影响任何 MAX_USER_CONNECTIONS 限制；它不是按小时限制的。

如果启用了二进制日志记录，除非指定了 LOCAL 或 NO_WRITE_TO_BINLOG 选项，否则 MySQL 会将 FLUSH 语句写入二进制日志。

FLUSH 语句需要 RELOAD 权限。

## GRANT

```
GRANT priv_type [ (col_list) ] [, priv_type [ (col_list) ] ] ...
  ON [TABLE | FUNCTION | PROCEDURE]
  (*.* | db_name.* | db_name.tbl_name | tbl_name | db_name.routine_name)
  TO account [IDENTIFIED BY [PASSWORD] 'password']
  [, account [IDENTIFIED BY [PASSWORD] 'password'] ] ...
  [REQUIRE security_options]
  [WITH grant_or_resource_options]
```

GRANT 语句授予一个或多个 MySQL 账户访问权限。要使用此语句，您必须具有 GRANT OPTION 权限，并且必须拥有您试图授予的权限。
