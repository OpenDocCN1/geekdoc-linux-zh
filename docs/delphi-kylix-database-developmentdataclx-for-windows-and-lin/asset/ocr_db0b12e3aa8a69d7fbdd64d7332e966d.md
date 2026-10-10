You can learn a lot about how datasets work by handling all these events and logging their calls to either a log file or a list box. In the following example, I’ve done just that. Listing 4.1 contains the complete source code for the EventLog application.

# **LISTING 4.1**  EventLog—MainForm.pas

```
```pascal
unit MainForm;

interface

uses
  SysUtils, Variants, Classes, QGraphics, QControls, QForms,
  QDialogs, DB, DBClient, QComCtrls, QGrids, QDBGrids, QExtCtrls, QStdCtrls,
  QDBCtrls;

type
  TLogEventType = (logBeforeCancel, logBeforeClose, logBeforeDelete,
    logBeforeEdit, logBeforeInsert, logBeforeOpen, logBeforePost,
    logBeforeScroll, logAfterCancel, logAfterClose, logAfterDelete,
    logAfterEdit, logAfterInsert, logAfterOpen, logAfterPost, logAfterScroll);

  TfrmMain = class(TForm)
    ClientDataSet1: TClientDataSet;
    pnlClient: TPanel;
    pnlLog: TPanel;
    grid: TDBGrid;
    lvLog: TListView;
    DataSource1: TDataSource;
    pnlBottom: TPanel;
    btnConnect: TButton;
    lblRecPos: TLabel;
    btnDisconnect: TButton;
    btnClearLog: TButton;
    DBNavigator1: TDBNavigator;
    btnOptions: TButton;
    procedure ClientDataSet1AfterCancel(DataSet: TDataSet);
    procedure ClientDataSet1AfterClose(DataSet: TDataSet);
    procedure ClientDataSet1AfterDelete(DataSet: TDataSet);
    procedure ClientDataSet1AfterEdit(DataSet: TDataSet);
    procedure ClientDataSet1AfterOpen(DataSet: TDataSet);
    procedure ClientDataSet1AfterPost(DataSet: TDataSet);
    procedure ClientDataSet1AfterScroll(DataSet: TDataSet);
    procedure btnConnectClick(Sender: TObject);
```
```