
### `getJSONObject()`

```
getJSONObject()
getJSONObject(
eSQLObjectType eObjType,
pSQLCursor ppCur)
```

给定一个 `eSQLObjectType`，此方法返回一个 `SQLCursor`，其中包含数据库可用对象的列表。

返回的游标中的列：

| 列 | 类型 |
| --- | --- |
| 1.RECNO | fldINT32 |
| 2.CATALOG_NAME | fldZSTRING |
| 3.SCHEMA_NAME | fldZSTRING |
| 4.OBJECT_NAME | fldZSTRING |

游标按对象名 (`OBJECT_NAME`) 排序。

### `getTables()`

```
getTables()
Tables(
pCHAR pszTableNamePattern,
UINT32 uTableType,
pSQLCursor ppCur)
```

给定一个 `eSQLTableType`，此方法返回一个 `SQLCursor`，其中包含数据库中的表、视图或同义等列表。可以将一个或多个 `eSQLTableType` 进行逻辑或操作并传递给 `uTableType`，以获取多种类型的列表。也可以在第一个参数中为表名指定搜索模式。如果为 NULL，则在搜索时将不使用任何条件。

返回的游标中的列：

| 列 | 类型 |
| --- | --- |
| 1.RECNO | fldINT32 |
| 2.CATALOG_NAME | fldZSTRING |
| 3.SCHEMA_NAME | fldZSTRING |
| 4.TABLE_NAME | fldZSTRING |
| 5.TABLE_TYPE | fldINT32 |

游标按表名 (`TABLE_NAME`) 排序。

### `getProcedure()`

```
getProcedure()
getProcedures (
    pCHAR pszProcNamePattern,
    UINT32 uProcType,
    ppSQLCursor ppCur)
```

给定一个 `eSQLType`，此方法返回一个 `SQLCursor`，其中包含数据库中过程、函数等的列表。可以将一个或多个 `eSQLType` 进行逻辑或操作并传递给 `uProcType`，以获取多个存储过程的列表。也可以在第一个参数中为过程名指定搜索模式。如果为 NULL，则在搜索时将不使用任何条件。

返回的游标中的列为：

| 列 | 类型 |
|---|---|
| 1.RECNO | fldINT32 |
| 2.CATALOG_NAME | fld_ZSTRING |
| 3.SCHEMA_NAME | fldZSTRING |
| 4.PROC_NAME | fldZSTRING |
| 5.PROC_TYPE | fldINT32 |
| 6.IN_PARAMS | fldINT16 |
| 7.OUT_PARAMS | fldINT16 |

游标列按过程名 (`PROC_NAME`) 排序。

### `getColumns()`

```
getColumns()
getColumns (
    pCHAR pszTableName,
    pCHAR pszColumnName,
    UINT32 uColType,
    ppSQLCursor ppCur)
```

给定一个表名，此方法返回一个 `SQLCursor`，其中包含表的列列表。也可以在第二个参数中指定列名的搜索模式。可以将一个或多个 `eSQLType` 进行逻辑或操作并传递给 `uColType`，以获取多种特定类型。

返回的游标中的列

| 列 | 类型 |
| --- | --- |
| 1.RECNO | fldINT32 |
| 2.CATALOG_NAME | fldZSTRING |
| 3.SCHEMA_NAME | fldZSTRING |
| 4.TABLE_NAME | fldZSTRING |
| 5.COLUMN_NAME | fldZSTRING |
| 6.COLUMN_POSITION | fldINT16 |
| 7.COLUMN_TYPE | fldINT32 |
| 8.COLUMN_DATATYPE | fldINT16 |
| 9.COLUMN_TYP | fldZSTRING |
| 10.COLUMN_SUBTYPE | fldINT16 |
| 11.COLUMN_PRECISION | fldINT32 |
| 12.COLUMN_SCALE | fldINT16 |
| 13.COLUMN_LENGTH | fldINT32 |
| 14.COLUMN_NULLABLE | fldINT16 |

游标列按过程名 (`COLUMN_NAME`) 排序。

### `getProcedureParams()`

