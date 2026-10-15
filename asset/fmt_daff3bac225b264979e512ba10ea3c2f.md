
> 注意：在第一次使用 Visual Explain（可视化解释）时会自动创建解释表。

# 收集解释数据

可以收集不同类型的解释数据。它们的区别在于将填充的解释表列。解释数据选项有：

- `EXPLAIN` - 捕获访问计划的详细信息并存储在解释表中。不存储快照信息。
- `EXPLAIN SNAPSHOT` - 捕获 SQL 查询的当前内部表示和相关信息。快照信息存储在 `EXPLAIN_STATEMENT` 表的 `SNAPSHOT` 列中。

并不是所有的解释工具都需要相同类型的解释数据。某些工具使用通过 `EXPLAIN` 选项捕获的数据，而其他工具（如 Visual Explain）则解释快照数据。

创建解释表后，你可以开始捕获填充它们的解释数据。并不是所有的 SQL 语句都可以被解释。可解释的 SQL 语句包括：`SELECT`、`SELECT INTO`、`UPDATE`、`INSERT`、`DELETE`、`VALUES` 和 `VALUES INTO` 语句。

根据你想要解释的 SQL 语句数量或应用程序类型，你应该使用不同的方法。这些方法包括：

- `EXPLAIN` 语句 - 为 SQL 语句收集解释数据
- `CURRENT EXPLAIN MODE` 特殊寄存器 - 指定动态 SQL 语句的解释数据收集
- `CURRENT EXPLAIN SNAPSHOT` 特殊寄存器 - 指定动态 SQL 语句的解释快照数据收集
- `BIND` 选项 - 指定包中静态和/或动态嵌入 SQL 语句的解释数据收集

这些这些方法都将逐一检查。

## EXPLAIN 语句

当你想要为单个动态 SQL 语句收集解释信息时，`EXPLAIN` 语句非常有用。可以从命令行处理器（CLI）、命令中心或应用程序内部调用 `EXPLAIN` 语句。

你可以控制 `EXPLAIN` 语句在解释表中存储的解释信息量。默认只捕获解释表信息而不存储快照信息。如果你希望修改此行为，请使用以下 `EXPLAIN` 语句选项：

- `WITH SNAPSHOT` - 将解释和解释快照数据捕获到解释表中。
- `FOR SNAPSHOT` - 仅捕获解释快照信息。除了 `EXPLAIN_INSTANCE` 和 `EXPLAIN_STATEMENT` 表中通常找到的信息外，不捕获其他解释信息。

当未指定其他解释选项时使用默认情况。在默认情况下，`EXPLAIN` 语句将仅收集解释数据。不捕获解释快照数据。

执行 `EXPLAIN` 语句的用户必须对解释表具有 `INSERT` 权限。

> **注意：** 使用 `EXPLAIN` 语句解释的 SQL 语句不会被执行；只捕获解释数据。

现在将检查使用 `EXPLAIN` 语句收集访问计划信息的示例。解释语句所示所示。此示例为解释表收集了所有可用的解释信息。

```sql
EXPLAIN ALL WITH SNAPSHOT "SELECT * FROM candidate"
```

> **注意：** 除了我们示例使用的关键字 `ALL`，可以使用关键字 `PLAN` 和 `PLAN SELECTION`。你的 `EXPLAIN` 语句必须包含其中一个。

上一个示例所示 `EXPLAIN` 语句提供了许多解释表，包括 `EXPLAIN_STATEMENT` 表的 `SNAPSHOT` 列。

`EXPLAIN_INSTANCE` 表中的 `SNAPSHOT_TAKEN` 列表示每个解释语句是否存在 Visual Explain 快照。

`EXPLAIN` 语句也可以嵌入到填充解释表的应用程序中。一旦填充了解释表，就可以对其进行查询。可以检查特殊的算符，以确定查询是否使用了理想的访问计划。

## 解释特殊寄存器

收集解释信息的另一种方法是使用解释特殊寄存器。DB2 使用两个特殊寄存器来收集动态语句的解释信息。这些寄存器可以交互式设置，也可以在 SQL 程序中使用。使用 `SET` 语句修改值。

- `CURRENT EXPLAIN MODE` - 用于仅填充解释数据。不拍摄快照。
- `CURRENT EXPLAIN SNAPSHOT` - 用于捕获解释快照数据。

使用以下语句进行设置：

```sql
SET CURRENT EXPLAIN MODE
SET CURRENT EXPLAIN SNAPSHOT
```

选项有：

- `NO` - 不为动态语句捕获解释信息。
- `YES` - 将为动态 SQL 语句填充解释表或快照信息。
- `EXPLAIN` - 在不执行 SQL 语句的情况下，为动态 SQL 语句填充解释表或快照信息。

这两个选项仅适用于 `EXPLAIN MODE` 寄存器。它们将在讨论索引顾问（Index Advisor）的部分中进行说明。

- `RECOMMEND INDEXES`
- `EVALATE INDEXES`

> 注意：一旦你将寄存器设置为 `YES`，任何后续动态语句都将被解释。

## 解释 BIND 选项

`BIND` 命令在第 691 页的“开发考虑”中讨论。然而，在本节中，将审查与解释信息相关的 bind 选项。

可以指定两个解释 bind 选项：`EXPLAIN` 和 `EXPLSNAP`。`EXPLSNAP` 选项收集快照信息。如果你想使用 Visual Explain 查看访问计划，则使用 `EXPLSNAP` 选项。`EXPLAIN` 选项仅填充解释信息，不包含快照。

> 注意：DRDA 服务器无法执行解释快照。

### SQL 监控

图 12–23 显示了 `BIND` 命令的选项以及当使用这些选项时填充的解释表。

| BIND 选项 EXPLAIN/EXPLSNAP | 静态 SQL | 动态 SQL |
|---|---|---|
| NO | | |
| YES | | |
| ALL | | |
| | | 填充解释表 |

图 12–23 为 `BIND` 命令使用 `EXPLAIN` 或 `EXPLSNAP` 选项

现在将使用 bind 选项捕获解释数据。

```sql
BIND checkid.bnd EXPLSNAP ALL
```
