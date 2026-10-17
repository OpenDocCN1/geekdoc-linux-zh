
## 局限性

尽管 `TDBGrid` 功能强大，但它确实存在一些局限性。最显著的一点是它不显示备忘录（memos）或图像。你可以使用网格的自定义绘图功能手动绘制图像或备忘录，但由于每个网格行的高度相同，当一个备忘录有 3 行而另一个有 30 行长时，这可能会导致困难。

许多可用的第三方网格移除了这一限制（以及其他限制）。在本章末尾，将对一些你可能想要了解的第三方网格进行快速概述。

## TClientDataSetGrid

`TClientDataSetGrid` 是由 John Kaster 编写的 `TDBGrid` 派生类。它利用了客户端数据集的一些功能，提供当用户点击列标题时自动对网格进行排序的功能。

此外，`TClientDataSetGrid` 可以自动将列信息持久化到单独的配置文件并从该文件加载。它不支持将列信息保存到或加载自 ini 文件或 Windows 注册表，因此你可能仍然希望使用前面章节中提供的 `SaveColumnConfiguration` 和 `LoadColumnConfiguration` 过程。(`TClientDataSetGrid` 在 Code Central 上可用，ID 为 15099，网址为 http://codecentral.borland.com/。)

### 自动排序

如前所述，`TClientDataSetGrid` 允许用户按单列或多列进行升序或降序排序。它甚至可以一列按升序排序，另一列按降序排序。

要启用此功能，必须将组件的 `TitleSort` 属性设置为 `True`。默认情况下为 `False`，允许组件与非客户端数据集一起使用。如果你将 `TitleSort` 设置为 `True`，`TClientDataSetGrid` 不能与不派生自 `TCustomClientDataSet` 的数据集一起使用。

为了指示当前的排序顺序，`TClientDataSetGrid` 在已排序列的标题中绘制三维箭头。用于绘制这些箭头的颜色通过 `ArrowColor`、`ArrowHighlight` 和 `ArrowShade` 属性设置。

图 6.4 显示了网格按 Name 排序，然后按 Birthday 排序时的外观。

![](img/52a35759a0f10dade27a840504be5d82_277_0.png)

**图 6.4**

`TClientDataSetGrid` 提供关于当前排序顺序的视觉反馈。

要排序，点击其中一个列标题。该列的标题单元格中会绘制一个向上箭头。要切换到降序，再次点击该列标题。

如果你想在多列上进行排序，按住 Shift 键并点击下一个要排序的列标题。按住 Shift 键并第二次点击该列标题，仅对该列进行降序排序。按住 Shift 键并第三次点击该列，将其从当前排序顺序中移除。对你想要排序的每一列重复此操作。

实际上，做比说容易。如果上述解释听起来很复杂，你可能想要亲自尝试点击列标题，以及按住 Shift 键点击列标题，看看效果。

### 列自定义

除了自动排序功能外，`TClientDataSetGrid` 还提供了一个单独的对话框，可用于设置网格的可见列（如图 6.5 所示）。要显示此对话框，请调用网格的 `ConfigureColumns` 方法，如下所示：

```pascal
TClientDataSetGrid.ConfigureColumns;
```

![](img/52a35759a0f10dade27a840504be5d82_278_0.png)

**图 6.5**

> *TClientDataSetGrid* 允许用户隐藏他们不想看到的列。

使用此对话框，用户可以隐藏或显示单个列。

如果你希望网格自动保存和恢复其列配置（包括列顺序和单个列的可见性状态），请将 `ConfigFile` 属性设置为你希望用于持久化列信息的文件名。请确保为每个网格使用不同的文件名，因为该组件的当前版本不支持在单个文件中保存多个配置。

> **注意**
>
> 由于 `TCIiontbaSetGrid` 的代码是免费公开的，我希望未来能有积极的 Delphi 程序员为其提供增强功能。我个人的愿望清单包括：
>
> - 将列配置保存到 ini 文件和 Windows 注册表，以及从这些位置加载配置。
> - 增强“列配置”对话框，使其除了隐藏或显示列之外，还支持列重新排序。
> - 增强“列配置”对话框，使其支持锁定单个列，以防止被隐藏或移动。
> - 添加对 `OnColumnSized` 事件的支持。

## TDBCtrlGrid

我不会花太多时间在 `TDBCtrlGrid` 上，因为它不兼容 CLX，而且目前没有针对 `TDBCtrlGrid` 的新开发工作。

`TDBCtrlGrid` 是一种网格组件，尽管它依赖于其他数据感知组件来执行实际的数据输入和输出。要在应用程序中使用 `TDBCtrlGrid`，请将其放置在窗体上，并将 `DataSource` 属性连接到数据源。然后，使用其他数据感知组件（如 `TDBEdit`、`TDBCheckBox` 等）来填充网格。

`TDBCtrlGrid` 在运行时复制这些组件，为网格中显示的每条记录显示每个组件。网格中的每个单元格对应于数据集中的单个记录。

大多数数据感知控件都是可复制的（即，它们可以用于 `TDBCtrlGrid`）。有些则不是（包括我在前一章中创建的 `TDBDateTimePicker` 组件）。为了让控件可复制，它必须在 `ControlStyle` 属性中包含 `csReplicable` 选项（通常在组件的构造函数中设置）。以下是 `TDBEdit` 构造函数中的代码片段：

```pascal
constructor TDBEdit.Create(AOwner: TComponent);
begin
inherited Create(AOwner);
inherited ReadOnly := True;
ControlStyle := ControlStyle + [csReplicable];
…;
end;
```

以下部分讨论 `TDBCtrlGrid` 引入的属性和事件。

### 属性

`TDBCtrlGrid` 引入了一些可用于自定义其外观和感觉的属性。表 6.7 列出了这些属性。

**表 6.7 TDBCtrlGrid 属性**

| 属性 | 描述 |
| :--- | :--- |
| `AllowInsert` | 当为 True 时，用户可以滚动超过网格中的最后一条记录以插入新记录。 |
| `AllowDelete` | 当为 True 时，用户可以通过按 Ctrl+Delete 删除当前记录。 |
| `ColCount` | 确定网格中显示的列数。 |
| `Orientation` | 确定网格滚动以显示更多数据的方向。 |
| `PanelBorder` | 可能的值为 gbNone 和 gBRaised。gBRaised 使网格具有凸起的外观。通过将 PanelBorder 设置为 gbNone 并将 TDBCtrlGrid 放置在具有所需斜角的窗格上，可以实现其他外观，如下沉或凸起。 |
| `PanelHeight` | 指单个窗格（单元格）的高度，以像素为单位。 |
| `PanelWidth` | 指单个窗格（单元格）的宽度，以像素为单位。 |
| `RowCount` | 确定网格中同时显示的行数。 |
| `SelectedColor` | 确定当前单元格的背景颜色。 |
| `ShowFocus` | 当为 True 时，会在当前单元格周围绘制一个焦点矩形。 |

`ColCount`、`PanelWidth` 和 `Width` 属性直接相关。`ColCount`×`PanelWidth` 大约等于 `Width`（考虑网格边框和垂直滚动条）。只要 `Align` 设置不阻止，设置 `ColCount` 会自动调整 `Width`。例如，将 `Align` 设置为 alLeft 不允许网格调整大小。在这种情况下，设置 `ColCount` 会自动调整 `PanelWidth`。

同样，`RowCount`、`PanelHeight` 和 `Height` 属性也是相关的。设置一个属性会影响其他属性。

## 事件

`TDBCtrlGrid` 只包含一个新事件，名为 `OnPaintPanel`。`OnPaintPanel` 在每个窗格即将被绘制之前触发。`OnPaintPanel` 看起来像这样：

```pascal
procedure TForm1.DBCtrlGrid1PaintPanel(DBCtrlGrid1: TDBCtrlGrid;
  Index: Integer);
begin
end;
```

`Index` 指即将绘制的窗格的基于零的索引，是一个介于 0 和 `RowCount`— 1 之间（包含两端）的数字。

你可能注意到没有 Rect 参数传递给此函数，因此乍一看并不明显如何确定当前单元格的边界矩形。进入此方法时，网格画布的原点设置为当前窗格的左上角。换句话说，画布上的点 (0, 0) 指的是窗格的左上角。点 (`PanelWidth`, `PanelHeight`) 指的是右下角。这使得您可以使用画布进行诸如在窗格上绘制背景图像等操作（如下一个取自列表 6.4 的代码片段所示）。

```pascal
```
