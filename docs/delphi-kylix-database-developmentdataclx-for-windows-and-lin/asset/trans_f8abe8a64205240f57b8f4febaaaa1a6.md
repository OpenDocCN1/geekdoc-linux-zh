
## **列表 6.1**（续）

```pascal
procedure TfrmMain.cbAlwaysShowSelectionClick(Sender: TObject);
begin
    UpdateOption(dgAlwaysShowSelection, cbAlwaysShowSelection.Checked);
end;

procedure TfrmMain.cbConfirmDeleteClick(Sender: TObject);
begin
    UpdateOption(dgConfirmDelete, cbConfirmDelete.Checked);
end;

procedure TfrmMain.cbCancelOnExitClick(Sender: TObject);
begin
    UpdateOption(dgCancelOnExit, cbCancelOnExit.Checked);
end;

procedure TfrmMain.cbMultiSelectClick(Sender: TObject);
begin
    UpdateOption(dgMultiSelect, cbMultiSelect.Checked);
end;

// Grid event handlers

procedure TfrmMain.gridColExit(Sender: TObject);
begin
    lbEvents.Items.Add('OnColExit - Col ' + IntToStr(grid.SelectedIndex) +
         ', Field ' + grid.SelectedField.FieldName + '');

// By calling Abort here, you can prevent focus from leaving this column
// Abort;
end;

procedure TfrmMain.gridColEnter(Sender: TObject);
begin
    lbEvents.Items.Add('OnColEnter - Col ' + IntToStr(grid.SelectedIndex) +
         ', Field ' + grid.SelectedField.FieldName + '');
end;

procedure TfrmMain.gridEditButtonClick(Sender: TObject);
begin
    lbEvents.Items.Add('OnEditButtonClick - Col ' +
         IntToStr(grid.SelectedIndex) + ', Field ' +
         grid.SelectedField.FieldName + '');
end;

procedure TfrmMain.gridCellClick(Column: TColumn);
begin
  lbEvents.Items.Add('OnCellClick - Col ' + IntToStr(grid.SelectedIndex) +
  ', Field ' + grid.SelectedField.FieldName + '');
end;

procedure TfrmMain.gridColumnMoved(Sender: TObject; FromIndex,
  ToIndex: Integer);
begin
  lbEvents.Items.Add('Column moved from ' + IntToStr(FromIndex) +
  ' to ' + IntToStr(ToIndex));
end;

// Command buttons

procedure TfrmMain.btnClearEventLogClick(Sender: TObject);
begin
  lbEvents.Items.Clear;
end;

procedure TfrmMain.btnShowSelectionsClick(Sender: TObject);
var
  Index: Integer;
  s: string;
begin
  if not (dgMultiSelect in grid.Options) then
    raise Exception.Create('dgMultiSelect not set');

  if grid.SelectedRows.Count = 0 then
    raise Exception.Create('No rows selected');

  for Index := 0 to grid.SelectedRows.Count - 1 do begin
    ClientDataSet1.Bookmark := grid.SelectedRows[Index];
    if s <> '' then
      s := s + #13;
    s := s + Format('id: %s', [ClientDataSet1.FieldByName('ID').AsInteger,
      ClientDataSet1.FieldByName('Name').AsString]);
  end;
  ShowMessage(s);
end;

end.
```

+   6 数据感知网格

图 6.3 展示了 Options 应用程序在运行时的状态。

![](img/fe651f295b5f960d5463c4fb581d2281_264_0.png)

Options 应用程序允许你试验 TDBGrid 组件的选项。

## 自定义绘制

从图 6.2 中可以看出，网格的默认外观看起来不错，但并非特别引人注目。通过使用自定义绘制，我们可以显著改善网格的外观。

要在你的网格中实现自定义绘制，你需要处理网格的 OnDrawColumnCell 事件。你可能会注意到网格中包含一个类似名称的事件 OnDrawDataCell。OnDrawDataCell 是一个已过时的事件，为了与早期版本的 Delphi 保持向后兼容性而保留。你应该在任何新的编程项目中都不要使用它。

为 OnDrawColumnCell 事件新创建的处理程序看起来像这样：

```pascal
procedure TForm1.DBGrid1DrawColumnCell(Sender: TObject; const Rect: TRect;
         DataCol: Integer; Column: TColumn; State: TGridDrawState);
         begin
         end;
```

