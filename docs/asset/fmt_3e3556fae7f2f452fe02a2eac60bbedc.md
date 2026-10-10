
要进行排序，请单击其中一个列标题。该列的标题单元格中会绘制一个向上箭头。若要切换为降序，请再次单击该列标题。

如果您想对多列进行排序，请按住 `Shift` 键并单击要排序的下一个列标题。按住 `Shift` 键第二次单击列标题，将仅对该列进行降序排序。按住 `Shift` 键第三次单击该列，会将其从当前排序顺序中移除。对您想要排序的每一列重复此操作。

说难做易。如果前面的解释听起来很复杂，不妨亲自试一试：点击列标题，或者按住 `Shift` 键并点击列标题，观察其效果。

## 列自定义

除了自动排序功能外，`TClientDataSetGrid` 还提供了一个独立的对话框，可用于设置网格中可见的列（如图 6.5 所示）。要显示此对话框，请调用网格的 `ConfigureColumns` 方法，如下所示：

```python
CClientDataSetGrid1.ConfigureColumns;
```

![](img/fe651f295b5f960d5463c4fb581d2281_277_0.png)

**图 6.5**

*TClientDataSetGrid 允许用户隐藏其不想看到的列。*

使用此对话框，用户可以隐藏或显示单个列。

如果您希望网格自动保存并恢复其列配置（包括列顺序以及单个列的可见性状态），请将 `ConfigFile` 属性设置为您希望用于持久化列信息的文件名称。请确保为每个网格使用不同的文件名，因为当前版本的组件不支持在单个文件中保存多个配置。

### 注意

> 由于 `TClientDataSetGrid` 的代码是免费提供的，我希望看到一些富有进取心的 Delphi 程序员在未来为其提供增强功能。我个人的愿望列表包括：
>
> - 将列配置保存和加载到 ini 文件以及 Windows 注册表中。
> - 增强 `列配置` 对话框，使其除了隐藏或显示列之外，还支持重新排序列。
> - 增强 `列配置` 对话框，使其支持锁定单个列，以便这些列无法被隐藏或移动。
> - 添加对 `OnColumnSized` 事件的支持。

## TDBCtrlGrid

我不会在 `TDBCtrlGrid` 上花太多时间，因为它不兼容 CLX，并且目前也没有关于 `TDBCtrlGrid` 的新开发。

`TDBCtrlGrid` 是一个类似网格的组件，尽管它依赖于其他数据感知组件来执行实际的数据输入和输出。要在应用程序中使用 `TDBCtrlGrid`，请将其拖放到窗体上，并将 `DataSource` 属性连接到您的数据源。然后，使用其他数据感知组件（如 `TDBEdit`、`TDBCheckBox` 等）来填充网格。

`TDBCtrlGrid` 在运行时复制这些组件，为网格中显示的每条记录显示相应的组件。网格中的每个单元格对应数据集中的单个记录。

大多数数据感知控件都是可复制的（即，它们可用于 `TDBCtrlGrid` 中）。有些则不是（包括我在前一章中创建的 `TDateTimePicker` 组件）。为了使控件可复制，它必须在其 `ControlStyle` 属性中包含 `csReplicable` 选项（通常在组件的构造函数中设置）。以下是 `TDBEdit` 构造函数中的一段代码：

```pascal
constructor TDBEdit.Create(AOwner: TComponent);
begin
   inherited Create(AOwner);
   inherited ReadOnly := True;
   ControlStyle := ControlStyle + [csReplicable];
   ...
end;
```

以下各节讨论了 `TDBCtrlGrid` 引入的属性和事件。

### 属性

`TDBCtrlGrid` 引入了一组可用于自定义其外观和感觉的属性。表 6.7 列出了这些属性。

**表 6.7 TDBCtrlGrid 属性**

| 属性 | 描述 |
| :------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| AllowInsert | 当为 True 时，用户可以滚动超出网格中的最后一条记录以插入新记录。 |
| AllowDelete | 当为 True 时，用户可以通过按 Ctrl+Delete 删除当前记录。 |
| ColCount | 确定网格中显示的列数。 |
| Orientation | 确定网格显示更多数据时的滚动方向。 |
| PanelBorder | 可能的值为 gbNone 和 gbRaised。gbRaised 使网格具有凸起的外观。通过将 PanelBorder 设置为 gbNone 并将 TDBCtrlGrid 放置在一个具有所需倒角的窗体面板上，可以实现其他外观，例如凹陷或凸起。 |
| PanelHeight | 指单个面板（单元格）的高度（以像素为单位）。 |
| PanelWidth | 指单个面板（单元格）的宽度（以像素为单位）。 |
| RowCount | 确定网格中一次显示的行数。 |
| SelectedColor | 确定当前单元格的背景颜色。 |
| ShowFocus | 当为 True 时，在当前单元格周围绘制焦点矩形。 |

`ColCount`、`PanelWidth` 和 `Width` 属性直接相关。`ColCount` × `PanelWidth` 大约等于 `Width`（考虑网格边框和垂直滚动条）。只要 `Align` 设置不阻止，设置 `ColCount` 会自动调整 `Width`。（例如，将 `Align` 设置为 `aClient` 时，不允许网格调整大小。在这种情况下，设置 `ColCount` 会自动调整 `PanelWidth`。）

类似地，`RowCount`、`PanelHeight` 和 `Height` 属性也相互关联。设置其中一个属性会影响其他属性。

### 事件

`TDBCtrlGrid` 仅包含一个名为 `OnPaintPanel` 的新事件。`OnPaintPanel` 在即将绘制每个面板之前触发。`OnPaintPanel` 如下所示：

```pascal
procedure TForm1.DBCtrlGrid1PaintPanel(DBCtrlGrid: TDBCtrlGrid; Index: Integer);
begin
end;
```

`Index` 指的是即将绘制的面板的基于零的索引，其数值在 0 到 `RowCount-1` 之间（包含两端）。

您可能会注意到，传递给此函数时没有 Rect 参数，因此乍一看很难确定当前单元格的边界矩形。进入此方法时，网格画布的原点被设置为当前面板的左上角。换句话说，画布上的点 (0, 0) 指的是面板的左上角。点 (`PanelWidth`, `PanelHeight`) 指的是右下角。这使得您可以使用画布进行诸如在面板上绘制背景图像等操作（如下面取自列表 6.4 的代码片段所示）。

```pascal
procedure TForm1.DBCtrlGrid1PaintPanel(DBCtrlGrid: TDBCtrlGrid;
Index: Integer);
begin
if Index <> DBCtrlGrid1.PanelIndex then
DBCtrlGrid1.Canvas.Draw(0, 0, Image1.Picture.Graphic);
end;
```
