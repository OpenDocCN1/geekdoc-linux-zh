
组件被放置在名为“包”的共享对象中。由于包对于 Kylix 开发至关重要，我将在本章的很大篇幅讨论它们。事实上，包是本章的主题。与包的主题密切相关的是如何在 Kylix 中构建共享对象。本章的最后将包含关于该主题的简要介绍。

你在本章中所学习的内容取决于你对 Pascal 对象模型的了解。对于想要深入开发的开发者来说，理解面向对象编程（OOP）是至关重要的。

对于此类项目，最好的方法是从一个简单的示例开始，逐渐过渡到包含更多对象的示例。在列表 8.1 中，你将找到第一个版本的单元代码，它最终包含了 `TEdit`、`TPanel` 和 `TLabel` 控件的派类，以及许多其他控件。浏览一遍代码，检查其基本结构，然后阅读我关于如何使用该组件将其组装起来的简要讨论。列表 8.2 包含了测试该单元的程序源码。

## 列表 8.1 继承自 TEdit 的简单组件代码；此代码位于单元目录下的 ElvesControlA.pas

```pascal
/////////////////////////////////////////////////////////////////
// Purpose: 创建组件的第一个示例
// Project: Elves.dpk
// Copyright 2001! by Charlie Calvert
//
unit ElvesControlA;

interface

uses
  Classes, QGraphics, QControls, QStdCtrls;

type
TSmallEditA = class(TEdit)
private
  { 私有声明 }
protected
  { 保护性声明 }
public
  { 公有声明 }
  constructor Create(AOwner: TComponent); override;
public
  { 发布的声明 }
end;

procedure Register;

implementation

constructor TSmallEditA.Create(AOwner: TComponent);
begin
```

### 列表 8.1 继续

```pascal
inherited Create(AOwner);
Color := cBlue;
Font.Color := cYellow;
Font.Name := 'Times New Roman'
Font.Size := 12;
Font.Style := [fsBold];
```

```pascal
procedure Register;
begin
  RegisterComponents('Elves', [TSmallEditA]);
end;
end.
```

## 列表 8.2 TestElvesA.dpr 程序的主表窗，作为 ElfControls 单元的测试平台

```pascal
///////////////////////////////////////////////////////
// Purpose: 测试SmallEditA 控件
// Project: TestElvesA.dpr
// Copyright: 2001 by Charlie Calvert
//
unit Main;

interface

uses SysUtils, Classes, QGraphics,
QControls, QForms, QDialogs,
StdCtrls;

type
Form1 = class(TForm)
  RunTestBtn: TButton;
  procedure RunTestBtnClick(Sender: TObject);
  procedure FormResize(Sender: TObject);
end;

var
Form1: TForm;

implementation
```

### 列表 8.2 继续

```pascal
uses
  ElfControlsA;

{SR *.xfm}

procedure TForm1.RunTestBtnClick(Sender: TObject)
var
  MyEdit: TSmallEditA;
begin
  MyEdit := TSmallEditA.Create(Self);
  MyEdit.Parent := Self;
  MyEdit.Show;
end;

---
这段代码现在可以用 Anchors 属性替换。
---

procedure TForm1.FormResize(Sender: TObject)
begin
  RunTestBtn.Left := 5;
  RunTestBtn.Top := Height - (RunTestBtn.Height + 10);
end;
```

创建此单元、测试它并将其编译为与组件调面板（Component Palette）与其他工具合并的组件是非常简单的。要开始操作，选择 `File`（文件）、`New`（新建）并创建一个应用程序。从对象库（Object Repository）的第一页选择 `File`（文件）、`Component`（组件）。这样做会导致图 8.1 所示的对话框出现。

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_407_0.png)

图 8.1

新组件对话框。

组件向导是一个集成到 IDE 中的简单代码生成器，使用了 Tools API。生成器首先询问你想要创建的组件名称。然后要求你从下拉列表中选择组件的父类。在你定义了想要创建的组件类型后，可以选择组件调面板中你希望它所属的页面。为了延续我的第一个示例，你应该用以下信息填充空白：

类名（Class Name）：`TElSmallEdit`

祖先（Ancestor）：`TEdit`

调面板页面（Palette Page）：`Elvis`

为了回报你的努力，组件向导生成了列表 8.3 中的代码，其中除了类声明的第一行、全局变量声明以及传递给 `RegisterComponents` 方法的参数外，一切都是样板代码。

## 列表 8.3 组件向导的标准样板输出

```pascal
unit Unit2;

interface

uses
  SysUtils, Types, Classes,
Graphics, Controls, QForms,
Dialogs, QStdCtrls;

TElSmallEdit = class(TEdit)
private
  { 私有声明 }
protected
  { 保护性声明 }
public
  { 公有声明 }
published
  { 发布的声明 }
end;

procedure Register;

implementation
```

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_408_0.png)

### 列表 8.3 继续

```pascal
procedure Register;
begin
  RegisterComponents('Elves', [TElSmallEdit]);
end;

end.
```

组件向导首先给你一个 `uses` 子句，包含

```pascal
uses
SysUtils, Types, Classes,
Graphics, Controls, QForms,
Dialogs, QStdCtrls;
```

对象的许多功能都定义在它所继承的类中。例如，`TEdit` 控件从 `TEdit` 控件开发了许多功能，然而源代码随大多数 Kylix 版本一起提供。下一步是提供基础类声明，你在指定的

```pascal
type
TElSmallEdit = class(TEdit)
private
  { 私有声明 }
protected
  { 保护性声明 }
public
  { 公有声明 }
published
  { 发布的声明 }
end;
```

## 双向工具

Borland 将 Kylix 称为双向工具。双向工具允许你通过视觉或手动方式进行编辑。换句话说，你可以找到 CLX 的源代码是可以用的，而且它们都是用 Object Pascal 编写的。双向工具非常重要，因为这意味着没有对你隐藏的内容，没有存储的秘密。这一概念适用于 Kylix 的所有方面。

这里没有什么大秘密。据我所知，CLX 的源代码都是可用的，而且它们都是用 Object Pascal 编写的。例如，Kylix 组件技术的源码是免费提供的。不是用 Object Pascal 编写的部分，即 Qt 库，仍然从 `www.trolltech.com` 免费获取。

出于某种原因，我未能找到围绕 Qt API 的 C 封装源码。我不知道为什么这些代码没有被提供，原因可能涉及 Borland 与 TrollTech 之间的合同。如果还有其他缺失部分，在我看来它们可能非常晦涩，并且并不重要。然而，该文件的最新二进制版本可以在 SourceForge 上作为 `libqtintf` 获取。

在将组件放置到组件调面板之前，你必须先向系统注册它：

```pascal
procedure Register;
begin
  RegisterComponents('Elves', [TElSmallEdit]);
end;
```
