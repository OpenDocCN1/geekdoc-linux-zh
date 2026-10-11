
`GetMem(FMyPointer, 10);`

`end;`

`dest TMObject.Destroy;`

`begin`

`FreeMem(FMyPointer, 10);`

`inherited;`

`end;`

`procedure TMObject.SaySourceName;`

`begin`

`WriteLn(ClassName);`

`end;`

`var`

`MyObject: TMObject;`

```
```

## 理解 Delphi 与 Linux

### 列表 3.6 续

```pascal
begin
  MyObject := TMyObject.Create;
  MyObject.SayName;
  FreeNil(MyObject);
end.
```

许多程序包含需要分配和释放的指针。对于属于另一个对象的内存，你应该执行以下两种操作之一：

- 将指针或对象声明为方法作用域的变量，然后在单个方法内部为该对象分配和释放内存。这就是本章早些章节中“指针”标题下 `ButtonClick` 方法中处理的变量 `P`。在这种情况下，`P` 属于 `ButtonClick` 方法，因此 `ButtonClick` 方法承担了为该内存分配和释放内存的任务。
- 第二种方法在 `AllocateTwo` 程序中显示。在该程序中，变量 `FMyPointer` 被声明为 `Pointer`。但与 VB 和 Java 的对比是不恰当的，因为 Pascal 处理指针的方式与 C++ 相同。如果你为对象分配了内存，就必须释放内存，否则会有内存泄漏的风险！

# 对象与接口

作者 Charlie Calvert

# 第 4 章

## 本章内容

- Kylix 对象模型 152
- 接口 169
- 变体 196
- RTT 与浮点类型 205
- 帧 212
- 命令行编译器 217
- 总结 218

你将需要了解关于 Kylix 对象模型的基本事实，才能理解本书其余部分的大部分内容。本章将以简练的形式介绍相关信息。

这里提供的信息面向已经理解面向对象编程的资深程序员。如果你不清楚什么是对象、什么是多态，或者继承是如何工作的，那么你需要阅读其他书籍来获得进一步的启示。

# 注意

本章将不会涵盖的一个主题是构造函数和析构函数的实际工作。关于该主题的内容可以在第 3 章“基础 Pascal 语法”中的“指针、构造函数和析构函数”部分找到。

另一个与对象相关的未涵盖的主题是属性。你可以在第 10 章“高级组件设计”中的“属性”部分阅读属性的内容。属性是 Pascal 对象模型的一部分。许多使用属性可以实现的有趣功能都与组件和对象检查器（Object Inspector）有关。因此，如果你先不理解元素，很难对属性能做的事情给出完整的总结；我关于属性的讨论是在组件设计部分，而不是本节。

## Kylix 对象模型

没有比直接跳入核心问题更好的开始方式了。以下是在 Pascal 中声明对象的方法：

```pas
TMyObject = class(TObject)
// 此处显示类声明的特定细节
end;
```

在这种情况下，`TMyObject` 是正在被声明的类名。对象名称后面紧跟着一个等号和关键字 `class`。接下来，你插入一个括号以及你的类所继承的对象的名称。如果你不包含最后这部分，则假设该类继承自 `TObject`。在 Pascal 中，除 `TObject` 之外，所有类都有一个祖先。Object Pascal 程序员无法声明没有祖先的类。

类的结束由关键字 `end` 标记，后跟一个分号。你的声明体出现在单词 `TMyObject` 和最后的 `end` 之间的行中。

## 在何处声明对象

类的声明出现在类型（type）节部分。你可以在一个类型节中声明任意数量的对象，并且可以在代码中拥有任意数量的类型节。

你进行的大多数声明出现在 Pascal 单元（unit）中。然而，包含类声明的类型节可以出现在 DPR 文件的顶部。在单元中，它可以出现在任何使用 `interface` 子句的地方。在实现（implementation）部分，它可以出现在任何函数、过程或方法的声明之外，也不会出现在最终化（finalization）或初始化（initialization）子句内部。

在列表 4.1 和 4.2 中，你将看到一些声明类的正确和错误位置的示例。列表 4.1 显示了正确的处理方法。列表 4.2 显示了如果你还不熟悉该语言，可能会容易犯的所有类错误。

列表 4.1 两个正确的声明类——`TMyObject` 在 `uses` 子句之后的 `interface` 部分，`TMyObject2` 在 `implementation` 部分

```pascal
unit Unit2;

interface

uses
SysUtils;

type
TMyObject = class(TObject)
procedure Foo;
end;

implementation

type
TMyObject2 = class(TObject)
procedure Foo;
end;

procedure TMyObject.Foo;
begin
end;
```

## 理解 Delphi 与 Linux

列表 4.1 续

```pascal
procedure TMyobject2.Foo;
begin
end;
```

# JAVA 与 C++

在学习列表 4.1 中的声明时，请注意 `TMyObject.Foo` 和 `TMyObject2.Foo` 的实现都出现在单元的 `implementation` 部分。在 Java 中，对象的声明和实现统一在一个列表中。在 C++ 中，你通常在头文件中声明对象并在 CPP 文件中实现它们。Object Pascal 中的语法。在 Kylix 中，对象的声明可以在 `interface` 或 `implementation` 部分。

# Object Pascal 中的作用域

方法或变量可以是私有（private）、受保护（protected）、公开（public）或发布（published）作用域：

```pas
TEdit1 = class
private
  // 私有声明
protected
  // 受保护声明
public
  // 公开声明
published
  // 发布声明
end;
```

私有方法或变量对单元内的类可见。单元中的任何类都可以访问它们。

受保护方法或变量仅对单元的后代可见。

公开方法或变量可以从程序的任何位置访问。如果你在 `Unit1` 中，你可以访问 `Unit2` 中的任何方法和变量。如果你在第二个单元中，只要第二个单元列出了第一个单元，你就可以访问它们。

发布变量和方法与公开方法或变量具有相同的作用域。但它们具有额外的运行时信息（RTTI）。特别是类发布部分中的 RTTI 是 IDE 在对象检查器中显示属性时使用的。对象检查器中显示的所有属性根据定义都是在类的公开部分声明的。对于不是组件的类，使用发布部分通常没有意义。

# 类相互引用作用域问题

在一个单元中声明多个类时，你通常想访问第二个类中的某个类。考虑以下代码：

```pas
type
TLineCollection = class
FLine: TLine;
end;
```

```pas
TLine = class
FLineCollection: TLineCollection;
end;
```

在这些声明中，`TLine` 引用 `TLineCollection`，而 `TLineCollection` 引用 `TLine`。根据 Object Pascal 的正常作用域规则，`TLineCollection` 不可能包含对 `TLine` 对象的引用：

`FLine: TLine;`

这里的问题仅仅是 `TLineCollection` 的声明在 `TLine` 声明之前。编译器从上到下读取代码。因此，编译器在到达 `TLineCollection` 的声明时，对 `TLine` 一无所知。这种知识缺失会导致编译器发出错误，说明你正尝试使用一个它一无所知的变量。

解决这个问题的方法很简单——写一行代码预声明 `TLine` 类：

```pas
type
TLine = class;
```

# 对象与接口
第4章

```pascal
TLineCollection = class
  FLine: TLine;
end;
```

```pascal
TLine = class
  FLineCollection: TLineCollection;
end;
```
