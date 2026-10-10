# Example: Creating, Populating, and Manipulating a Client Dataset

The following example illustrates how to create, populate, and manipulate a client dataset at runtime. Code is also provided to save the dataset to disk and to load it.

Listing 3.1 shows the complete source code for the CDS (ClientDataset) application.

# **LISTING 3.1**  CDS\u2014MainForm.pas

```
```
unit MainForm;

interface
uses
  SysUtils, Types, IdGlobal, Classes, QGraphics, QControls, QForms, QDialogs,
  QStdCtrls, DB, DBClient, QExtCtrls, QGrids, QDBGriDs, QActnList;

const
  MAX_RECS = 10000;

type
  TfrmMain = class(TForm)
    DataSource1: TDataSource;
    pnlClient: TPanel;
    pnlBottom: TPanel;
    btnPopulate: TButton;
    btnSave: TButton;
    btnLoad: TButton;
    ActionList1: TActionList;
    btnStatistics: TButton;
    Populate1: TAction;
    Statistics1: TAction;
    Load1: TAction;
    Save1: TAction;
    DBGriD1: TDBGriD;
    lblFeedback: TLabel;
    procedure FormCreate(Sender: TObject);
    procedure PopulateExecute(Sender: TObject);
    procedure StatisticsExecute(Sender: TObject);
    procedure SaveExecute(Sender: TObject);
    procedure LoadExecute(Sender: TObject);
  private
    { Private declarations }
    FCDS: TClientDataSet;
  public
```
```