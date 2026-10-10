
### 图 5.20 `SYSCAT.TABLES` 检查等待状态

对应于已加载表的 `SYSCAT.TABLES` 条目的 `STATUS` 标志指示了该表的检查等待状态。`STATUS` 的值必须为 `N`，且 `ACCESS MODE` 的值必须为 `F`，表示表处于正常状态并可以完全访问。

在图 5.20 的示例中，`CALPAR` 和 `CALFOR` 都表示需要检查约束（`STATUS` = `'C'`）。`CALPAR` 是父表，`CALFOR` 是其从表。`CALFOR` 在其一个列上定义了检查约束。在这种情况下，由于两个表都已加载，因此它们都处于检查等待状态。

执行 `SET INTEGRITY` 语句来检查两个表的约束。`CALFOR` 有两行在 `CALPAR` 中没有父键，因此这些行被移动到 `FOREXP` 异常表。`CALPAR` 表没有任何检查违规，因此执行此 `SET INTEGRITY` 语句后没有行添加到 `PAREXP` 表。

## DB2 通用数据库：Linux、UNIX 和 Windows 管理

要移除等待状态，请使用 `SET INTEGRITY` 语句。`SET INTEGRITY` 语句检查表的约束违规，并将表移出等待状态。如果所有加载操作都是以 `INSERT` 模式执行的，可以使用 `SET INTEGRITY` 语句来增量地处理约束（即它将只检查表的追加部分是否存在约束违规）。例如：

```
db2 load from infile.ixf of xf insert into table
db2 set integrity for table immediate checked
```
