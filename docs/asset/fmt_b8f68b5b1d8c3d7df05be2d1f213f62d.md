
# 选项列表控件

选项列表控件仅在 Web 窗体中可用，它们允许你提供一个由多个复选框或单选按钮组成的列表，这些复选框或单选按钮充当一个控件。你还可以向页面添加单个 `CheckBox` 和 `RadioButton` 控件并与之交互。单独使用这些控件可以控制每个项的布局和外观，应用不同的字体和颜色。使用两个选项列表可以轻松创建选项序列，并且可以绑定到数据库以自动提供选择列表。有关 `CheckBox` 和 `RadioButton` 控件的更多信息，请参阅“添加选项控件”一节；“将字段绑定到列表控件”一节演示了如何将控件绑定到数据库。

已列出。你可以使用这些列表在窗体上生成选择菜单，同时简化页面。要提供这些列表，请编辑 `Items` 集合。通过“列表项集合编辑器”，可以使用 `Name` 属性为每个项指定标题，并为每个项分配一个 `Value`，以区分各项。如果未设置 `Value` 属性，控件会将 `Name` 中的文本分配给 `Value` 属性。

`SelectedIndexChanged` 事件允许你处理选择。它是一个非回发事件，会存储下来，并在用户调用需要服务器连接的事件（例如单击按钮）时触发。有关事件的更多信息，请参阅“Web 窗体简介”一节。对于 `RadioButtonList`，请使用 `SelectedItem` 或 `SelectedIndex` 属性访问所选的单个项。对于 `CheckBoxList`，请使用 `For Each` 循环遍历 `Items` 集合，检查每个项的 `Selected` 属性以判断用户是否选择了该项。

`CheckBoxList` 和 `RadioButtonList` 控件分别创建一系列 `CheckBox` 或 `RadioButton` 控件。对于每个 `RadioButtonList`，用户只能选择列出的控件之一；对于每个 `CheckBoxList`，用户可以选择任意数量的项。

![](img/d6f772854306e15fb6df39b861a7b541_257_0.png)

- 1 创建 Web 应用程序项目，或打开一个现有项目。
- 2 单击 `CheckBoxList` 或 `RadioButtonList` 控件。
- 3 将该控件添加到窗体。
- 注意：请参阅“创建 Web 应用程序”创建 Web 应用程序项目，并参阅“使用 Web 窗体”将控件添加到 Web 窗体。
- 4 在控件的“属性”窗口中，单击 `Items` 属性。
- 5 单击 ...

## 额外内容

除了标准字体和颜色更改之外，你还可以使用两个选项控件都提供的一组属性来更改其默认外观。默认情况下，`CheckBoxList` 和 `RadioButtonList` 控件都会从上到下列出 `Items` 集合中包含的选项。你可以将 `RepeatDirection` 属性从 `Vertical` 改为 `Horizontal`，使项列表从左到右排列，而不是从上到下。你可以设置 `RepeatColumns`，让列表控件将项拆分成多列。值为 0 或 1 时，控件显示一列；值为 2 时显示两列，依此类推。

通常，选项列表控件在项更改后不会立即触发事件。它们会一直等到控件向服务器回发时才触发事件。你可以更改此默认行为，使选项列表控件向服务器回发并立即触发 `SelectedIndexChanged` 事件。将 `AutoPostBack` 属性设置为 `True` 即可实现此行为。这需要用户的 Web 浏览器重新加载页面，因此，除非与 Web 服务器建立直接网络连接，否则会导致性能问题。

![](img/d6f772854306e15fb6df39b861a7b541_258_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_258_1.png)

出现“列表项集合编辑器”。

- 6 单击“添加”。
- 7 为该项键入 `Text` 和 `Value` 属性。
如果需要，可以设置 `Selected = True`。
- 8 根据需要重复步骤 6 至 7。
- 9 单击“确定”。
- 10 按 `F5` 运行项目。

`CheckBoxList` 或 `RadioButtonList` 允许选择它包含的项。

# 使用验证控件

验证控件使您能够检查用户输入的数据值，以确保这些值是有意义的。验证控件会自动生成客户端脚本以提供此验证。

