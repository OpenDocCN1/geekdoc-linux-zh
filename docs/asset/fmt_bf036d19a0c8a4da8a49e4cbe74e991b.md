
函数可以通过两种方式返回值。可以通过给函数名赋值来为函数返回值。另一种（更常见）方法是使用 `result` 关键字（如上例所示）从函数返回结果。与使用 `return` 的其他语言不同，给 `result` 赋值不会结束函数。`Result` 可以在函数内部作为局部变量使用，并根据需要进行多次赋值。

## 参数传递 (Parameter Passing)

理解向函数和过程传递参数的细节是高效安全编程风格的关键。默认情况下，变量是按值传递。这意味着当变量作为参数传递给函数或过程时，系统会创建该值的副本并将该副本传递给方法。在方法内部，参数充当局部变量，可以自由地访问和赋值。然而，当方法完成后，副本会被销毁。从程序员的角度来看，这意味着传递的变量将恢复到其原始值。有些人认为这是一种良好的安全性，另一些人认为这缺乏灵活性。事实上，这完全取决于子程序的意图。有时，子程序的参数仅用于提供信息，而在其他情况下，方法的完全是为了填充参数。

![](img/d784fa8294cae585d61ec86b987ea212_121_0.png)

图 5-1：按值传递

参数传递的第二种方法称为引用传递。当变量按引用传递时，应用程序直接将变量的地址传递给方法。方法每次读取或为参数赋值时，都在访问所传递地址处的值。这意味着对参数进行的任何更改都会直接修改原始值且是永久的。要按引用传递参数，需要在参数前加上 `var` 关键字。再次，有些人认为这是危险的，但实际上，这可能正是方法的目的。

![](img/d784fa8294cae585d61ec86b987ea212_121_1.png)

图 5-2：按引用传递

再次查看“过程”部分的 `SortNumbers` 示例，注意用于交换数字的代码涉及多行。即使在这个小示例中，将此功能抽象到单独的方法中也是好主意，因为它涉及多行代码。`SwapNumbers` 过程显示了两个数字的交换。

```pascal
procedure SwapNumbers(var A,B : Integer);
var Temp: Integer;
begin
  Temp := A;
  A := B;
  B := Temp;
end;
```

注意相同类型的多个参数可以用列表格式传递，而不是逐个声明。一旦过程被声明并实现，就可以简单地从程序的另一个区域引用它来调用。

## 重载子程序 (Overloaded Subroutines)

子程序的编写者通常无法确定用户（调用块）将拥有哪些信息。例如，客户对象可以用不同的数量来创建。重载子程序允许程序员在同一个代码作用范围内声明同名方法的多个版本。这使得客户端应用程序在用户界面设计上（需要哪些信息等）具有更大的灵活性。

```pascal
function GetCustomer(CustomerId : Integer):TCustomer;overload;
function GetCustomer(CustomerName : String):TCustomer;overload;
```

## 子程序 (Subroutines)

重载子程序是为代码提供灵活性的极佳方法。如果没有它们，我们被迫创建名称相似的子程序，并记住每个版本所需的参数！重载子程序的关键在于创建区分不同的参数列表。应用程序根据调用发送给子程序的参数动态地确定哪个子程序是合适的。每个版本的子程序都必须在它的声明末尾添加 `overload` 指令。这通知编译器这些子程序应该被单独处理（尽管它们的名称相同）。调用不具有歧义是至关重要的；也就是说，应用程序必须清晰地确定意图要调用哪一个子程序。例如，假设应用程序需要检索与特定订单关联的客户。此版本的 `GetCustomer` 子程序可能会这样声明：

```pascal
// 会导致编译器错误！
function GetCustomer(OrderId : Integer):TCustomer;overload; // 注意：此处逻辑上为歧义示例，下文有说明
```

这是一个歧义子程序的示例（当它与上面显示的其他 `GetCustomer` 版本一起声明时）。如果调用了此子程序，编译器将无法知道提供的整数是给 `OrderId` 还是 `CustomerId`。返回类型或子程序类型（过程或函数）都不足以清晰地确定该子程序。以下两个子程序声明也会导致编译错误。

