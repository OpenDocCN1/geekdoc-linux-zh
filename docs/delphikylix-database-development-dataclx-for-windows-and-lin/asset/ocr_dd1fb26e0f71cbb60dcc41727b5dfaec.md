# LISTING 4.9  Continued

```
DataSource1: TDataSource;
DBGrid1: TDBGrid;
btnUpdate: TButton;
btnInsert: TButton;
btnRange: TButton;
btnInsert2: TButton;
procedure FormCreate(Sender: TObject);
procedure FormDestroy(Sender: TObject);
procedure btnUpdateClick(Sender: TObject);
procedure btnInsertClick(Sender: TObject);
procedure btnRangeClick(Sender: TObject);
procedure btnInsert2Click(Sender: TObject);
private
{ Private declarations }
FCloneDS: TClientDataSet;
public
{ Public declarations }
end;

var
frmMain: TfrmMain;

implementation

{$R *.fmf}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
ClientDataSet1.LoadFromFile('C:\Employee.cds');

ClientDataSet1.AddIndex('byID', 'ID', [ixPrimary, ixUnique]);
ClientDataSet1.IndexName := 'byID';

FCloneDS := TClientDataSet.Create(nil);
FCloneDS.CloneCursor(ClientDataSet1, False, False);
end;

procedure TfrmMain.FormDestroy(Sender: TObject);
begin
FCloneDS.Free;
end;

procedure TfrmMain.btnUpdateClick(Sender: TObject);
begin
```