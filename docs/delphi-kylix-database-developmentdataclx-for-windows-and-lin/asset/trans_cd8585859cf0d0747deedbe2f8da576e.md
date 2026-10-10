

var
  listParams: TList;
  Params: TParams;
begin
  listParams := TList.Create;
  try
    SQLConnection1.GetProcoredProcedureParams('CONTACTS\BYSTATE', listParams);
    Params := TParams.Create;
    try
      LoadParamListItems(Params, listParams);

      // Do something with Params here...
    finally
      Params.Free;
    end;
  finally
    FreeProcParams(listParams);
  end;

注意此代码片段末尾对 `FreeProcParams` 的调用。`FreeProcParams` 会释放并置空 `listParams` 这个 TList，因此您无需显式释放该列表。

**列表 1.2** 展示了一个示例应用的完整源代码，该应用使用 TSQLConnection 从 InterBase 数据库中获取表、字段、索引、存储过程和参数名称。

## 列表 1.2 MetaData—MainForm.pas

```pascal
unit MainForm;

interface

uses
  SysUtils, Classes, QGraphics, QControls, QForms, QDialogs, QExtCtrls,
  DBXpress, QComCtrls, QStdCtrls, DB, SqlExpr;

type
  TfrmMain = class(TForm)
    conn: TSQLConnection;
    pnlBottom: TPanel;
    lblConnection: TLabel;
    pnlClient: TPanel;
    grpTableScope: TGroupBox;
    btnTable: TCheckBox;
    btnView: TCheckBox;
    btnSynonym: TCheckBox;
    btnSystemTable: TCheckBox;
    btnConnect: TButton;
    btnDisconnect: TButton;
    Label4: TLabel;
    Label5: TLabel;
    OpenDialog1: TOpenDialog;
    PageControl1: TPageControl;
    tabTables: TTabSheet;
    tabProcedures: TTabSheet;
    cbProcedure: TComboBox;
    Label2: TLabel;
    Label3: TLabel;
    cbTable: TComboBox;
    lbFields: TListBox;
    lbIndexes: TListBox;
    Label1: TLabel;
    Label6: TLabel;
    Label7: TLabel;
    lvParameters: TListView;
    procedure btnConnectClick(Sender: TObject);
    procedure cbTableClick(Sender: TObject);
    procedure btnDisconnectClick(Sender: TObject);
    procedure cbProcedureClick(Sender: TObject);
    procedure connAfterConnect(Sender: TObject);
    procedure connAfterDisconnect(Sender: TObject);
    procedure FormClose(Sender: TObject; var Action: TCloseAction);
  private
    { Private declarations }
  public
    { Public declarations }
  end;

var
  frmMain: TfrmMain;

implementation

{$R *.xfm}

procedure TfrmMain.btnConnectClick(Sender: TObject);

procedure CheckScope(Value: Boolean; TableScope: TTableScope);
begin
  if Value then
    conn.TableScope := conn.TableScope + [TableScope]
  else
    conn.TableScope := conn.TableScope * [TableScope];
end;

begin
  if OpenDialog1.Execute then begin
    conn.Params.Values['Database'] := OpenDialog1.FileName;
    CheckScope(btnTable.Checked, tsTable);
    CheckScope(btnView.Checked, tsView);
    CheckScope(btnSynonym.Checked, tsSynonym);
    CheckScope(btnSystemTable.Checked, tsSysTable);
    conn.Open;
  end;
end;

procedure TfrmMain.btnDisconnectClick(Sender: TObject);
begin
  conn.Close;
end;

procedure TfrmMain.cbTableClick(Sender: TObject);
begin
  conn.GetFieldNames(cbTable.Items[cbTable.ItemIndex], lbFields.Items);
  conn.GetIndexNames(cbTable.Items[cbTable.ItemIndex], lbIndexes.Items);
end;

procedure TfrmMain.cbProcedureClick(Sender: TObject);
var
  listParams: TList;
  Params: TParams;
  Index: Integer;
  Param: TParam;
  ListItem: TListItem;
begin
  listParams := TList.Create;
  try
    conn.GetProcedureParams(cbProcedure.Items[cbProcedure.ItemIndex], listParams);
    Params := TParams.Create;
    try
      LoadParamListItems(Params, listParams);

      lvParameters.Items.BeginUpdate;
      try
        lvParameters.Items.Clear;

        for Index := 0 to Params.Count - 1 do begin
          Param := Params[Index];
          ListItem := lvParameters.Items.Add;
          ListItem.Caption := Param.Name;
          case Param.DataType of
            ftUnknown: ListItem.SubItems.Add('Unknown');
            ftString: ListItem.SubItems.Add('String');
            ftSmallInt: ListItem.SubItems.Add('SmallInt');
            ftInteger: ListItem.SubItems.Add('Integer');
            ftWord: ListItem.SubItems.Add('Word');
            ftBoolean: ListItem.SubItems.Add('Boolean');
            ftFloat: ListItem.SubItems.Add('Float');
            ftCurrency: ListItem.SubItems.Add('Currency');
            ftBCD: ListItem.SubItems.Add('BCD');
            ftDate: ListItem.SubItems.Add('Date');
            ftTime: ListItem.SubItems.Add('Time');
            ftDateTime: ListItem.SubItems.Add('DateTime');
            ftBytes: ListItem.SubItems.Add('Bytes');
            ftVarBytes: ListItem.SubItems.Add('VarBytes');
            ftAutoInc: ListItem.SubItems.Add('AutoInc');
            ftBlob: ListItem.SubItems.Add('Blob');
            ftMemo: ListItem.SubItems.Add('Memo');
            ftGraphic: ListItem.SubItems.Add('Graphic');
            ftFmtMemo: ListItem.SubItems.Add('FmtMemo');
            ftParadoxOle: ListItem.SubItems.Add('ParadoxOle');
            ftDBaseOle: ListItem.SubItems.Add('DBaseOle');
            ftTypedBinary: ListItem.SubItems.Add('TypedBinary');
            ftCursor: ListItem.SubItems.Add('Cursor');
            ftFixedChar: ListItem.SubItems.Add('FixedChar');
            ftWideString: ListItem.SubItems.Add('WideString');
            ftLargeInt: ListItem.SubItems.Add('LargeInt');
            ftADT: ListItem.SubItems.Add('ADT');
            ftArray: ListItem.SubItems.Add('Array');
            ftReference: ListItem.SubItems.Add('Reference');
            ftDataSet: ListItem.SubItems.Add('DataSet');
            ftOraBlob: ListItem.SubItems.Add('OraBlob');
            ftOraClob: ListItem.SubItems.Add('OraClob');
            ftVariant: ListItem.SubItems.Add('Variant');
            ftInterface: ListItem.SubItems.Add('Interface');
            ftIDispatch: ListItem.SubItems.Add('IDispatch');
            ftGuid: ListItem.SubItems.Add('Guid');
            ftTimeStamp: ListItem.SubItems.Add('TimeStamp');
            ftFMTBcd: ListItem.SubItems.Add('FM TBcd');
          end;
        end;
      finally
        lvParameters.Items.EndUpdate;
      end;
    finally
      Params.Free;
    end;
  finally
    FreeProcParams(listParams);
  end;
end;

procedure TfrmMain.connAfterConnect(Sender: TObject);
begin
  btnTable.Enabled := False;
  btnView.Enabled := False;
  btnSynonym.Enabled := False;
  btnSystemTable.Enabled := False;

  lblConnection.Font.Color := clGreen;
  lblConnection.Caption := conn.Params.Values['Database'];

  conn.GetTableNames(cbTable.Items, btnSystemTable.Checked);
  conn.GetProcedureNames(cbProcedure.Items);

  cbTable.ItemIndex := 0;
  cbTableClick(cbTable);
  PageControl1.ActivePage := tabTables;
  ActiveControl := cbTable;

  cbProcedure.ItemIndex := 0;
  cbProcedureClick(cbProcedure);
end;

procedure TfrmMain.connAfterDisconnect(Sender: TObject);
begin
  btnTable.Enabled := True;
  btnView.Enabled := True;
  btnSynonym.Enabled := True;
  btnSystemTable.Enabled := True;

  lblConnection.Font.Color := clRed;
  lblConnection.Caption := 'Not connected';

  cbTable.Items.Clear;
  cbProcuder.Items.Clear;
  lbFields.Items.Clear;
  lbIndexes.Items.Clear;
end;

procedure TfrmMain.FormClose(Sender: TObject; var Action: TCloseAction);
begin
  conn.Close;
end;

end.
```

