# LISTING 9.4 Continued

```
```pascal
resource string
  SConnectCaption = 'Database Server';
  SConnectPrompt  = 'Server:';

{$R *.dfm}

procedure TDM.DataModuleCreate(Sender: TObject);
begin
  cdsContacts.Open;
end;

procedure TDM.DataModuleDestroy(Sender: TObject);
begin
  cdsContacts.Close;
  SocketConnection1.Close;
end;

// Dataset events

procedure TDM.cdsContactsNewRecord(DataSet: TDataSet);
begin
  DataSet.FieldByName('CONTACTID').AsInteger :=
    GetNextID(DataSet as TCustomClientDataSet, 'CONTACTID');
end;

procedure TDM.cdsContactsCalcFields(DataSet: TDataSet);
begin
  DataSet.FieldByName('FullName').AsString :=
    DataSet.FieldByName('FIRST').AsString + ' ' +
    DataSet.FieldByName('LAST').AsString;
end;

procedure TDM.cdsContactsReconcileError(DataSet: TCustomClientDataSet;
  E: EReconcileError; UpdateKind: TUpdateKind;
  var Action: TReconcileAction);
begin
  Action := HandleReconcileError(DataSet, UpdateKind, E);
end;

procedure TDM.cdsTodosNewRecord(DataSet: TDataSet);
begin
  DataSet.FieldByName('TODOID').AsInteger :=
    GetNextID(DataSet as TCustomClientDataSet, 'TODOID');
end;
```
```