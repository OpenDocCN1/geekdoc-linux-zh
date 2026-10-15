

## Extra

UserControl 还包含若干从 ContainerControl 类继承的默认属性，该类允许控件在其内部包含其他控件。ContainerControl 继承自 ScrollableControl，而 ScrollableControl 继承自 Control，以提供 Windows Forms 层次结构中所有部分的基本功能。诸如 BackColor、ForeColor、Tag、Enabled 和 AutoScroll 之类的属性会自动通过 UserControl 所继承的各个类应用到你的用户控件中。有关如何处理和重写这些内置属性的更多信息，请参阅“Handle Default Properties”部分。

与 Visual Basic 不同，你无法创建用户可将其用作容器的 UserControl。在开发 UserControl 时，你可以添加任何必要的属性。用户无法向 UserControl 添加控件，因此你无法复制 GroupBox 或 Panel 控件的功能。你可能希望直接创建这些容器控件的自己的版本，而不是构建一个 UserControl。要继承现有控件，请在 Visual Basic 帮助中搜索，输入 Inherit from existing Windows Forms Controls。

![](img/d6f772854306e15fb6df39b861a7b541_296_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_296_1.png)

- 5. 新控件的视觉设计器出现。
- 
- 6. 向视觉设计器添加任何必要的控件。

注意：请参阅“Using Standard Controls”部分以将控件添加到 UserControl。

- 6. 在代码编辑器中，向控件添加必要的成员。

注意：请参阅“Add a Member”部分以向控件添加类成员。

- 7. 单击 Build -> Build 使控件或库可用。
- 
- 8. 如果控件存在于控件项目中，你现在可以引用该库。如果你在 Windows 应用程序中创建了控件，请转到窗体并将其添加到窗体中。

注意：要引用 Control Library 项目，请参阅“Reference a Library”部分。

## Extra

与属性一样，你可以重写 User Control 类的方法和事件。例如，控件提供一个 Click 事件，每当用户单击 UserControl 的一部分且该部分不包含构成控件时就会触发。你可能不希望包含应用程序为代码中的空白区域的单击提供代码。你可以重写 OnClick 方法以防止此事件到达父控件。

### Example:

```
Protected Overrides Sub OnClick(ByVal e As System.EventArgs)
' do nothing... hide the event from the parent.
End Sub
```

你也可以使用 OnEvent，其中 Event 是特定事件的名称，来修改某些信息，并按通常方式传递事件。由于事件存在于 Control 类中，你无法正常引发它们。相反，你必须使用 Shadows 关键字在 UserControl 类中再次定义事件。

### Example:

```
Public Shadows Event Click(ByVal sender As Object, ByVal e As System.EventArgs)
Protected Overrides Sub OnClick(ByVal e As System.EventArgs)
' perform necessary preprocessing
...
' raise the normal event
RaiseEvent Click(Me, e)
End Sub
```

![](img/d6f772854306e15fb6df39b861a7b541_298_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_298_1.png)

- 7 要重写属性或事件功能，请从组件列表中选择 (Overrides)。
- 8 选择要重写的属性或方法。

- 9 添加代码以提供属性或方法的新的功能。
- 示例重写了背景颜色并使用所选颜色绘制渐变。
- 10 单击 Build -> Build 构建项目。

当你将控件添加到窗体并尝试修改属性时，适当的代码会监视或重写该功能。

如果使用控件库，你必须引用控件库。
注意：要引用控件库，请参阅 "Reference a Library." 部分。

## ADD A MEMBER

你可以在用户控件中提供属性和方法，使其与容器交互以自定义控件的外观和功能。类似于 Button 控件的 Text 属性，该属性设置按钮上显示的标题，你可以创建修改控件外观和功能的属性。你还可以添加自定义方法，允许容器发送命令并指定控件的操作。

要向用户控件添加属性，你访问代码编辑器并将属性定义添加到定义用户控件的现有类中。你将控件的容器的属性定义为 Public，以便容器可以访问它们。有关向类添加属性的更多信息，请参阅第 7 章。

要向用户控件添加方法，请在现有用户控件类内部定义该方法。将方法定义为 Public，以便控件的容器可以调用该方法。如果你想创建控件的继承版本，请确保必要的属性包含 Overridable 关键字。有关向类添加方法的更多信息，请参阅第 7 章。

当你构建控件并将其添加到 Form 时，你可以在属性窗口中访问你定义的属性。你也可以在代码中操作属性和方法。属性窗口确定属性的类型并使用最合适的选择系统。例如，如果你创建了类型为 Color 的属性，属性窗口会自动为你的属性提供颜色选择下拉列表。如果你有一个类型为 Size 或 Point 的属性，设计器会将对象的属性显示为你的属性的子部分。

![](img/d6f772854306e15fb6df39b861a7b541_299_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_299_1.png)

## ADD A PROPERTY

- 1. 打开现有的用户控件，双击用户控件的表面以进入代码编辑器。
- 2. 定义私有成员变量。
- 3. 在类的空行上，键入 Public Property 后跟属性的名称。
- 4. 按 Enter。
- 5. 在属性内部键入代码以设置和检索属性指定的值。
- 6. 单击 Build 构建控件。

注意：要使用私有成员变量，请参阅第 7 章。

注意：要向类添加属性，请参阅第 7 章。

你现在可以将 UserControl 添加到窗体并访问控件的属性。

