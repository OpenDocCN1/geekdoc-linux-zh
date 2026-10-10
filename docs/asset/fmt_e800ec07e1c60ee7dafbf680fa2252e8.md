
模式应用程序的核心部分包含在单个方法中：`btnRetrieveClick`。`btnRetrieveClick` 确定用户选择的模式类型，并确保如果请求的模式类型是列、索引或存储过程参数，用户必须输入对象名称。

一旦确定了模式类型，调用适当的 `setSchemaInfo`、打开数据集并使用模式信息加载列表视图就是一件简单的事了。某些列（即 `TABLE_TYPE`、`PROC_TYPE`、`COLUMN_TYPE`、`COLUMN_DATATYPE`、`COLUMN_SUBTYPE` 和 `INDEX_TYPE`）是位图数值列。该程序调用少数几个辅助例程来显示这些值的文本表示形式。其余列按原样显示。

运行此应用程序时您会发现，不同的模式类型返回不同的数据字段。表 2.3 至 2.7 解释了每种模式类型返回的列。

### 表 2.3 stTables 和 stSystemTables 模式列

表 2.3 列出了模式类型为 `stTables` 或 `stSystemTables` 时返回的列。

| **表 2.3** | stTables 和 stSystemTables 模式列 |
|---|---|
| **列** | **描述** |
| RECNO | 绝对记录号。第一条记录为 1，第二条为 2，依此类推。 |
| CATALOG_NAME | 包含该表的目录或数据库的名称。 |
| SCHEMA_NAME | 表的所有者。 |
| TABLE_NAME | 表名。 |
| TABLE_TYPE | 代表表类型的位图值。有关此字段可能值的解释，请参阅列表 2.4 或 `DBXPress.pas` 的源代码。 |

### 表 2.4 stProcedures 模式列

表 2.4 列出了模式类型为 `stProcedures` 时返回的列。

| **表 2.4** | stProcedures 模式列 |
|---|---|
| **列** | **描述** |
| RECNO | 绝对记录号。第一条记录为 1，第二条为 2，依此类推。 |
| CATALOG_NAME | 包含该存储过程的目录或数据库的名称。 |
| SCHEMA_NAME | 存储过程的所有者。 |
| PROC_NAME | 存储过程的名称。 |
| PROC_TYPE | 代表存储过程类型的位图值。有关此字段可能值的解释，请参阅列表 2.4 或 `DBXPress.pas` 的源代码。 |
| IN_PARAMS | 存储过程的输入参数数量。 |
| OUT_PARAMS | 存储过程的输出参数数量。 |

### 表 2.5 stColumns 模式列

表 2.5 列出了模式类型为 `stColumns` 时返回的列。

| **表 2.5** | stColumns 模式列 |
|---|---|
| **列** | **描述** |
| RECNO | 绝对记录号。第一条记录为 1，第二条为 2，依此类推。 |
| CATALOG_NAME | 包含该表的目录或数据库的名称。 |
| SCHEMA_NAME | 列的所有者。 |
| TABLE_NAME | 包含该列的表的名称。 |
| COLUMN_NAME | 列的名称。 |
| COLUMN_POSITION | 列在表定义中的基于零的位置。 |
| COLUMN_TYPE | 代表列类型的位图值。有关此字段可能值的解释，请参阅列表 2.4 或 `DBXpress.pas` 的源代码。 |
| COLUMN_DATATYPE | 逻辑字段类型。有关此字段可能值的解释，请参阅列表 2.4 或 `DBXpress.pas` 的源代码。 |
| COLUMN_TYPENAME | SQL 列类型（VARCHAR、BLOB 或类似类型）。 |
| COLUMN_SUBTYPE | 逻辑字段子类型。有关此字段可能值的解释，请参阅列表 2.4 或 `DBXpress.pas` 的源代码。 |
| COLUMN_LENGTH | 列的大小（以字节为单位）。 |
| COLUMN_PRECISION | 列的精度。因列类型而异。例如，对于字符串是字符数，对于 BCD 值是有效数字的位数。 |
| COLUMN_SCALE | 数值比例。对于 BCD 列，它是小数点右侧的数字位数。 |
| COLUMN_NULLABLE | 如果列可以包含 NULL 值，则为一；如果不能包含 NULL 值，则为零。 |

### 表 2.6 stProcedureParams 模式列

表 2.6 列出了模式类型为 `stProcedureParams` 时返回的列。

