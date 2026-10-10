
```pascal
procedure TfrmMain.ClientDataSet1AfterScroll(DataSet: TDataSet);
begin
  if FLogScrollEvents then
    Log(logAfterScroll);

  lblRecPos.Caption := Format('Record %d of %d',
    [DataSet.RecNo, DataSet.RecordCount]);
end;

procedure TfrmMain.ClientDataSet1BeforeCancel(DataSet: TDataSet);
begin
  Log(logBeforeCancel);
end;

procedure TfrmMain.ClientDataSet1BeforeClose(DataSet: TDataSet);
begin
  Log(logBeforeClose);
end;

procedure TfrmMain.ClientDataSet1BeforeDelete(DataSet: TDataSet);
begin
  Log(logBeforeDelete);

  if FPromptOnDelete then begin
    if MessageDlg('Are you sure you want to delete the current record?',
      mtWarning, [mbYes, mbNo], 0) <> mrYes then
      Abort;
  end;
end;

procedure TfrmMain.ClientDataSet1BeforeEdit(DataSet: TDataSet);
begin
  Log(logBeforeEdit);
end;

procedure TfrmMain.ClientDataSet1BeforeInsert(DataSet: TDataSet);
begin
  Log(logBeforeInsert);
end;

procedure TfrmMain.ClientDataSet1BeforeOpen(DataSet: TDataSet);
begin
  Log(logBeforeOpen);
end;

procedure TfrmMain.ClientDataSet1BeforePost(DataSet: TDataSet);
begin
  Log(logBeforePost);
end;

procedure TfrmMain.ClientDataSet1BeforeScroll(DataSet: TDataSet);
begin
  if FLogScrollEvents then
    Log(logBeforeScroll);
end;

procedure TfrmMain.btnConnectClick(Sender: TObject);
begin
  ClientDataSet1.LoadFromFile('C:\Employee.cds');
end;

procedure TfrmMain.btnDisconnectClick(Sender: TObject);
begin
  ClientDataSet1.Close;
end;

procedure TfrmMain.btnClearLogClick(Sender: TObject);
begin
  lvLog.Items.Clear;
end;

procedure TfrmMain.btnOptionsClick(Sender: TObject);
var
  frmOptions: TfrmOptions;
begin
  frmOptions := TfrmOptions.Create(nil);
  try
    frmOptions.LogScrollEvents := FLogScrollEvents;
    frmOptions.PromptOnDelete := FPromptOnDelete;
    if frmOptions.ShowModal = mrOK then
    begin
      FLogScrollEvents := frmOptions.LogScrollEvents;
      FPromptOnDelete := frmOptions.PromptOnDelete;
    end;
  finally
    frmOptions.Free;
  end;
end;
```

![](img/fe651f295b5f960d5463c4fb581d2281_167_0.png)

图 4.1 展示了该应用程序在运行时的情形。主窗口的上半部分是一个数据感知网格，允许用户插入、编辑和删除记录。窗口的中间部分包含一个列表视图，它记录了对数据集执行的所有操作日志。窗口的底部是用于打开和关闭数据集、清除日志以及设置演示选项的按钮。

通过点击主窗口底部的“选项…”按钮，用户可以选择是否记录滚动事件以及是否在删除前进行确认，如图 4.1 所示。

![](img/fe651f295b5f960d5463c4fb581d2281_168_0.png)

# 图 4.1 EventLog 应用程序演示了客户端数据集事件。

列表 4.2 包含了该应用程序选项窗口的源代码，它允许用户指定程序在删除记录时是否提示用户，以及程序是否将数据集事件记录到列表框中。

# 列表 4.2 EventLog—OptionsForm.pas

```pascal
unit OptionsForm;

interface

uses
  SysUtils, Variants, Classes, QGraphics, QControls, QForms,
  QDialogs, QStdCtrls, QExtCtrls;

type
  TfrmOptions = class(TForm)
    pnlClient: TPanel;
    pnlBottom: TPanel;
    btnOk: TButton;
    btnCancel: TButton;
    cbLogScrollEvents: TCheckBox;
    cbPromptOnDelete: TCheckBox;

  private
    procedure SetLogScrollEvents(const Value: Boolean);
    function GetLogScrollEvents: Boolean;
    function GetPromptOnDelete: Boolean;
    procedure SetPromptOnDelete(const Value: Boolean);
    { Private declarations }
  public
    { Public declarations }
    property LogScrollEvents: Boolean
      read GetLogScrollEvents write SetLogScrollEvents;
    property PromptOnDelete: Boolean
      read GetPromptOnDelete write SetPromptOnDelete;

  end;

implementation

{$R *.xfm}

{ TfrmOptions }

function TfrmOptions.GetLogScrollEvents: Boolean;
begin
  Result := cbLogScrollEvents.Checked;
end;

function TfrmOptions.GetPromptOnDelete: Boolean;
begin
  Result := cbPromptOnDelete.Checked;
end;

procedure TfrmOptions.SetLogScrollEvents(const Value: Boolean);
begin
  cbLogScrollEvents.Checked := Value;
end;

procedure TfrmOptions.SetPromptOnDelete(const Value: Boolean);
begin
  cbPromptOnDelete.Checked := Value;
end;

end.
```

# 禁用数据感知组件

这一主题实际上适用于所有 Delphi 数据集，但我是在客户端数据集的背景下讨论它的，因为通常不会将数据感知组件直接连接到 dbExpress 数据集。通常，数据感知组件是连接到客户端数据集的。

如本章所学，数据感知组件会主动跟踪其连接的数据集中的当前记录。虽然这通常是一件好事，但有时你希望防止数据感知组件更新。这种情况最常发生在你滚动数据集以对记录执行操作时，你不想看到所有数据感知组件快速更新。例如，请查看以下代码片段：
