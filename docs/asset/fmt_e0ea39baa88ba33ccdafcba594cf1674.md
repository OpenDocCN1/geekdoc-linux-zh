
如前面的章节所示，`StarBasic` 宏可以执行几乎所有的 `StarOffice` 操作。`StarOffice` 的层级结构非常广泛，需要另一本书才能介绍完。幸运的是，你不需要熟悉整个层级结构就可以使用 `StarBasic`。

本章将介绍使用 `StarBasic` 进行日常工作的典型解决方案。你将学习需要的对象以及无法通过宏录制获取的一些 `StarOffice` 对象。最后，通过新学到的知识，你将学习如何编写整个应用程序。

# 介绍 Application 对象

正如你所看到的，你可以更改文本的值或颜色、在 `Calc` 格中输入公式、添加图形，并在 `StarOffice` 工具的帮助下执行任务。然而，有时你需要访问整个程序的功能或属性。这就是为什么代表 `StarOffice` 的对象出现在编程层级结构中。这个对象简单地称为 `Application`。

你可以在所示程序中使用 `Application` 对象来打开地址簿：

```vb
Sub OpenAddressBook
    Application.AddressBook()
End Sub
```

要引用对象的属性和方法，需要在...之间加上。现在查看以下程序。它显示了通过工具、选项和通用对话框中的用户数据类别访问的详细信息。所有数据存储在 `Address` 对象的属性中，由 `Application` 所有：

```vb
Sub ShowUserData
    MsgBox("当前用户是：" & chr(13) & _
        "姓名:" & Application.Address.FirstName & " " & _
        Application.Address.LastName & chr(13) & _
        "ID:" & Application.Address.ID & chr(13) & _
        "街道:" & Application.Address.Street & chr(13) & _
        "城市:" & Application.Address.City, chr(13) & _
        "邮编:" & Application.Address.ZIPCode & chr(13) & _
        "邮箱:" & Application.Address.EMail & chr(13) & _
        "电话（家庭）：" & Application.Address.PhonePrivate, & _
        48,"信息")
End Sub
```

如前面的代码所示，方法、属性和对象的所有权通过元素之间的点号（`.`）来表示。左侧的元素代表右侧元素的父级，在整个层次结构中都是如此，如下所示：

```
Application.Address.FirstName
```

```
"Address 对象的属性
```

```
"Address 对象
```

```
Application 对象
```

如果你需要反复引用属于某个对象的属性，可以使用 `With` 语句，该语句在第 38 节“理解 `StarBasic` 结构和语句”末尾有解释。

- 有关使用 `With` 语句的详细信息和示例，请参见“控制你的程序”，第 1302 页。接下来的程序产生的结果与之前的版本相同；不同的是，你使用快捷方式来引用 `Application.Address` 对象：

```
Sub ShowUserData
With Application.Address
  MsgBox("The current user is:" & chr(13) & \
  "Name: " & .FirstName & " & & .LastName & chr(13) & \
  "ID: " & .ID & chr(13) & \
  "Street: " & .Street & chr(13) & \
  "City: " & .City & chr(13) & \
  "ZIPCode: " & .ZIPCode & chr(13) & \
  "E-mail: " & .Email & chr(13) & \
  "Phone (home): " & .PhonePrivate
End
```

## 介绍集合

在 `StarOffice` 层次结构中，有若干类集合对象，例如文档（`Documents`）、表格（`Tables`）和窗口（`Windows`）。此类类别中的任何对象都可以同时打开多个实例。也就是说，所有文档都可以同时在 `StarOffice` 中打开——例如一个包含多个表格的电子表格或一个包含框架的网站。集合对象是对象的容器。可以将其想象为访问所有同类对象的方式（就像超市里装有相似物品的展示篮筐）。

为了实现这种访问，`StarOffice` 提供了几个集合对象，用于访问当前会话中可以的所有的所有对象。例如，`Windows(1)` 表示 `StarDesktop` 窗口，`Documents ("LetterBoss")` 表示某个特定的文档，而 `Graphics(1)` 表示文本文档中的第一个图形。

在接下来的示例中，你将学习如何操作集合。在那里，你将确切了解到什么是集合以及在哪些任务中有用。

## 第 39 节 使用 StarBasic 编程

### 引用活动对象

你使用短语 `[Untitled:1]` 访问新文档窗口。该短语代表会话开始时出现的 `Untitled1` 文档的第一个窗口（而不是随后打开的同类其他窗口）。这意味着你拥有对一个窗口对象唯一实例的访问权限。要引用 `Untitled1` 的文档对象，你需要使用集合 `Documents ("Untitled1")`。通过 `Documents`，你可以访问文档中的所有项。

如果你想创建可以在不同文档中使用的宏，如果能够访问实际打开的窗口或文档将是非常棒的。因此，`StarBasic` 提供了 `ActiveWindow` 和 `ActiveDocument` 对象。它们指向执行宏时所在的文档的实例窗口。你可以让宏录制器生成此类对象。

通过将对象赋值给对象变量来保留对对象的访问是一个好主意。这样做可以更快地访问它们的属性和方法。额外的好处是，即使使用户将焦点放在另一个窗口上，你的宏仍然可以访问特定的对象。

```
Sub WorkWithWindowsAndDocuments
Dim ActiveWindow As Object
Dim ActiveDocument As Object
ActiveWindow = ActiveWindow
ActiveDocument = ActiveDocument
...
  '在此执行你的操作
End Sub
```

`StarBasic` 还有另外两个对象称为 `Selection` 和 `ActiveCell`。它们指向被选中的对象；通常，`Selection` 是实际 `StarWriter` 文档中的文本，而 `ActiveCell` 是 `StarCalc` 表格中当前选中的单元格。但要注意，`Selection` 只指向“真实的”被选对象。`Insert("Hello")` 仅在光标位于文本文档某处时有效；如果选了图片，它将不起作用。要确认 `Selection` 引用的是什么，可以像这样请求它的类名：

```
Sub InsertHallo
If Selection.ClassName <> "Text" Then
  MsgBox("Sorry, no text selected.",16,"Error")
Else
  Selection.Insert("Hello")
EndIf
End Sub
```

### 将宏分配给事件

`StarOffice` 包含了若干事件，例如启动程序（`Start Program`）或保存文档（`Save Document`），你可以为这些事件分配宏。事件分为两大类：`StarOffice` 事件和属于特定文档或模板的事件。例如，你可以将宏分配给关闭 `StarOffice` 时触发的事件。该宏可以在关闭时对你的工作文件夹进行备份。由 `Letter AutoPilot` 生成的模板通常会在创建文档时分配宏。该宏可以规范化文档，例如通过将今天的日期放在信件的顶部。

通过将宏分配给 `StarOffice` 或文档事件，你可以完成很多方便的操作。你可以通过创建在新建文档上运行的宏来自动化你的工作。与其反复填写标准表格，这并不符合大家的想法。相反，你只需创建一个模板并保存。

## 示例：录制打印

假设你想每次打印文档时都获取详细信息。为此，你把宏分配给 `Print` 事件。要开始操作，请确保你的文档处于活动状态，然后选择“工具”、“宏”，并选择 `Document` 库。在宏对话框中，首先在“宏名称”中输入宏名称 `InsertDate`（否则将分配一个脚本名称）。然后点击“新建”按钮创建一个新模块。`StarBasic IDE` 出现。

此时，你可以用以下内容替换空子程序：
