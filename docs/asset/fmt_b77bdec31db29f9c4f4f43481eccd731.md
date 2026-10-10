
```pascal
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
    if frmFilter.ShowModal = mrOk then begin
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
        if frmRange.ShowModal = mrOk then
            ClientDataSet1.SetRange([frmRange.LowValue], [frmRange.HighValue]);
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

可以看到，主窗体从磁盘加载员工数据集，在 `Salary` 字段上创建索引，并激活该索引。然后，它允许用户对数据集应用范围、筛选或两者同时应用。

### 列表 3.5 RangeFilter—FilterForm.pas

```pascal
unit FilterForm;

interface

uses
  SysUtils, Classes, QGraphics, QControls, QForms,
  QDialogs, QStdCtrls, QExtCtrls;

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
    btnOK: TButton;
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
  Result := Format('%s %s '%s'',
    [cbField.Text, cbRelationship.Text, ecValue.Text]);
end;

end.
```

此窗体中唯一有趣的代码是 `GetFilter` 函数，它只是将三个输入控件的值组合成一个筛选字符串，并将其返回给主应用程序。

### 列表 3.6 RangeFilter—RangeForm.pas

```pascal
unit RangeForm;

interface

uses
  SysUtils, Classes, QGraphics, QControls, QForms, QDialogs, QExtCtrls,
  QStdCtrls;

type
  TfrmRange = class(TForm)
    pnlClient: TPanel;
    pnlBottom: TPanel;
    Label1: TLabel;
    Label2: TLabel;
    ecLower: TEdit;
    ecUpper: TEdit;
    btnOk: TButton;
    btnCancel: TButton;
    procedure btnOkClick(Sender: TObject);
  private
    function GetHighValue: Double;
    function GetLowValue: Double;
    { Private declarations }
  public
    { Public declarations }
    property LowValue: Double read GetLowValue;
    property HighValue: Double read GetHighValue;
  end;

implementation

{$R *.xfm}

{ TfrmRange }

function TfrmRange.GetHighValue: Double;

begin
  Result := StrToFloat(ecUpper.Text);
end;

function TfrmRange.GetLowValue: Double;

begin
  Result := StrToFloat(ecLower.Text);
end;

procedure TfrmRange.btnOkClick(Sender: TObject);

var
  LowValue: Double;
  HighValue: Double;

begin
  try
    LowValue := StrToFloat(ecLower.Text);
    HighValue := StrToFloat(ecUpper.Text);
    if LowValue > HighValue then begin
      ModalResult := mrNone;
      ShowMessage('The upper salary must be >= the lower salary');
    end;
  except
    ModalResult := mrNone;
    ShowMessage('Both values must be a valid number');
  end;
end;
```

此范围形式会提示用户输入薪资的下限和上限。
