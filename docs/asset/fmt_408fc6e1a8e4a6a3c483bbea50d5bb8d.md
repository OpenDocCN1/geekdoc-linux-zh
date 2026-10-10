
清单 9.5 中展示的事件代码值得讨论。我在源代码中对相关的事件处理程序组进行了归类。

表单的 `OnCreate` 事件处理程序将数据模块的 `TSocketConnection.AfterConnect` 和 `AfterDisconnect` 事件处理程序设置为指向主表单的 `DoConnectDisconnect` 方法。这样一来，当与应用程序服务器建立连接或断开连接时，主表单就能获知连接或断开状态。`DoConnectDisconnect` 仅使状态栏失效，随后状态栏会更新以显示新的连接状态。

这些事件处理程序在运行时而非设计时分配，因为事件处理程序并不位于与数据模块相同的单元中。由于数据模块不使用主表单，因此无法在设计时分配事件处理程序。

`dsContactsDataChange` 在联系人数据源检测到数据变化时触发。事件处理程序检查修改的字段是 `nil`（意味着当前记录发生了变化）还是引用了 `IMAGE` 字段（意味着当前记录的图像发生了变化）。如果是，代码将从数据集加载当前图像并将其显示在主表单上。

`ImageLoad1Execute` 和 `ImageClear1Execute` 分别在用户为当前联系人加载新图像或清除联系人图像时触发。这两个事件处理程序都将联系人数据集置于编辑模式，然后分别清除图像或加载新图像。无论发生这两种事件中的哪一种，`dsContactsDataChange` 都会自动触发，从而导致显示的图像更新。

文件菜单中唯一有趣的操作是连接/断开菜单项。`FileConnect1Execute` 简单地切换套接字连接的 `Connected` 属性以连接到应用程序服务器或断开连接。`FileConnect1Update` 则负责根据当前的连接状态适当地设置操作的标题。

最后，待办事项弹出菜单包含几个用于操作当前联系人待办事项的选项。`TodoAddExecute` 和 `TodoEditExecute` 显示 `frmTodo` 表单，允许用户输入或修改待办事项。`TodoMarkDoneExecute` 将当前待办事项的完成日期和时间设置为当前的日期和时间。

主表单中其余的代码应该相当自明，所以我不再详细赘述。

该应用程序中的最后一个单元是 `TodoForm.pas`。清单 9.6 包含此文件的源代码，它允许用户为联系人输入新的待办事项或编辑现有的待办事项。

### 清单 9.6 ConMan—TodoForm.pas

```pascal
unit TodoForm;

interface

uses

  Windows, Messages, SysUtils, Variants, Classes, Graphics, Controls, Forms,

  Dialogs, ExtCtrls, ComCtrls, StdCtrls;

type

  TfrmTodo = class(TForm)

    pnlClient: TPanel;

    pnlBottom: TPanel;

    Label1: TLabel;

    edDescription: TEdit;

    Label2: TLabel;

    dtDate: TDateTimePicker;

    dtTime: TDateTimePicker;

    Label3: TLabel;

    btnCancel: TButton;

    btnOK: TButton;

    procedure FormCreate(Sender: TObject);

  private

    { Private declarations }

  public

    { Public declarations }

  end;

implementation

{$R *.dfm}

procedure TfrmTodo.FormCreate(Sender: TObject);

begin

  dtDate.Date := Date;

  dtTime.Time := StrToTime('12:00 pm');

end;

end.
```
