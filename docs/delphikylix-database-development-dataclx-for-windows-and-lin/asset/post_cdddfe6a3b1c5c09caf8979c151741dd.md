
The cdsContactsNewRecord and cdsTodosNewRecord events make a call to the local method GetNextID. GetNextID clones the dataset in question and moves to the first record in the dataset. The first record is the record with the lowest numbered ID. It then assigns the next lower number to the ID of that record, ensuring that the record has a negative primary key.

The reason this is done is to ensure that all records that have not yet been added to the database have a negative ID. The server-side data module checks for a negative ID and then calls the database's GEN ID stored procedure to assign a unique ID. This ensures that all added records receive a unique ID, regardless of what computer they were added from. (Remember that multiple users may be running this application at the same time.)

# Note

An alternative to using the cloned dataset to retrieve the next negative ID is to set up a private variable and retrieve the next ID at program startup. That way you can simply decrement the variable to obtain the next ID. The reason I don't do this is because in real-world applications I sometimes have 40 or 50 datasets in my data module. I don't like to set up 40 or 50 variables—one for each dataset. Instead, I use the common function to retrieve the next ID on the fly.

Note that cloning a dataset does temporarily require a small amount of memory, and also takes a small amount of time to do. If you need to generate temporary IDs as quickly as possible, you should consider using a private variable instead.

Listing 9.5 contains the source code for the client's main form, which is where the bulk of the code for this application lies.

## LISTING 9.5 ConMan—MainForm.pas

