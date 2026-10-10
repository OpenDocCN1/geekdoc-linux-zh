

![](img/fe651f295b5f960d5463c4fb581d2281_53_0.png)

## 图 1.7
*事务可以嵌套或重叠。*

并非所有数据库都支持多事务。不幸的是，要确定数据库是否支持多事务，无法通过检查某个简单的属性来实现。`TSQLConnection` 包含一个名为 `FSupportsMultiTrans` 的私有字段，但没有公共访问接口。不过，情况并非毫无希望，你可以使用以下函数来获取该属性的值：

```pascal
function SupportsMultiTrans(conn: TSQLConnection): Boolean;
var
  Supported: LongBool;
  PropSize: SmallInt;
begin
  conn.MetaData.GetOption(eMetaSupportsTransactions, @Supported,
    SizeOf(Integer), PropSize);
  Result := Supported;
end;
```

如果数据库不支持多事务，你应当避免在事务处于活动状态时调用 `StartTransaction`。你可以通过检查 `InTransaction` 属性来测试当前是否有活动的事务，如下所示：

```pascal
if not SQLConnection1.InTransaction then
  // 此时开始事务是安全的
```

如果数据库支持多事务，你可以嵌套它们，如下面的代码片段所示：

```pascal
var
  TransOuter: TTransactionDesc;
  TransInner: TTransactionDesc;
begin
  TransOuter.TransactionID := 1;
  TransOuter.IsolationLevel := xlREADCOMMITTED;
  SQLConnection1.StartTransaction(TransOuter);
  try
    // 在此处执行一些 SQL 语句
    TransInner.TransactionID := 2;
    TransInner.IsolationLevel := xiREADCOMMITTED;
    SQLConnection1.StartTransaction(TransInner);
    try
      // 在此处执行更多的 SQL 语句
      SQLConnection1.Commit(TransInner);
    except
      SQLConnection1.Rollback(TransInner);
      raise;
    end;
    // 在此处再执行一些 SQL 语句
    SQLConnection1.Commit(TransOuter);
  except
    SQLConnection1.Rollback(TransOuter);
    raise;
  end;
end;
```

请注意，在上述代码中，事务被包裹在 `try/except` 块中。如果在执行代码过程中发生异常，事务将被回滚。

## 代码清单 1.5
Trans—MainForm.pas

```pascal
unit MainForm;

interface

uses
  SysUtils, Classes, QGraphics, QControls, QForms, QDialogs, QExtCtrls,
  DBXpress, QStdCtrls, DB, SqlExpr;

type
  TfrmMain = class(TForm)
  pnlClient: TPanel;
  conn: TSQLConnection;
  btnConnect: TButton;
  btnDisconnect: TButton;
  1bOutput: TListBox; // OCR error: '1' likely 'l', but preserving variable name style or correcting to lbOutput
  btnCommit: TButton;
  btnRollback: TButton;
  btnMultiLevel1: TButton;
  btnOverlapping: TButton;

  procedure btnConnectClick(Sender: TObject);
  procedure btnDisconnectClick(Sender: TObject);
  procedure btnCommitClick(Sender: TObject);
  procedure btnRollbackClick(Sender: TObject);
  procedure btnMultiLevellClick(Sender: TObject);
  procedure btnOverlappingClick(Sender: TObject);
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

function SupportsMultiTrans(conn: TSQLConnection): Boolean;
var
  Supported: LongBool;
  PropSize: SmallInt;
begin
  conn.MetaData.GetOption(eMetaSupportsTransactions, @Supported,
    SizeOf(Integer), PropSize);
  Result := Supported;
end;

procedure TfrmMain.btnConnectClick(Sender: TObject);
begin
  conn.Open;
  if conn.TransactionsSupported then
    lbOutput.Items.Add('Connection supports transactions')
  else
    lbOutput.Items.Add('Connection does not support transactions');

  if SupportsMultiTrans(conn) then
    lbOutput.Items.Add('Connection supports multiple transactions')
  else
    lbOutput.Items.Add('Connection does not support multiple transactions');
end;

procedure TfrmMain.btnDisconnectClick(Sender: TObject);
begin
  conn.Close;
end;

procedure TfrmMain.btnCommitClick(Sender: TObject);
var
  TransDesc: TTransactionDesc;
begin
  TransDesc.TransactionID := 1;
  TransDesc.IsolationLevel := xlREADCOMMITTED;
  conn.StartTransaction(TransDesc);
  conn.ExecuteDirect('DELETE FROM TODOS');
  conn.Commit(TransDesc);
  lbOutput.Items.Add('Transaction committed');
end;

procedure TfrmMain.btnRollbackClick(Sender: TObject);
var
  TransDesc: TTransactionDesc;
begin
  TransDesc.TransactionID := 1;
  TransDesc.IsolationLevel := xlREADCOMMITTED;
  conn.StartTransaction(TransDesc);
  conn.ExecuteDirect('DELETE FROM CONTACTS');
  conn.Rollback(TransDesc);
  lbOutput.Items.Add('Transaction rolled back');
end;

procedure TfrmMain.btnMultiLevelClick(Sender: TObject);
var
  TransDesc1: TTransactionDesc;
  TransDesc2: TTransactionDesc;
begin
  TransDesc1.TransactionID := 1;
  TransDesc1.IsolationLevel := xlREADCOMMITTED;
  conn.StartTransaction(TransDesc1);
  conn.ExecuteDirect('UPDATE CONTACTS SET PHONE = ''Trans 1'' WHERE ID = 3');

  TransDesc2.TransactionID := 2;
  TransDesc2.IsolationLevel := xlREADCOMMITTED;
  conn.StartTransaction(TransDesc2);
  conn.ExecuteDirect('UPDATE CONTACTS SET PHONE = ''Trans 2'' WHERE ID = 2');
  conn.Rollback(TransDesc2);
  lbOutput.Items.Add('Second transaction rolled back');

  conn.Commit(TransDesc1);
  lbOutput.Items.Add('First transaction committed');
end;

procedure TfrmMain.btnOverlappingClick(Sender: TObject);
var
  TransDesc3: TTransactionDesc;
  TransDesc4: TTransactionDesc;
begin
  TransDesc3.TransactionID := 3;
  TransDesc3.IsolationLevel := xlREADCOMMITTED;
  conn.StartTransaction(TransDesc3);
  conn.ExecuteDirect('UPDATE CONTACTS SET PHONE = ''Trans 3'' WHERE ID = 3');

  TransDesc4.TransactionID := 4;
  TransDesc4.IsolationLevel := xlREADCOMMITTED;
  conn.StartTransaction(TransDesc4);
  conn.ExecuteDirect('UPDATE CONTACTS SET PHONE = ''Trans 4'' WHERE ID = 2');

  conn.Rollback(TransDesc3);
  lbOutput.Items.Add('Transaction 3 rolled back');

  conn.Commit(TransDesc4);
  lbOutput.Items.Add('Transaction 4 committed');
end;

procedure TfrmMain.connAfterConnect(Sender: TObject);
begin
  btnConnect.Enabled := False;
  btnDisconnect.Enabled := True;
  btnCommit.Enabled := True;
  btnRollback.Enabled := True;
  btnMultiLevel.Enabled := True;
  btnOverlapping.Enabled := True;
end;

procedure TfrmMain.connAfterDisconnect(Sender: TObject);
begin
  btnConnect.Enabled := True;
  btnDisconnect.Enabled := False;
  btnCommit.Enabled := False;
  btnRollback.Enabled := False;
  btnMultiLevel1.Enabled := False;
  btnOverlapping.Enabled := False;
end;

procedure TfrmMain.FormClose(Sender: TObject; var Action: TCloseAction);
begin
  conn.Close;
end;

end.
```

