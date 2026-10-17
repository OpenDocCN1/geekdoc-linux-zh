
# 15 迁移

# Unix 和 Linux 上的 Oracle DBA

### 图 15.3
选择一个要迁移或升级的实例。

![](img/0735bb12e1d45128c662b4b409eb1bf1_426_1.png)

### 图 15.4
验证 `ORACLE_HOME` 目录和 `init.ora` 的位置。

`ODMA` 将暂停几秒钟；您将看到显示正在收集数据库信息的消息。

7. 您现在可以选择迁移类型：默认（Default）或自定义（Custom）。自定义选项最大的好处是它允许您更改数据库名称和国家字符集。选择图 15.5 所示默认选项。

### 图 15.5
选择默认迁移。

![](img/0735bb12e1d45128c662b4b409eb1bf1_427_0.png)

8. `ODMA` 将询问您是否已经备份了数据库。如果已经备份，请点击“下一步（Next）”，如图 15.6 所示。

![](img/0735bb12e1d45128c662b4b409eb1bf1_427_1.png)

图 15.6
您是否已经备份了数据库？

9. 下一个屏幕（如图 15.7 所示）会询问您是否准备好开始迁移或升级。验证设置是否正确，如果准备好继续，请点击“下一步（Next）”。

# Oracle 数据迁移助手：开始迁移或升级
第 15 章

在点击“下一步”开始迁移或升级之前，您可以查看您所选操作的摘要。

| 属性 | 值 |
|---|---|
| 所选的界面 | |
| 从此版本开始升级 | 8.1.6.0 |
| 升级到此版本 | 9.0.1.0 |
| 当前数据库名称 | |
| 新数据库名称 | demo |
| 验证所有 PL/SQL 模块 | 是 |

迁移和升级操作需要一段时间，取决于数据库的大小和计算机的速度。点击“下一步”开始迁移或升级步骤。

![](img/0735bb12e1d45128c662b4b409eb1bf1_428_0.png)

图 15.7
开始迁移。

10. `ODMA` 将最后询问一次您是否准备好继续。它规定，在必要时，它将使用 `SHUTDOWN IMMEDIATE` 关闭数据库。选择“是（Yes）”继续。

![](img/0735bb12e1d45128c662b4b409eb1bf1_428_1.png)

图 15.8
关闭数据库。

11. `ODMA` 会提供迁移或升级过程中的状态；见图 15.9。
您可以预计迁移或升级大约需要 20 分钟到一个小时。记住，`ODMA` 主要处理 `SYSTEM` 表空间内部的数据数据字典，而不是您表中的实际数据。因此，请使用 `SYSTEM` 表空间中的对象数量来估算所需时间，而不是数据库的 GB 字节大小。

12. `ODMA` 将提议用新版本更新 `listener.ora` 中的数据库条目。如果您愿意，也可以手动执行此。

13. 最后一个屏幕将注明进程已完成。完成后，点击“完成（Finish）”退出工具。

# Unix 和 Linux 上的 Oracle DBA

迁移过程现在应该已经完成。接下来，您需要执行迁移后任务。

![](img/0735bb12e1d45128c662b4b409eb1bf1_429_0.png)

图 15.9
`ODMA` 状态

# 迁移后任务

在理想情况下，迁移一切顺利。如果过程中出现问题，您可能需要从备份中恢复。然而，即使一切看起来都按计划进行，您仍然需要执行以下步骤。注意这些步骤与您在升级后必须执行的步骤非常相似：

- 检查 `ORACLE_HOME/assistants/dbma/log/demo` 目录下的日志。使用 `grep` 作为快速搜索 Oracle 错误的方法，如下：

```bash
$ pwd

/u01/app/oracle/product/9.0.1/assistants/dbma/log/demo

$ grep -i ora
```

