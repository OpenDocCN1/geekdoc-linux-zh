
LOAD_TO_FILE 001 +00000000 成功。
LOAD_TO_FILE 002 +00000000 成功。
PARTITION 001 +00000000 成功。
PARTITION 002 +00000000 成功。
PRE_PARTITION 000 +00000000 成功。

分区代理摘要：
已读取行数 = 32
已拒绝行数 = 0
已分区行数 = 32

## 装载时使用 ALLOW READ ACCESS 的示例

ALLOW READ ACCESS 选项在装载大量数据时非常有用，因为它几乎始终允许用户访问表数据，即使在装载操作正在进行或装载操作失败之后也是如此。在 ALLOW READ ACCESS 模式下，装载操作的行为与应用程序的隔离级别无关。也就是说，任何隔离级别的读取方始终可以读取原有数据，但在装载操作完成之前，它们无法读取新装载的数据。

除了最后阶段之外，整个装载操作期间都提供读访问。在数据提交之前，装载实用程序会在表上获取排他锁（Z-lock）。装载实用程序将一直等待，直到所有持有该表锁的应用程序释放锁。这可能会导致数据提交出现延迟。可以使用 LOCK WITH FORCE 选项强制冲突的应用程序退出，使装载操作无需等待即可继续。

在示例 5-35 中，首先我们创建名为 LOADREAD 的表，然后插入三行作为已有数据；接着，我们将使用 ALLOW READ ACCESS 从 DEL 格式的源文件装载其他行，并且在装载进行的同时尝试从另一个会话访问该表。

### 示例 5-35 使用 ALLOW READ ACCESS 装载数据

```
db2inst1@DBLNX08:"/itso> db2 "create table loadread(col1 int not null primary key, col2 char(10))"
DB20000I The SQL command completed successfully.
db2inst1@DBLNX08:"/itso> db2 "insert into loadread values(1,'aaaa'),(2,'bbbb'),(3,'cccc')"
DB20000I The SQL command completed successfully.
```

```
db2inst1@UDBLNX08:"/itso> db2 "load from loadapp.del of del insert into loadread allow read access"
```

| 代理类型 | 节点 | SQL 代码 | 结果 |
|---|---|---|---|
| LOAD | 000 | +00000000 | 成功。 |
| LOAD | 001 | +00000000 | 成功。 |
| LOAD | 002 | +00000000 | 成功。 |
| PARTITION | 001 | +00000000 | 成功。 |
| PRE_PARTITION | 000 | +00000000 | 成功。 |
| 结果： | 3/3 个 LOAD 均成功完成。 | | |

分区代理摘要：
已读取行数 = 2
已拒绝行数 = 0
已分区行数 = 2

装载代理摘要：
已读取行数 = 2
已跳过行数 = 0
已装载行数 = 2
已拒绝行数 = 0
已删除行数 = 0
已提交行数 = 2

当发出 LOAD 命令并且装载正在运行时，我们可以打开另一个会话，以只读操作访问同一个表。在装载操作即将结束前，示例中的 SELECT 语句会很快返回结果集。但当装载操作处于最后阶段、装载尚未像前一个示例那样返回成功消息时，由于与装载操作发生资源争用，SELECT 语句无法成功执行。此时，装载实用程序需要在数据提交之前获取表上的排他锁（Z-lock）（参见示例 5-36）。

装载操作完成后，新装载的数据对其他应用程序可见。

### 示例 5-36 并发访问正在执行装载的表

```
db2inst1@UDBLNX08:"/itso> db2 "select * from loadread"
```

COL1 COL2

### 示例 5-38 并发应用程序被 LOAD 操作强制退出

```
db2inst0@DBLNX08:"/itso> db2 "select * from loadread"

COL1        COL2
------------ ------------
1           aaaa
2           bbbb
3           cccc

3 record(s) selected.

db2inst0@DBLNX08:"/itso> db2 "select * from loadread"
SQL1224N  A database agent could not be started to service a request, or was terminated as a result of a database system shutdown or a force command.
SQLSTATE=55032
```

如果指定了 REPLACE 选项，则不支持 ALLOW READ ACCESS 选项，否则会返回错误代码 SQL3340N 且原因代码为 1。由于 LOAD REPLACE 操作在装载新数据之前会截断现有的表数据，因此在装载操作完成之前没有原有数据可供查询。

对于从 CLP 启动的分区数据库装载操作，消息文件不会显示在控制台中，也不会被保留。要在分区数据库装载完成后保存或查看这些文件的内容，必须指定 LOAD 命令的 MESSAGES 选项。建议使用完全限定的 MESSAGES 文件名，例如 /db2home/db2inst1/myload.msg。

如果使用了 MESSAGES 选项，装载操作完成后，每个分区上的消息文件都会被传输到客户端计算机，并使用 MESSAGES 选项指定的基名称存放在文件中。对于分区数据库装载操作，与生成该文件的装载进程相对应的文件名列于表 5-1 中。

## 表 5-1 分区 LOAD 操作生成的消息文件类型

| 进程类型 | 文件名 |
|---|---|
| Load Agent | <message-file-name>.-load.<partitionnumber> |
| Partitioning Agent | <message-file-name>.-part.<partitionnumber> |
| Pre-partitioning Agent | <message-file-name>.-prep.<partitionnumber> |

有关上表中列出的代理类型的更多信息，请参阅 IBM DB2 UDB Data Movement Utilities Guide and Reference V8（SC09-4830）和 IBM DB2 UDB Command Reference V8（SC09-4828）。
