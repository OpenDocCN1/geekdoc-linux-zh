

默认情况下，字段按照声明的顺序返回。通过将 `sONAME` 作为最后一个参数传递给 `GetFieldNames`，字段名称将以字母顺序返回。

## 获取额外的字段元数据

如果您想获取某个字段的额外元数据，请调用 `TSQLMetaData.GetFieldMetaData`，其定义如下：

```pascal
function GetFieldMetaData(const ATableName,
  AColNameName: string): TFieldMetaData;
```

该方法接受表名和字段名作为参数，并返回一个 `TFieldMetaData` 记录，其中包含关于相关字段的信息。`TFieldMetaData` 的定义如下：

```pascal
TFieldMetaData = record
  ColumnName: string;
  ColumnPosition: LongInt;
  ColumnDataType: LongInt;
  ColumnTypeName: string;
  ColumnSubType: LongInt;
  ColumnLength: LongInt;
  ColumnPrecision: LongInt;
  ColumnScale: LongInt;
  ColumnNulable: LongInt;  // 1=非空, 0=空
end;
```

如图所示，它指定了列（或字段）名称、基于零的索引、列中包含的数据类型以及关于该字段的其他相关信息。

## 获取索引数据

`TSQLMetaData` 提供的一个有用方法是获取表中索引信息的方式。提供了两种形式。第一种形式根据给定的名称检索有关任何索引的信息。为此提供了两种方法。

```pascal
procedure GetIndexFieldNames(const ATableName, AIndexName: string;
  AList: TStrings);
```

`GetIndexFieldNames` 返回一个字符串列表，该列表由构成表 `ATableName` 上索引 `AIndexName` 的字段组成。

```pascal
function GetIndexFields(const ATableName, AIndexName: string): string;
```

`GetIndexFields` 将相同的列表作为分号分隔的列表返回。

索引数据检索的第二种形式是检索关于主键的数据，而不是任意索引。要检索构成主键的字段列表，可以将主键名称传递给 `GetIndexFieldNames` 或 `GetIndexFields`。但是，您可能不知道主键的名称。在这种情况下，您可以调用 **GetPrimaryKeyFieldNames** 或 **GetPrimaryKeyFields**。

```pascal
procedure GetPrimaryKeyFieldNames(const ATableName: string;
    AList: TStrings);
function GetPrimaryKeyFields(const ATableName: string): string;
```

这两个方法执行与 **GetIndexFieldNames** 和 **GetIndexFields** 相同的功能，只是它们始终在主键上工作。

### 其他方法

**TSQLMetaData** 还提供了一组方法，用于返回给定表的 INSERT、UPDATE 和 SELECT SQL 语句。这三个方法列举如下：

```pascal
function GetInsertStatement(const ATableName: string;
    ASQL: TStrings): Integer;
function GetUpdateStatement(const ATableName: string;
    ASQL: TStrings): Integer;
function GetSelectStatement(const ATableName: string;
    ASQL: TStrings): Integer;
```

给定一个表名，这三个方法在 `ASQL` 参数中返回相应的 INSERT、UPDATE 或 SELECT SQL 语句。

### 数据泵

**TSQLDataPump** 提供了 BDE 中 **TBatchMove** 组件的替代方案，允许您将数据从一个表轻松移动到另一个表。

为此，**TSQLDataPump** 发布了 **SQLMetaDataSource** 和 **SQLMetaDataDestination** 属性，它们分别引用指向源和目的地数据库连接的 **TSQLMetaData** 组件。

指定源和目标数据库后，将 **SQLSource** 属性设置为源数据库的有效 SELECT 语句，例如：

```sql
SELECT EMP_NO, FIRST_NAME, LAST_NAME, PHONE_EXT, HIRE_DATE, DEPT_NO,
JOB_CODE, JOB_GRADE, JOB_COUNTRY, SALARY FROM EMPLOYEE
```

接下来，将 **DestinationTable** 属性设置为目标数据库中表的名称，然后双击 **DestinationFields** 属性，这允许您设置源表中字段与目标表中字段之间的映射。

最后，将 **DataMoveMode** 设置为要执行的相应操作。表 B.1 列出了可能使用的模式。

![](img/52a35759a0f10dade27a840504be5d82_396_0.png)

**表 B.1** 有效的 DataMoveMode 值

| 值 | 描述 |
| :--- | :--- |
| dmAlwaysInsert | 将所有选定的记录插入目标表中。 |
| DmAppend | 将选定的记录追加到目标表中。 |
| dmAppendUpdate | 如果记录已存在于目标表中，则更新该记录。否则，将记录追加到目标表中。 |
| DmDelete | 从目标表中删除匹配的记录。 |
| DmUpdate | 更新目标表中匹配的记录。 |

此时，所有必需的属性都已设置，因此您只需要调用 `TSQLDataPump.Execute` 即可执行批量移动操作。

