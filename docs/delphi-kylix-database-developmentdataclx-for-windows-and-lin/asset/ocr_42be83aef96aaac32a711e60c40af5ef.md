# LISTING 4.9 Continued

```
Screen.Cursor := crHourglass;
try
FClonedDS.First;
while not FClonedDS.EOF do begin
FClonedDS.Edit;
FClonedDS.FieldName('Salary ').AsFloat :=
FClonedDS.FieldName(' Salary ').AsFloat * 1.10;
FClonedDS.Post;

FClonedDS.Next;
end;
finally
Screen.Cursor := crDefault;
end;

procedure TfmrMain.btnInsertClick(Sender: TObject);
begin
if FClonedDS.State <> dsBrowse then
Exit;

FClonedDS.Append;
FClonedDS.FieldName('ID').AsInteger := 99999;
FClonedDS.FieldName('Name').AsString := 'Eric Harmon';
FClonedDS.FieldName(' Birthday ').AsString := '1/1/1967';
FClonedDS.FieldName('Salary ').AsFloat := 1.00;
end;

procedure TfmrMain.btnInsert2Click(Sender: TObject);
begin
if FClonedDS.State <> dsInsert then
Exit;

try
FClonedDS.Post;
CllentDataSet1.GotoCurrent(FClonedDS);
except
FClonedDS.Cancel;
raise;
end;

procedure TfmrMain.btnRangeClick(Sender: TObject);
begin
```