图 1.8 显示了 Trans 应用运行时的情形。

![](img/fe651f295b5f960d5463c4fb581d2281_58_0.png)

## 图 1.8
*Trans 演示了如何执行嵌套事务。*

## 在 SQL 操作期间提供反馈

在 SQL 操作执行期间提供反馈有几个很好的理由。考虑以下两点：

- 某些 SQL 操作速度很快，但某些操作则极慢。在大型数据库上执行的非常复杂的 `SELECT` 语句可能需要几分钟（甚至几小时）才能执行完毕。
- 特别是在将 `TSqlConnection` 与数据集配合使用（在第 3 章中讨论）时，连接可能会代表你执行一些 SQL 命令。为了学习和调试的目的，拦截发送到数据库的所有 SQL 命令是非常有用的。

在这两种情况下，能够以日志文件、数据库、CodeSite（来自 Raize Software，位于 www.raize.com）或其他调试工具的形式，向应用的最终用户（或向你自身）提供反馈或日志记录功能，都是很有帮助的。

### 在执行 SQL 语句时更改光标

你可以提供的最简单的反馈形式是在执行 SQL 语句时将光标更改为沙漏。要在应用中提供此功能，你只需将连接的 `SQLHourGlass` 属性设置为 `True`。由于 `SQLHourGlass` 不是发布的属性，因此你无法在设计时设置它。

```pascal
SQLConnection1.SQLHourGlass := True;
```

### 创建回调事件以监控 SQL 命令

如果你想拦截从 `TSqlConnection` 传送到数据库的每一个 SQL 命令，你可以设置所谓的跟踪回调事件。

通过调用 `TSqlConnection.SetTraceCallbackEvent` 来设置跟踪回调事件。`SetTraceCallbackEvent` 接受两个参数：用于 SQL 活动的回调事件，以及传递给回调事件的用户定义整数值。

回调事件的格式定义如下：

```pascal
TSQLCallbackEvent = function(CallType: TRACECat; CBIInfo: Pointer): CBRTType; stdcall;
```

在进入回调函数时，`CallType` 总是被设置为 `cbTRACE`。`CBInfo` 是指向 `SQLTRACEDesc` 记录的指针，其定义如下：

```pascal
SQLTRACEDesc = packed record           { trace callback info }
  pszTrace   : array [0..1023] of Char;
  eTraceCat  : TRACECat;
  ClientData : Integer;
  uTotalMsgLen : Word;
end;
```

