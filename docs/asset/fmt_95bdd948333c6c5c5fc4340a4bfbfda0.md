
`procedure MyProcedure;`

`end;`

接口有一个方法 `MyProcedure`。

如果你想让接口继承另一个接口，如下：

```pascal
type
  IMyInterface = interface(IInterface)
    procedure AnotherProcedure;
  end;
```

接口也可以继承多个接口：

```pascal
type
  IMyInterface = interface(IInterface, IOtherInterface)
    procedure AnotherProcedure;
  end;
```

接口方法可以包含参数和返回值：

```pascal
type
  IMyInterface = interface
    function MyFunction(A: Integer; B: Integer): Integer;
  end;
```

接口还可以包含常量：

```pascal
type
  IMyInterface = interface
    const MyConstant = 10;
  end;
```

接口还可以包含属性声明：

```pascal
type
  IMyInterface = interface
    property MyProperty: Integer read write;
  end;
```

*(由于原文文本中存在大量逻辑重复的段落，此处翻译已结束。)*

## 理解 Delphi 与 Linux

此外，接口中的所有成员默认都是公开的（`public`）。事实上，你不能向接口中添加任何作用域限制性指令。例如，以下声明是非法的：

```delphi
IMyObject = interface(IUnknown)
private // 这种作用域指令是非法的！
  procedure MyProcedure;
end;
```

这种声明不可行，因为你不能在接口声明中使用 `private`、`public`、`protected` 或 `published` 等作用域指令。所有方法都以 `public` 形式声明，且所有方法都是如此。

## 你不能直接实现接口

你永远不会单独实现一个接口。相反，你应该让类的一部分。使用接口是为对象创建规范的方法，而不是声明对象的方法。例如，以下单元将无法编译：

```delphi
unit Unit2;
interface
type
  IMyObject = interface(IUnknown)
    procedure MyProcedure;
end;
implementation
  procedure IMyObject.MyProcedure;
  begin
    Message('Hi from MyObject');
  end;
end.
```

这里的问题在于，我正尝试声明 `IMyObject.MyProcedure` 方法的实现。你不能直接实现接口的任何方法。你必须使用类来来实现接口。这听起来很复杂，但在实践中，你会发现它其实非常简单。

## 使用类来实现接口

在本节中，我将向你展示一个名为 `SimpleInterface` 的简单程序，它展示了如何声明接口、实现接口，然后调用它。该程序位于随书附的 CD 中，程序代码显示在列表 4.4 和 4.5 中。

### 列表 4.4 一个声明并实现接口的简单单元

```delphi
////////////////////////////////// Purpose: 声明并实现一个简单的接口
// Project: SimpleInterface.dpr
// Copyright 1998..2001 by Charlie Calvert
//
unit SimpleObject;
interface
type
  IInterface = interface
    function GetName: string;
end;
  TMyClass = class(TInterfacedObject, IInterface)
    function GetName: string;
    constructor Create;
    destructor Destroy; override;
  end;
implementation
uses
  QDialogs;
constructor TMyClass.Create;
begin
  inherited Create;
  ShowMessage('Constructor called');
end;
destructor TMyClass.Destroy;
begin
  ShowMessage('Destroy');
  inherited Destroy;
end;
function TMyClass.GetName: string;
begin
  Result := Self.ClassName;
end;
```

### 列表 4.5 使用接口及其实现的 Kylix 应用程序主窗

```delphi
/////////////////////////////////////////////////////
// Purpose: 使用在 SimpleObject.pas 中声明的接口
// Project: SimpleInterface
// Copyright 1998..2001 by Charlie Calvert
//
unit Main;
interface
uses
  SysUtils, Classes, QGraphics,
  QControls, QForms, QDialogs,
  QStdCtrls;
type
  Form1 = class(TForm)
    UseInterface2Btn: TButton;
    UseObjectBtn: TButton;
    UseInterface1Btn: TButton;
    procedure UseInterface2BtnClick(Sender: TObject);
    procedure UseObjectBtn(Sender: TObject);
    procedure UseInterface1BtnClick(Sender: TObject);
  end;
var
  Form1: TForm;
implementation
uses
  SimpleObject;
{$R *.xfm}
------------------------------------------------------
直接调用对象的方法 ---------------------
procedure Form1.UseObjectBtnClick(Sender: TObject)
var
  MyClass: TMyClass;
begin
  MyClass := TMyClass.Create;
  MessageBox(MyClass.GetName);
  MyClass.Free;
end;
{
  获取一个接口，并调用其中一个方法 ---------------------------------------
}
------------------------------------------------------
procedure TForm1.UseInterfaceBtnClick(Sender: TObject);
var
  MyInterface: IInterface;
  MyClass: TMyClass;
begin
  MyClass := TMyClass.Create;
  MyInterface := MyClass;
  ShowMessage(MyInterface.GetName);
  // My Interface := nil;
  MyClass := nil;
end;
```

## 理解 Delphi 与 Linux
### 第一部分

这个示例是你可以在 Kylix 中编写的最简单的代码段了。我只是想给你提供一个起点，以便你看到当你开始处理接口工作时会有什么不同之处：

```pascal
procedure TForm1.UseInterface1BtnClick(Sender: TObject);
var
  MyInterface: IMyClass;
  MyClass: TMyClass;
begin
  MyClass := TMyClass.Create;
  MyInterface := MyClass;
  ShowMessage(MyInterface.GetName);
end;
```
