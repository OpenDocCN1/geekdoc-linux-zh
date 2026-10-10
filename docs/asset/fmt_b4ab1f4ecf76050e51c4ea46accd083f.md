
`Result := SQLID.ParamByName('AValue').AsInteger;`

`end;`

```pascal
procedure TfrmMain.DataSetProvider1BeforeUpdateRecord(Sender: TObject;
    SourceDS: TDataSet; DeltaDS: TCustomClientDataSet;
    UpdateKind: TUpdateKind; var Applied: Boolean);
begin
    Log('TDataSetProvider.BeforeUpdateRecord');
    if UpdateKind = ukInsert then
        if DeltaDS.FieldByName('ID').OldValue <= 0 then
            DeltaDS.FieldByName('ID').NewValue := GetNextID;
end;
```

```pascal
procedure TfrmMain.Log(const s: string);
begin
    LogEvents.Items.Add(s);
end;
```

```pascal
procedure TfrmMain.DataSetProvider1AfterApplyUpdates(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TDataSetProvider.AfterApplyUpdates');
end;
```

```pascal
procedure TfrmMain.DataSetProvider1AfterExecute(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TDataSetProvider.AfterExecute');
end;
```

```pascal
procedure TfrmMain.DataSetProvider1AfterGetParams(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TDataSetProvider.AfterGetParams');
end;
```

```pascal
procedure TfrmMain.DataSetProvider1AfterGetRecords(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TDataSetProvider.AfterGetRecords');
end;
```

```pascal
procedure TfrmMain.DataSetProvider1AfterRowRequest(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TDataSetProvider.AfterRowRequest');
end;
```

```pascal
procedure TfrmMain.DataSetProvider1AfterUpdateRecord(Sender: TObject;
    SourceDS: TDataSet; DeltaDS: TCustomClientDataSet;
    UpdateKind: TUpdateKind);
begin
    Log('TDataSetProvider.AfterUpdateRecord');
end;
```

```pascal
procedure TfrmMain.DataSetProvider1BeforeApplyUpdates(Sender: TObject;
    var OwnerData: OleVariant);
```

## 清单 7.1

```pascal
begin
  Log('TDataSetProvider.BeforeApplyUpdates');
end;

procedure TfrmMain.DataSetProvider1BeforeExecute(Sender: TObject;
  var OwnerData: OleVariant);
begin
  Log('TDataSetProvider.BeforeExecute');
end;

procedure TfrmMain.DataSetProvider1BeforeGetParams(Sender: TObject;
  var OwnerData: OleVariant);
begin
  Log('TDataSetProvider.BeforeGetParams');
end;

procedure TfrmMain.DataSetProvider1BeforeGetRecords(Sender: TObject;
  var OwnerData: OleVariant);
begin
  Log('TDataSetProvider.BeforeGetRecords');
end;

procedure TfrmMain.DataSetProvider1BeforeRowRequest(Sender: TObject;
  var OwnerData: OleVariant);
begin
  Log('TDataSetProvider.BeforeRowRequest');
end;

function TfrmMain.DataSetProvider1DataRequest(Sender: TObject;
  Input: OleVariant): OleVariant;
begin
  Log('TDataSetProvider.OnDataRequest');
end;

procedure TfrmMain.DataSetProvider1GetData(Sender: TObject;
  DataSet: TCustomClientDataSet);
begin
  Log('TDataSetProvider.OnGetData');
end;

procedure TfrmMain.DataSetProvider1GetDataSetProperties(Sender: TObject;
  DataSet: TDataSet; out Properties: OleVariant);
begin
  Log('TDataSetProvider.OnDataSetProperties');
end;

procedure TfrmMain.DataSetProvider1GetTableName(Sender: TObject;
  DataSet: TDataSet; var TableName: String);
begin
  Log('TDataSetProvider.OnGetTableName');
end;

procedure TfrmMain.DataSetProvider1UpdateData(Sender: TObject;
  DataSet: TCustomClientDataSet);
begin
  Log('TDataSetProvider.OnUpdateData');
end;

procedure TfrmMain.DataSetProvider1UpdateError(Sender: TObject;
  DataSet: TCustomClientDataSet; E: EUpdateError; UpdateKind: TUpdateKind;
  var Response: TResolveResponse);
begin
  Log('TDataSetProvider.OnUpdateError');
end;

procedure TfrmMain.ClientDataSet1AfterApplyUpdates(Sender: TObject;
  var OwnerData: OleVariant);
begin
  Log('TClientDataSet.AfterApplyUpdates');
end;

procedure TfrmMain.ClientDataSet1AfterExecute(Sender: TObject;
  var OwnerData: OleVariant);
begin
  Log('TClientDataSet.AfterExecute');
end;

procedure TfrmMain.ClientDataSet1AfterGetParams(Sender: TObject;
  var OwnerData: OleVariant);
begin
  Log('TClientDataSet.AfterGetParams');
end;

procedure TfrmMain.ClientDataSet1AfterGetRecords(Sender: TObject;
  var OwnerData: OleVariant);
begin
```
