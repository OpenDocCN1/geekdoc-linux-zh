
Visual Basic .NET 将 `Date` 类型存储为 64 位整数，这提高了操作的执行速度。但新的存储日期方法破坏了将 `Date` 变量作为 `Double` 数据类型工作的兼容性。.NET Framework 提供了 `ToOADate` 和 `FromOADate` 方法来将日期在 `Double` 变量类型之间进行转换。

### Integer and Long

在 Visual Basic 6 中，数值数据类型 `Integer` 存储 16 位值，而 `Long` 类型存储 32 位值。为了提供对更大数字的支持，VB.NET 将 `Integer` 表示为 32 位值，`Long` 表示为 64 位值。一种新的变量类型 `Short` 表示 16 位值。

### Fixed-Length Strings

在 Visual Basic 6 中，你可以通过指定 `String` 类型后跟乘号 `*` 和长度来声明变量为定长字符串。

Visual Basic .NET 的通用语言运行时 `CLR` 不支持定长字符串。一个兼容性类使你能够创建定长字符串。你调用兼容性类 `FixedLengthString`，你可以在 `Visual Basic.Compatibility` 命名空间中找到它。

### Currency

在 Visual Basic 6 中，`Currency` 数据类型以整数格式存储 64 位数字，但在值的第四个位置插入小数点。此外在 VB 6 中，虽然你不能声明 `Decimal` 类型的变量，但 `Variant` 类型支持 `Decimal` 类型，它存储具有移动小数点的 96 位整数值。

Visual Basic .NET 放弃 `Currency` 类型而只使用 `Decimal` 数据类型。`Decimal` 提供更高的精度，并且 `CLR` 直接支持 `Decimal`。

### Type

VB 6 中的 `Type` 语句声明用户定义类型。

Visual Basic .NET 不支持 `Type` 语句；相反，你使用 `Structure` 语句。你可以在第 7 章了解结构。

### Empty

Visual Basic 6 中的 `Variant` 初始化为 `Empty`，当你在数值表达式中使用它们时会自动转换为零，或当你在字符串表达式中使用它们时转换为空字符串。

Visual Basic .NET 将 `Object` 变量初始化为 `Nothing`，如果必要，它也会自动转换为零或空字符串。

### Null and Null Propagation

在 Visual Basic 6 中，`Null` 值是 `Variant` 变量的子类型，表示变量不包含有效数据。此外，在 VB 6 中，如果表达式的任何部分求值为 `Null`，`Null` 值会“传播”通过表达式，整个表达式变为 `Null`。

Visual Basic .NET 不支持 `Null` 传播，并且仅将 `Null` 变量作为 `ADO.NET` 的变量类型支持。`CLR` 将包含 `Null` 值的 `Variant` 转换为变量类型 `DBNull`。你可以使用 `IsDBNull` 函数来测试类型。不再在涉及字符串数据的表达式中，`Object` 返回 `Null`，而是返回空字符串值。

### Local Variable Scope

在 Visual Basic 6 中，你可以从包含声明的行使用变量一直到过程结束。

Visual Basic .NET 对变量使用块作用域。这意味着你可以从包含声明的行访问局部变量，直到它出现的块结束。因此，如果你在 `Do Loop` 块内声明一个变量，你在循环结束时无法访问该变量。

### Arrays

VB 6 允许你定义具有任意下界和上界的数组。你可以使用 `Option Base` 语句在 VB 6 中定义默认下界。

在 VB .NET 中，所有数组都是零基的；这意味着数组的第一个索引始终为零。你不能设置数组的下界。有关声明和使用数组的更多信息，请参阅第 4 章。

### ReDim

Visual Basic 6.0 在固定大小和动态数组之间区分。你使用 `Dim` 语句声明固定大小数组；你使用无界的 `Dim` 定义动态数组，然后用 `ReDim` 调整数组大小。

在 Visual Basic .NET 中，所有数组都是动态的，这意味着你始终使用 `Dim` 声明初始数组大小，并且可以稍后更改数组的大小。这可能导致升级后的 VB 6 代码冗余地初始化数组两次。

### Assignment

