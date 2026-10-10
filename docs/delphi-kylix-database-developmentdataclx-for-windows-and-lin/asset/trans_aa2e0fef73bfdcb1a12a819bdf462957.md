
## 清单 5.2

（续）

```pascal
constructor TETHDBListBox.Create(AOwner: TComponent);
begin
    FValues := TStringList.Create;

    inherited Create(AOwner);
end;

destructor TETHDBListBox.Destroy;
begin
    FValues.Free;

    inherited;
end;

procedure TETHDBListBox.CreateWnd;
begin
    inherited;

    FDataLink := TFieldDataLink(SendMessage(Handle, CM_GETDATALINK, 0, 0));
    FDataLink.OnDataChange := DataChange;
    FDataLink.OnUpdateData := UpdateData;
end;

procedure TETHDBListBox.SetValues(const Value: TStrings);
begin
    FValues.Assign(Value);
    DataChange(Self);
end;

function TETHDBListBox.GetListValue(Index: Integer): string;
begin
    if (Index < FValues.Count) and (FValues[Index] <> '') then
        Result := FValues[Index]
    else if Index < Items.Count then
        Result := Items[Index]
    else
        Result := '';
end;

function TETHDBListBox.IndexOfItem(const Value: string): Integer;
var
    I: Integer;
    Index: Integer;
begin
   I := -1;
   for Index := 0 to Items.Count - 1 do
      if Value = GetListValue(Index) then begin
         I := Index;
         Break;
      end;

   Result := I;
end;

procedure TETHDBListBox.DataChange(Sender: TObject);
begin
   if FDataLink.Field <> nil then
      ItemIndex := IndexOfItem(FDataLink.Field.Text)
   else
      ItemIndex := -1;
end;

procedure TETHDBListBox.UpdateData(Sender: TObject);
begin
   if ItemIndex >= 0 then
      FDataLink.Field.Text := GetListValue(ItemIndex)
   else
      FDataLink.Field.Text := '';
end;
end.
```

TETHDBListBox 的源代码与 TETHDBComboBox 相似，因此此处不再详细展开。

## TDBImage

TDBImage 用于显示数据集 BLOB 字段中包含的位图。不幸的是，TDBImage 不能用于显示非位图图像（如 JPEG、PNG 等）。第 4 章“高级客户端数据集操作”解释了如何从数据库 BLOB 字段中存储和检索非位图图像。

> **注意**
>
> 清单 3.4 展示了如何在不使用 TDBImage 数据感知组件的情况下，显示来自数据集的图像数据。

## 仅限 VCL 的数据感知控件

VCL 支持一些在 CLX 下不支持的额外数据感知控件。这些控件包括：

- TDBRichEdit
- TDBChart
- TDBCtrlGrid

这些组件未包含在 CLX 中，因为它们依赖于以下之一：底层的 Win32 实现（TDBRichEdit）、尚未可用的第三方组件（TDBChart）或不受支持/已废弃的功能（TDBCtrlGrid）。

尽管如此，这些组件在 VCL 应用中仍有其用途，因此我将在本章中介绍 TDBRichEdit，并在下一章介绍 TDBCtrlGrid。由于许多应用都需要日期输入，我将在本章稍后部分介绍 Win32 TDateTimePicker 组件的数据感知实现。

TDBRichEdit 与 TDBMemo 类似，因为它用于显示和编辑多行文本。然而，TDBMemo 显示和编辑的是非格式化文本，而 TDBRichEdit 处理的是富文本（使用 RTF（富文本格式）格式化的文本）。

富文本允许用户使用不同的字体样式和格式化技术（如项目符号、编号、制表符和缩进）来格式化段落、单词或单个字符。虽然 TDBRichEdit 及其非数据感知对应组件 TRichEdit 通过一系列属性和方法支持此功能，但需要提供菜单、工具栏或两者兼具来调用相应方法的工作由你来完成。

即使不编写任何代码，TDBRichEdit 仍可用于显示格式化文本。

## 查找型数据感知控件

前面部分讨论了连接到单个数据集中单个字段的简单数据感知组件。在本节中，我将介绍查找组件。查找组件将数据存储到数据集中的单个字段，但显示来自另一个数据集的可用数据列表。

