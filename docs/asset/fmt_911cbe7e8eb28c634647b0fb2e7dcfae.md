
```pascal
unit MainForm;

interface

uses
SysUtils, Types, Classes, QGraphics, QControls, QForms, QDialogs, QStdCtrls, QExtCtrls, DBXpress, DB, SqlExpr;

type
TfrmMain = class(TForm)
pnClient: TPanel;
conn: TSQLConnection;
btnCreate: TButton;
btnPopulate: TButton;
btnConnect: TButton;
btnDelete: TButton;
btnDisconnect: TButton;
btnParameters: TButton;
btnDrop: TButton;
lbOutput: TListBox;
procedure btnCreateClick(Sender: TObject);
procedure btnConnectClick(Sender: TObject);
procedure btnPopulateClick(Sender: TObject);
procedure btnDisconnectClick(Sender: TObject);
procedure btnDeleteClick(Sender: TObject);
procedure btnParametersClick(Sender: TObject);
procedure btnDropClick(Sender: TObject);
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
begin
  conn.Open;
end;

procedure TfrmMain.btnDisconnectClick(Sender: TObject);
begin
  conn.Close;
end;

procedure TfrmMain.btnCreateClick(Sender: TObject);
begin
  conn.ExecuteDirect('CREATE TABLE TESTING (NAME VARCHAR(20) NOT NULL, '
    + 'AGE INTEGER, PRIMARY KEY (NAME))');
  lbOutput.Items.Add('Created TESTING table');
end;

procedure TfrmMain.btnPopulateClick(Sender: TObject);
begin
  conn.ExecuteDirect('INSERT INTO TESTING VALUES ('Eric', 34)');
  conn.ExecuteDirect('INSERT INTO TESTING VALUES ('Tina', 33)');
  lbOutput.Items.Add('Added Eric and Tina to TESTING table');
end;

procedure TfrmMain.btnDeleteClick(Sender: TObject);
begin
  conn.ExecuteDirect('DELETE FROM TESTING WHERE NAME = 'Tina'');

  lbOutput.Items.Add('Deleted Tina from TESTING table');
end;

procedure TfrmMain.btnParametersClick(Sender: TObject);
const
  SQL = 'INSERT INTO TESTING VALUES (:Name, :Age)';
var
  Params: TParams;
begin
  Params := TParams.Create(nil);
  try
    Params.CreateParam(ftString, 'PName', ptInput);
    Params.CreateParam(ftInteger, 'Page', ptInput);

    // Add first name
    Params.ParamByName('PName').AsString := 'Mike';
    Params.ParamByName('Page').AsInteger := 34;
    conn.Execute(SQL, Params);

    lbOutput.Items.Add('Added Mike to TESTING table');
  finally
    Params.Free;
  end;
end;

procedure TfrmMain.btnDropClick(Sender: TObject);
begin
  conn.ExecuteDirect('DROP TABLE TESTING');

  lbOutput.Items.Add('Removed TESTING table');
end;

procedure TfrmMain.connAfterConnect(Sender: TObject);
begin
  btnConnect.Enabled := False;
  btnCreate.Enabled := True;
  btnPopulate.Enabled := True;
  btnDelete.Enabled := True;
  btnParameters.Enabled := True;
  btnDrop.Enabled := True;
  btnDisconnect.Enabled := True;

  lbOutput.Items.Add('Connected');
end;

procedure TfrmMain.connAfterDisconnect(Sender: TObject);
begin
    btnConnect.Enabled := True;
    btnCreate.Enabled := False;
    btnPopulate.Enabled := False;
    btnDelete.Enabled := False;
    btnParameters.Enabled := False;
    btnDrop.Enabled := False;
    btnDisconnect.Enabled := False;

    lbOutput.Items.Add('Disconnected');
end;

procedure TfrmMain.FormClose(Sender: TObject; var Action: TCloseAction);
begin
    conn.Close;
end;

end.
```

图 1.6 显示了运行时的 `DDLSQL` 程序。

![](img/fe651f295b5f960d5463c4fb581d2281_48_0.png)

## 图 1.6

*`DDLSQL` 在运行完所有按钮后的状态。*

## 事务支持

大多数 SQL 数据库（在 3.23 版本之前的 `MySQL` 版本是个显著的例外）都支持事务。一个事务必须满足四项准则，即所谓的**事务的 `ACID` 特性**。具体而言，事务具有

- * **原子性。** 事务必须作为一个整体要么成功，要么失败。部分成功、部分失败是不可接受的。
- * **一致性。** 事务结束后，数据必须处于一致状态。所有数据都必须符合当前的引用完整性约束。
- * **隔离性。** 在一个事务中进行的更改在对事务提交之前，必须对其他事务不可见。
- * **持久性。** 一旦事务提交，其更改必须是永久性的。没有任何因素（包括系统崩溃）可以改变已提交事务的效果。

用例子来描述事务是最直观的，因此我将介绍事务支持中最常被引用的一个示例。

想象一个银行，其数据库中包含客户和账户信息。用户 John Q. Customer 在该银行既有储蓄账户又有支票账户。他前往附近的 ATM 机，并决定从他的储蓄账户向支票账户转账 $100。

用 SQL 术语来说，这构成两个操作：一条记录储蓄账户提款的 `INSERT` 语句，以及一条记录存入支票账户的 `INSERT` 语句。假设 ATM 软件是使用 `Delphi` 和 `dbExpress` 编写的，它可能包含类似下面的代码：
