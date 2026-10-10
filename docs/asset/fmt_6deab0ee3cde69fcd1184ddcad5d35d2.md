
![](img/fe651f295b5f960d5463c4fb581d2281_241_0.png)

## 示例应用程序

代码清单 5.4 是一个示例应用程序，它使用了本章中讨论的许多（但并非全部）数据感知组件。从代码清单 5.4 中可以看出，该应用程序的代码量非常少。得益于 `VCL/CLX`，数据感知组件几乎封装了在应用程序中显示和更新数据集所需的所有内容。

## 代码清单 5.4

`DataAware—MainForm.pas`

```pascal
unit MainForm;

interface

uses
  SysUtils, Classes, QGraphics, QControls, QForms, QDialogs, DB, DBClient,
  QStdCtrls, QExtCtrls, QButtons, Mask, QComCtrls, QDBCtrls, QMask;

type
TfrmMain = class(TForm)
ClientDataSet1: TClientDataSet;
DataSource1: TDataSource;
cdsLookup: TClientDataSet;
dsLookup: TDataSource;
cdsLookupID: IntegerField;
cdsLookupDescription: TStringField;
DBNavigator1: TDBNavigator;
pnlBottom: TPanel;
ClientDataSet1Weekday: TStringField;
ClientDataSet1WeekdayValue: TIntegerField;
ClientDataSet1Image: TBlobField;
ClientDataSet1Active: TStringField;
ClientDataSet1Age: TIntegerField;
ClientDataSet1ItemID: TIntegerField;
ClientDataSet1Salary: TFloatField;
ClientDataSet1Enabled: TBooleanField;
LblCurrent: TLabel;
Lb1State: TLabel;
OpenDialog1: TOpenDialog;
Panel1: TPanel;
lbDSEvents: TListBox;
Label3: TLabel;
pnlClient: TPanel;
PageControl1: TPageControl;
tabSimple: TTabSheet;
txtAge: TDBText;
Label1: TLabel;
txtWeekday: TDBText;
txtSalary: TDBText;
Label6: TLabel;
Label7: TLabel;
ecAge: TDBEdit;
DBRadioGroup1: TDBRadioGroup;
cbActive: TDBCheckBox;
cbEnabled: TDBCheckBox;
ecSalary: TDBEdit;
tabComboList: TTabSheet;
Label12: TLabel;
cbWeekday: TDBComboBox;
lb1Weekday: TDBListBox;
raLookup: TTabSheet;
Label4: TLabel;
lblLookup: TDBLookupListBox;
cblLookup: TDBLookupComboBox;
tabImage: TTabSheet;
Label5: TLabel;
img: TDBImage;
btnLoad: TButton;
btnClear: TButton;
procedure FormCreate(Sender: TObject);
procedure DataSource1DataChange(Sender: TObject; Field: TField);
procedure ClientDataSet1NewRecord(DataSet: TDataSet);
procedure DataSource1StateChange(Sender: TObject);
procedure btnLoadClick(Sender: TObject);
procedure btnClearClick(Sender: TObject);
procedure DataSource1UpdateData(Sender: TObject);
  private
    { Private declarations }
  public
    { Public declarations }
  end;

var
  frmMain: TfrmMain;

implementation

{$R *.xfm}

procedure TfrmMain.FormCreate(Sender: TObject);

  procedure AddLookupItem(ID: Integer; const Description: string);
  begin
    cdsLookup.Append;
    cdsLookupID.AsInteger := ID;
    cdsLookupDescription.AsString := Description;
    cdsLookup.Post;
  end;

begin
  // Create the lookup dataset and populate with some data
  cdsLookup.CreateDataSet;
  AddLookupItem(1, 'Widgit');
  AddLookupItem(2, 'Gadget');
  AddLookupItem(3, 'Thingamabob');

  ClientDataSet1.CreateDataSet;
end;

procedure TfrmMain.ClientDataSet1NewRecord(DataSet: TDataSet);
begin
  DataSet.FieldName('Enabled').AsString := 'T';
  DataSet.FieldName('Active').AsString := 'T';
end;

procedure TfrmMain.DataSource1DataChange(Sender: TObject; Field: TField);
begin
  if Field = nil then
    lbDSEvents.Items.Add('Data Change: Field = nil')
  else
    lbDSEvents.Items.Add('Data Change: Field = ' + Field.FieldName);

  lblCurrent.Caption := Format('('Record %d of %d)',
    [ClientDataSet1.RecNo, ClientDataSet1.RecordCount]);
end;

procedure TfrmMain.DataSource1StateChange(Sender: TObject);
begin
  lbDSEvents.Items.Add('State Change');

  case DataSource1.State of
    dsInactive: lblState.Caption := 'Inactive';
    dsBrowse: lblState.Caption := 'Browse';
    dsEdit: lblState.Caption := 'Edit';
    dsInsert: lblState.Caption := 'Insert';
  end;
end;

procedure TfrmMain.DataSource1UpdateData(Sender: TObject);
begin
  lbDSEvents.Items.Add('Update Data')
end;

procedure TfrmMain.btnLoadClick(Sender: TObject);
begin
  if OpenDialog1.Execute then begin
    ClientDataSet1.Edit;
    ClientDataSet1Image.LoadFromFile(OpenDialog1.FileName);
  end;
end;

procedure TfrmMain.btnClearClick(Sender: TObject);
```

# 列表 5.4（续）

```pascal
begin
if not ClientDataSet1Image.IsNull then begin
ClientDataSet1Edit;
ClientDataSet1Image.Clear;
end;
end.
```

图 5.3 展示了该数据感知应用程序在运行时的情景。
