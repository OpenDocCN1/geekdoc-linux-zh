
![](img/6e977c6eee8c1535039c864d41da5ccf_186_0.png)

- 4 给属性赋值：使用 `myObject.Property = "Value"`，将 `myObject` 替换为对象变量，将 `Property1` 替换为属性名，并将 `"Value"` 替换为适当的值或变量。
- 5 要响应事件，选择你的对象变量。
- 6 在事件列表中，点击一个要处理的事件。
- 7 为该事件输入响应代码。
- 8 按 F5 运行项目。
- 你从你的类中创建一个对象，并使用你定义的方法、属性和事件。

# 定义接口

面向对象编程语言中的每个类都包含两个部分：接口（interface）和实现（implementation）。接口定义了类用户可用的方法、事件和属性。实现使你能够隐藏类的其他部分，包括方法、属性和变量。在大多数情况下，这些允许你创建一个独立的接口，然后稍后再定义它。这使你能够使用同一组方法和属性但具有不同实现创建多个类。

使用 `Interface..End Interface` 块来定义接口。该代码块出现在任何类或模块之外。除非另有指定，否则 VB 将接口定义为 `Public`（公共）。有关访问性关键字的说明，请参阅“创建类”。

在块内部，使用 `Property` 语句定义属性。在 `Property` 关键字之后，VB 导出属性名称、括号内的参数以及 `As` 变量。

例如，你可以定义 `TwoNumbers` 来处理两个数字。类 `TwoNumbers` 可以实现接口以相加数字，并实现接口以相乘数字。这使得该类的用户能够使用定义为 `TwoNumbers` 的变量，并在两个类之间交替使用。

使用 `Function` 或 `Sub` 键以及方法名定义公共方法。你可以指定类实现该方法必须使用的参数，并作为 `Function` 方法返回类型。要定义事件，使用 `Event` 语句，并在其跟上事件名称和参数。

![](img/6e977c6eee8c1535039c864d41da5ccf_187_0.png)
![](img/6e977c6eee8c1535039c864d41da5ccf_187_1.png)
![](img/6e977c6eee8c1535039c864d41da5ccf_187_2.png)
![](img/6e977c6eee8c1535039c864d41da5ccf_187_3.png)
![](img/6e977c6eee8c1535039c864d41da5ccf_187_4.png)
![](img/6e977c6eee8c1535039c864d41da5ccf_187_5.png)
![](img/6e977c6eee8c1535039c864d41da5ccf_187_6.png)
![](img/6e977c6eee8c1535039c864d41da5ccf_187_7.png)
![](img/6e977c6eee8c1535039c864d41da5ccf_187_8.png)
![](img/6e977c6eee8c1535039c864d41da5ccf_187_9.png)

- 1 在你想添加类的模块中，输入 `Interface Member`，将 `MyInterface` 替换为接口名称。
- 2 按回车键。
VB 自动创建 `End Interface` 语句。
- 3 要定义接口，输入 `Property`，并在需要时跟上 `ReadOnly` 或 `WriteOnly`。
- 对于索引属性，在括号中添加参数。
- 4 输入属性名称，后跟 `()`。
- 5 输入 `As` 后跟上属性类型。

## 补充

你可以定义一个接口，并在另一个接口中使用 `Inherits` 语句将定义的成员导入新接口中。有关继承，请参阅第 8 章。

示例：

```
Interface Automobile

  ReadOnly Property NumberOfWheels() As Integer

  End Interface

Interface Truck

  Inherits Automobile

  ReadOnly Property TowingAbility() As Integer

  End Interface

Class MyBig

  Implements Truck

  ReadOnly Property NumberOfWheels() As Integer Implements Truck.NumberOfWheels

    Get

      Return 4

    End Get

  End Property

  ReadOnly Property TowingAbility() As Integer Implements Truck.TowingAbility

    Get

      Return 2

    End Get

  End Property

End Class
```

![](img/6e977c6eee8c1535039c864d41da5ccf_188_0.png)
![](img/6e977c6eee8c1535039c864d41da5ccf_188_1.png)

- 6 要定义方法，使用 `Sub` 或 `Function` 并跟上方法名称。
- 7 括号中的任何参数。
- 8 对于 `Function`，输入 `As` 并跟上返回值。
- 9 要定义事件，输入 `Event` 并跟上事件名称。
- 10 在括号内输入必要的参数。
- 11 接口定义完成。你可以创建一个类来通过它。
注意：参阅“实现接口”。

# 实现接口

当你定义接口时，可以使用它来构建类。每个类必须实现接口中指定的所有方法、属性和事件。任意数量的类都可以构建接口。要定义接口，参阅“定义接口”。

要实现特定属性、方法或事件的接口，在行末尾使用 `Implements` 关键字。在关键字后指定接口成员。

要从接口创建类，使用 `Class...End Class` 块。有关创建类，类名不需要与接口相关，且不能与接口相同。在类块的第一行，使用 `Implements` 语句指定要实现的接口。在关键字后跟上接口名称。

在许多情况下，你希望实现的成员名称与接口相同，以便多个类可以交替使用。你可以使用接口名称定义变量，并赋值实现它的类的实例。这允许你处理具有不同函数的类，由于导出了接口，VB 允许你在一个变量中操作它们。

![](img/6e977c6eee8c1535039c864d41da5ccf_189_0.png)
![](img/6e977c6eee8c1535039c864d41da5ccf_189_1.png)

- 1 在所需的代码模块中，定义一个供类实现的接口。
- 2 创建一个新类。
- 3 在类块内部，根据接口名称输入 `Implements`。
- 4 实现接口中的方法，使用 `Sub` 或 `Function` 定义方法。
- 5 在行末，输入 `MyInterface.I`。

参阅“定义接口”部分创建接口。
注意：参阅“定义类”部分创建类。
注意：参阅“定义方法”部分正确设置方法。
将 `MyInterface.I` 替换为接口名称和实现的接口方法。

## 补充

你可以使用类来实现多个接口。为了这样做，在类块的开头放置多个关键字，并实现它们的所有成员。你可以使用类中的一个成员来实现接口的多个成员。在输入方法或属性声明后，用逗号分隔多个成员。当你有类似的接口或接口提供相同的方法时，可以实现多个成员。你可以简单地在一个类中编写代码并实现两个接口方法。

示例：

```
Interface Animal
Sub Eat()
Property Age() As Integer
End Interface
Interface Plant
Sub GetNutrients() As Integer
End Interface
Class VenusFlytrap, Animal, Plant
Sub Insects() Implements Animal.Rat, Plant.GetNutrients
End Sub
Property Age() As Integer Implements Animal.Age, Plant.Age
End Property
End Class
```

![](img/6e977c6eee8c1535039c864d41da5ccf_190_0.png)
![](img/6e977c6eee8c1535039c864d41da5ccf_190_1.png)

```
implementsInterface - Microsoft Visual Basic, [Design] - ImplementClass.vb

File Edit View Project Debug Help

Read1

Model: ImplementClass.vb
```
