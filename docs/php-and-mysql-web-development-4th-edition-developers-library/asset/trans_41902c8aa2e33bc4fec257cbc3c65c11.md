

可以通过启动服务器时指定 `--default-storage-engine` 选项来配置服务器使用不同的默认引擎。在运行时，您可以通过设置 `storage_engine` 系统变量来更改默认存储引擎。

在 MySQL 5.0 中，服务器配置为知道一组固定的存储引擎，其中一些始终启用，而另一些可能不可用。如果 `CREATE TABLE` 语句指定了一个已知但不可用的存储引擎，MySQL 将使用默认引擎创建表并生成一个警告。例如，如果服务器已知 `ARCHIVE` 引擎但其不可用，当您尝试创建 `ARCHIVE` 表时，您会看到类似以下内容：

```
mysql> CREATE TABLE t (i INT) ENGINE = ARCHIVE;
Query OK, 0 rows affected, 1 warning (0.01 sec)
mysql> SHOW WARNINGS;

+---------+------+------------------------------------+
| Level | Code | Message                            |
+---------+------+------------------------------------+
| Warning | 1266 | Using storage engine MyISAM for table 't' |
+---------+------+------------------------------------+
```

如果您指定了一个未知的存储引擎，将会发生错误。

在 MySQL 5.1 及更高版本中，服务器使用可插拔架构，允许在运行时加载存储引擎。因此，“服务器已知”的概念转变为指“当前已加载的引擎”。如果您创建表但指定了一个未加载的存储引擎，将会发生两个警告：

```
mysql> CREATE TABLE t (i INT) ENGINE = ARCHIVE;
Query OK, 0 rows affected, 2 warnings (0.01 sec)
mysql> SHOW WARNINGS;

+---------+------+---------------------------------------------+
| Level | Code | Message                                     |
+---------+------+---------------------------------------------+
| Warning | 1286 | Unknown table engine 'ARCHIVE'             |
| Warning | 1266 | Using storage engine MyISAM for table 't'  |
+---------+------+---------------------------------------------+
```

要确保表使用特定的存储引擎，请务必包含 `ENGINE` 表选项。由于默认引擎可以更改，如果您省略 `ENGINE`，可能不会得到预期的默认引擎。此外，请验证 `CREATE TABLE` 语句没有产生任何警告，这通常表明指定的引擎不可用，因此使用了默认引擎。

若要防止在您指定的引擎不可用时 MySQL 替换为默认存储引擎，请启用 `NO_ENGINE_SUBSTITUTION` SQL 模式。

要确定表使用哪个存储引擎，请发出 `SHOW CREATE TABLE` 语句并查看输出中的 `ENGINE` 选项：

```
mysql> SHOW CREATE TABLE t\G
*************************** 1. row ***************************
Create Table: CREATE TABLE `t` (
`i` int(11) DEFAULT NULL
) ENGINE=MyISAM DEFAULT CHARSET=latin1
```

存储引擎也可以在 SHOW TABLE STATUS 或 INFORMATION_SCHEMA.TABLES 表的输出中查看。

某些表选项仅适用于特定的存储引擎。例如，`MIN_ROWS = n` 选项对于 MEMORY 表很有用，它可以使 MEMORY 存储引擎优化内存使用：

```
CREATE TABLE mytbl ( ... ) ENGINE = MEMORY MIN_ROWS = 10000;
```

如果 MEMORY 引擎认为 `MIN_ROWS` 的值很大，它可能会分配较大的内存块，以避免进行大量分配调用带来的开销。

`MAX_ROWS` 和 `AVG_ROW_LENGTH` 选项可以帮助您确定 MyISAM 表的大小。默认情况下，MyISAM 创建的表使用内部行指针大小，允许表文件增长到 256TB。如果您指定了 `MAX_ROWS` 和 `AVG_ROW_LENGTH` 选项，这就告诉 MyISAM 它应该使用一个指针大小，使得表至少可以容纳 `MAX_ROWS` 行。

要修改现有表的存储特性，可以在 ALTER TABLE 语句中使用表选项。例如，要将 `mytbl` 从其当前存储引擎更改为 InnoDB，请执行以下操作：

