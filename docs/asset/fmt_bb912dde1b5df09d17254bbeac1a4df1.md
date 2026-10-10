
### 表 6.3 TColumn 标题属性

正如前文所述，Delphi 不会自动将数值字段的标题 `Alignment` 属性设置为 `tRightJustify`。因此，在创建持久列时，您应该确保检查标题的对齐方式。

## 网格选项

设置好要在网格中显示的列之后，您可以设置网格全局选项，这些选项决定了网格的整体外观和风格。表 6.4 列出了可用的选项。

### 表 6.4 TDBGrid 选项

| 选项 | 描述 |
| :--- | :--- |
| `dgRowSelect` | 设置后，单击某一行会高亮显示整行，而不是选择单个单元格。本章稍后介绍的自定义绘制网格方法也可以手动实现行高亮。 |
| `dgAlwaysShowSelection` | 设置此选项即使网格没有焦点也会高亮显示当前单元格。 |
| `dgConfirmDelete` | 如果网格的 `ReadOnly` 属性未设置，此选项会导致 VCL 在用户于网格中按下 `Ctrl+Delete` 时显示删除确认消息。如果未设置此选项，用户按下 `Ctrl+Delete` 时会直接删除当前记录。请注意，即使未设置 `dgEditing`，`Ctrl+Delete` 也会删除当前记录。 |
| `dgCancelOnExit` | 此选项影响当用户通过 `Tab` 键退出网格时，对新插入行的处理方式。设置后，未输入任何数据的新插入行将被取消。如果未设置，留空的插入行将被提交到数据集。 |
| `dgMultiSelect` | 设置后，用户可以按住 `Ctrl` 键并单击各个行，从而在网格中选择多个行。 |

默认情况下，`Options` 设置为 [`dgEditing`, `dgTitles`, `dgIndicator`, `dgColumnResize`, `dgColLines`, `dgRowLines`, `dgTabs`, `dgConfirmDelete`, `dgCancelOnExit`]。我发现，当我使用 `TDBGrid` 时，我会关闭 `dgEditing` 和 `dgIndicator` 选项，并将网格的 `ReadOnly` 属性设置为 `True`。我不允许用户在网格中直接编辑，而是在他们按下 `Enter` 键时显示一个对话框，让他们在那里编辑当前记录的字段值。当然，效果可能因人而异，你可以根据自己的应用情况决定最喜欢的一组选项。

## 事件

除了前面列出的属性外，`TDBGrid` 还提供了许多事件，你可以响应这些事件以对流体的显示和功能进行更精细的控制。这些事件列在表 6.5 中。

### 表 6.5 TDBGrid 事件

| 事件 | 描述 |
| :--- | :--- |
| `OnCellClick` | 当用户单击一个单元格时触发。当用户单击标题单元格、指示器或网格背景时不触发。 |
| `OnColEnter` | 焦点进入当前列后立即触发。 |
| `OnColExit` | 焦点离开当前列前立即触发。在此处理程序中调用 `Abort` 可防止网格切换到新列。 |
| `OnColumnMoved` | 用户移动列后（但未在用户调整列大小后）在运行时触发。 |
| `OnDrawColumnCell` | 在即将绘制单元格时触发。它用于实现自定义绘制，将在本章稍后解释。 |
| `OnDrawDataCell` | 已弃用，仅为保持向后兼容性而包含。 |
| `OnEditButtonClick` | 当用户单击单元格中的省略号按钮时触发。 |
| `OnTitleClick` | 当用户单击标题单元格时发生（假设设置了 `dgTitles` 选项）。`TClientDataSet` 内部使用此事件，在用户单击列标题时自动对底层数据集进行排序。 |

以下示例程序（如列表 6.1 所示）演示了不同网格事件的触发时机。下一节“自定义绘制”将更详细地探讨 `OnDrawColumnCell` 事件。

### 列表 6.1 Options—MainForm.pas