**图 1.4** 显示了从 CONMAN 数据库返回的表、字段和索引名称。

![图 1.4：CONTACTS 表的列和字段列表。](img/fe651f295b5f960d5463c4fb581d2281_37_0.png)

**图 1.5** 显示了 CONTACTSBSYSTATE 存储过程的参数列表。

![图 1.5：CONNECTBYSTATE 过程输出的长参数列表中的参数名称和类型。](img/fe651f295b5f960d5463c4fb581d2281_38_0.png)

**列表 1.2** 中的大部分代码相当简单直接。然而，有两点值得注意，我想特别指出。

首先，`cbProcedureClick` 方法展示了如何循环遍历存储过程的参数，以确定其名称、类型及其他属性。

其次，VCL/DataCLX 中存在一个 bug，实际上阻止了您同时获取表、视图和系统表的元数据。如果您同时勾选“表”、“视图”和“系统表”，`GetTableNames`（位于 `connAfterConnect` 方法中）将不会返回任何信息。请在您的应用中留意这一点。如果需要获取这三种类型的所有信息，您可以执行类似以下操作：

```pascal
var
  SL: TStringList;
begin
  SL := TStringList.Create;
  try
    SQLConnection1.TableScope := [tsTable, tsView];
    SQLConnection1.GetTableNames(ListBox1.Items, False);
    SQLConnection1.GetTableNames(SL, True);
    ListBox1.Items.AddStrings(SL);
  finally
    SL.Free;
  end;
end;
```

这段代码首先仅获取表和视图信息，并将结果放入列表框。接下来，它仅获取系统表，并将结果放入一个临时字符串列表。最后，它将临时字符串列表中的字符串添加到列表框中。因此，列表框中包含表、视图和系统表。

从上述讨论中可以看出，TSQLConnection 返回的模式信息极其基础。除了存储过程参数外，唯一的数据是

