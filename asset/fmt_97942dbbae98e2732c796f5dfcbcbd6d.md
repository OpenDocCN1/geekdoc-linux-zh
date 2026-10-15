
`procedure TfrmMain DataSetProvider1BeforeUpdateRecord(Sender: TObject; SourceDS: TDataSet; DeltaDS: TCustomClientDataSet; UpdateKind: TUpdateKind; var Applied: Boolean);`

```pascal
begin

  if UpdateKind = ukInsert then

    if DeltaDS.FieldByName('ID').OldValue <= 0 then

      DeltaDS.FieldByName('ID').NewValue := GetNextID;

end;
```

`GetNextID` 看起来像这样：

```pascal
function TfrmMain.GetNextID: Integer;

begin

  sqlID.ExecSQL;

  Result := sqlID.ParamByName('AValue').AsInteger;

end;
```

`sqlID` 是一个 `TSqlDataSet` 组件，它在数据库服务器上执行存储过程，该存储过程进而通过名为 `AValue` 的输出参数返回下一个唯一的 ID 号码。

我暂时不会提供一个使用此技术的程序示例，但你将在本章后续的示例中看到此技术的实现。

## 拦截数据

表 7.4 列出了两个事件 `OnGetData` 和 `OnUpdateData`，它们可用于拦截从提供程序到客户端的数据传输，以及从客户端到提供程序的数据传输。

在本章中，我们正在处理单个应用程序；换句话说，数据的客户端部分和服务器部分都包含在同一个应用程序中。在下一章中，我们将创建可能存在于不同机器上的客户端和服务器应用程序，这些机器可能就在走廊的另一端，也可能位于不同的洲。

当数据在机器之间传输时，不幸的是，总是有可能某些黑客正在尝试窃听数据交换。如果数据包含任何敏感信息，例如账户号码或类似内容，你可能希望在通过网络或穿越赛博空间发送该数据之前对其进行加密。

`OnGetData` 和 `OnUpdateData` 提供了在服务器端实现此功能的两个钩子。下面的代码片段展示了 `OnGetData` 和 `OnUpdateData` 的实现，它们分别在数据传向客户端时进行加密，在数据传回时进行解密。代码中引用的 `EncryptData` 和 `DecryptData` 函数是虚构的例程，如果你要在自己的应用程序中实现此功能，则需要提供这些例程。

### 注意

对于支持 DES、Blowfish 和 Rijndael (`AES`) 等加密标准的优秀的第三方加密库，请查看 TurboPower Software 位于 `www.tpx.turbopower.com/products/LockBox` 的 `LockBox` 产品。

```pascal
procedure TForm1.ProviderGetData(Sender: TObject;
  DataSet: TCustomClientDataSet);
begin
  while not DataSet.EOF do begin
    DataSet.Edit;
    DataSet.FieldByName('AccountNumber').AsString :=
      EncryptData(DataSet.FieldByName('AccountNumber').AsString);
    DataSet.Post;
    DataSet.Next;
  end;
end;

procedure TFrmMain.DataSetProvider1UpdateData(Sender: TObject;
  DataSet: TCustomClientDataSet);
begin
  while not DataSet.EOF do begin
    if DataSet.UpdateStatus <> usDeleted then begin
      DataSet.Edit;
      DataSet.FieldByName('AccountNumber').AsString :=
        DecryptData(DataSet.FieldByName('AccountNumber').AsString);
      DataSet.Post;
      DataSet.Next;
    end;
  end;
end;
```

在客户端，`AccountNumber` 字段将被加密。`ClientDataSet1.FieldByName('AccountNumber').AsString` 将返回一个加密的账户代码，然后你需要在显示之前对其进行解密。请注意，这里所示的代码是加密/解密数据的一种相当简单的实现方式。首先，只有账户号码被加密和解密。在实际应用程序中，你可能希望通过遍历数据集中的所有字段来加密和解密所有字符串字段。

第 7 章 300

## 可选参数

可选参数是与客户传递给客户端的数据集相关的自定义数据。可选参数与整个数据集相关，而不是与单个记录相关。你可以使用可选参数将数据传回客户端，例如提供数据的时间和日期、在服务器上运行查询所需的时间长度，或任何其他数据。

要将可选参数传递给客户端，请为 `TDataSetProvider` 的 `OnGetDataSetProperties` 事件提供事件处理程序。在此事件处理程序内部，使用 `Properties` 参数设置要发送回客户端的值。下面的代码片段展示了如何同时发送执行查询所需的时间和查询执行的时间。

```pascal
procedure TForm1.DataSetProvider1GetDataSetProperties(Sender: TObject;  
    DataSet: TDataSet; out Properties: OleVariant);
begin
    Properties := VarArrayCreate([0, 1], varVariant);
    Properties[0] := VarArrayOf(['TimeQueried', Now, True]);
    Properties[1] := VarArrayOf(['QueryPerformance', FTimeToQuery, True]);
end;
```

`Properties` 是一个变体数组的变体数组。此代码片段创建了一个包含两个变体的数组。数组中的每个变体都是一个包含三个值的数组：可选参数的名称、参数的值，以及一个指示是否应将可选参数作为增量的一部分发送回服务器的布尔值。

在此示例中，`FTimeToQuery` 是一个私有变量，使用以下代码计算：

```pascal
procedure TForm1.SQLDataSet1BeforeOpen(DataSet: TDataSet);
begin
    FTimeToQuery := GetTickCount;
end;

procedure TForm1.SQLDataSet1AfterOpen(DataSet: TDataSet);
begin
    FTimeToQuery := GetTickCount - FTimeToQuery;
end;
```

`SQLDataSet1` 是 `TDataSetProvider` 的底层数据集。

在客户端，你可以使用以下代码检索这些值：

```pascal
procedure TForm1.btnGetPropertiesClick(Sender: TObject);
var
    QP: DWord;
    TimeQueried: TDateTime;
begin
    QP := ClientDataSet1.GetOptionalParam('QueryPerformance');
    TimeQueried := ClientDataSet1.GetOptionalParam('TimeQueried');
```

```pascal
ShowMessage('The query took ' + IntToStr(OP + 'ms and was executed on ' +
 DateToStr(TimeQueried) + ' at ' + TimeToStr(TimeQueried));
 end;
```
