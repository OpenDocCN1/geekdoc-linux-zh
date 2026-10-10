# **LISTING 7.1** Continued

```
begin
    Log('TClientDataSet.AfterRefresh');
end;

procedure TfrmMain.ClientDataSet1AfterRowRequest(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TClientDataSet.AfterRowRequest');
end;

procedure TfrmMain.ClientDataSet1BeforeApplyUpdates(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TClientDataSet.BeforeApplyUpdates');
end;

procedure TfrmMain.ClientDataSet1BeforeExecute(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TClientDataSet.BeforeExecute');
end;

procedure TfrmMain.ClientDataSet1BeforeGetParams(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TClientDataSet.BeforeGetParams');
end;

procedure TfrmMain.ClientDataSet1BeforeGetRecords(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TClientDataSet.BeforeGetRecords');
end;

procedure TfrmMain.ClientDataSet1BeforeRefresh(DataSet: TDataSet);
begin
    Log('TClientDataSet.BeforeRefresh');
end;

procedure TfrmMain.ClientDataSet1BeforeRowRequest(Sender: TObject;
    var OwnerData: OleVariant);
begin
    Log('TClientDataSet.BeforeRowRequest');
end;
```