例如，假设我们正在处理一个包含 ORDERDETAIL 表和 PARTS 表的标准订单录入系统。PARTS 表由 PartNumber 字段和 Description 字段（以及其他字段）组成。ORDERDETAIL 表也包含一个 PartNumber 字段，该字段引用 PARTS 表。

在你的应用程序中，你可能希望用户能够查看零件号及其描述列表，选择一个零件，并将对应的零件号自动存储到 ORDERDETAIL 表中。

这正是查找型数据感知控件的设计目的——从一个数据集显示列表，并允许用户选择一项以存储到另一个数据集中。

为了完成与查找数据集的链接，查找型数据感知组件提供了四个额外的属性：`ListSource`、`ListField`、`KeyField` 和 `ListFieldIndex`。

- `ListSource` 引用用于检索值列表的数据集的数据源。
- `ListField` 是要在组件中显示的字段名的分号分隔列表。
- `KeyField` 确定要存储在数据集中的字段。
- `ListFieldIndex` 是一个零基数字，确定用于组件内增量搜索的字段。例如，假设你将 `ListField` 属性设置为 `FirstName;LastName`。这指示组件在列表中显示名字和姓氏。如果将 `ListFieldIndex` 设置为 1，当用户在控件中输入时，它将对 `LastName` 字段执行自动增量搜索。

查找型数据感知组件由 `TDBLookupComboBox` 和 `TDBLookupListBox` 组成。这些组件的外观和行为类似于 `TDBComboBox` 和 `TDBListBox`（分别对应），不同之处在于，它们不是手动填充项目，而是 `TDBLookupComboBox` 和 `TDBLookupListBox` 从通过组件的 `ListSource` 属性引用的数据集中检索项目。

**注意**

使用 TDBLookupComboBox 和 TDBLookupListBox 可以复制 TETHDBComboBox 和 TETHDBListBox 组件的功能。为此，创建一个 TClientDataSet，其中包含在 TETHDBComboBox 或 TETHDBListBox 中设置的 Items 和 Values 关联。如果你在应用程序中只有这种情况出现一次，你可能选择走这条路线。然而，如果你有多个此类情况，你的表单将布满查找数据集，你可能发现使用 TETHDBComboBox 和 TETHDBListBox 更为方便。

## TDBNavigator

本章讨论的其余组件用于显示和编辑数据，但 TDBNavigator 提供了一种类导航和操作数据集的手段而无需编写代码。视觉上，TDBNavigator 看起来像工具栏，因为它包含一组水平排列的预定义按钮（实际上是 TSpeedButtons），这些按钮列于表 5.8 中。

### 表 5.8：TDBNavigator 按钮

| 按钮 | 数据集方法 |
| :--- | :--- |
| [图标：第一个] | First |
| [图标：前一个] | Prior |
| [图标：下一个] | Next |
| [图标：最后一个] | Last |
| [图标：插入] | Insert |
| [图标：删除] | Delete |
| [图标：编辑] | Edit |
| [图标：确认] | Post |
| [图标：取消] | Cancel |
| [图标：刷新] | Refresh（在第 7 章“数据集提供程序”中讨论） |

当用户点击 TDBNavigator 中的某个按钮时，VCL/CLX 会自动调用对应的数据集方法。你可以通过 VisibleButtons 属性控制显示哪些按钮，该属性实现为 Pascal 集合：只需从 VisibleButtons 属性中移除你不希望显示的按钮即可。

虽然更改按钮上显示的图像的方法是可行的，但该方法并未得到良好的文档记录。TDBNavigator 封装了多个 TSpeedButtons 以显示单个图像，因此你可以通过控件数组访问单个快速按钮（如下面代码片段所示）：

```pascal
(DBNavigator1.Controls[0] as TSpeedButton).Glyph.LoadFromFile('C:\First.bmp');
```

Controls 数组中的索引是一个介于零到九之间的数字，指的是按钮在导航器按钮数组中的绝对位置。然而，访问按钮的一种更可靠的方法是使用 TNavigateBtn 枚举类型，该类型在 DBCtrls.pas 中定义如下：

```pascal
TnavigateBtn = (nbFirst, nbPrior, nbNext, nbLast, nbInsert, nbDelete, nbEdit, nbPost, nbCancel, nbRefresh);
```