| **表 2.6** | stProcedureParams 模式列 |
|---|---|
| **列** | **描述** |
| RECNO | 绝对记录号。第一条记录为 1，第二条为 2，依此类推。 |
| CATALOG_NAME | 包含该存储过程的目录或数据库的名称。 |

# 表 2.6（续）

| 列 | 描述 |
| :--- | :--- |
| SCHEMA_NAME | 过程参数的所有者。 |
| PROCEDURE_NAME | 包含该参数的过程的名称。 |
| PARAM_NAME | 参数的名称。 |
| PARAM_POSITION | 参数的基于零的位置。注意，输入参数和输出参数各自拥有独立的列表，因此第一个输入参数的位置为零，第一个输出参数的位置也为零。 |
| PARAM_TYPE | 对于输入参数为 1，输出参数为 2，输入/输出参数为 3，返回值为 4。 |
| PARAM_DATATYPE | 逻辑参数类型。有关该字段可能值的解释，请参阅列表 2.4，或 `DBXpress.pas` 的源代码。 |
| PARAM_SUBTYPE | 逻辑参数子类型。有关该字段可能值的解释，请参阅列表 2.4，或 `DBXpress.pas` 的源代码。 |
| PARAM_TYPENAME | SQL 参数类型（如 VARCHAR、BLOB 等）。 |
| PARAM_LENGTH | 参数的字节大小。 |
| PARAM_PRECISION | 参数的精度。因参数类型而异。例如，对于字符串，它是字符数；对于 BCD 值，它是有效数字的位数。 |
| PARAM_SCALE | 数字比例。对于 BCD 参数，它是小数点右侧的数字位数。 |
| PARAM_NULLABLE | 如果参数可以包含 NULL 值，则为 1；如果不能包含 NULL 值，则为 0。 |

### 表 2.7 stIndexes 架构列

表 2.7 列出了当架构类型为 `stIndexes` 时返回的列。

# 表 2.7 stIndexes 架构列

| 列 | 描述 |
| :--- | :--- |
| RECNO | 绝对记录编号。第一条记录为 1，第二条为 2，依此类推。 |
| CATALOG_NAME | 包含该索引的目录或数据库的名称。 |
| SCHEMA_NAME | 索引的所有者。 |
| TABLE_NAME | 定义该索引的表的名称。 |
| INDEX_NAME | 索引的名称。 |
| COLUMN_NAME | 构成该索引的一部分的列的名称。 |
| COLUMN_POSITION | 列在索引中的位置。 |
| PKEY_NAME | 如果是主键，这是主键的名称。 |
| INDEX_TYPE | 一个位映射值，表示列的类型。有关该字段可能值的解释，请参阅列表 2.4，或 `DBXpress.pas` 的源代码。 |
| SORT_ORDER | 升序列为 A，降序列为 D。 |
| FILTER | 这代表过滤/范围索引上的过滤条件，或表达式索引上的表达式。例如，(LAST + FIRST)。仅某些数据库（如 Oracle）支持此功能。 |

# 摘要

本章讨论了 dbExpress 数据集组件 `TSQLDataSet`，包括以下关键概念：

- `TSQLDataSet` 是一种单向、只读、轻量级的数据访问机制。它可以用于从数据库中的表、查询或存储过程中检索数据。
- dbExpress 数据集支持两种导航选项：移动到数据集的开头以及移动到结果集中的下一条记录。
- 要从 `TSQLDataSet` 中检索数据，通常调用 `FieldByName` 方法。
- `TSQLDataSet` 支持 BLOB 信息。为了提高查询性能，您可以设置 `TSQLDataSet` 的 `BlobSize` 属性以指定每个 BLOB 字段要检索的最大数据量。
- 为了使重复查询更高效，您可以通过在 SQL 语句中创建占位符来实现参数化。然后，您可以为该参数设置不同的值。SQL 语句仅被编译一次——即在第一次执行时。
- 要对从数据库返回的数据进行排序，您可以在数据集的 `CommandText` 属性中指定 ORDER BY 子句。
- 您可以轻松地在表和查询之间建立主/从关系。
- 可以使用 dbExpress 数据集来检索数据库中表、查询和存储过程的详细架构信息。

下一章开始对客户端数据集进行为期两章的探索。

# 客户端数据集基础

![](img/fe651f295b5f960d5463c4fb581d2281_105_0.png)

# 本章内容

- 什么是客户端数据集？ 94
- 客户端数据集的优缺点 94
- 创建客户端数据集 95
- 填充和操作客户端数据集 105
- 遍历客户端数据集 113
- 客户端数据集索引 118
- 过滤器和范围 126
- 搜索 136
