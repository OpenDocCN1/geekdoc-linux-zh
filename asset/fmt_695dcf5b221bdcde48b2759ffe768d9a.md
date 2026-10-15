
```pascal
unit MainForm;

interface

uses

  SysUtils, Variants, Classes, QGraphics, QControls, QForms,

  QDialogs, QExtCtrls, QDBCtrls, QGrids, QDBGrids, DB, DBClient, GStdCtrls;

type

  TfrmMain = class(TForm)

    pnlClient: TPanel;

    pnlBottom: TPanel;

    cdsCustomer: TClientDataSet;

    cdsOrder: TClientDataSet;

    dsCustomer: TDataSource;

    dsOrder: TDataSource;

    gridCustomer: TDBGrid;

    gridOrder: TDBGrid;

    navCustomer: TDBNavigator;

    navOrder: TDBNavigator;

    cdsCustomerName: TStringField;

    cdsCustomerAddress: TStringField;

    cdsCustomerCity: TStringField;

    cdsCustomerState: TStringField;

    cdsCustomerZip: TStringField;

    cdsCustomerPhone: TStringField;

    cdsCustomerOrders: TDataSetField;

    cdsOrderQuantity: TIntegerField;

    cdsOrderDescription: TStringField;

    cdsOrderUnitPrice: TFloatField;

    cdsOrderTotalPrice: TFloatField;

    btnLoad: TButton;

    btnSave: TButton;

    OpenDialog1: TOpenDialog;

    SaveDialog1: TSaveDialog;

    procedure cdsOrderCalcFields(DataSet: TDataSet);

    procedure FormCreate(Sender: TObject);

    procedure btnSaveClick(Sender: TObject);

    procedure btnLoadClick(Sender: TObject);

  private

    { Private declarations }

  public

    { Public declarations }

  end;

var

  frmMain: TfrmMain;

implementation

{$R *.xfm}

procedure TfrmMain.cdsOrderCalcFields(DataSet: TDataSet);

begin

   DataSet.FieldByName('TotalPrice').AsFloat :=

        DataSet.FieldByName('Quantity').AsInteger *

        DataSet.FieldByName('UnitPrice').AsFloat;

end;

procedure TfrmMain.FormCreate(Sender: TObject);

begin

   cdsCustomer.CreateDataSet;

end;

procedure TfrmMain.btnSaveClick(Sender: TObject);

begin

   if SaveDialog1.Execute then

      cdsCustomer.SaveToFile(SaveDialog1.FileName);

end;

procedure TfrmMain.btnLoadClick(Sender: TObject);

begin

   if OpenDialog1.Execute then

      cdsCustomer.LoadFromFile(OpenDialog1.FileName);

end;

end.
```

![](img/52a35759a0f10dade27a840504be5d82_188_0.png)

查看代码，你会发现只有四个方法。`FormCreate` 创建主数据集。理解这一点很重要，因为这也创建了细节数据集。你很少需要在代码中直接操作细节数据集。

同样，`btnSaveClick` 和 `btnLoadClick` 将主数据集保存和加载到/从磁盘，这也处理了所有细节数据集的保存和加载。

运行此应用程序时，你必须要么从头输入一些数据，要么从文件加载数据集。随本书源代码附带的是一个名为 `NESTED.CDS` 的预先创建的数据文件。你可能希望加载此文件，而不是手动输入客户和订单。

图 4.5 展示了 Nested 应用程序在运行时的状态。

![](img/52a35759a0f10dade27a840504be5d82_189_0.png)

### 图 4.5
嵌套数据集会自动显示当前主记录的细节数据。

关于这个应用程序有几点有趣的地方。首先，当你在顶部的网格中从一个客户切换到另一个客户时，该客户的订单会显示在底部的网格中。这是自动完成的，无需编写代码。

其次，如果你添加或修改一个订单，你会注意到客户记录进入了编辑模式（如当前客户记录指示列中显示的图形所示）。如果你通过程序操纵嵌套数据集，请记住以下几点：在添加或修改细节记录后，需要提交主记录。

## 撤销支持

`TCustomClientDataSet` 及其派生类支持内置的撤销功能，因此你可以在应用程序中提供假设（what-if）场景。例如，你可以允许用户更改数据集中某些字段的值（或许用于绘制数据或否则以其他方式显示对数据的分析）。如果用户不喜欢结果，他可以通过撤销其更改来恢复到之前的数据，可以逐个撤销，也可以一次性撤销大量更改。

### 取消

你可能已经熟悉 `Cancel` 方法，但为了完整性，我还是在这里提一下。

撤销支持的最基本级别是简单地丢弃在提交之前对当前记录的更改。`Cancel` 方法提供了这种支持：

```pascal
ClientDataSet1.Edit;
ClientDataSet1.FieldByName('Last').AsString := 'Carter';
// 在这里做更多事情，然后决定不保存更改。
ClientDataSet1.Cancel;
```

### 变更日志

为了支持更高级的撤销操作，客户端数据集包含一个变更日志。变更日志用于记录对数据集所做的每次更改，直到这些更改被合并到数据中、撤销或取消。以下各部分将研究用于提交和回滚更改的不同方法。

当你调用 `SaveToFile` 或 `SaveToStream` 时，变更日志会随数据一起保存。当数据集从文件或流中读取回来时，变更日志将处于保存之前的状态。这意味着你甚至可以在应用程序的多次运行之间执行撤销操作。

### LogChanges

为了使变更日志处于活动状态，数据集的 `LogChanges` 属性必须设置为 `True`（这是默认值）。如果你不打算在应用程序中提供撤销支持，可以将 `LogChanges` 设置为 `False`，这略微减少内存需求并提高性能。

> **注意**
> 在创建将客户端数据集连接到数据集提供者的应用程序时（如第 7 章“数据集提供者”中所述），你不应该将 `LogChanges` 设置为 `False`。这是因为将 `LogChanges` 设置为 `False` 会阻止你对客户端数据集进行更改并将这些更改应用于底层数据库。

## UndoLastChange（撤销上一次更改）

通过调用 `UndoLastChange`，您可以撤销对数据集最近一次的更改（无论该更改是针对哪条记录）。

`UndoLastChange` 接受一个单一的布尔参数（`FollowChange`），用于指示数据集是否应定位到受撤销操作影响的记录。如果 `FollowChange` 为 `True`，客户端数据集会将光标定位到被撤销或恢复的记录。如果 `FollowChange` 为 `False`，最近修改的记录仍会被恢复，但当前记录不会改变。

```pascal
ClientDataSet.First;
ClientDataSet.Next;
ClientDataSet.Edit;
ClientDataSet.FieldName('Last').AsString := 'Williams';
ClientDataSet.Post;
ClientDataSet.First;
ClientDataSet.Edit;
ClientDataSet.FieldName('Last').AsString := 'Carter';
ClientDataSet.Post;
```
