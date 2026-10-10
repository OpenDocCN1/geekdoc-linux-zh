

这些字段及其含义如表 1.8 所示。

## 表 1.8
SQLTraceDesc 字段说明

| 字段 | 定义 |
| :--- | :--- |
| pszTrace | 刚刚从或发送到数据库的以 NULL 结尾的命令。 |
| eTraceCat | 刚刚发送或接收的命令类别。表 1.9 列出了该字段的可能值。 |
| ClientData | 作为 SetTraceCallbackEvent 的第二个参数传递的用户自定义值。 |
| uTotalMsgLen | pszTrace 中包含的字符串的长度（以字符计）。 |

表 1.9 描述了 eTraceCat 字段的可能值。

## 表 1.9
eTraceCat 值

| 值 | 定义 |
| :--- | :--- |
| tracePREPARE | 一条查询语句已发送到服务器进行准备。 |
| traceEXECUTE | 一条查询语句已发送到服务器进行执行。 |
| traceERROR | 服务器返回了一条错误消息。 |
| traceSTMT | 一个供数据库执行的操作已发送到服务器。 |
| traceCONNECT | 一个与连接或断开连接相关的操作已发送到服务器。 |
| traceTRANSACT | 一个与事务相关的操作已发送到服务器。 |
| traceBLOB | 一个与 BLOB 相关的操作已发送到服务器。 |
| traceVENDOR | 一个供应商特定的 API 调用已发送到服务器。 |
| traceDATAIN | 在 INSERT 或 UPDATE 命令期间，参数数据已发送到服务器。 |
| traceDATAOUT | 数据已从服务器获取。 |
| traceMISC | 不属于上述任何类别的其他任何命令。 |

> **注意**
> 并非所有这些选项目前都得到支持。其中许多是为未来扩展而设置的。目前，所有供应商调用和执行的 SQL 命令都会被跟踪。

以下代码片段设置了一个回调事件：

```
function SQLCallback(CallType: TRACECat; CBInfo: Pointer): CBTRType; stdcall; 
var 
CBI: pSQLTRACEDesc; 
begin 
CBI := pSQLTRACEDesc(CBInfo); 
ShowMessage(CBI.pszTrace); 
end;

begin 
SQLConnection1.SetTraceCallbackEvent(SQLCallback, 1); 
end;
```

![](img/fe651f295b5f960d5463c4fb581d2281_61_0.png)

不要将 0 作为 SetTraceCallbackEvent 的第二个参数传入，否则你的回调事件永远不会被调用，你将不得不绞尽脑汁去弄清楚为什么回调事件不起作用。

要移除回调处理器，请执行以下代码行：

```
SQLConnection1.SetTraceCallbackEvent(nil, 0);
```

# TSQLMonitor

TSQLMonitor 提供了一种现成的、易于使用的机制来捕获数据库事件。你可以将数据库消息记录到列表框、日志文件或其他目标中，当它们发生时即可。你也可以允许消息在监控器的内部缓冲区中累积，并一次性将它们转储到文件（或其他目标）中。

要使用 TSQLMonitor，请将其与你的 TSQLConnection 组件一起放置在一个窗体或数据模块中。要开始记录事件，请将监控器的 SQLConnection 属性设置为 TSQLConnection 组件，并将 Active 属性设置为 True。

监控数据库消息有两种方式：你可以选择在 TSQLMonitor 获知每个消息时立即记录每个消息，或者你可以允许组件缓冲这些消息，并在稍后将其保存到日志文件或字符串列表中。以下各部分解释了这些选项。

## 在消息发生时记录

实际上，有两种不同的方法可以在消息发生时记录数据库消息。第一种是通过使用 TSQLMonitor 的 AutoSave 和 FileName 属性。将 FileName 设置为你想要创建的日志文件的名称，例如 C:\TRACE.LOG。将 AutoSave 设置为 True，组件会自动将所有数据库消息记录到指定的文件名中。如果文件不存在，它将被自动创建。如果文件已存在，消息将被追加到其中。

第二种即时记录消息的方法是为 OnTrace 或 OnLogTrace 事件编写事件处理程序。OnTrace 在组件收到指示消息已在应用程序和数据库服务器之间传递时触发。事件处理程序如下所示：

```
procedure TForm1.SQLMonitor1Trace(Sender: TObject; CBInfo: pSQLTRACEDesc;
var LogTrace: Boolean);
begin

end;
```

在事件处理程序中，如果你因某种原因不想将消息保存到内部列表，可以将 LogTrace 设置为 False。默认情况下，消息会被记录。

