# LISTING 4.3 Continuned

```
uses
Types, IdGlobal, SysUtils, Variants, Classes, QGraphics, QControls, QForms,
QDialogs, QStdCtrls, DB, DBClient, QExtCtrls, QActnList, QGrids, QDBGrids,
QDBCtrls;

type
TfrmMain = class(TForm)
DataSource1: TDataSource;
pnlClient: TPanel;
pnlBottom: TPanel;
btnDisableEnable: TButton;
DBGid1: TDBGrid;
ClientDataSet1: TClientDataSet;
btnBaseline: TButton;
procedure FormCreate(Sender: TObject);
procedure btnDisableEnableClick(Sender: TObject);
procedure btnBaselineClick(Sender: TObject);
private
{ Private declarations }
procedure PerformWork;
public
{ Public declarations }
end;

var
frmMain: TfrmMain;

implementation

{$R *.xfm}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
ClientDataSet1.LoadFromFile('C:\Employee.cds');
end;

procedure TfrmMain.PerformWork;
var
Bookmark: TBookmark;
begin
Bookmark := ClientDataSet1.GetBookmark;
try
ClientDataSet1.First;
while not ClientDataSet1.EOF do begin
```