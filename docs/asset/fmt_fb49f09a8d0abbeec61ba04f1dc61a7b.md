
虽然这行得通，但如果您要多次执行相同的通用查询，其效率较低。例如，假设您想先检索所有美国联系人，然后是加拿大所有联系人，最后是所有墨西哥联系人。您可以编写如下代码：

```pascal
SQLDataSet1.CommandType := ctQuery;

SQLDataSet1.CommandText := 'SELECT * FROM CONTACTS ' +
'WHERE COUNTRY = "United States"';

SQLDataSet1.Open;

ProcessDataSet;

SQLDataSet1.Close;

SQLDataSet1.CommandText := 'SELECT * FROM CONTACTS WHERE COUNTRY = "Canada"';

SQLDataSet1.Open;

ProcessDataSet;

SQLDataSet1.Close;

SQLDataSet1.CommandText := 'SELECT * FROM CONTACTS WHERE COUNTRY = "Mexico"';

SQLDataSet1.Open;

ProcessDataSet;

SQLDataSet1.Close;
```

在此示例中，`ProcessDataSet` 是某个虚构的方法，它会对查询结果进行某种操作。

虽然上述代码运行正确，但远非最佳。每次设置 `SQLDataSet1.CommandText` 时，后端数据库引擎都必须解析并准备 SQL 语句。实现相同结果的一种更好方法是参数化查询，如下所示：

```pascal
SQLDataSet1.CommandText := 'SELECT * FROM CONTACTS WHERE COUNTRY = :Country';
```

这会建立一个名为 `Country` 的参数，它在 SQL 语句中充当占位符。通过为此参数设置不同的值，您可以为不同国家发出相同的 SQL 语句，如下所示：

```pascal
SQLDataSet1.CommandType := ctQuery;

SQLDataSet1.CommandText := 'SELECT * FROM CONTACTS WHERE COUNTRY = :Country';

SQLDataSet1.ParamByName('Country').AsString := 'United States';

SQLDataSet1.Open;

ProcessDataSet;

SQLDataSet1.Close;

SQLDataSet1.ParamByName('Country').AsString := 'Canada';

SQLDataSet1.Open;

ProcessDataSet;

SQLDataSet1.Close;

SQLDataSet1.ParamByName('Country').AsString := 'Mexico';

SQLDataSet1.Open;

ProcessDataSet;
```

在此场景中，SQL 语句仅准备一次——即第一次执行时。之后，无需再次准备该语句，因为唯一变化的只是 `Country` 参数。

**NOTE**

请注意，参数名称不需要与其引用的列名称相同。在前面的示例中，该参数可以命名为 `ACountry`、`CountryParam` 或 `Fred`。

还有一个额外的属性控制参数的处理方式：`ParamCheck` 属性。当 `ParamCheck` 设置为 True 时，参数会自动由 dbExpress 创建（如前面的示例所示）。但是，如果您将 `ParamCheck` 设置为 False，则您需要自己创建参数。以下代码片段展示了如何这样做：

```pascal
SQLDataSet1.CommandType := ctQuery;

SQLDataSet1.ParamCheck := False;

SQLDataSet1.CommandText := 'SELECT * FROM CONTACTS WHERE COUNTRY = :Country';

SQLDataSet1.Params.CreateParam('Country', ftString, ptInput);

SQLDataSet1.ParamByName('Country').AsString := 'United States';

SQLDataSet1.Open;
```

请注意，通常只有在发出创建接受参数作为存储过程一部分的 DDL 语句时，您才会将 `ParamCheck` 设置为 False。因为这听起来有些混淆，我们来看一个例子：

```pascal
SQLDataSet1.CommandType := ctQuery;

SQLDataSet1.ParamCheck := False;

SQLDataSet1.CommandText :=
'CREATE PROCEDURE CONTACTSBYTITLE(ATITLE VARCHAR(20)) ' +
'RETURNS (      INTEGER, ' +
'FIRST      VARCHAR(20) ' +
```

## 排序服务器返回的数据

服务器返回的数据有两种排序方式。一种与 `TSQLTable` 组件有关，另一种则用于 `TSQLQuery` 和 `TSQLDataSet` 组件。我将首先介绍 `TSQLTable` 组件。

### 从表中排序数据

如果你正在使用 `TSQLTable`，可以在打开数据集之前设置该组件的 `IndexName` 或 `IndexFieldNames` 属性。`IndexName` 指的是底层数据库中存储的索引名称。例如，在 ConMan 数据库中，我定义了一个名为 `IX_CONMANE` 的索引，该索引由 `LAST` 和 `FIRST` 列组成（按此顺序）。

```
SQLTable1.IndexName := 'IX_CONMANE';
```

如果你不知道底层索引的名称，可以改为设置 `IndexFieldNames` 属性。`IndexFieldNames` 是构成索引的字段列表，以分号分隔。

```
SQLTable1.IndexFieldNames := 'LAST;FIRST';
```

> **注意**
>
> 你不需要确保在 `IndexFieldNames` 属性中设置的字段上定义了索引。在幕后，`TSQLTable` 会为其传递给数据库的 SQL 语句创建一个 `ORDER BY` 子句（基于 `IndexFieldNames` 中列出的字段）。

### 从查询中排序数据

如果你使用的是 `TSQLQuery` 或 `TSQLDataSet` 组件，排序结果集的方法更为直接：你自己只需在 SQL 语句中添加一个 `ORDER BY` 子句，如下所示：

```
SQLDataSet1.CommandText := 'SELECT * FROM CONTACTS ORDER BY LAST, FIRST';
```