OnLogTrace 在消息被添加到内部跟踪列表后触发。其事件处理程序如下所示：

```
procedure TForm1.SQLMonitor1LogTrace(Sender: TObject; CBInfo: pSQLTRACEDesc);
begin

end;
```

参数与传递给 OnTrace 事件处理程序的前两个参数相同。

## 缓冲消息

你可以允许 TSQLMonitor 组件在内部列表中缓冲这些消息，而不是在每条消息到达时逐一处理。然后，你可以稍后将它们保存到文件或字符串列表中。

要将列表保存到文件，请像下面这样调用组件的 SaveToFile 方法：

```
SQLMonitor1.SaveToFile('C:\EventList.LOG');
```

或者，你可以通过访问 TraceList 属性将消息保存到字符串列表中，该属性是一个包含消息列表的 TStringList 对象。通过调用 TraceList 上的方法和/或属性，你可以访问列表中的单个行。

### 使用多种反馈机制

TSQLConnection 并没有设计成轻松支持同时向多个目标发送数据库跟踪事件。换句话说，你不能同时使用 TSQLMonitor 和用户定义的反馈事件。因此，如果你想要分配一个回调事件，你应该将 TSQLMonitor 的 Active 属性设置为 False（假设你的应用程序中也有一个 TSQLMonitor 组件）。

另一件你应该避免的事情是在分配新回调时意外覆盖现有的回调处理器。要检查是否存在现有的回调事件（包括 TSQLMonitor 组件的存在），你应该检查只读 TSQLConnection.TraceCallbackEvent 属性的值，以确保它是 nil。

如果 TSQLConnection.TraceCallbackEvent 不是 nil，则已经安装了回调处理器。此时，你有三个选择：

- 选择不安装你的反馈事件。
- 保存指向现有反馈事件的指针，调用 SetTraceCallbackEvent 安装你自己的事件处理程序，并在完成后恢复现有的回调事件。
- 保存指向现有反馈事件的指针，调用 SetTraceCallbackEvent 安装你自己的事件处理程序，并在你的新事件处理程序内部调用现有的事件处理程序。

列表 1.6 显示了一个示例应用程序的源代码，该应用程序通过 TSQLMonitor 组件或程序员定义的回调事件来跟踪数据库操作。

## 列表 1.6
反馈—MainForm.pas

```
unit MainForm;

interface

uses
  SysUtils, Classes, QGraphics, QControls, QForms, QDialogs, DBXpress,
  QExtCtrls, SqlExpr, DB, QStdCtrls;

type
  TfrmMain = class(TForm)
    conn: TSQLConnection;
    pnClient: TPanel;
    lbTrace: TListBox;
    Label1: TLabel;
    btnDump: TButton;
    btnConnect: TButton;
    btnDisconnect: TButton;
    btnExecSQL: TButton;
    btnLogTrace: TCheckBox;
    monitor: TSQLMonitor;
    cbUseCallback: TCheckBox;
    procedure btnDumpClick(Sender: TObject);
    procedure btnConnectClick(Sender: TObject);
    procedure btnDisconnectClick(Sender: TObject); 
    procedure btnExecSQLClick(Sender: TObject); 
    procedure connAfterConnect(Sender: TObject); 
    procedure connAfterDisconnect(Sender: TObject); 
    procedure FormClose(Sender: TObject; var Action: TCloseAction); 
    procedure cbUseCallBackClick(Sender: TObject); 
    procedure monitorTrace(Sender: TObject; CBIInfo: pSQLTRACEDesc;
      var LogTrace: Boolean);
  
  private
    { Private declarations }
  public
    { Public declarations }
  end;
  
  var
      frmMain: TfrmMain;
  
  implementation
  
  {$R *.xfm}
  
  function MySQLCallBack(CallType: TRACECat; CBIInfo: Pointer): CBTRType; stdcall;
  var
      CBI: pSQLTRACEDesc;
  begin
    Result := cbvUseDEF;
    if CBIInfo <> nil then begin
      CBI := pSQLTRACEDesc(CBIInfo);
      frmMain.lbTrace.Items.Add('CallBack: ' + CBI.pszTrace);
    end;
  end;
  
  procedure TfrmMain.btnConnectClick(Sender: TObject);
  begin
    conn.Open;
    
    cbUseCallBackClick(cbUseCallBack);
  end;
  
  procedure TfrmMain.btnDisconnectClick(Sender: TObject);
  begin
    conn.Close;
  end;
```

