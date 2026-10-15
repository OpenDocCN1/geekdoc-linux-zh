
## 清单 7.2 续

```pascal
unit MainForm;
interface
uses
  SysUtils, Types, Classes, Graphics, Controls, Forms, Dialogs,
  StdCtrls, DBXpress, FMTBcd, DB, SQLExpr, Grids, QDBGrids, Provider,
  DBClient, Variants;

type
  TfrmMain = class(TForm)
    DataSource1: TDataSource;
    DBGrid1: TDBGrid;
    SQConnection1: TSqlConnection;
    SQLDataSet1: TSQLDataSet;
    DataSetProvider1: TDataSetProvider;
    ClientDataSet1: TClientDataSet;
    sqLID: TSQLDataSet;
    btnApplyUpdates: TButton;
    procedure FormCreate(Sender: TObject);
    procedure DataSetProvider1BeforeUpdateRecord(Sender: TObject;
      SourceDS: TDataSet; DeltaDS: TCustomClientDataSet;
      UpdateKind: TUpdateKind; var Applied: Boolean);
    procedure btnApplyUpdatesClick(Sender: TObject);
    procedure ClientDataSet1NewRecord(DataSet: TDataSet);
```

```pascal
private
    { Private declarations }
    FNextID: Integer;
    function GetNextID: Integer;
public
    { Public declarations }
end;

var
    TfrmMain: TfrmMain;

implementation

{$R *.xfm}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
    ClientDataSet1.Open;
end;

procedure TfrmMain.ClientDataSet1NewRecord(DataSet: TDataSet);
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

![](img/fe651f295b5f960d5463c4fb581d2281_317_0.png)

## 清单 7.2（续）

```pascal
// Insert into the first table
SQL := Format('INSERT INTO CONTACTS (CONTACTID, FIRST, LAST) ' +
             'VALUES (%d, %s, %s)',
             [ID, QuotedStr(DeltaDS.FieldName('FIRST').NewValue),
             QuotedStr(DeltaDS.FieldName('LAST').NewValue)]);
Connection.Execute(SQL, nil, nil);

// Insert into the second table
SQL := Format('INSERT INTO CONTACTS2 (CONTACTID, SPOUSE) ' +
             'VALUES (%d, %s)',
             [ID, QuotedStr(DeltaDS.FieldName('SPOUSE').NewValue)]);
Connection.Execute(SQL, nil, nil);
end;
```
