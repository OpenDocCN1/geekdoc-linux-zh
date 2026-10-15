
`TLine` 的前向声明孤零零地坐在那里，看起来有些凄凉。尽管如此，编译器识别了 `TLine` 对象这个勇敢的哨哨，并将其视为足够的证据来接受 `TLineCollection` 中对 `TLine` 的引用。

> 我偶尔会发现自己交替使用“类（class）”和“对象（object）”这两个词。从技术上讲，类是对象的代码和声明。另一方面，对象是类的实例化实例。你在编写代码时看到的是类，而在运行时你创建的是对象。源文件包含类的声明；而编译后的程序则在运行时创建并操作对象。

在理论上，类和对象之间的界限很容易理解。在实践中，除了最严谨的程序员外，类和对象之间的界限在口语和头脑中变得变得有些模糊。在这两个实体之间的区别真正重要的少数情况下，我会尽量详细地说明这一事实。在其他时候，我会尝试避免这样做，以免陷入对两个易混淆术语之间细微差异的过度迂学式的依赖。

类似的语法情况出现在对其他对象所继承的父对象的正确名称上。在我在这里展示的示例中，`TObject` 是 `TObject2` 的父类，而 `TObject2` 是 `TObject` 的子类。很少（如果有的话）会将这种比喻推得那么远，以至于开始谈论孙子和祖父母。相反，如果这种关系跨越了几“代”，我经常使用“祖先（ancestor）”和“后代（descendant）”来指代这种关系。尽管如此，在大多数情况下，我将父类（parent）、子类（child）和后（descendant）视为同义词。

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_182_0.png)

## 声明方法

你通过编写 `procedure` 或 `function` 关键字，随后是类名、点、方法名，最后是任何参数或返回值来声明 Object Pascal 方法：

```pascal

type

  TObject = class(TObject)

    procedure Foo;

    function Goober(InValue: Integer): String;

  end;

```

```pascal

procedure TMyObject.Foo;

begin

end;

```

```pascal

function TMyObject.Goober(InValue: Integer): String;

begin

end;

```

在类声明内部声明方法时，不需要包含类名：

```pascal

type

  TMyObject = class(TMyObject)

    procedure TMyObject.Foo; // 错误。方法声明中不包含类名。

  end;

```

所示代码将导致编译器的错误，而不是警告。

# Pascal 继承模型：virtual 和 override

虚方法（virtual methods）和动态方法使多态成为可能。在本节中，我将向你展示这些技术在 Object Pascal 程序中体现的语法。再次，除非你先理解多态和继承，否则本节中显示的任何语法对你来说都没有意义。然而，我假设本书的读者已经理解了这些术语，并在其他语言（如 C++ 或 Java）中有使用它们的经验。

如果你想允许对象的用户覆盖它的任何方法，你必须将一个或多个方法声明为 `virtual`：

```pascal

  TMyObject = class(TMyObject)

    procedure Foo; virtual; // TMyObject.Foo 是虚方法

  end;

```

如果你想覆盖一个虚方法，请使用指令：

```pascal

  TMyObject2 = class(TMyObject)

    procedure Foo; override; // TMyObject2.Foo 覆盖了 TMyObject.Foo;

  end;

```

如果你想声明一个同名但不是虚的新方法，可以使用普通的 Object Pascal 方法语法：

```pascal

  TMyObject3 = class(TMyObject)

    procedure Foo; // 没有覆盖虚方法 TMyObject。

  end;

```

在 `TMyObject` 中声明 `Foo` 会导致编译器生成一个警告，说明你用自己的 `Foo` 副本“隐藏”了虚方法 `TMyObject.Foo`。如果你想抑制此警告，使用 `reintroduce` 指令：

```pascal

  TMyObject3 = class (TMyObject)

    procedure Foo; reintroduce;

  end;

```

通常情况下，你不想重新引入隐藏虚方法的方法名。在大多数情况下，这是一个良好的编程实践。

> 如果你将虚方法的覆盖实例放在 `protected` 或 `private` 部分，而该被覆盖的方法最初声明在 `public` 部分，编译器也会表示不满。问题的解决方法显而易见：将你的新方法移回 `public` 部分。

# 在声明中使用 dynamic 代替 virtual

`dynamic` 和 `virtual` 这两个词在 Object Pascal 中的语义基本相同。它们互为同义词。它们之间的区别仅在于运行时的性能。它们的意思相同，但语法背后的技术为程序提供了独特的性能特性。

如果你想节省内存，可以使用 `dynamic` 替换 `virtual`：

```pascal

  TMyObject = class(TObject)

    procedure Bar(i: Integer); dynamic;

  end;

```

要覆盖方法，请使用你覆盖虚方法的语法：

```pascal

  TMyObject2 = class(TMyObject)

    procedure Foo; override; // TObject2.Foo 覆盖了 TMyObject.Foo;

  end;

```

动态方法比虚方法占用的内存少，但执行时间更长。虚方法比动态方法占用内存多，但执行速度更快。

## 理解 Delphi 与 Linux

> 注意
虚方法包含在原始实例和所有后代实例的虚方法表（VMT）中。因此，它们很容易访问，但占据了大量的内存。（你可以将 VMT 认为是内存中的一个记录或数组，其中包含了为该对象及其祖先声明的所有虚方法列表）。虚方法并不在原始对象的 VMT 以及其每个后代的 VMT 中占用内存。相反，动态方法存储在单一表中，每次调用时都会查找。查找动态方法的时间比调用虚方法长。然而，它只出现一次，占用的空间更小。如果你不确定使用哪种技术，Delphi 团队建议你使用虚方法。

# 列表 4.3 ObjectUnit

```pascal

unit ObjectUnit;

interface

type

  TMyObject = class(TObject)

    procedure Foo; virtual;

    function Goober(InValue: Integer): String;

  end;

implementation

uses SysUtils;

procedure TMyObject.Foo;

begin

  // 实现

end;

function TMyObject.Goober(InValue: Integer): String;

begin

  Result := IntToStr(InValue);

end;

  TMyObject2 = class(TMyObject)

    procedure Foo; override;

  end;

procedure TMyObject2.Foo;

begin

  inherited;

end;

  TMyObject3 = class(TMyObject)

    procedure Foo; reintroduce;

  end;

procedure TMyObject3.Foo;

begin

  // 实现

end;

  TMyObject4 = class(TMyObject)

    procedure BeEsoteric; virtual; abstract;

  end;

procedure TMyObject.Bar(i: Integer);

begin

  //

end;

```

# 列表 4.3 续

```
MyObject4.Free;

end;
```