```
getProcedureParams()
getProcedureParams (
    pCHAR pszProcName,
    pCHAR pszParamName,
    ppSQLCursor ppCur)
```

给定一个过程，此方法返回一个 `SQLCursor`，其中包含参数列表。也可以在第二个参数中指定参数名的搜索模式。

返回的游标中的列

| 列 | 类型 |
| --- | --- |
| 1.RECNO | fldINT32 |
| 2.CATALOG_NAME | fldZSTRING |
| 3.SCHEMA_NAME | fldZSTRING |
| 4.PROC_NAME | fldZSTRING |
| 5.PARAM_NAME | fldZSTRING |
| 6.PARAM_TYPE | fldINT32 |
| 7.PARAM_DATATYPE | fldINT16 |
| 8.PARAM_SUBTYPE | fldINT16 |
| 9.PARAM_TYP | fldZSTRING |
| 10.PARAM_PRECISION | fldINT32 |
| 11.PARAM_SCALE | fldINT16 |
| 12.PARAM_LENGTH | fldINT32 |
| 13.PARAM_NULLABLE | fldINT16 |

游标列按过程名 (`PARAM_NAME`) 排序。

### `getIndices()`

```
getIndices()
Indices (
    pCHAR pszTableName,
UINT32 uIndexType,
ppSQLCursor ppCur)
```

给定一个表名，此方法返回一个 `SQLCursor`，其中包含表中的索引列表。可以将一个或多个 `SQLIndexType` 传递给 `uIndexType`，以获取多种特定类型（如 Unique）的列表。

## 数据访问层

可以向 `SQLMetaData` 添加新方法，以返回关于表和列权限、可用 SQL 函数和 SQL 关键字、引用完整性约束等元数据。

## 数据类型映射

数据源以各种格式表示数据，通用接口 `dbExpress` 应该提供一组通用数据类型以获取单个字段的值。`dbExpress` 定义了一组逻辑数据类型，这些涵盖了各种数据库支持的大部分 SQL 数据类型。这些逻辑数据类型与 BDE 中的类型匹配，以确保兼容性，并让现有应用程序轻松地适配。

然而，从 SQL 到逻辑数据类型的映射可能与 BDE 中不同。例如，引入了新的 `fldDateTime` 来表示时间戳数据而不产生任何数据丢失。在数值方面，无法放入 double 的命名数据被直接映射到 BCD，从而消除了启用或禁用 BCD 的需要。尽管 SQL 与逻辑类型之间及其反之存在转换，但对性能的影响可以忽略不计。

在内部，`dbExpress` 将特定特定的 SQL 类型映射到数据库物理数据类型，并将一个或多个物理数据类型映射到一个逻辑数据类型。与 BDE 不同，`dbExpress` 不会向客户端暴露物理数据类型；但在当前框架下，数据库驱动开发者可以选择以物理数据类型的形式返回它们。

在核心接口之上，应用程序开发者可以创建一个缓存层，从而对结果提供正向和反向滚动。数据库连接有时是非常昂贵的，因此可以构建一个连接池层。跨数据源的模式创建、导入和导出接口以及所有其他数据访问需求都可以轻松构建。然而，保持核心运行时数据访问层的轻量和简单是非常关重要的，以便提供高性能的数据库连接，并易于适配新的数据源。

## dbExpress 驱动开发

此信息基于 `dbExpress` 架构师 `Ramesh Theivendran` 提供的文档。

数据库连接在几乎每个业务应用程序中起着至关重要的作用。某些应用程序频繁访问数据（例如：报告生成应用程序），某些则很少访问。如果你查看这些应用程序的连接需求，它们都通过执行 SQL 来获取数据和元数据。动态 SQL 处理是数据库最需要的。动态 SQL 允许应用程序在运行时处理任何有效的 SQL 语句。大多数数据库厂商客户端库提供动态 SQL 处理的接口，如 Oracle 的 `OCI` 或 `PRO*C`（动态方法4）、`DB2` 和其他 ODBC 数据源的 `CLI`、`Sybase` 的 `CTLIB` 以及 `Informix` 的 `E/SQL`。

## 数据访问层

第 16 章
