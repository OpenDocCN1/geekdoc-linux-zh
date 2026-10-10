
## 示例 8.2（续）

```pascal
procedure TMethodsDM.RemoteDataModuleDestroy(Sender: TObject);
begin
  PostMessage(frmMain.Handle, UM_CONNECT, -1, 0);
end;

initialization
  TComponentFactory.Create(ComServer, TMethodsDM,
    Class_MethodsDM, ciMultiInstance, tmApartment);
end.
```

示例 8.3 包含了客户端应用程序主窗体的源代码。

## 示例 8.3：MethodsClient—MainForm.pas

```pascal
unit MainForm;

interface

uses
  Windows, Messages, SysUtils, Variants, Classes, Graphics, Controls, Forms,
  Dialogs, DB, Grids, DBGids, StdCtrls, MethodsServer_TLB, ComObj, ActiveX;

type
  TTest = class(TAutoIntfObject, ITestCallback)
  protected
    procedure Test; safecall;
  end;

  TfrmMain = class(TForm)
    DBGrid1: TDBGrid;
    DataSource1: TDataSource;
    btnGetServerTime: TButton;
    btnTestCallbacks: TButton;
    procedure FormCreate(Sender: TObject);
    procedure btnGetServerTimeClick(Sender: TObject);
    procedure btnTestCallbacksClick(Sender: TObject);
  private
    { Private declarations }
    FTest: TTest;
  public
    { Public declarations }
  end;

var
  frmMain: TfrmMain;

implementation

uses DataModule;

{$R *.dfm}

procedure TfrmMain.FormCreate(Sender: TObject);
begin
  DM.cdsContacts.Open;
end;

procedure TfrmMain.btnGetServerTimeClick(Sender: TObject);
var
  D: TDateTime;
begin
  D := DM.SocketConnection1.AppServer.GetServerTime;
  ShowMessage(TimeToStr(D));
end;

procedure TfrmMain.btnTestCallbacksClick(Sender: TObject);
var
  typeLib: ITypeLib;
begin
  OleCheck(LoadRegTypeLib(LIBID_MethodsServer, 1, 0, 0, typeLib));
  FTest := TTest.Create(typeLib, ITestCallback);
  DM.SocketConnection1.AppServer.SetCallback(FTest as IDispatch);
  DM.SocketConnection1.AppServer.TestCallbacks;
end;

procedure TTest.Test;
begin
  ShowMessage('In callback');
end;
end.
```

## 公文包模式

多层应用程序非常适合一种称为“公文包模式”的架构。在办公室时，用户通常连接到服务器，并使用实时数据运行应用程序。在离开办公室之前，用户会将可能需要的数据下载到本地机器，以便在离开办公室期间使用。公文包模式的总体概述如下：

在办公室时，用户直接通过应用程序服务器使用实时数据。在路上时，用户操作数据的本地副本，并根据需要添加或修改数据。返回办公室后，用户重新连接到服务器，并将所有更新同步回服务器。

这种魔法是通过你在这本书中已经掌握的技术实现的。当连接到服务器时，数据集提供程序为客户端应用程序的客户端数据集提供实时数据副本。在用户离开办公室之前，通过调用 `TClientDataSet.SaveToFile` 将数据保存到本地。

在路上时，客户端无法连接到应用程序服务器；相反，它通过调用 `TClientDataSet.LoadFromFile` 加载数据的本地副本。更改会累积在更改日志中，并在用户退出应用程序之前通过调用 `TClientDataSet.SaveToFile` 进行持久化保存。

当用户返回办公室时，客户端应用程序再次调用 `TClientDataSet.LoadFromFile` 加载数据的本地副本，然后调用 `TClientDataSet.ApplyUpdates` 将更新解析并同步回应用程序服务器。

请注意，服务器应用程序本身没有任何变化——只有客户端应用程序包含支持公文包模式的代码。

由于 Delphi 附带了一个有用的公文包演示应用程序，因此我在此不会重复其功能。相反，我建议您查看 Delphi 的演示。对于典型的 Delphi 安装，请查看 `C:\Program Files\Borland\Delphi6\Demos\Midas\Briefcase`。

**注意：** 与其在应用程序中调用 `LoadFromFile` 和 `SaveToFile`，你只需将客户端数据集的 `FileName` 属性赋值给要保存和加载的本地文件名即可。Delphi 会在适当的时候负责加载和保存数据。