```
ALTER TABLE mytbl ENGINE = InnoDB;
```

有关更改存储引擎的更多信息，请参阅第 2.6.5 节，“修改表结构”。

### 2.6.2.2 临时表创建

如果表尚不存在才创建表，请使用 CREATE TABLE IF NOT EXISTS。您可以使用此语句来处理那些对所需的表是否已预先建立不做假设的应用程序。应用程序可以例行尝试创建表。IF NOT EXISTS 修饰符对于使用 mysql 作为批处理任务运行的脚本特别有用。在这种情况下，普通的 CREATE TABLE 语句效果不佳。任务第一次运行时，它会创建表，但第二次运行时，由于表已存在，会发生错误。如果您使用 IF NOT EXISTS，则不会有这个问题。任务第一次运行时，它会像往常一样创建表。对于第二次及后续运行，表创建尝试会被静默忽略，不会出错。这使得任务可以继续处理，就好像尝试成功了一样。

如果您使用 IF NOT EXISTS，请注意 MySQL 不会比较 CREATE TABLE 语句中的表结构与现有表的结构。如果存在具有给定名称但结构不同的表，该语句不会失败。如果这是您不希望承担的风险，最好改用 DROP TABLE IF EXISTS 后跟不带 IF NOT EXISTS 的 CREATE TABLE。

### 2.6.2.3 临时表

如果在表创建语句中添加 **TEMPORARY** 关键字，服务器将创建一个临时表，该表在您的服务器连接终止时自动消失：

```
CREATE TEMPORARY TABLE tbl_name ...;
```

这很方便，因为您不必麻烦地发出 **DROP TABLE** 语句来删除表，而且如果您的连接异常终止，表也不会残留。例如，如果您有一个存储在批处理文件中的复杂查询，并使用 **mysql** 运行它，而您决定不等待其完成，您可以放心地终止脚本，服务器将删除脚本创建的任何 **TEMPORARY** 表。

若要使用特定存储引擎创建临时表，请在 **CREATE TEMPORARY TABLE** 语句中添加 **ENGINE** 表选项。

虽然服务器在您的客户端会话结束时自动删除 **TEMPORARY** 表，但您可以在完成后立即显式删除它，以便服务器释放与其相关的任何资源。如果会话将持续一段时间，特别是对于临时 **MEMORY** 表，这是一个好主意。

**TEMPORARY** 表仅对创建该表的客户端可见。不同的客户端可以各自创建一个同名的 **TEMPORARY** 表而不会冲突，因为每个客户端只能看到它自己创建的表。

**TEMPORARY** 表的名称可以与现有的永久表相同。这不是错误，现有的永久表也不会被覆盖。相反，在 **TEMPORARY** 表存在期间，永久表对创建 **TEMPORARY** 表的客户端变得隐藏（不可访问）。假设您在 *sample* 数据库中创建了一个名为 *member* 的 **TEMPORARY** 表。原始的 *member* 表变得隐藏，对 *member* 的引用指向 **TEMPORARY** 表。如果您发出 **DROP TABLE member** 语句，**TEMPORARY** 表被删除，原始的 *member* 表“重新出现”。如果您没有删除 **TEMPORARY** 表就断开与服务器，服务器会自动为您删除它。下次连接时，原始的 *member* 表再次可见。（如果您将隐藏该表的 **TEMPORARY** 表重命名为不同的名称，原始表也会重新出现。）

名称隐藏机制仅工作于一层。也就是说，您不能创建两个同名的 **TEMPORARY** 表。

在考虑是否使用 **TEMPORARY** 表时，请牢记以下注意事项：

-   如果您的客户端程序在连接丢失时自动重新连接到服务器，当您重新连接时，任何 **TEMPORARY** 表都将消失。如果您正在使用 **TEMPORARY** 表来“隐藏”同名永久表，那么永久表现在将变为您使用的表。例如，在未检测到重新连接后执行的 **DROP TABLE** 将删除永久表。为避免此问题，请改用 **DROP TEMPORARY TABLE**。
-   因为 **TEMPORARY** 表仅对创建它们的连接可见，如果您使用不保证每个语句使用相同连接的连接池机制，它们就不起作用。

