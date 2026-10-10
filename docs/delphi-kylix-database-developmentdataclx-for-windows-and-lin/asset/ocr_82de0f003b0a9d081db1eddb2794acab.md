# LISTING 7.2  Continued

```
private
    { Private declerations }
    FNextID: Integer;
    function GetNextID: Integer;
public
    { Public declerations }
end;

var
    TfrmMain: TfrmMain;

implementation

{$R *.xfm}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
    CliNetDataSet1.Open;
end;

procedure TfrmMain.CliNetDataSet1NewRecord(DataSet: TDataSet);
begin
    Dec(FNextID);
    DataSet.FieldByName('CONTACTID').AsInteger := FNextID;
end;

function TfrmMain.GetNextID: Integer;
begin
    sqlID.ExecSQL;
    Result := sqlID.ParamByName('AValue').AsInteger;
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
    Connection := (SourceDS as TCustomSQLDataSet).SQLConnection;

case UpdateKind of
    ukInsert: begin
        ID := GetNextID;
```

# 7

![](bbox=[0.88, 0.32, 0.99, 0.43])