# **LISTING 7.1**
Continued

```
```
procedure TfrmMain.TDataSetProvider1GetTableName(Sender: TObject;
  DataSet: TDataSet; var TableName: String);
begin
  Log('TDataSetProvider.OnGetTableName');
end;
```

```

```
```
procedure TfrmMain.TDataSetProvider1UpdateData(Sender: TObject;
  DataSet: TCustomClientDataSet);
begin
  Log('TDataSetProvider.OnUpdateData');
end;
```

```

```
```
procedure TfrmMain.TDataSetProvider1UpdateError(Sender: TObject;
  DataSet: TCustomClientDataSet; E: EUpdateError; UpdateKind: TUpdateKind;
  var Response: TResolveResponse);
begin
  Log('TDataSetProvider.OnUpdateError');
end;
```

```

```
```
procedure TfrmMain.ClientDataSet1AfterApplyUpdates(Sender: TObject;
  var OwnerData: OleVariant);
begin
  Log('TClientDataSet.AfterApplyUpdates');
end;
```

```

```
```
procedure TfrmMain.ClientDataSet1AfterExecute(Sender: TObject;
  var OwnerData: OleVariant);
begin
  Log('TClientDataSet.AfterExecute');
end;
```

```

```
```
procedure TfrmMain.ClientDataSet1AfterGetParams(Sender: TObject;
  var OwnerData: OleVariant);
begin
  Log('TClientDataSet.AfterGetParams');
end;
```

```

```
```
procedure TfrmMain.ClientDataSet1AfterGetRecords(Sender: TObject;
  var OwnerData: OleVariant);
begin
  Log('TClientDataSet.AfterGetRecords');
end;
```

```

```
```
procedure TfrmMain.ClientDataSet1AfterRefresh(DataSet: TDataSet);
```

```