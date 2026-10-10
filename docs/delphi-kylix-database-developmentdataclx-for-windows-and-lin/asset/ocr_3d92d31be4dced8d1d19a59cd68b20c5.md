If you would like to view only those records that have been added to the dataset, you can set `StatusFilter` to `usInserted`. To view only added or modified records, set `StatusFilter` to `usInserted, usModified`.

# Viewing the Change Log

Because, in reality, the change log is just another dataset, you can view it in a grid just like you can with any other dataset. To do this, you need to assign the change log from the data of one dataset to the data of another dataset, like this:

```
cdsChangeLog.Data := C1ientDataSet1.Delta;
```

If `C1ientDataSet1`'s change log is empty, this statement causes a `Delta is empty` exception to be raised. So, you should always check the `ChangeCount` property before attempting to do this.

The following sample application demonstrates the techniques discussed in this section. Listing 4.7 contains the source code for the main form of the application.

# LISTING 4.7 ChangeLog—MainForm.pas

```
unit MainForm;

interface

uses
  SysUtils, Variants, Classes, QGraphics, QControls, QForms,
  QDialogs, QStdCtrls, DB, DBCClient, QExtCtrls, QActnList, QGrids, QDBGrids;

type
  TfrmMain = class(TForm)
    DataSource1: TDataSource;
    pnlClient: TPanel;
    DBGrid1: TDBGrid;
    C1ientDataSet1: TC1ientDataSet;
    pnlBottom: TPanel;
    btnRemoveFilter: TButton;
    btnFilter: TButton;
    btnUndo: TButton;
    btnRevertRecord: TButton;
    btnCancelUpdates: TButton;
    btnSetSavepoint: TButton;
    btnGotolSavepoint: TButton;
    btnViewChangeLog: TButton;
    procedure FormCreate(Sender: TObject);
    procedure btnRemoveFilterClick(Sender: TObject);
    procedure btnFilterClick(Sender: TObject);
```