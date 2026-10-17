
# MainForm

```pascal
unit MainForm;

interface

uses
  SysUtils, Classes, Graphics, Controls, Forms, Dialogs, DB, Grids,
  DBGrids, DBClient, ExtCtrls, StdCtrls, DBCtrls;

type
  TfrmMain = class(TForm)
    ClientDataSet: TClientDataSet;
    DataSource1: TDataSource;
    pnOptions: TPanel;
    pnClient: TPanel;
    grid: TDBGrid;
    cbEditing: TCheckBox;
    cbAlwaysShowEditor: TCheckBox;
    cbTitles: TCheckBox;
    cbIndicator: TCheckBox;
    cbColumnResize: TCheckBox;
    cbColLines: TCheckBox;
    cbRowLines: TCheckBox;
    cbTabs: TCheckBox;
    cbRowSelect: TCheckBox;
    cbAlwaysShowSelection: TCheckBox;
    cbConfirmDelete: TCheckBox;
    cbCancelOnExit: TCheckBox;
    cbMultiSelect: TCheckBox;
    btnShowSelections: TButton;
    DBNavigator1: TDBNavigator;
    IbEvents: TListBox;
    Label1: TLabel;
    Label2: TLabel;
    btnClearEventLog: TButton;
    procedure FormCreate(Sender: TObject);
    procedure gridCellClick(Column: TColumn);
    procedure gridColExit(Sender: TObject);
    procedure gridColEnter(Sender: TObject);
    procedure gridColumnMoved(Sender: TObject; FromIndex,
        ToIndex: Integer);
    procedure gridEditButtonClick(Sender: TObject);
    procedure cbEditingClick(Sender: TObject);
    procedure cbAlwaysShowEditorClick(Sender: TObject);
    procedure cbTitlesClick(Sender: TObject);
    procedure cbIndicatorClick(Sender: TObject);
    procedure cbColumnResizeClick(Sender: TObject);
    procedure cbColLinesClick(Sender: TObject);
    procedure cbRowLinesClick(Sender: TObject);
    procedure cbTabsClick(Sender: TObject);
    procedure cbRowSelectClick(Sender: TObject);
    procedure cbAlwaysShowSelectionClick(Sender: TObject);
    procedure cbConfirmDeleteClick(Sender: TObject);
    procedure cbCancelOnExitClick(Sender: TObject);
    procedure cbMultiSelectClick(Sender: TObject);
    procedure btnShowSelectionsClick(Sender: TObject);
    procedure btnClearEventLogClick(Sender: TObject);
  private
    procedure RetrieveOptions;
    procedure UpdateOption(Option: TDBGridOption; Active: Boolean);
    { Private declarations }
  public
    { Public declarations }
  end;

var
    frmMain: TfrmMain;

implementation

{$R *.xfm}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
    ClientDataSet1.LoadFromFile('C:\Employee.CDS');

    RetrieveOptions;
end;

// Options set/get methods

procedure TfrmMain.RetrieveOptions;
begin
    cbEditing.Checked := (dgEditing in grid.Options);
    cbAlwaysShowEditor.Checked := (dgAlwaysShowEditor in grid.Options);
    cbTitles.Checked := (dgTitles in grid.Options);
    cbIndicator.Checked := (dgIndicator in grid.Options);
    cbColumnResize.Checked := (dgColumnResize in grid.Options);
    cbColLines.Checked := (dgColLines in grid.Options);
    cbRowLines.Checked := (dgRowLines in grid.Options);
    cbTabs.Checked := (dgTabs in grid.Options);
    cbRowSelect.Checked := (dgRowSelect in grid.Options);
    cbAlwaysShowSelection.Checked := (dgAlwaysShowSelection in grid.Options);
    cbConfirmDelete.Checked := (dgConfirmDelete in grid.Options);
    cbCancelOnExit.Checked := (dgCancelOnExit in grid.Options);
    cbMultiSelect.Checked := (dgMultiSelect in grid.Options);
end;

procedure TfrmMain.UpdateOption(Option: TDBGridOption; Active: Boolean);
begin
    if Active then
        grid.Options := grid.Options + [Option]
    else
        grid.Options := grid.Options - [Option];

    RetrieveOptions;
end;

procedure TfrmMain.cbEditingClick(Sender: TObject);
begin
  UpdateOption(dgEditing, cbEditing.Checked);
end;

procedure TfrmMain.cbAlwaysShowEditorClick(Sender: TObject);
begin
  UpdateOption(dgAlwaysShowEditor, cbAlwaysShowEditor.Checked);
end;

procedure TfrmMain.cbTitlesClick(Sender: TObject);
begin
  UpdateOption(dgTitles, cbTitles.Checked);
end;

procedure TfrmMain.cbIndicatorClick(Sender: TObject);
begin
  UpdateOption(dgIndicator, cbIndicator.Checked);
end;

procedure TfrmMain.cbColumnResizeClick(Sender: TObject);
begin
  UpdateOption(dgColumnResize, cbColumnResize.Checked);
end;

procedure TfrmMain.cbColLinesClick(Sender: TObject);
begin
  UpdateOption(dgColLines, cbColLines.Checked);
end;

procedure TfrmMain.cbRowLinesClick(Sender: TObject);
begin
  UpdateOption(dgRowLines, cbRowLines.Checked);
end;

procedure TfrmMain.cbTabsClick(Sender: TObject);
begin
  UpdateOption(dgTabs, cbTabs.Checked);
end;

procedure TfrmMain.cbRowSelectClick(Sender: TObject);
begin
  UpdateOption(dgRowSelect, cbRowSelect.Checked);
end;
```
