
`DataModuleDestroy` 关闭 `cdsContacts` 表，并且如果已建立连接，也关闭到应用程序服务器的连接。由于设置了 `cdsContacts.FileName` 属性，程序会自动将数据写入文件 `CONMAN.CDS`。此外，`todo` 数据集也存储在同一个 CDS 文件中，因为它是 `cdsContacts` 的嵌套数据集。

`cdsContactsNewRecord` 和 `cdsTodosNewRecord` 事件会调用本地方法 `GetNextID`。`GetNextID` 克隆相关数据集并移动到该数据集中的第一条记录。第一条记录是具有最低编号 ID 的记录。然后将下一个较低的编号分配给该记录的 ID，以确保该记录具有负主键。

这样做的目的是确保所有尚未添加到数据库中的记录都具有负 ID。服务器端的数据模块检查负 ID，然后调用数据库的 `GEN_ID` 存储过程以分配唯一的 ID。这确保了无论记录是从哪台计算机添加的，所有添加的记录都会获得唯一的 ID。（请记住，可能有多个用户同时在运行此应用程序。）

**注意**

使用克隆数据集检索下一个负 ID 的一种替代方法是设置一个私有变量，并在程序启动时检索下一个 ID。这样，你只需递减该变量即可获得下一个 ID。我不这样做的原因是，在实际应用中，我的数据模块中有时会有 40 或 50 个数据集。我不喜欢设置 40 或 50 个变量——每个数据集一个。相反，我使用通用函数在需要时检索下一个 ID。请注意，克隆数据集会临时需要一小部分内存，并且执行时也需要一小段时间。如果你需要尽可能快地生成临时 ID，应考虑使用私有变量。

清单 9.5 包含客户端主窗体的源代码，这里包含了该应用程序的大部分代码。

# ConMan 应用程序

## 清单 9.5

`ConMan—MainForm.pas`

```pascal
unit MainForm;

interface

uses
    Windows, Messages, SysUtils, Variants, Classes, Graphics, Controls, Forms,
    Dialogs, DBActns, StdActns, ComCtrls, BandActn, ExtCtrls, Menus, Grids, DBGrids,
    DB, StdCtrls, DBCtrl, Mask, ExtDlgs;

type
    TfrmMain = class(TForm)
    StatusBar1: TStatusBar;
    ImageList1: TImageList;
```

### 列表 9.5（续）