## 无状态服务器

在上一章中，我向你展示了如何限制应用程序服务器在特定时间内返回的数据量。限制服务器返回数据量的代价是，你必须在每次服务器获取新数据包时，告知服务器从哪里开始检索数据。Delphi 数据库应用是无状态的，这意味着服务器端的数据库组件不会跟踪其在数据集中的当前位置。当提供程序从 `TSQLDataSet` 或其他数据集组件检索数据时，数据集被打开，数据被发送到提供程序，然后数据集被关闭。由于数据集只在短时间内被访问，单个服务器端数据集可以服务于多个客户端应用程序，从而减少内存负载并提高性能。这在使用本地连接时并不是什么大问题，但在使用远程连接时则成为一个重要的考量因素。

从概念上讲，在无状态服务器上增量获取数据的工作方式如下：

-   提供程序获取一组记录，并记住该批次中最后一条记录的 ID。
-   提供程序通知客户端应用程序最后一条记录。
-   客户端记住最后获取的记录。
-   当客户端从服务器获取下一批记录时，它会通知服务器之前获取的最后一条记录。
-   服务器检索之前获取的最后一条记录之后的下一批记录。

要实施无状态服务器，你需要为服务器上的三个提供程序事件以及客户端上的两个客户端数据集事件提供事件处理程序。让我们从服务器开始：

在应用程序服务器中，你需要将 `TSQLDataSet` 设置为一个参数化查询，如下所示：

```sql
SELECT * FROM CONTACTS WHERE ID > :MinID ORDER BY ID
```

这将仅选择 ID 大于已获取的最后 ID 的联系人。现在，为提供程序的 `OnGetData` 事件提供事件处理程序。在此事件中，你将保存从联系人表中检索到的最后 ID。

```pascal
procedure TStatelessServerData.pvContactsGetData(Sender: TObject;
  DataSet: TCustomClientDataSet);
begin
  DataSet.Last;
  pvContacts.Tag := DataSet.FieldName('ID').AsInteger;
end;
```

![Figure 8-xx](img/52a35759a0f10dade27a840504be5d82_354_0.png)

调用 `DataSet.Last` 并不是直接操作 `TSQLDataSet` 组件。相反，它将移动到即将发送回客户端应用程序的那批记录的最后一行。该最后获取记录的 ID 暂时保存在提供程序的 `Tag` 属性中。

接下来，为提供程序的 `AfterGetRecords` 事件处理程序编写事件处理程序。在此处理程序中，你将通过 `OwnerData` 参数将最后检索到的 ID 传回客户端应用程序。

```pascal
procedure TStatelessServerData.pvContactsAfterGetRecords(Sender: TObject;
  var OwnerData: OleVariant);
begin
  OwnerData := pvContacts.Tag;
end;
```

最后，在服务器上，你需要处理提供程序的 `BeforeGetRecords` 事件处理程序。在此事件中，你将设置 `MinID` 参数的值，以便查询知道接下来要获取哪条记录。下面的代码片段展示了如何实现这一点：

```pascal
procedure TStatelessServerData.pvContactsBeforeGetRecords(Sender: TObject;
  var OwnerData: OleVariant);
begin
  if not VarIsEmpty(OwnerData) then
  begin
    sqlContacts.Params.ParamValues['MinID'] := OwnerData;
    sqlContacts.Refresh;
  end;
end;
```

这就是你在服务器上需要做的全部内容。在客户端应用程序中，你需要首先为客户端数据集的 `AfterGetRecords` 事件提供事件处理程序。在此事件处理程序中，你将保存从服务器检索到的最后 ID，如下面的代码片段所示：

```pascal
procedure TForm1.cdsContactsAfterGetRecords(Sender: TObject;
  var OwnerData: OleVariant);
begin
  cdsContacts.Tag := OwnerData;
end;
```

在此示例中，最后检索到的 ID（通过 `OwnerData` 参数提供）再次存储在客户端数据集的 `Tag` 属性中。你也可以设置一个名为 `FLastContactID` 的窗体变量来保存 ID。

最后，为客户端数据集的 `BeforeGetRecords` 事件提供事件处理程序。在此事件处理程序中，你将把最后检索到的 ID 传回服务器，以便服务器知道从哪里开始获取数据。