## 更多信息

这只是对 dbExpress Plus 所提供功能的一个简要概述。由于这是一个开源项目，因此代码可能会增长并提供比此处讨论的更多的功能是合情合理的。dbExpress Plus 的下载包还附带一个演示应用程序，该应用程序展示了如何使用本附录中讨论的许多方法。

# 索引

# 符号

- `+`（加法）运算符，128
- `*`（星号）运算符，129
- `\`（反斜杠），210
- `/`（数据分隔符），210
- `.`（小数点），207
- `#`（数字占位符），207
- `0`（数字占位符），207
- `[db]`（除法）运算符，128
- `"`（双引号），207
- `=`（等值测试）运算符，127
- `!`（感叹号），210
- `>`（大于）运算符，127
- `>=`（大于或等于）运算符，127
- `>`（大于号），210
- `<>`（大于/小于号），210
- `<>`（不等值测试）运算符，127
- `<`（小于）运算符，127
- `<=`（小于或等于）运算符，127
- `<`（小于号），210
- `[ts]`（乘法）运算符，128
- `#`（磅号），209
- `;`（分隔字符），207, 210
- `'`（单引号），207
- `0` 指定符，209
- `9` 指定符，209
- `–`（减法）运算符，128
- `,`（千位分隔符），207
- `:`（时间分隔符），210
- `_`（下划线），210

# A

- A 指定符，209
- accessing（访问）
  - fields (client datasets)（字段（客户端数据集）），103
  - *nonpersistent*（非持久）fields（字段），104-105
  - *persistent*（持久）fields（字段），103
  - Fields（字段）objects（对象），64
  - providers（提供者）on different form（在不同表单上），308
- ACID（Atomic, Consistent, Isolated, Durable）（原子性、一致性、隔离性、持久性）
  - properties（属性），37
  - action handlers（动作处理程序），228
- activating indexes（激活索引）
  - (client datasets)（（客户端数据集）），121
- Active（活动）property（属性），60
- Add Connection（添加连接）button（按钮），10
- Add（添加）method（方法），102
- Add to Interface（添加到接口）command（命令）(remote data module context menu)（（远程数据模块上下文菜单）），324
- Add To Interface（添加到接口）dialog box（对话框），324
- AddFieldDef（添加字段定义）method（方法），102
- AddIndex（添加索引）method（方法），121
- adding（添加）
  - fields (client datasets)（字段（客户端数据集）），102
  - modules (remote data modules)（模块（远程数据模块）），324
- Addition (+)（加法（+））operator（运算符），128
- Address（地址）property（属性），331
- Advanced application (MainForm.pas)（高级应用程序（MainForm.pas）），code listing（代码列表），76-79
- advantages（优势）
  - client datasets（客户端数据集），94-95
  - ConMan，373
- AfterApplyUpdates（应用更新后）event（事件），295
- AfterCancel（取消后）event（事件），150
- AfterClose（关闭后）event（事件），150
- AfterConnect（连接后）event（事件），14
- AfterDisconnect（断开连接后）event（事件），14
- AfterEdit（编辑后）event（事件），150
- AfterExecute（执行后）event（事件），295
- AfterGetParams（获取参数后）event（事件），295
- AfterGetRecords（获取记录后）event（事件），295, 342
- AfterInsert（插入后）event（事件），150
- AfterOpen（打开后）event（事件），150
- AfterPost（提交后）event（事件），150
- AfterRowRequest（请求行后）event（事件），295
- AfterScroll（滚动后）event（事件），150
- AfterUpdateRecord（更新记录后）event（事件），295
- aggregate expressions（聚合表达式），195
- aggregate fields（聚合字段），96
- aggregate types（聚合类型），195
- aggregates（聚合）
  - across datasets（跨数据集），196-197
  - determining position of record（确定记录位置），197
  - enabling/disabling（启用/禁用），197
  - grouped（分组），196
  - maintained（维护），192-193
    - *creating at design time*（*在设计时创建*），193-195
    - *creating at runtime*（*在运行时创建*），195
- Aggregates（聚合）property（属性），194-195
- Alignment（对齐）property（属性），242-244
- AllowDelete（允许删除）property（属性），267
- AllowInsert（允许插入）property（属性），267
- And（与）operator（运算符），128
- Apartment（套间）value（值），321
- Append（追加）method（方法），105
- application servers（应用程序服务器）
  - ConMan，352-353
  - creating（创建），318
  - testing（测试），328-329
- applications（应用程序）. See also individual applications（另见单独的应用程序）
  - client（客户端）
    - ConMan，358, 361-362, 371-372
    - CORBA connections（CORBA 连接），335
    - creating（创建），329-330
    - DCOM connections（DCOM 连接），333
    - HTTP connections（HTTP 连接），334
    - *intercepting data packets*（*拦截数据分组*），333
    - *multiple connection types*（*多种连接类型*），343-344