Web 表单提供了许多验证控件。`RequiredFieldValidator` 确保用户在输入控件（如文本框）中完成输入。`RangeValidator` 检查用户的输入是否落在有效的值范围内。`CompareValidator` 检查一个控件中的用户输入与另一个控件中的输入或与字符串值进行比较。有关正则表达式验证的信息，请参阅“使用正则表达式验证”部分。要创建验证错误列表，请参阅“提供验证摘要”部分。

验证控件绑定到表单上您指定的单个输入控件，使用 `ControlToValidate` 属性指定。`ErrorMessage` 属性在验证失败时出现在验证控件中。`Display` 属性控制控件如何显示错误。如果将 `Display` 设置为 `Static`，控件会在表单上使用空间，但在出现错误之前保持空白。使用 `Dynamic` 设置时，控件在出现错误之前不使用空间，然后变得可见。如果将页面布局设置为 `Flow`，这将移动页面上的元素以腾出空间供验证控件使用。`EnableClientScript` 属性启用使用 JavaScript 在客户端执行验证。否则，控件将使用往返服务器的方式执行验证。

对于 `CompareValidator` 控件，您设置 `ControlToCompare` 属性或 `ValueToCompare` 属性以与要比较的文本进行比较。`Operator` 属性指定比较方式。`Type` 属性指定比较时使用的变量类型。

对于 `RangeValidator` 控件，将 `MinimumValue` 和 `MaximumValue` 属性设置为可接受输入的下限和上限。使用 `Type` 指定比较的变量类型。

![](img/d6f772854306e15fb6df39b861a7b541_259_0.png)

- 1 创建一个新的 Web 应用程序项目或打开一个现有项目。
- 2 向表单添加必要的输入控件并向表单添加验证控件。
- 3 在属性窗口中，单击 `ControlToValidate` 并单击适当的输入控件。
- 4 在 `ErrorMessage` 属性中输入错误消息。
- 5 对于 `CompareValidator`，单击 `ControlToCompare` 并选择一个控件，或为 `ValueToCompare` 属性输入一个值。
- 如有必要，单击 `Operator` 和 `Type` 以选择一个值。

注意：请参阅“创建 Web 应用程序”部分以创建新项目，并参阅“使用 Web 表单”以添加控件。

### 额外

除了 `RequiredFieldValidator` 控件之外，每个验证控件都接受空白输入而不会导致验证器错误。在您验证的输入控件中，您可能希望使用 `RangeValidator` 或 `RegularExpressionValidator` 控件进行测试，但不希望用户将输入控件留空。例如，`RangeValidator` 控件即使验证范围为 10 到 100 也接受空白值。您可以要求用户为输入控件提供条目，然后通过添加 `RequiredFieldValidator` 以及 `RangeValidator`、`RegularExpressionValidator` 或其他验证控件来验证条目。然后，您在每个验证控件的 `ControlToValidate` 属性中指定相同的输入控件。您可以使用两个验证控件各自的 `ErrorMessage` 属性为每个验证控件适当自定义错误消息。为了节省使用两个不同验证控件关联到单个控件的空间，您可以添加验证摘要控件。有关 `ValidationSummary` 控件的更多信息，请参阅“提供验证摘要”部分。

![](img/d6f772854306e15fb6df39b861a7b541_260_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_260_1.png)

- 6 对于 `RangeValidator` 控件，设置 `MinimumValue` 和 `MaximumValue` 属性。
- 如有必要，单击 `Type` 并选择一个值。
- 根据需要重复步骤 2 到 6。
- 7 按 `F5` 运行您的项目。

验证控件会适当地验证输入控件中的数据。

# 使用正则表达式验证

一种对字符串进行复杂条件集测试的方法，正则表达式指定字符串必须遵循的格式。您可以在 Web 窗体上使用 `RegularExpressionValidator` 控件，利用正则表达式来验证复杂的输入数据，例如电话号码、社会安全号码，或其他遵循标准格式的字符串。要设置验证控件，您将 `ControlToValidate` 属性设置为有效的输入控件，并使用 `ErrorMessage` 属性指定消息。有关验证控件的标准属性的更多信息，请参阅“使用验证控件”部分。
