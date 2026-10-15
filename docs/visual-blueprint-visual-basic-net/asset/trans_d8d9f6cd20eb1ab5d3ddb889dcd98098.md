

## 创建项目

一个项目包含一个单独的应用程序或组件。你必须使用一个项目来指定构成应用程序的文件，例如窗体和类。你将 VB .NET 中的项目放在解决方案中。即使解决方案只包含一个项目，也必须存在该项目。当你创建一个新项目时，VB .NET 会自动创建解决方案。

当你在开发环境中创建一个新项目时，它会提供一个对话框让你选择想要的应用程序类型。对话框左侧显示各种编程语言和其他项目类型的条目。右侧，对话框列出各个项目模板。本书主要关注 Windows 应用程序、控制台应用程序和 ASP.NET Web 应用程序这三种项目类型。Windows 应用程序使用 Windows 窗体来开发图形化 Windows 应用程序。控制台应用程序生成基于文本的 Windows 应用程序，你可以在其中尝试编程概念，而无需设置和修改 Windows 窗体控件。ASP.NET Web 应用程序生成 Web 窗体应用程序。

新建项目对话框还会询问你希望将项目存储在何处。VB .NET 将每个项目存储在其自己的文件夹中以避免命名问题。你为项目指定的名称用作 VB .NET 为项目创建的文件的名称。当你创建项目时，项目的组件会加载到解决方案资源管理器中。这是访问应用程序各部分的主要控制台。如果你创建一个 Windows 应用程序项目，你会看到一个包含单个类 Form1 的项目，它是应用程序的主窗体。控制台应用程序项目会创建一个模块文件，你可以在其中放置代码。

![](img/d6f772854306e15fb6df39b861a7b541_33_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_33_1.png)

- 打开开发环境。
  注意：有关更多信息，请参阅“使用开发工作室”。
- 单击 File > New > Project。

如果打开了起始页，你可以单击新建项目按钮。有关起始页的更多信息，请参阅“使用开发工作室”部分。

- 从项目类型中单击 Visual Basic Projects。
  新建项目对话框出现。
- 单击适当的项目模板。

## 额外

Visual Basic .NET 中的每个项目都有一个 AssemblyInfo.vb 文件，并构成一个单一的程序集，即 .NET Framework 分配给系统中单个组件的术语。你可以使用此文件定义属性和信息，编译器会将其包含在你的项目中。该文件以空模板开始，并将可为程序集定义的各种属性设置为空白值。你可以为这些属性输入标准文本信息，其中包括 AssemblyTitle、AssemblyDescription、AssemblyCompany、AssemblyProduct 等。该文件还包含一个 GUID 以使项目兼容 COM 以及项目的版本号。该文件是一个 .VB 文件，你可以通过在解决方案资源管理器中双击其名称在源代码编辑器中打开它。

### 示例：

```
Imports System.Reflection
Imports System.Runtime.InteropServices

<Assembly: AssemblyTitle("Product.NET Main Application")>
<Assembly: AssemblyDescription("Main interface of the product.")>
<Assembly: AssemblyCompany("NETCompany")>
<Assembly: AssemblyProduct("Product.NET")>
<Assembly: AssemblyCopyright("(c) NET Company 2001")>
<Assembly: AssemblyTrademark("*")>
<Assembly: CLSCompliant(True)>
<Assembly: Guid("F7DE8FF1-4F26-4D20-B60E-36D6C604C36C")>
<Assembly: AssemblyVersion("1.0.*")>
```

![](img/d6f772854306e15fb6df39b861a7b541_34_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_34_1.png)

- 为项目输入文件名。
  注意：VB.NET 使用不带扩展名的文件名来创建项目名称。
- 可选地，你可以输入新文件夹或单击浏览以更改 VB.NET 创建项目文件夹的位置。
- 单击确定。

VB.NET 创建项目并打开其默认资源。