与所有网格事件一样，Sender 参数引用网格对象。Rect 指的是即将绘制的单元格的包围矩形。DataCol 是即将绘制的列的绝对位置基于零的索引。State 是一个包含表 6.6 中列出的一个或多个值的集合。

### 表 6.6 TGridDrawState 值

| 值 | 描述 |
| :--- | :--- |
| *gdSelected* | 单元格被选中。 |
| *gdFocused* | 单元格具有焦点。 |
| *gdFixed* | 单元格是固定的（即，它是指示器单元格）。 |

gdSelected 和 gdFocused 之间的差异可能会让人困惑（尤其是因为这些值会随着 Options 属性的变化而略微改变含义），所以我将在这里澄清一下。

当 dgRowSelect 未设置时（这是默认情况），只有当前单元格设置了 gdSelected 值。如果网格当前具有焦点，当前单元格除了设置 gdSelected 值外还设置了 gdFocused。

当 dgRowSelect 已设置时，当前行中的所有单元格都设置了 gdSelected 值。此外，如果网格具有焦点，该行中的第一个单元格（不包括指示器）设置了 gdFocused。当使用 dgRowSelect 时，你可能希望忽略 gdFocused 值，因为它没有实际意义。

## DefaultDrawing 属性

网格的 DefaultDrawing 属性决定了网格中的绘制方式。当此属性为 True（默认值）时，VCL/CLX 以常规方式绘制网格中的每个单元格，然后将在控制权传递给你设置的 OnDrawColumnCell 处理程序。OnDrawColumnCell 对网格中的每个单元格都会被调用，因此你希望确保你写在该事件处理程序中的代码执行速度很快。

当 DefaultDrawing 为 False 时，Delphi 用适当的背景颜色绘制单元格，并设置网格的 Brush 和 Font 属性以准备绘制单元格。然后，它调用 OnDrawColumnCell，以便你可以自己绘制单元格的内容。

在实践中，你会发现当你实现自定义绘制时，Delphi 的默认绘制代码大约完成了你需要的大部分工作。你可能只想更改选中单元格的颜色，在特定列中绘制图像，或者也许用红色绘制负值。

DefaultDrawing 属性可能会让人联想到两种极端情况。一方面，如果它为 True，则使用其默认设置绘制单元格，然后你反过来在它上面进行绘制。另一方面，如果它为 False，你需要手动绘制每一个单元格——甚至那些不需要特殊绘制的单元格。

幸运的是，情况并非如此。解决方案是将 DefaultDrawing 设置为 False，然后在 OnDrawColumnCell 事件处理程序中调用网格的 DefaultDrawColumnCell，如下所示：

```pascal
procedure TForm1.DBGrid1DrawColumnCell(Sender: TObject; const Rect: TRect;
DataCol: Integer; Column: TColumn; State: TGridDrawState);
begin
if Column.FieldName = 'Salary' then begin
if Column.Field.AsFloat > 50000.0 then begin
DBGrid1.Canvas.Brush.Color := clYellow;
if gdFocused in State then
DBGrid1.Canvas.Font.Color := clRed;
end;
end;
DBGrid1.DefaultDrawColumnCell(Rect, DataCol, Column, State);
end;
```

这段代码片段仅改变了 Salary 列的绘制方式。如果工资大于 50,000 美元，则单元格的背景用黄色绘制。如果单元格具有焦点，则工资用红色绘制。

对于所有其他单元格，以及小于或等于 50,000 美元的工资，单元格将正常绘制。对 DefaultDrawColumnCell 的调用会在对画刷和字体颜色进行适当更改（如果有）之后处理单元格的绘制。

按照 Delphi 内部 VCL/CLX 绘制代码的工作方式，你在这个处理程序中只需要设置画布的 Brush 和 Font 属性，使其反映你在绘制单元格时要使用的颜色和字体。然后，对 DefaultDrawColumnCell 的调用将使用你指定的设置来绘制单元格内容。

![](img/fe651f295b5f960d5463c4fb581d2281_266_0.png)

请注意，在前面的代码片段中，我检查了列的 FieldName 属性，以查看代码是否正在绘制 Salary 列。你可能会想用 DataCol 参数来检查这一点。然而，DataCol 是正在绘制的单元格基于零的绝对索引。如果用户在运行时重新排列列，这个值会发生变化。

以下示例程序演示了自定义绘制网格单元格的几种方法。列表 6.2 包含 CustomDraw 应用程序的完整源代码。

## 列表 6.2 CustomDraw—MainForm.pas

```pascal
unit MainForm;
interface
```
