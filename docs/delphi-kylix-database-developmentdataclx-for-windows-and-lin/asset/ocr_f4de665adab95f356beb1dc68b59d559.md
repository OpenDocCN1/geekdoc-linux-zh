# **LISTING 4.7** Continued

```
```pascal
procedure btnUndoClick(Sender: TObject);
procedure btnRevertRecordClick(Sender: TObject);
procedure btnCancelUpdatesClick(Sender: TObject);
procedure btnSetSavepointClick(Sender: TObject);
procedure btnGoToSavepointClick(Sender: TObject);
procedure btnViewChangeLogClick(Sender: TObject);
private
  { Private declarations }
  FSavePoint: Integer;
public
  { Public declarations }
end;
var
  frmMain: TfrmMain;
implementation
uses ChangeLogForm;
{$R *.xfm}
procedure TfrmMain.FormCreate(Sender: TObject);
begin
  ClientDataSet1.LoadFromFile('C:\Employee.cds');
  ClientDataSet1.MergeChangeLog;
end;
procedure TfrmMain.btnFilterClick(Sender: TObject);
begin
  ClientDataSet1.StatusFilter := [usInserted];
end;
procedure TfrmMain.btnRemoveFilterClick(Sender: TObject);
begin
  ClientDataSet1.StatusFilter := [];
end;
procedure TfrmMain.btnUndoClick(Sender: TObject);
begin
  ClientDataSet1.UndoLastChange(True);
end;
procedure TfrmMain.btnRevertRecordClick(Sender: TObject);
begin
  ClientDataSet1.RevertRecord;
end;
```
```