- 在迁移期间，`ODMA` 会检查旧的 `init.ora`，移除过时的参数，并将修改后的版本放在新的 `ORACLE_HOME` 中。实际文件不是软链接。带有过时参数的旧副本仍存在于 `ORACLE_BASE/admin/SID/file` 中，且 `ORACLE_HOME` 中的软链接也将存在。
- 为旧的 `init.ora` 创建一个备份副本，然后删除 `ORACLE_HOME` 中的软链接。执行这些步骤是因为你想减少使用旧软件重启数据库的可能性。

# 迁移
第 15 章

```bash
$ cd $ORACLE_BASE/admin/demo/file

$ ls

initdemo.ora

$ cp initdemo.ora initdemo-816.ora

$ rm initdemo.ora

$ cd /u01/app/oracle/product/8.1.6/dbbs

$ ls -l initdemo.ora

lrw-xr-wx 1 oracle dba 45 Feb 17 10:44 initdemo.ora -> /u01/app/oracle/admin/demo/file/initdemo.ora
```

接下来，将 `ORACLE_HOME` 中修改后的 `init.ora` 移动到 `ORACLE_BASE/admin/SID/file`。然后，在 `ORACLE_HOME` 中创建一个指向 `ORACLE_BASE/admin/SID/file` 中 `init.ora` 的软链接。这种方式将始终使用更新后的 `init.ora`。

```bash
$ cp $ORACLE_BASE/admin/demo/file /u01/app/oracle/product/9.0.1/dbbs/initdemo.ora

$ ls

initdemo-816.ora initdemo.ora

$ cd /u01/app/oracle/product/9.0.1/dbbs

$ ln -s $ORACLE_BASE/admin/demo/file/initdemo.ora

$ ls -l initdemo.ora

lrw-xr-wx 1 oracle dba 45 Jul 3 21:27 initdemo.ora -> /u01/app/oracle/admin/demo/file/initdemo.ora
```

# 注意
服务器参数文件

Oracle 9 允许用二进制副本 `spfile.ora` 替换文本的 `init.ora` 文件。您可以创建 `SPFILE`，也可以继续使用文本的 `init.ora` 文件。使用这种类型文件的优点以及如何创建它见第 19 章“9i 新特性”。

3. 检查 `init.ora`；`ODMA` 应该删除了过时参数。您可以使用 `diff` 比较文件。
`$ diff initdemo-816.ora initdemo.ora`

4. 设置 `init.ora` 中的 `COMPATIBLE` 参数以表示新版本。注意此值未由 `ODMA` 更新。在这种情况下，您需要将其设置为 `COMPATIBLE=9.0.0`。

![](img/0735bb12e1d45128c662b4b409eb1bf1_430_0.png)

# Unix 和 Linux 上的 Oracle DBA

5. 如图 15.10 所示使用新的 Oracle 启动数据库。在验证迁移成功，使用 `STARTUP RESTRICT` 防止其他用户登录。

![](img/0735bb12e1d45128c662b4b409eb1bf1_431_0.png)

图 15.10
使用新软件启动数据库。

注意为什么您必须使用 `sqlplus / as sysdba`？因为 `connect internal` 不再支持，在 9i 中无法工作。

6. 检查 alert 日志中的错误。

```
$ pwd

/u01/app/oracle/admin/demo/bdump

$ ls "alert"

alert.demo.log
```

7. 运行 `$ORACLE_HOME/rdbms/admin/utlrp.sql` 来重新编译无效对象。

```sql
SQL> @$ORACLE_HOME/rdbms/admin/utlrp.sql
```

8. 检查无效对象并根据需要重新编译它们。如有需要，使用第 5 章介绍的动态 SQL。

```sql
SQL> select owner, count(*) from dba_objects
   2 where status = 'INVALID'
   3 group by owner;
```
OWNER COUNT(*)
CTXSYS 3
MDSYS 15
ORDSYS 159
SYS 216

# 迁移
第 15 章

9. 检查索引状态。查找任何因迁移而变为不可用的位图索引（bitmap indexes）。如有必要，重建它们。

```sql
SQL> select owner, index_name, table_name from dba_indexes
2 where index_type = 'BITMAP' and status = 'UNUSABLE';
```
