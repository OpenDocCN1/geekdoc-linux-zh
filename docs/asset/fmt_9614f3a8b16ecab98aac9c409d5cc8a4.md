
代码探索器现在就像图 5.11 所示。你可以清楚地看到 `TForm1` 和 `TMyObject` 的所有成员，可以看到程序中的变量，但 `uses` 子句仍然隐藏。

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_256_0.png) # 图 5.11
正确设置后的代码探索器可以为你提供代码的清晰视图。

# 代码生成：编辑器和管理器中的类补全

在 `TObject` 类声明中添加几个方法：

```
TMyObject = class(TObject)

  function Avidya: Pointer;

  function FMyObject: TComponent;

  end;
```

注意，一旦输入新方法，它就会出现在代码探索器中。在 `var` 部分添加变量，并在输入代码时观察代码探索器的输出。

右键点击代码探索器并选择“属性”。显示“显示语法”（Declaration Syntax），并点击“确定”。现在代码探索器将为你显示变量类型和函数的返回值，如图 5.12 所示。

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_257_0.png) # 图 5.12 代码生成的变量类型和函数返回类型

正如你所看到的，输入类声明中的代码会自动出现在管理器中。例如，如果你在表单创建一个新的过程，你可以转向代码探索器并在那里看到声明。相反情况也是如此。在代码探索器中点击 `Form` 下方的某个部分。弹出菜单。从菜单中选择“新建”（New）。你将能够声明一个新方法或变量。确保你输入了完整的语法，包括参数、括号和最后的分号。例如，在此处：

`function Avidya: Pointer;`

现在回到编辑器查看你造了什么。代码 5.4 讲述了故事。

### 代码 5.4 此处显示的 Avidya 方法是在代码探索器内部创建的

`unit Main;`

```
interface

uses

  SysUtils, Types, Classes,

  Variants, QGraphics, QControls,

  QForms, QDialogs, QStdCtrls;

type

  TForm1 = class(TForm)

  private

    FInteger: Integer;

    FMyString: String;

  public

    procedure Foo;

    procedure Goober;

    function Avidya: Pointer;

  end;

  TMyObject = class(TObject)

    procedure Foo;

    procedure Goober;

    function Vishnu: Pointer;

  end;

var

  Form1: TForm1;

  FSammy: Integer;

  Fred: Integer;

  Sam: TBuddha;

implementation

function TForm1.Avidya: Pointer;

begin

  Result := nil; // 这一行不是 IDE 生成的。

end;

end.
```

当你在代码探索器中声明 `Avidya` 方法时，该方法的声明被插入到 `Form` 类中，位于单元的最后语句之前。`Avidya` 有时被翻译为错误，而 `Vidya` 代表的是知识。因此，我认为有必要添加 `Result := nil;` 这行代码。与 `Avidya` 方法相关的所有其他代码都是自动生成的。

事实证明，还有其他方法可以自动插入代码实现的大纲。假设你在类声明中声明了几个方法，如代码 5.4 所示。聚焦编辑器中的该行，按下 `Ctrl-Shift-C`。此操作会自动勾勒出你声明的所有方法的实现。为了确切表达我的意思，请对比代码 5.4 和 5.5。要将一个文件转换为另一个文件，只需 `Ctrl-Shift-C`。即使是 `{ TObject }` 这行代码也是自动插入的。

# 代码 5.5 按 Ctrl-Shift-C 自动生成 TObject 的所有方法

### 列表 5.5 继续

```
var

  Form1: TForm;

  FSammy: Integer;

  Fred: Integer;

  Sam: TBuddha;
```

`implementation`

```
{$R * *.xfm}
```

```procedure
function TForm1.Avidya: Pointer;
begin
  Result := nil;
end;
```

```procedure
procedure TForm1.Foo;
begin
end;
```

```procedure
procedure TForm1.Goober;
begin
end;
```

> { TMyObject }

```procedure
procedure TMyObject.Foo;
begin
end;
```

```procedure
procedure TMyObject.Goober;
begin
end;
```

```function
function TMyObject.Vishnu: Pointer;
begin
end.
```

## 理解 Delphi 与 Linux

> 注意
> 当你按下 `Ctrl+Shift+C` 时，光标所在的位置会产生影响。例如，如果你将光标置在 `TMyObject` 的声明上，则会创建 `TMyObject` 的方法。如果你将光标置在 `TForm1` 的某个方法上，则会创建 `TForm1` 的所有方法。进一步的实验将帮助你学习放置光标的最佳方法。

你也可以执行我在最后几个段落中描述的反相反操作。特别是，你可以先输入方法的实现部分，然后按 `Ctrl+Shift+C` 将其插入到对象声明的 `Private` 部分。

例如，启动一个新项目。进入单元（`unit`）的实现部分（`implementation`），并声明一个名为 `TForm1.Theoretic` 的简单过程：

```
procedure TForm1.Theoretic;
begin
end;
```

现在，将光标置于声明新过程的顶行任意位置，然后按 `Ctrl+Shift+C`。`Theoretic` 方法的声明将自动插入到你的单元中：

```
TForm1 = class(TForm)
private
  {私有声明}
  procedure Theoretic; // 自动插入的代码
public
  {公共声明}
end;
```

要从方法的声明移动到实现部分，或反之，只需按 `Ctrl+Shift+向上箭头` 或 `Ctrl+Shift+向下箭头` 即可。

## 类补全：自动实现属性

属性将在第 10 章“高级组件设计”中讨论。然而，关于属性的几点可以在本书的这部分进行讨论。

要自动实现属性，只需输入其声明的核心内容，就像我在这里为 `Dharma` 属性所做的那样：

```
TForm1 = class(TForm)
private
```
{私有声明}
procedure Theosophy;
public
{公共声明}
property Dharma: Integer;
end;
```

如果你将光标置于名为 `Dharma` 的属性上并按 `Ctrl+Shift+C`，将会生成与此属性相关的代码：

`property Dharma: Integer read FDharma write SetDharma;`

```
procedure TForm1.SetDharma(const Value: Integer);
begin
FDharma := Value;
end;
```

你可以在列表 5.6 中看到完整的源代码。

# 列表 5.6 在 Kylix 中按 Ctrl+Shift+C 自动生成的示例方法和属性

```
unit Unit;
```

```
interface

uses
SysUtils, Types, Classes,
Variants, QGraphics, QControls,
QForms, QDialogs;
```

```
type
TForm1 = class(TForm)
private
FDharma: Integer;
procedure Theosophy;
procedure SetDharma(const Value: Integer);
{ 私有声明 }
public
{ 公声明 }
property Dharma: Integer read FDharma write SetDharma;
end;
```

```
var
Form1: TForm1;
```

## 理解 Delphi 与 Linux

### 列表 5.6 继续

`implementation`
