

## TDBNavigator 按钮

| 按钮 | 数据集方法 |
| :--- | :--- |
| | First |
| | Prior |
| | Next |
| | Last |
| | Insert |
| | Delete |
| | Edit |
| | Post |
| | Cancel |
| | Refresh (在第七章“数据集提供程序”中讨论) |

当用户单击 TDBNavigator 中的某个按钮时，VCL/CLX 会自动调用对应的数据集方法。您可以通过 VisibleButtons 属性来控制显示哪些按钮，该属性以 Pascal 集合的形式实现：只需从 VisibleButtons 属性中移除您不希望显示的按钮即可。

可以更改一个或多个按钮上显示的图像，尽管执行此操作的方法没有很好的文档说明。TDBNavigator 封装了多个 TSpeedButton 以显示各个图像，因此您可以通过控件数组访问单独的快速按钮（如下面的代码片段所示）：

```pascal
(DBNavigator1.Controls[0] as TSpeedButton).Glyph.LoadFromFile('C:\First.bmp');
```

Controls 数组的索引是一个介于零和九之间的数字，它指的是按钮在导航器按钮数组中的绝对位置。然而，访问按钮更可靠的方法是使用在 DBCtrls.pas 中定义的 TNavigateBtn 枚举类型，定义如下：

```pascal
TNavigateBtn = (nbFirst, nbPrior, nbNext, nbLast,
                  nbInsert, nbDelete, nbEdit, nbPost, nbCancel, nbRefresh);
```

使用此类型，我们可以编写以下代码代替上面的代码：

```pascal
(DBNavigator1.Controls[Ord(nbFirst)] as TSpeedButton).Glyph.LoadFromFile('C:\First.bmp');
```

### 创建自己的数据感知组件

当您理解提供现有标准控件的数据感知版本所需采取的步骤时，创建自己的数据感知组件并不那么困难。在本节中，我将提供 **Win32 TDateTimePicker** 组件的数据感知版本的可用代码。在此过程中，我将概述创建数据感知组件所需的步骤。阅读以下各部分时，请参照列表 5.3 中显示的源代码。

### TFieldDataLink

**TFieldDataLink** 是一个辅助类，用于在数据感知组件和底层数据集字段之间建立链接。TFieldDataLink 仅提供少量您在编写数据感知组件时需要关注的方法、属性和事件。表 5.9、5.10 和 5.11 分别列出了最常用的方法、属性和事件。

**表 5.9 TFieldDataLink 方法**

| **方法** | **描述** |
| :--- | :--- |
| Edit | 尝试将数据集置于编辑模式。如果数据集不允许编辑，*Edit* 返回 **False**，否则返回 **True**。 |
| Modified | 当数据感知组件发生变化时（例如用户在其中输入，或通过其他方式如点击或与组件的其他交互改变了组件的内容），调用 *Modified* 方法。 |
| Reset | 当发生导致底层字段内容重置为其原始值的操作时，调用 *Reset* 方法。例如，数据感知组件可能支持一个键（如 **Ctrl+R**）来重置字段的原始值。 |

**表 5.10 TFieldDataLink 属性**

| **属性** | **描述** |
| :--- | :--- |
| CanModify | 只读属性，如果相应的字段可以被修改则返回 **True**，如果不能则返回 **False**。如果数据集、字段或数据感知组件是只读的，*CanModify* 返回 **False**。 |
| Control | 引用链接的数据感知控件。 |
| Field | 引用数据感知控件绑定到的字段对象。字段对象可以是持久字段，也可以是非持久字段的自动生成的字段对象。 |
| FieldName | 数据感知组件绑定到的字段的名称。 |

**表 5.11 TFieldDataLink 事件**

| **事件** | **描述** |
| :--- | :--- |
| OnDataChange | 当底层字段发生变化时触发。 |
| OnEditingChange | 当关联的数据源从编辑模式切换到浏览模式，或反之时触发。 |
| OnUpdateData | 当数据感知组件中包含的数据应写入数据集时触发。 |
| OnActiveChange | 当底层数据集从活动状态变为非活动状态，或反之时触发。 |

接下来的章节解释了如何将 TFieldDataLink 类整合到组件中以创建该组件的数据感知版本。它们还展示了利用前几表中列出的方法、属性和事件的正确方式。

### 设置 TFieldDataLink

创建数据感知组件的第一步是向组件添加一个类型为 TFieldDataLink 的私有字段。

接下来，重写 Create 和 Destroy 构造函数和析构函数。

