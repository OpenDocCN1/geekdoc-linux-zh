
- 此示例向组件添加了一个存储字符串的属性以及一个操纵字符串的方法。

注意：第 7 章添加属性和事件。第 4 章添加方法。

- 双击设计区域。
- 打开代码编辑器。
- 向组件添加任何属性、方法和事件。
- 编译。
- Visual .NET 使用该库。
- 你可以通过在另一个应用程序中引用它并将组件添加到工具箱中来使用你的组件。

注意：第 1 章构建项目，以及“引用库”部分引用库。

# VISUAL BASIC .NET

## 创建 WINDOWS FORMS 控件

你可以创建一个 Windows Forms 控件，在其中你可以创建一组控件供整个项目复用。此外，你可以将控件放置在库中以便在多个项目中使用。`UserControl` 对象提供了设计你自己的控件及其事件模型的能力。有关在不使用标准控件的情况下创建控件的更多信息，请参见“从头开始创建控件”部分。

当你将控件添加到项目时，Windows Forms 设计器（与 Windows Forms 设计器类似）会为你提供一个没有标题栏的空间。你可以在工具栏上添加任意数量的控件。有关通过组合标准控件设计用户控件的更多信息，请参见“使用标准控件”部分。

要为控件命名，请更改 `UserControl` 对象的 `Name` 属性。`Name` 属性会修改类名，因此该函数将成为将控件添加到项目时显示在工具箱中的控件的默认名称。

你还可以使用控件继承自 `UserControl` 的事件来创建不依赖于其他控件的自定义用户控件。这允许你通过自定义绘制方法和你创建任何一组控件。

如果你想使用一个控件或一组控件，可以创建一个 Windows 控件库来存放这些控件。当你创建此项目时，.NET 会构建一个符合 .NET 标准的 DLI，你可以在其他项目中引用它。要创建 Windows 控件库项目，请选择“新建项目”对话框，输入你给项目的名称，该名称将作为程序集的名称。模板会自动提供一个 `UserControl`，但你可以向项目添加任意数量的控件。

### 创建 WINDOWS FORMS 控件

![](img/6e977c6eee8c1535039c864d41da5ccf_295_0.png)

- 打开控件库或 Windows 项目。
- 要创建控件库项目，在创建项目时选择 Windows 控件库模板。
- 2 如果你正在使用 Windows 应用程序项目，点击“添加控件”。
- 控件库项目已包含一个你可以使用的 `UserControl`。
- 3 打开“新建项”对话框。
- 4 为你的新控件输入一个名称。

![](img/6e977c6eee8c1535039c864d41da5ccf_295_1.png)

## 附加

与属性一样，你也可以重写 `UserControl` 类的方法和事件。例如，该控件提供了一个 `Click` 事件，每当用户点击 `UserControl` 中不包含子控件的区域时，该事件就会触发。你可能不希望应用程序为点击控件空白区域提供代码。你可以重写 `OnClick` 方法来防止此事件传递到父控件。

```text
Example:

Protected Sub OnClick(ByVal e As System.EventArgs)

    do... hide the event from the parent.
```

你还可以使用 `OnEvent`（其中 `OnEvent` 是特定事件的名称）来修改其内容并像往一样传递事件。由于事件存在于 `Control` 类中，你无法正常地抛出它们。相反，你必须使用 `Shadows` 关键字在你的 `UserControl` 类中定义该事件。

```text
Example:

Public Shadows Event Click(ByVal sender As Object, ByVal e As System.EventArgs)
```

```text
    raise raise the normal event

    RaiseEvent(Me.Click)
```

![](img/6e977c6eee8c1535039c864d41da5ccf_298_0.png)

![](img/6e977c6eee8c1535039c864d41da5ccf_298_1.png)

- 若要重写属性或事件功能，请从组件列表中选择 (`Overrides`)。
- 选择要重写的属性或方法。
- 添加代码以为该属性或方法构建新功能。
- 示例显示了背景颜色并使用生成项目绘制了渐变。
- 点击“生成”来生成项目。

如果你使用了控件库，必须引用该控件库。适当的代码将监控或重写该函数。

注意：要引用控件库请参“引用库”章节。

## 添加成员

你可以在用户控件中创建属性和方法，通过它们与容器的交互来自定义控件的外观和功能。类似于 `Button` 控件的 `Text` 属性（该属性设置按钮上的标题），你可以创建属性来更改控件的外观和功能。你还可以添加自定义方法，允许控件发送命令并指定控件的操作。

要向你的用户控件添加内容，请访问代码编辑器并在现有类中添加属性定义。你将控件的属性定义为 `Public`，有关向类中添加属性的get，请参阅第 7 章。

要向你的用户控件添加内容，请在用户控件类内部定义该方法。将方法定义为 `Public` 以允许控件调用该方法。如果你想创建控件的继承版本，请确保必要的属性包含 `Overable` 关键字。有关向类中添加方法的更多信息，请参阅第 7 章。

当你生成并将其添加到表单（`Form`）时，你可以在窗口中访问你定义的属性。你可以同时操作属性和方法。“属性”窗口决定了你所使用的属性类型。例如，如果你创建一个 `Color` 类型的属性，“属性”窗口会自动为你的属性提供颜色选择下拉列表。如果你有一个 `Size` 或 `Point` 类型的属性，设计器会将对象的属性作为你属性的子部分显示。

![](img/6e977c6eee8c1535039c864d41da5ccf_299_0.png)

### 添加成员

```text
Ch12:AddMember - Microsoft Visual Basic .NET (Design) - UserControl.vb

...

Start Page | UserControl | Debug

Ch12:AddMember

Public Class UserControl

    Inherits System.Windows.Forms.UserControl

    Windows Form Designer generated code

    Private Sub UserControl_Load(ByVal sender As System.Object, e As EventArgs)

 Sub

    Private MyValue As Integer = 10

    Public Property MyValue() As Integer Get

End Class
```

![](img/6e977c6eee8c1535039c864d41da5ccf_299_1.png)

## 添加属性

1. 打开现有的用户控件，双击控件表面进入代码编辑器。
2. 定义一个私有成员。

注意：变量请使用私有成员，请参阅第 7 章。

3. 在类的空行上，定义属性定义。
4. 使用属性名让控件访问该值。
5. 添加代码以为该属性构建新功能。
6. 点击“生成”来生成项目。

![](img/6e977c6eee8c1535039c864d41da5ccf_299_2.png)

## 开发组件

## 附加

你可以重写 `UserControl` 类的方法和事件。例如，控件提供了一个 `Click` 事件，每当用户点击 `UserControl` 中不包含子控件的区域时，该事件就会触发。你还可以使用自定义事件。

示例：

```text
Private items As New Collection(Object)

Public Property Selection()

    Get

        Return items

    End Get

    Public Sub Add(item As Object)

        items.Add(item)

    End Sub

End Property
```
