# **LISTING 7.1** Continued

```
```text
begin
  ClientDataSet1.Open;
end;

procedure TfrmMain.Timer1Timer(Sender: TObject);
begin
  lblUpdates.Caption := IntToStr(ClientDataSet1.ChangeCount) + ' Update(s)';
end;

procedure TfrmMain.btnApplyUpdatesClick(Sender: TObject);
begin
  ShowMessage('ApplyUpdates returned a value of ' +
    IntToStr(ClientDataSet1.ApplyUpdates(0)));
end;

procedure TfrmMain.btnCancelUpdatesClick(Sender: TObject);
begin
  ClientDataSet1.CancelUpdates;
end;

procedure TfrmMain.ClientDataSet1ReconcileError(
  DataSet: TCustomClientDataSet; E: EReconcileError;
  UpdateKind: TUpdateKind; var Action: TReconcileAction);
begin
  Action := HandleReconcileError(DataSet, UpdateKind, E);
end;

function TfrmMain.GetNextID: Integer;
begin
  sqlID.ExecSQL;
  Result := sqlID.ParamByName('AValue').AsInteger;
end;

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
```