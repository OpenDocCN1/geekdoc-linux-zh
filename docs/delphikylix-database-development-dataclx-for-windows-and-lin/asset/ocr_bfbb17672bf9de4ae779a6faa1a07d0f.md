# **LISTING 3.7** Search—MainForm.pas

```
```
unit MainForm;

interface

uses
  SysUtils, Classes, Variants, QGraphics, QControls, QForms, QDialogs,
  QStdCtrls, DB, DBClient, QExtCtrls, QActNlist, QGrids, QDBGrids;

type
  TfrmMain = class(TForm)
    DataSource1: TDataSource;
    pnlClient: TPanel;
    pnlBottom: TPanel;
    btnSearch: TButton;
    btnGotoBookmark: TButton;
    btnEndBookmark: TButton;
    btnLookup: TButton;
    DBOldID: TDBGrid;
    ClientDataSet1: TClientDataSet;
    btnSetRecNo: TButton;
    procedure FormCreate(Sender: TObject);
    procedure btnGetToBookmarkClick(Sender: TObject);
    procedure btnGotToBookmarkClick(Sender: TObject);
    procedure btnSetRecNoClick(Sender: TObject);
    procedure btnSearchClick(Sender: TObject);
    procedure btnLookupClick(Sender: TObject);
  private
    { Private declarations }
    FBookmark: TBookmark;
  public
    { Public declarations }
  end;

var
  frmMain: TfrmMain;

implementation

uses SearchForm;

{$R *.xfm}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
```
```

![](bbox=[0.88, 0.45, 0.98, 0.58])