```pascal
unit MainForm;

interface

uses
  Windows, Messages, SysUtils, Variants, Classes, Graphics, Controls, Forms,
  Dialogs, DBActns, StdCtrls, ActnList, ImgList, ActnCtrls, ToolWin,
  ActnMan, ActnMenus, ComCtrls, BandActn, ExtCtrls, Menus, Grids, DBGrids,
  DB, StdCtrls, OBControls, Mask, ExtDlgs;

type
  TfrmMain = class(TForm)
    StatusBar1: TStatusBar;
    ImageList1: TImageList;
    MainMenu: TMainMenu;
    ActionList: TActionList;
    FileExit: TFileExit;
    EditCut: TEditCut;
    EditCopy: TEditCopy;
    EditPaste: TEditPaste;
    EditSelectAll: TEditSelectAll;
    EditUndo: TEditUndo;
    EditDelete: TEditDelete;
    DataSetFirst: TDataSetFirst;
    DataSetPrior: TDataSetPrior;
    DataSetNext: TDataSetNext;
    DataSetLast: TDataSetLast;
    DataSetInsert: TDataSetInsert;
    DataSetDelete: TDataSetDelete;
    DataSetEdit: TDataSetEdit;
    DataSetPost: TDataSetPost;
    DataSetCancel: TDataSetCancel;
    DataSetRefresh: TDataSetRefresh;
    File: TMenuItem;
    Exit: TMenuItem;
    Edit: TMenuItem;
    Copy: TMenuItem;
    Cut: TMenuItem;
    Paste: TMenuItem;
    SelectAll: TMenuItem;
    Delete: TMenuItem;
    Undo: TMenuItem;
    N1: TMenuItem;
    ToolBar: TToolBar;
    ToolButton1: TToolButton;
    ToolButton2: TToolButton;
    ToolButton3: TToolButton;
    pnlClient: TPanel;
    PageControl1: TPageControl;
    tabGrid: TTabSheet;
    tabForm: TTabSheet;
    gridContacts: TDBGrid;
    ntTodos: TPanel;
    Contact: TDataSource;
    dsTodos: TDataSource;
    PageControl2: TPageControl;
    TabTodos: TTabSheet;
    tabNotes: TTabSheet;
    gridTodos: TDBGrid;
    memoNotes: TDBMemo;
    DataSet1: TMenuItem;
    First1: TMenuItem;
    Prior1: TMenuItem;
    Next1: TMenuItem;
    Last1: TMenuItem;
    N2: TMenuItem;
    Insert1: TMenuItem;
    Edit2: TMenuItem;
    Post1: TMenuItem;
    Delete2: TMenuItem;
    Cancel1: TMenuItem;
    N3: TMenuItem;
    Refresh1: TMenuItem;
    FileConnect1: TAction;
    ConnectToDatabaseServer1: TMenuItem;
    N4: TMenuItem;
    DataSetNumUpdates: TAction;
    DataSetApplyUpdates: TAction;
    DataSetCancelUpdates: TAction;
    N5: TMenuItem;
    ApplyUpdates1: TMenuItem;
    CancelUpdates1: TMenuItem;
    popupTodos: TPopupMenu;
    MarkDone1: TMenuItem;
    ToolMarkDone1: TAction;
    TodoAdd: TAction;
    AddTodo1: TMenuItem;
    N6: TMenuItem;
    btnLoadImage: TButton;
    btnClearImage: TButton;
    ImageLoad1: TAction;
    ImageClear1: TAction;
    OpenPictureDialog1: TOpenPictureDialog;
    ToolButton4: TToolButton;
    ToolButton5: TToolButton;
    ToolButton6: TToolButton;
    ToolButton7: TToolButton;
    ToolButton8: TToolButton;
    ToolButton9: TToolButton;
    ToolButton10: TToolButton;
    ToolButton11: TToolButton;
    ToolButton12: TToolButton;
    ToolButton13: TToolButton;
    ToolButton14: TToolButton;
    ToolButton16: TToolButton;
    ToolButton17: TToolButton;
    imgPhoto: TImage;
    TodoEdit1: TAction;
    TodoDelete: TAction;
    EditTodo1: TMenuItem;
    PageControl3: TPageControl;
    tabClientGeneral: TTabSheet;
    tabClientAddress: TTabSheet;
    tabClientPhones: TTabSheet;
    Label1: TLabel;
    ecCompanyName: TDBEdit;
    Label12: TLabel;
    ecFirst: TDBEdit;
    Label13: TLabel;
    ecLast: TDBEdit;
    Label14: TLabel;
    ecDear: TDBEdit;
    Label15: TLabel;
    ecTitle: TDBEdit;
    Label16: TLabel;
    ecAddress1: TDBEdit;
    ecAddress2: TDBEdit;
    Label17: TLabel;
    Label18: TLabel;
    ecCity: TDBEdit;
    ecState: TDBEdit;
    Label19: TLabel;
    Label110: TLabel;
    ecPostalCode: TDBEdit;
    ecCountry: TDBEdit;
    Label11: TLabel;
    Label112: TLabel;
    ecPhone: TDBEdit;
    Label113: TLabel;
    ecFax: TDBEdit;
    ecCellular: TDBEdit;
    Label114: TLabel;
    Label115: TLabel;
    ecPager: TDBEdit;
    ecEmail: TDBEdit;
    Label116: TLabel;
    DeleteTodo1: TMenuItem;
    procedure FileConnect1Update(Sender: TObject);
    procedure FileConnect1Execute(Sender: TObject);
    procedure StatusBar1DrawPanel(StatusBar: TStatusBar;
      Panel: TStatusPanel; const Rect: TRect);
    procedure DataSetNumUpdatesUpdate(Sender: TObject);
    procedure DataSetApplyUpdatesExecute(Sender: TObject);
    procedure DataSetCancelUpdatesExecute(Sender: TObject);
    procedure OnHaveUpdates(Sender: TObject);
    procedure TodoMarkDone1Execute(Sender: TObject);
    procedure TodoAddExecute(Sender: TObject);
    procedure TodoMarkDone1Update(Sender: TObject);
    procedure ImageLoad1Execute(Sender: TObject);
    procedure ImageClear1Execute(Sender: TObject);
    procedure FormCloseQuery(Sender: TObject; var CanClose: Boolean);
    procedure dsContactsDataChange(Sender: TObject; Field: TField);
    procedure FormCreate(Sender: TObject);
    procedure TodoEditExecute(Sender: TObject);
    procedure TodoEditUpdate(Sender: TObject);
    procedure TodoDeleteExecute(Sender: TObject);
  private
    procedure DoConnectDisconnect(Sender: TObject);
    { Private declarations }
  public
    { Public declarations }
  end;

var
  frmMain: TfrmMain;

implementation

uses DataModule, TodoForm;

resourcestring
  SConnect = '&Connect to Database Server';
  SDisconnect = '&Disconnect from Database Server';
  SOneUpdate = '1 update pending';
  SUpdates = '%d updates pending';
  SOnline = 'Online';
  SOffline = 'Offline';
  SChangesPending = 'The current contact has been changed. ' +
    'Do you want to save changes to this record?';

{$R *.dfm}

// Form event handlers

procedure TfrmMain.FormCreate(Sender: TObject);
begin
  DM.SocketConnection1.AfterConnect := DoConnectDisconnect;
  DM.SocketConnection1.AfterDisconnect := DoConnectDisconnect;
end;

procedure TfrmMain.FormCloseQuery(Sender: TObject; var CanClose: Boolean);
begin
  if DM.cdsContacts.State <> dsBrowse then
  begin
    case MessageDlg(SChangesPending, mtWarning, [mbYes, mbNo, mbCancel], 0) of
      mrYes:    DM.cdsContacts.Post;
      mrNo:     DM.cdsContacts.Cancel;
      mrCancel: CanClose := False;
    end;
  end;
end;

procedure TfrmMain.DoConnectDisconnect(Sender: TObject);
begin
  // Repaint the status bar to reflect the new connection status
  StatusBar1.Invalidate;
end;

// Status bar event handlers

procedure TfrmMain.StatusBar1DrawPanel(StatusBar: TStatusBar;
  Panel: TStatusPanel; const Rect: TRect);
begin
  if Panel.Index = 0 then
  begin
    if DM.SocketConnection1.Connected then
    begin
      StatusBar.Canvas.Font.Color := clGreen;
      StatusBar.Canvas.TextRect(Rect, Rect.Left + 2, Rect.Top + 1,
        SOnline);
    end
    else
    begin
      StatusBar.Canvas.Font.Color := clRed;
      StatusBar.Canvas.TextRect(Rect, Rect.Left + 2, Rect.Top + 1,
        SOffline);
    end;
  end;
end;

// Database component event handlers

procedure TfrmMain.dsContactsDataChange(Sender: TObject; Field: TField);
var
  BlobStream: TStream;
begin
  if (Field = nil) or (Field = DM.cdsContactsIMAGE) then
  begin
    BlobStream := DM.cdsContacts.CreateBlobStream(DM.cdsContactsIMAGE, bmRead);
    try
      if BlobStream.Size = 0 then
        imgPhoto.Picture := nil
      else
        imgPhoto.Picture.Bitmap.LoadFromStream(BlobStream);
    finally
      BlobStream.Free;
    end;
  end;
end;

// Image controls

procedure TfrmMain.ImageLoad1Execute(Sender: TObject);
begin
  if OpenPictureDialog1.Execute then
  begin
    DM.cdsContacts.Edit;
    DM.cdsContactsIMAGE.LoadFromFile(OpenPictureDialog1.FileName);
  end;
end;

procedure TfrmMain.ImageClear1Execute(Sender: TObject);
begin
  DM.cdsContacts.Edit;
  DM.cdsContactsIMAGE.Clear;
end;

// File menu

procedure TfrmMain.FileConnect1Execute(Sender: TObject);
begin
  DM.SocketConnection1.Connected := not DM.SocketConnection1.Connected;
end;

procedure TfrmMain.FileConnect1Update(Sender: TObject);
```
