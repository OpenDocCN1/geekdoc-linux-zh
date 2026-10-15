

## 5.3.2 将文件导入数据库表或视图

IMPORT 实用程序将输入文件中的数据插入到表或可更新视图中。如果接收导入数据的表或视图已包含数据，则可以替换或追加到现有数据。

如果输入文件的格式为 IXF（Integrated eXchange Format），您还可以使用 import 创建新表。

使用 import 运行是否带创建新表选项所需的权限和特权是不同的。要使用 import 实用程序创建新表，您必须具有 SYSADM 权限、DBADM 权限，或数据库的 CREATETAB 特权。要替换现有表或视图中的数据，您必须具有 SYSADM 权限、DBADM 权限，或表或视图的 CONTROL 特权。要向现有表或视图追加数据，您必须具有表或视图的 SELECT 和 INSERT 特权。

import 实用程序可以通过命令行处理器（CLP）、Control Center 中的 Import 笔记本或应用程序编程接口（API），sqldmpr 来调用。您还可以为 IMPORT 实用程序指定 MESSAGES 参数，以记录与 IMPORT 操作相关的错误、警告和信息性消息。

> 注意：如果针对远程数据库的导入操作生成的输出消息量超过 60 KB，该实用程序将保留前 30 KB 和后 30 KB。

### 示例 5-28 通过 DB2 CLP 使用 IMPORT

```
db2inst1@UDLBNX08:/db2home/db2inst1> db2 "create table emp4imp like emp"
DB20000I  The SQL command completed successfully.
db2inst1@UDLBNX08:/db2home/db2inst1> db2 "import from ./itso/datmov/emp.ixf of ixf commitcount 20000 messages emp4imp.msg insert into emp4imp"

Number of rows read       = 100000
Number of rows skipped    = 0
Number of rows inserted   = 100000
Number of rows updated    = 0
Number of rows rejected   = 0
Number of rows committed  = 100000
```

在前面的示例（示例 5-28）中，使用了 COMMITCOUNT 参数。这意味着 DB2 将在每导入 n 条记录后执行一次 COMMIT。如果在使用 COMMITCOUNT 参数时导入因某种原因被中断，已提交的行仍将保留在目标表中，尽管导入过程失败。对于这种情况，您可以使用 REPLACE 或 REPLACE_CREATE 选项通过截断数据对象来删除表中的所有现有数据并插入导入的数据。或者您也可以使用指定了 RESTARTCOUNT 参数的 INSERT 选项，以避免重新导入已存在于表中的行。在示例 5-29 中，使用了 MESSAGES 参数来监控导入操作的状态。您可以检查生成的消息文件，该文件为 ASCII 格式。

### 示例 5-29 通过消息文件监控 IMPORT 进程

```
db2inst1@UDBLNX08:> tail -f emp4imp.msg
SQL3153N  The T record in the PC/IXF file has name "emp.ixf", qualifier "", and source "".

SQL3109N  The utility is beginning to load data from file "./itso/datmov/emp.ixf".

SQL3221W  ...Begin COMMIT WORK. Input Record Count = "20000".
SQL3222W  ...COMMIT of any database changes was successful.

SQL3221W  ...Begin COMMIT WORK. Input Record Count = "40000".
SQL3222W  ...COMMIT of any database changes was successful.

SQL3221W  ...Begin COMMIT WORK. Input Record Count = "60000".
SQL3222W  ...COMMIT of any database changes was successful.

SQL3221W  ...Begin COMMIT WORK. Input Record Count = "80000".
SQL3222W  ...COMMIT of any database changes was successful.

SQL3221W  ...Begin COMMIT WORK. Input Record Count = "100000".
SQL3222W  ...COMMIT of any database changes was successful.

SQL3110N  The utility has completed processing. "100000" rows were read from the input file.

SQL3221W  ...Begin COMMIT WORK. Input Record Count = "100000".
SQL3222W  ...COMMIT of any database changes was successful.

SQL3149N  "100000" rows were processed from the input file. "100000" rows were successfully inserted into the table. "0" rows were rejected.
```

与 EXPORT 类似，我们也可以使用 DB2 Control Center 来调用 IMPORT 实用程序。要在 Control Center 中打开 Import 笔记本：

- 1. 从 Control Center 开始，展开对象树直到找到 Tables 文件夹。

