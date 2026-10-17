
```delphi
unit MainForm;

interface

uses
  SysUtils, Classes, QGraphics, QControls, QForms, QDialogs, QStdCtrls,
  DB, DBClient, QExtCtrls, QGrids, QDBGrids;

type
   TfrmMain = class(TForm)
     DataSource1: TDataSource;
     pnlClient: TPanel;
     pnlBottom: TPanel;
     btnFilter: TButton;
     btnRange: TButton;
     DBGird1: TDBGird;
     ClientDataSet1: TClientDataSet;
     btnClearRange: TButton;
     btnClearFilter: TButton;
     procedure FormCreate(Sender: TObject);
     procedure btnFilterClick(Sender: TObject);
     procedure btnRangeClick(Sender: TObject);
     procedure btnClearRangeClick(Sender: TObject);
     procedure btnClearFilterClick(Sender: TObject);
   private
     { Private declarations }
   public
     { Public declarations }
   end;

var
  frmMain: TfrmMain;

implementation

uses FilterForm, RangeForm;

{$R *.xfm}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
  ClientDataSet1.LoadFromFile('C:\Employee.CDS');
  ClientDataSet1.AddIndex('bySalary', 'Salary', []);
  ClientDataSet1.IndexName := 'bySalary';
end;

procedure TfrmMain.btnFilterClick(Sender: TObject);
var
 frmFilter: TfrmFilter;
begin
  frmFilter := TfrmFilter.Create(nil);
try
if frmFilter.ShowModal = mrOK then begin
  ClientDataSet1.Filter := frmFilter.Filter;
  ClientDataSet1.Filtered := True;
end;
finally
  frmFilter.Free;
end;
end;

procedure TfrmMain.btnClearFilterClick(Sender: TObject);
begin
  ClientDataSet1.Filtered := False;
end;

procedure TfrmMain.btnRangeClick(Sender: TObject);
var
  frmRange: TfrmRange;
begin
  frmRange := TfrmRange.Create(nil);
  try
    if frmRange.ShowModal = mrOK then
      ClientDataSet1.SetRange([[frmRange.LowValue]], [frmRange.HighValue]);
  finally
    frmRange.Free;
  end;
end;

procedure TfrmMain.btnClearRangeClick(Sender: TObject);
begin
  ClientDataSet1.CancelRange;
end;

end.
```

如您所见，主窗体从磁盘加载员工数据集，在 `Salary` 字段上创建索引，并使该索引处于活动状态。然后，它允许用户对数据集应用范围、筛选，或者两者都应用。

### 列表 3.5 包含筛选窗体的源代码。筛选窗体是一个简单的窗体，允许用户选择要筛选的字段，并输入要筛选的值。

## 列表 3.5 RangeFilter—FilterForm.pas

```delphi
unit FilterForm;

interface

uses
  SysUtils, Classes, QGraphics, QControls, QForms, QDialogs, QStdCtrls,
  QExtCtrls;

type
  TfrmFilter = class(TForm)
    pnlClient: TPanel;
    pnlBottom: TPanel;
    Label1: TLabel;
    cbField: TComboBox;
    Label2: TLabel;
    cbRelationship: TComboBox;
    Label3: TLabel;
    ecValue: TEdit;
    btnOk: TButton;
    btnCancel: TButton;
  private
    function GetFilter: string;
    { Private declarations }
  public
    { Public declarations }
    property Filter: string read GetFilter;
  end;

implementation

{$R *.xfm}

{ TfrmFilter }

function TfrmFilter.GetFilter: string;
begin
  Result := Format('%s %s ''%s'',
    [cbField.Text, cbRelationship.Text, ecValue.Text]);
end;

end.
```

此窗体中唯一有趣的代码是 `GetFilter` 函数，它只是将三个输入控件的值组合成一个筛选字符串，并将其返回给主应用程序。

### 列表 3.6 包含范围形式的源代码。范围形式会提示用户输入薪资下限和上限。

## 列表 3.6 RangeFilter—RangeForm.pas
