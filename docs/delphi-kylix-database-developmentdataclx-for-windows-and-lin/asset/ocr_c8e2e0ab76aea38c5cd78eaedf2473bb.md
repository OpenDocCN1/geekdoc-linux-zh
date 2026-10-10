# **LISTING 5.4**    Continued

```
procedure TfrmMain.ClientDataSet1NewRecord(DataSet: TDataSet);
begin
  DataSet.FieldName('Enabled').AsString := 'T';
  DataSet.FieldName('Active').AsString := 'T';
end;

procedure TfrmMain.DataSource1DataChange(Sender: TObject; Field: TField);
begin
  if Field = nil then
    lbDSEvents.Items.Add('Data Change: Field = nil')
  else
    lbDSEvents.Items.Add('Data Change: Field = ' + Field.FieldName);

  lblCurrent.Caption := Format('('Record %d of %d)',
    [ClientDataSet1.RecNo, ClientDataSet1.RecordCount]);
end;

procedure TfrmMain.DataSource1StateChange(Sender: TObject);
begin
  lbDSEvents.Items.Add('State Change');

  case DataSource1.State of
    dsInactive: lblState.Caption := 'Inactive';
    dsBrowse: lblState.Caption := 'Browse';
    dsEdit: lblState.Caption := 'Edit';
    dsInsert: lblState.Caption := 'Insert';
  end;
end;

procedure TfrmMain.DataSource1UpdateData(Sender: TObject);
begin
  lbDSEvents.Items.Add('Update Data')
end;

procedure TfrmMain.btnLoadClick(Sender: TObject);
begin
  if OpenDialog1.Execute then begin
    ClientDataSet1.Edit;
    ClientDataSet1Image.LoadFromFile(OpenDialog1.FileName);
  end;
end;

procedure TfrmMain.btnClearClick(Sender: TObject);
```