在 Visual Basic 6 中，`Set` 语句将对象引用分配给变量名。在 VB .NET 中，因为所有变量都是对象，语言仅支持一种形式的赋值，即等号。

### Calling Procedures

VB 6 提供两种过程调用形式：使用 `Call` 语句，要求你将参数括在括号中，以及简单地键入过程名称而不使用括号。

Visual Basic .NET 要求两种方法都使用括号以提高一致性。此外，默认参数传递方法从 VB 6 中的 `ByRef` 更改为 Visual Basic .NET 中的 `ByVal`。这可能导致细微的错误，因此在升级时请确保在必要的地方重新添加 `ByRef` 关键字。

## 使用升级向导

您可以使用项目升级向导将 Visual Basic 6.0 项目自动转换为完全原生的 Visual Basic .NET 应用程序。由于 VB .NET 在核心语言上做了大量更改，Microsoft 提供了一个升级向导来协助应用程序的移植。

要调用升级向导，请使用标准的打开项目对话框打开一个 Visual Basic 6 项目。升级向导接收一个项目，创建一个新的 .NET 项目目录，并将项目中存在的所有文件转换为支持 Visual Basic .NET 的新文件。向导不会以任何方式更改或覆盖现有文件。

升级向导包含五个步骤。第一步提供向导完成的动作摘要。第二步检查 Visual Basic 6 项目的项目类型并尝试在 .NET Framework 中提供匹配。两个选项为 `EXE` 和 `DLL`/自定义控件库。

向导应自动确定适当的类型。向导还提供一个复选框，如果您想为公共类生成默认接口。 如果您的项目提供了许多公共 COM 对象，您应该选择此框。然后您可以选择创建新的 VB .NET 项目的目录并执行转换。

转换完成后，VB .NET 项目打开。升级向导创建一个名为 `UpgradeReport.htm` 的文件，其中包含项目中各个模块的升级问题。此报告会提醒您代码中无法转换或需要特别注意的部分。请参阅上一节“Visual Basic 6 的语言更改”，以获取从 Visual Basic 6 转换为 Visual Basic .NET 时发生的重大更改列表。在大多数情况下，您的项目在转换后可以运行，您可以测试功能以查看转换过程中是否出现任何问题。

![](img/d6f772854306e15fb6df39b861a7b541_31_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_31_1.png)

- 1. 打开一个 VB 6 项目文件。Visual Basic 升级向导出现。
- 2. 单击下一步跳过向导的第一屏。
- 3. 验证向导在第 2 步中选择了适当的应用程序类型。
- 4. 单击下一步。

### 额外

为了提供兼容性函数，.NET Framework 在使用升级向导时包含 `Microsoft.VisualBasic.Compatibility` 命名空间。此命名空间包含存在于 Visual Basic 6 语言中的函数。.NET Framework 复制了 Visual Basic 6 中内置的大部分函数，使得语言中的许多函数变得不必要。为了使升级过程尽可能简单，这些函数提供与 VB 6 函数相同的接口，同时仍符合 .NET 受管代码。例如，VB .NET 不包括创建控件数组的能力。因此，为了使 VB 6 项目成功升级，兼容性库为语言中的每个基本控件包含控件数组。VB .NET 还完全移除了 `FileListBox` 和 `DriveListBox` 等控件。兼容性库为升级后的项目提供这些控件。许多已移除的函数如 `SendKeys` 也存在于此命名空间中。

您可以使用 Visual Basic 6 继续维护现有应用程序而不是升级。Visual Basic 6 和 Visual Basic .NET 可以共存于单个系统上。如果您维护一个在 VB 6 中运行良好的非常大的产品，您可能希望将应用程序保留在 VB 6 中。您可能会发现升级过程很困难，因为语言中存在大量根本性更改。

![](img/d6f772854306e15fb6df39b861a7b541_32_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_32_1.png)

您可以单击浏览以更改升级项目的目录。

5 单击下一步。

步骤 4 出现并通知您向导已收集所有必要信息。

6 在向导的步骤 4 上单击下一步。

向导处理项目。

向导打开新项目。

在解决方案资源管理器中双击 `UpgradeReport.htm` 文件以查看错误。

## 创建项目
