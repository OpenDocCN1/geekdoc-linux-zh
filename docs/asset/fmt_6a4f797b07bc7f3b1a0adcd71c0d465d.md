
```sql
select p.project_id,p.name ,p.segment1
from pa_projects_all p
  (select pcdl.project_id
  from PA_COST_DISTRIBUTION_LINES_ALL pcdl
  UNION
  select pei.project_id
  from pa_expenditure_items_all pei) pv
where (p.project_id = pv.project_id) and
  (p.segment1 = :bl)
```

### 执行计划

```sql
SELECT STATEMENT Cost=321,61 bytes=2745 =
NESTED LOOPS Cost=321,61 bytes=2745 =
TABLE ACCESS BY INDEX ROWID PA_PROJECTS_ALL Cost=2,1 bytes=32 =
INDEX UNIQUE SCAN PA_PROJECTS_U2 Cost=1,1 bytes=
VIEW Cost=,41917 bytes=544921
SORT Cost=321,41917 bytes=149562
UNION-ALL Cost=
INDEX FULL SCAN PA_COST_DISTRIBUTION_LINES_N12 Cost=126,32864
  bytes=131456
TABLE ACCESS FULL PA_EXPENDITURE_ITEMS_ALL Cost=105,9053 bytes=18106
```

在上述示例中，由于存在 `UNION` 操作符，内联视图不可合并的；因此对相邻表 `PA_EXPENDITURE_ITEMS_ALL` 执行了全表扫描。然而，如果可以将视图重写为 `UNION ALL` 操作符而不是 `UNION` 操作符，则可以使用推连接视图功能来提升索引的使用，如下：

```sql
select p.project_id,p.name ,p.segment1
from pa_projects_all p
  (select pcdl.project_id
  from PA_COST_DISTRIBUTION_LINES_ALL pcdl
  UNION ALL
  select pei.project_id
  from pa_expenditure_items_all pei) pv
where (p.project_id = pv.project_id) and
  (p.segment1 = :bl)
```

### 执行计划

```sql
SELECT STATEMENT Cost=3,419 bytes=150884 =
NESTED LOOPS Cost=3,419 bytes=150884 =
TABLE ACCESS BY INDEX ROWID PA_PROJECTS_ALL Cost=2,1 bytes=32 =
INDEX UNIQUE SCAN PA_PROJECTS_U2 Cost=1,1 bytes=
VIEW Cost=,41917 bytes=17668
UNION-ALL PARTITION Cost=
INDEX RANGE SCAN PA_COST_DISTRIBUTION_LINES_N12 Cost=2,115 bytes=460 =
INDEX RANGE SCAN PA_EXPENDITURE_ITEMS_N8 Cost=1,906 bytes=1812
```

执行计划显示 `PA_EXPENDITURE_ITEMS_N8` 是基于 `PROJECT_ID` 列使用的，因为推连接视图将 `project_id` 谓词推入了 `UNION ALL` 的每个分支中。如果你的应用程序包含 `UNION` 操作符的视图且有需要连接的 SQL 语句，可以使用此功能执行计划。在 Oracle 8 和 Oracle 9 中，可以启用顺序嵌套循环优化以提高嵌套循环连接的代价指标。在 CBO 认为嵌套循环连接比排序连接更贵的情况下，当结果集较大时，可以使用顺序嵌套循环优化。

## 4.6 优化器

执行计划显示 `PA_EXPENDITURE_ITEMS_N8` 是基于 `PROJECT_ID` 列使用的，因为推连接视图将 `project_id` 谓词推入了 `UNION ALL` 的每个分支中。如果你的应用程序包含 `UNION` 操作符的视图且有需要连接的 SQL 语句，可以使用此功能执行计划。在 Oracle 8 和 Oracle 9 中，可以启用顺序嵌套循环优化以提高嵌套循环连接的代价指标。在 CBO 认为嵌套循环连接比排序连接更贵的情况下，当结果集较大时，可以使用顺序嵌套循环优化。

该功能对于以前使用 RBO 并迁移到 CBO 的应用程序极其有用。在 RBO 中，许多开发者通常会使用 `+0` 或 `||` 来禁用非选择性索引或强制执行特定的连接顺序。如果应用程序以前完全基于 RBO，可能存在大量的 SQL 语句，通过这种经典的 RBO 技术，不需要从所有 SQL 语句中手动删除 `+0` 和 `||` 即可减少 CBO 的影响。

另一个在 8.1.6 中添加的 CBO 功能允许优化器将连接谓词推入 `UNION` 视图内部。由于包含 `UNION` 或 `UNION ALL` 等集合操作符的视图是不可合并的，此功能允许优化器将连接谓词推入包含 `UNION ALL` 操作符的不可合并视图。这提高了连接到包含 `UNION ALL` 操作符的视图的查询执行性能。可以通过设置 init.ora 参数 `_push_join_union_view=TRUE` 来启用推连接视图功能。接接示例说明了推连接视图功能的使用。

```sql
select p.project_id,p.name ,p.segment1
from pa_projects_all p
  (select pcdl.project_id
  from PA_COST_DISTRIBUTION_LINES_ALL pcdl
  UNION
  select pei.project_id
  from pa_expenditure_items_all pei) pv
where (p.project_id = pv.project_id) and
  (p.segment1 = :bl)
```

### 执行计划

```sql
SELECT STATEMENT Cost=321,61 bytes=2745 =
NESTED LOOPS Cost=321,61 bytes=2745 =
TABLE ACCESS BY INDEX ROWID PA_PROJECTS_ALL Cost=2,1 bytes=32 =
INDEX UNIQUE SCAN PA_PROJECTS_U2 Cost=1,1 bytes=
VIEW Cost=,41917 bytes=544921
SORT Cost=321,41917 bytes=149562
UNION-ALL Cost=
INDEX FULL SCAN PA_COST_DISTRIBUTION_LINES_N12 Cost=126,32864
  bytes=131456
TABLE ACCESS FULL PA_EXPENDITURE_ITEMS_ALL Cost=105,9053 bytes=18106
```

在上述示例中，内联视图由于存在 `UNION` 操作符而不可合并；因此对相邻表 `PA_EXPENDITURE_ITEMS_ALL` 执行了全表扫描。然而，如果可以将视图重写为 `UNION ALL` 操作符而不是 `UNION` 操作符，则可以使用推连接视图功能来提升索引的使用如下：

```sql
select p.project_id,p.name ,p.segment1
from pa_projects_all p
  (select pcdl.project_id
  from PA_COST_DISTRIBUTION_LINES_ALL pcdl
  UNION ALL
  select pei.project_id
  from pa_expenditure_items_all pei) pv
where (p.project_id = pv.project_id) and
  (p.segment1 = :bl)
```

### 执行计划

```sql
SELECT STATEMENT Cost=3,419 bytes=150884 =
NESTED LOOPS Cost=3,419 bytes=150884 =
TABLE ACCESS BY INDEX ROWID PA_PROJECTS_ALL Cost=2,1 bytes=32 =
INDEX UNIQUE SCAN PA_PROJECTS_U2 Cost=1,1 bytes=
VIEW Cost=,41917 bytes=17668
UNION-ALL PARTITION Cost=
INDEX RANGE SCAN PA_COST_DISTRIBUTION_LINES_N12 Cost=2,115 bytes=460 =
INDEX RANGE SCAN PA_EXPENDITURE_ITEMS_N8 Cost=1,906 bytes=1812
```