Create 负责创建 TFieldDataLink 对象并通过 Control 属性建立与此组件的连接。请注意列表 5.3 中，Create 方法将 csReplicateable 设置添加到 ControlStyle 属性中。这通知组件它可以在 TDataGrid 中使用，如下章所述。

Create 还为 TFieldDataLink 的 OnDataChange 和 OnUpdateData 事件设置事件处理程序。如果您愿意或需要，也可以为 OnEditingChange 和 OnActiveChange 事件创建处理程序，但我在此没有这样做。

Destroy 简单地释放 TFieldDataLink 组件，然后调用继承的 Destroy 方法。

最后，您应该处理 `CM_GETDATALINK` 消息并返回内部 `TFieldDataLink` 字段的引用。CMGetDataLink 在列表 5.3 中提供了此服务。

> **注意**
> 如果您记得在“TDBComboBox”部分中，我们在编写 TETHIDComboBox 和 TETHListBox 组件时利用了 CM_GETDATALINK 消息。如果 TDBComboBox 和 TDBListBox 的作者没有提供 CM_GETDATALINK 消息处理程序，我们将没有办法获取组件内部 `TFieldDataLink` 的引用。

### 设置与数据源的连接

您将采取的下一步是创建 DataSource 和 DataField 属性。这些属性只是调用 `GetDataSource/SetDataSource` 和 `GetDataField/SetDataField`。对于大多数数据感知组件，您可以直接复制列表 5.3 中展示的这些方法的代码。

此外，您应该提供一个重写的 **Notification** 方法，该方法在关联组件被释放时调用。对于大多数数据感知组件，我们希望如果在设计时用户从窗体或数据模块中移除了关联的 TDataSource 组件，我们能收到通知。如果发生这种情况，数据源的引用不再有效，因此我们将 DataSource 属性设置为 nil。

### 响应数据集的变化

此时，您应该创建一个 `DataChange` 事件处理程序。DataChange 执行更新数据感知组件的任务，使其反映关联数据字段的当前状态。在本文给出的示例中，DataChange 将组件的 Date 属性设置为关联字段的值。如果没有关联字段，组件显示今天的日期。

接下来，您应该提供 Loaded 事件的重写实现。Loaded  simply 在组件处于设计模式时调用 DataChange 事件。在运行时，DataChange 自动被调用。

### 更新数据集

现在组件能够在底层数据变化时正确更新自身，我们需要编写在组件变化时更新数据的代码。为此，我们需要编写 UpdateData 事件处理程序。

在许多情况下，`UpdateData` 包含一行代码，它从数据感知组件获取当前值并将其写入数据字段（如列表 5.3 所示）。

您还需要为数据感知组件编写一个或多个事件处理程序，当组件的值发生变化时触发。在许多情况下，这包括一个 `Change` 事件处理程序。在某些情况下，它需要一个 `Click` 处理程序代替（或除了）`Change` 事件处理程序。您应该熟悉您正在处理的组件，以便知道哪些事件可能会因组件值的变化而触发。

在这种情况下，我重写了 `TDateTimePicker` 的 `Click` 和 `Change` 动态方法，以添加对数据链接的 `Edit` 和 `Modified` 方法的调用。逻辑是这样的：首先，调用 `Edit` 尝试将底层数据集置于编辑模式。接下来，调用组件的继承方法。最后，调用 `Modified` 让数据链接知道字段已更改。

### 消息处理程序

通常，当焦点离开组件时，数据感知组件会更新数据集。为了实现这一点，我们必须以列表 5.3 中所示的 `CMExit` 方法的形式为 `CM_EXIT` 消息提供消息处理程序。

`CMExit` 方法尝试更新数据集。如果因任何原因失败，焦点将设置回组件，并且异常再次被抛出。通常，您可以将此消息处理程序的代码原封不动地复制到您自己的数据感知组件中。

### 动作处理程序

您应该在数据感知组件中提供的最后两个方法是 `ExecuteAction` 和 `UpdateAction` 的重写。这些重写方法确保组件与 Delphi 提供的标准 `DataSet` 动作正确配合工作。同样，您可以将此组件中的代码原封不动地复制到您自己的数据感知组件中。

### 数据感知 TDateTimePicker

列表 5.3 包含 `TETHDBDateTimePicker`（`TDateTimePicker` 的数据感知后代）的完整源代码。

**列表 5.3 ETHDBDateTimePicker.pas**

```pascal
unit ETHDBDateTimePicker;

interface

uses
Windows, Messages, SysUtils, Classes, Controls, ComCtrls, DB, DBCtrls;
```
