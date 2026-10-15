
```pascal
GetIndexNames('CONTACTS', ListBox1.Items);
```

### GetProcedureNames

要获取数据库中的存储过程列表，请调用`GetProcedureNames`方法。`GetProcedureNames`定义如下：

```pascal
procedure GetProcedureNames(List: TStrings);
```

从过程返回后，`List`包含存储过程名称列表。列表中以前存储的任何信息都会被删除。

```pascal
GetProcedureNames(ListBox1.Items);
```

### GetProcedureParams

`GetProcedureParams`返回给定存储过程的参数列表。定义如下：

```pascal
procedure GetProcedureParams(ProcedureName: string; List: TList);
```

第一个参数`ProcedureName`指定要检索参数名称的存储过程名称。第二个参数引用一个预先创建的`TList`，过程参数将返回到该列表中。从过程返回后，`List`包含存储过程的参数列表。

`List`本身不能直接使用。您应该调用辅助函数`LoadParamListItems`，将`TList`转换为`TParams`对象，这是一种更容易检查的结构。

以下代码片段展示了如何正确检索名为`CONTACTSBYSTATE`的存储过程的参数。

```pascal
var
  listParams: TList;
  Params: TParams;
begin
  listParams := TList.Create;
  try
    SQLConnection1.GetProcoredProcedureParams('CONTACTS\BYSTATE', listParams);
    Params := TParams.Create;
    try
      LoadParamListItems(Params, listParams);
      // Do something with Params here...
    finally
      Params.Free;
    end;
  finally
    FreeProcParams(listParams);
  end;
```

注意此代码片段末尾对`FreeProcParams`的调用。`FreeProcParams`会释放并置空`listParams`这个`TList`，因此您无需显式释放该列表。

`列表 1.2`展示了一个示例应用的完整源代码，该应用使用`TSQLConnection`从 InterBase 数据库中获取表、字段、索引、存储过程和参数名称。

## 列表 1.2 MetaData—MainForm.pas
