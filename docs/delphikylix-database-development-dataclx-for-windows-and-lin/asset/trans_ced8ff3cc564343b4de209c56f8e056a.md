

以下代码片段展示了执行返回结果集的 SQL 语句的一种方式。在下一章中，你将看到更简单的方法来实现这一点。

```delphi
SQLDataSet1 := TSQLDataSet.Create(nil);
try
  SQLConnection1.Execute('SELECT * FROM EMPLOYEE', nil, SQLDataSet1);
  // 在这里对 SQLDataSet1 执行一些操作...
finally
  SQLDataSet1.Free;
end;
```

上述代码还展示了执行非参数化 SELECT 语句的正确方式：只需将 `Params` 设置为 `nil` 即可。

以下示例程序 DDLSQL 演示了如何在程序化地创建测试表、填充数据以及销毁该表。它还展示了如何使用 Execute 方法从表中检索数据。列表 1.4 显示了 DDLSQL 的完整代码。

### 列表 1.4 DDLSQL—MainForm.pas

```delphi
unit MainForm;

interface

uses
  SysUtils, Types, Classes, QGraphics, QControls, QForms, QDialogs,
  QStdCtrls, QExtCtrls, DBExpress, DB, SQLExpr;

type
  TfrmMain = class(TForm)
    pnlClient: TPanel;
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
  conn.ExecuteDirect('CREATE TABLE TESTING (NAME VARCHAR(20) NOT NULL, ' +
    'AGE INTEGER, PRIMARY KEY (NAME)');
  lbOutput.Items.Add('Created TESTING table');
end;

procedure TfrmMain.btnPopulateClick(Sender: TObject);
begin
  conn.ExecuteDirect('INSERT INTO TESTING VALUES (''Eric'', 34)');
  conn.ExecuteDirect('INSERT INTO TESTING VALUES (''Tina'', 33)');
  lbOutput.Items.Add('Added Eric and Tina to TESTING table');
end;

procedure TfrmMain.btnDeleteClick(Sender: TObject);
begin
  conn.ExecuteDirect('DELETE FROM TESTING WHERE NAME = ''Tina''');
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
    Params.CreateParam(ftInteger, 'Age', ptInput);
    // Add first name
    Params.ParamByName('PName').AsString := 'Mike';
    Params.ParamByName('Age').AsInteger := 34;
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

![](img/52a35759a0f10dade27a840504be5d82_46_0.png)

![](img/52a35759a0f10dade27a840504be5d82_48_0.png)

![](img/52a35759a0f10dade27a840504be5d82_49_0.png)

### 图 1.6

*点击所有按钮运行后的 DDLSQL 程序。*

## 事务支持

大多数 SQL 数据库都提供事务支持，但 MySQL 3.23 之前的版本是一个显著的例外。事务必须满足四个标准，这些标准被称为事务的 ACID 属性。具体来说，事务具备以下特性：

-   **原子性（Atomic）**。事务必须要么全部成功，要么全部失败。事务的一部分成功而另一部分失败是不允许的。
-   **一致性（Consistent）**。在事务完成后，数据必须处于一致状态。所有数据都必须遵循当前的引用完整性约束。
-   **隔离性（Isolated）**。在一个事务中进行的更改，在该事务提交之前，对另一个事务是不可见的。
-   **持久性（Durable）**。一旦事务提交，其更改必须是永久的。任何因素（包括系统崩溃）都不能改变已提交事务的影响。

通过示例最容易理解事务，因此我将介绍关于事务支持最常被引用的示例。

想象一家银行，其数据库包含客户和账户信息。约翰·Q·客户（John Q. Customer）在该银行拥有一个储蓄账户和一个活期账户。他去附近的 ATM 机，决定从他的储蓄账户向活期账户转账 100 美元。

用 SQL 术语来说，这构成了两个操作：一条用于记录储蓄账户扣款的 INSERT 语句，以及另一条用于记录活期账户存款的 INSERT 语句。假设 ATM 软件是使用 Delphi 和 dbExpress 编写的，它可能包含类似于以下代码的内容：

```delphi
procedure TransferFunds(FromAccountID: Integer; ToAccountID: Integer; Amount: Double);
var
  SQL: string;
  Params: TParams;
begin
  Params := TParams.Create;
  try
    SQL := 'INSERT INTO ACCOUNTDETAIL (ACCOUNTID, TRANSDATE, AMOUNT) ' +
      'VALUES (:AccountID, :TransDate, :TransAmount)';
    Params.ParamByName('AccountID').Value := FromAccountID;
    Params.ParamByName('TransDate').Value := Date;
    Params.ParamByName('TransAmount').Value := -Amount;
    SQLConnection1.Execute(SQL, Params);

    Params.ParamByName('AccountID').Value := ToAccountID;
    Params.ParamByName('TransAmount').Value := Amount;
    SQLConnection1.Execute(SQL, Params);
  finally
    Params.Free;
  end;
end;
```

![](img/52a35759a0f10dade27a840504be5d82_50_0.png)

从概念上讲，这段代码片段为源账户创建了一笔扣款，并为目标账户创建了一笔存款。起初，你可能认为这段代码没有任何问题，但让我们看看可能发生的各种情况。

如果在记录扣款和记录存款之间发生了停电、连接故障或其他灾难性故障，会发生什么？钱会从储蓄账户中扣除，但永远不会被存入活期账户（这使得客户先生变得非常不满，甚至可能不再是该银行的客户）。

如果代码顺序颠倒，先创建存款再创建扣款，则可能发生相反的情况：存款被记录，但扣款从未发生（这使得客户先生非常高兴，并富有了 100 美元，但银行则亏损了）。

显然，ATM 软件需要有一种保证，要么扣款和存款都发生，要么都不发生。这就是事务设计所要处理的问题。

下面几节将描述如何检测特定数据库是否支持事务，如何开始（以及随后结束）一个事务，以及如何处理多个（和嵌套的）事务。

### 检查事务支持

如果你正在编写一个仅与单一数据库后端（如 Oracle 或 InterBase）一起工作的应用程序，你在开始编码之前就知道该数据库支持事务。如果你正在编写一个通用的应用程序，可以访问许多不同的数据库后端，那么你事先并不知道所选的数据库后端是否支持事务。

TSQLConnection 提供了一种方法来检测底层数据库引擎是否支持事务：`TransactionsSupported` 属性。在检查 `TransactionsSupported` 之前，你需要建立与数据库的连接，如下所示：

```delphi
SQLConnection1.Open;
// ...
if SQLConnection1.TransactionsSupported then
begin
  // 继续执行事务代码
end
else
begin
  // 不支持事务 - 执行替代代码或退出
end;
```

