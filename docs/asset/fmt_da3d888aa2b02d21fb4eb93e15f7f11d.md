
`db2 "create index artno on albums (artno)"`

在 DB2 Control Center 的面板中，右键点击 Indexes。
- 从弹出菜单选择 Create。
- 指定以下内容：
  - 索引名称：`artno`。
  - 表架构：`Instnn`。
  - 表名：`ALBUMS`。
  - 从可用列选择 `ARTNO` 并按 `>` 按钮将其移动到选中列中。
  - 如果 Unique 复选框已勾选，请取消。
  - 点击 OK。

执行 REBIND 以考虑新的访问路径。记录你的命令。记住在运行 rebind 之前连接到数据库。
提示：`db2 connect to musicdb`
`db2 rebind package myapp`

### 14. rebind 使用工作站上的原始 bnd 文件吗？
答。`REBIND` 不使用绑定文件。它只是导致数据库管理器优化包中的 SQL 语句。结果包的时间戳值不会更改。当源代码没有任何更改，但由于优化器可以使用新信息而希望重新优化过程时，`REBIND` 是非常有用的。

### 15. 在 Explained Statements History 窗口中，刷新视图。如何判断哪个是最新版本？
提示：在 Explained Statements History 中，点击菜单栏上的 view。
答。出现了另一个 `MYAPP` 版本。你可以通过 Latest Bind 为 Yes 来识别最新版本，或者查看 Explain Time。

### 16. 查看 `Latest Bind = Yes` 包的访问策略。
访问策略是否发生了变化？即使你在运行 `explain` 之前已经完成了 `REBIND`，你能够肯定地说说访问策略是合适的吗？
答。在“已解释语句历史”（Explained Statements History）中，右键点击 `Latest Bind = Yes` 的 `MYAPP` 副本，选择“显示访问计划”（Show Access Plan）。你可能需要通过缩小或使用概览窗口来调整视图以查看整个计划。

访问策略已经发生了变化。新的访问计划显示优化器选择了访问 `ARTNO` 中的新索引。你会看到一个排序（sort）和一个 RIDSCAN（RID扫描，RID扫描）——这标识了列表预取（List Prefetch）。现在有两个排序：一次按 RID 序列对选定的索引项进行排序，第二次按 `ARTNO` 顺序返回数据行。优化器选择列表预取是因为，对使用新索引访问 `ALBUMS` 表的效率进行准确估计，需要收集统计信息。此时，由于索引刚刚创建，`ARTNO` 索引的统计信息肯定尚未收集。此外，尚未确定是否更新了任何统计信息。

### 17. 由于 `ARTNO` 索引刚刚创建，你可以说明该索引的统计信息尚未收集（尽管 `CREATE INDEX` 有 `COLLECT STATISTICS` 选项，但我们没有指定它）。检查表统计信息是否更新的简单方法是查询 `SYSSTAT.TABLES` 视图。SQL 语句为：

```
db2 "select card from sysstat.tables where tabname = 'ALBUMS'"
```

### 18. 返回了什么值？它表示什么？
答。返回了值 `-1`。这表示该表尚未收集统计信息。

### 19. 检查是否已收集信息的另一种技术是使用 `REORGCHK`。在你的 telnet 会话中运行以下命令，以在不执行 `RUNSTATS` 的情况下显示应用于你表的公式结果。

```
db2 -r chk.out current statistics on table
```
