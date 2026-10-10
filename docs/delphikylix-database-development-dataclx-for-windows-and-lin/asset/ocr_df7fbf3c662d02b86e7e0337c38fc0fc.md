# **LISTING 7.2** Continued

```
private
 { Private declarations }
 FNextID: Integer;
 function GetNextID: Integer;
public
 { Public declarations }
end;
var
 frmMain: TfrmMain;
implementation
($R *.xfm)
procedure TfrmMain.FormCreate(Sender: TObject);
begin
 ClientDataSet1.Open;
end;

procedure TfrmMain.ClientDataSet1NewRecord(DataSet: TDataSet);
begin
 Dec(FNextID);
 DataSet.FieldName('CONTACTID') .AsInteger := FNextID;
end;

function TfrmMain.GetNextID: Integer;
begin
 sqlID.ExecSQL;
 Result := sqlID.ParamByName('AVALUE').AsInteger;
end;

procedure TfrmMain.DataSetProvider1BeforeUpdateRecord(Sender: TObject;
 SourceDS: TDataSet; DeltaDS: TCustomClientDataSet;
 UpdateKind: TUpdateKind; var Applied: Boolean);
var
 SQL: string;
 Connection: TSQLConnection;
 ID: Integer;
begin
 // Obtain a pointer to the connection from the source dataset
 Connection := ((SourceDS as TCustomSQLDataSet).SQLConnection;

case UpdateKind of
 ukInsert: begin
 ID := GetNextID;
```