```pascal
// 编译器错误！返回类型不区分子程序。
function GetCustomer(CustomerId : Integer):Integer;overload;
```

```pascal
// 编译器错误！子程序类型不区分子程序。
procedure GetCustomer(CustomerId : Integer);overload;
```

## 默认参数

Kylix 允许开发者为函数和过程参数提供默认值。这本质上创建了可选参数，开发者可以根据意愿提供或不提供这些参数。这是一个非常强大的工具，因为同一个方法可能会被两个不同的客户端调用，而每个客户端拥有的信息不同。例如，假设你创建了一个在屏幕上绘制矩形的过程。该方法可以通过以下方式之一进行定义：

```pascal
procedure TFrmMain.DrawRectangle(): override;
procedure TFrmMain.DrawRectangle(Height, Width: Integer); override;
procedure TFrmMain.DrawRectangle(Height, Width, Border: Integer; Color:TColor); override;
```

该方法的第三个版本为开发者如何创建矩形提供了最大的选择空间。事实上，此子程序的某些调用者可能不在乎矩形的颜色。对于大多数客户端来说，矩形应该是红色的，只有在少数情况下才需要不同的颜色。与其强制所有开发者记住他们创建的矩形是什么颜色，该子程序应该这样重新声明：

```pascal
procedure TFrmMain.DrawRectangle(Height, Width, Border: Integer);
Color:TColor = clRed;
```

此声明为 `Color` 参数提供了一个默认值，并为（调用者）提供了仅发送两个参数而省略第三个参数的选择。

> 警告：默认方法可能导致函数调用歧义。如果重载方法包含一个默认参数，且该参数是两个方法参数列表之间唯一区别属性，那么调用仍然是歧义的！下面的示例将无法编译：

```pascal
procedure TFrmMain.DrawRectangle(Height, Width, Border: Integer);
procedure TFrmMain.DrawRectangle(Height, Width, Border:Integer;Color:TColor = clRed);
```

## 数据存储

存储数据是几乎每个应用程序中的重要任务。数据必须被传递且不能被分解为简单的值，但可能由一组共同实体的值组成。Pascal 提供了多种存储复杂数据以及简单高效地引用和访问数据的方法。

## 集合

集合是具有相同顺序类型的唯一值的集合。集合基于其基类型，可以包含从 0（空集）到 256 个值。集合可以通过其类型声明，也可以通过特定的值集声明。如果使用具有超过 256 个元素的基类型声明集合，编译器将抛出错误。

注意关键字 `in` 的使用。`in` 操作符确定一个值是否包含在集合中。

```pascal
type
Letters = set of 'a'..'z';
nTIntSet = set of Integer; //错误：元素过多。
TIntSet = set of 0..200; // 有效的集合声明。
```

```pascal
{ 稍后的代码... }
```

```pascal
var
MySet : TIntSet;
begin
// 使用两个范围内的所有值初始化集合（1..10 和
// 100..110）。
MySet := [1..10,100..110];
if 55 in MySet then
ShowMessage('55 是集合的成员。');
end;
```

可以在变量声明中通过显式列出类型来动态声明集合。

```pascal
var
MyCharset : set of 'a'..'z';
```

## 数组

数组是一种持有有限数量元素并维护唯一索引的数据结构。所有元素必须是必须的类型（除非是变体数组，见第 9 章），并且可以包含原始类型和非原始类型。数组用于各种任务，从维护字符串列表到存储一组对象引用。

数组类型可以在类型部分中显式声明，也可以在使用时动态声明。每种声明类型都是可以接受的，但根据原则，应该由数组的预期用途来决定。如果你计划在源代码的一个区域中始终使用一个包含十个整数的数组，通常最好在类型部分显式声明该数组类型。然后可以使用该新类型轻松地定义该类型的数组变量。

```pascal
type
TIntArray = array[1..10] of integer;
```

```pascal
{ 当天晚些时候... }
```

```pascal
var
```
