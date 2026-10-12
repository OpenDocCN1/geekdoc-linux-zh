
理解类的一种简单方法是将类代码与物理对象联系起来。很多时候，类会代表这些现实世界中的对象。你可能会有一个名为`CAR`（汽车）的类，它有一个名为`occupants`（乘客）的属性，该属性可能用于追踪车内的人数。它甚至可能包含一个名为`brake()`（制动）的方法，该方法将执行与其同名的任务。像许多现实世界中的物品一样，类具有描述单个对象的属性组合，在`OOP`（面向对象编程）中称为*属性*，以及它们可以执行的一组动作，在面向对象世界中称为*方法*。

### 定义类

在`PHP5`中定义类是一个相对直接的过程——与定义函数非常相似，只是关键字不同：

```php
class Circle { // 类代码放在这里 }
```

此代码通过使用`class`关键字，后跟类名，以及一组大括号来定义一个简单的类。

在标准的`PHP5`类中，类定义主要有两个部分——属性和方法。属性表示对象中持有的数据，而方法则使用这些数据执行操作。

### 属性

在`PHP5`中创建类时，属性是你将存储对象所表示的各种数据片段的地方。

在`PHP5`中定义属性非常简单，如下所示：

```php
visibility $property_name;
```

在此定义中，`visibility`表示属性的代码可见性，它是三个值之一：`public`（公共）、`private`（私有）或`protected`（受保护）。这三个关键字的含义将在本章后面进行讨论。

属性定义的第二部分，`property_name`只是你希望属性拥有的名称。

例如，假设你想创建一个名为`Circle`的类。你可能想要有一个公共属性来保存半径，如下所示：

```php
class Circle
{
    public $radius;
}
```

可选地，你可以在定义中为属性指定初始值。假设你希望`Circle`的初始半径设置为`10`；你可以这样做：

```php
class Circle
{
    public $radius = 10;
}
```

然后，每次创建`Circle`对象时，它都会以初始半径`10`开始。

### 方法

你创建了属性来在对象内部存储数据，现在你需要创建一种方式来操作这些数据。要执行这些操作，你将在类内部创建函数，称为*方法*。

在`PHP5`中定义方法与在代码的其他地方创建标准函数非常相似：

```php
visibility function function_name (parameters)
{
    // 方法实现放在这里
}
```

与属性定义类似，方法定义需要一个可见性组件。除了可见性前缀外，方法的定义与标准`PHP`函数完全相同——只需使用`function`关键字，后跟函数名称，然后是括号内可选的参数列表。

再次使用`Circle`示例，你将添加一个方法来计算圆的面积：

```php
class Circle
{
    public $radius;

    public function calcArea($radius)
    {
        return pi() * pow($radius, 2);
    }
}
```

你简单地创建了一个名为`calcArea()`的方法，它接收一个参数`$radius`，并返回给定半径的圆的面积。

既然你已经创建了这些属性和方法，你需要一种方式来实际使用你的属性和方法。这就引入了*实例化*。

### 使用类：实例

为了访问类的属性并使用类的方法，你需要先实例化该类，或创建该类的实例。当类被实例化时，它会返回该类类型的*单个对象*，你可以使用它。在`PHP5`中，对象实例是使用`new`关键字创建的，如下所示：

```php
$c = new Circle();
```

一旦对象被创建，通过“箭头”运算符（连字符后立即跟一个大于号）访问个别属性和方法，如下面的代码所示：

```php
<?php

class Circle
{
    public $radius;

    public function calcArea($radius)
    {
        return pi() * pow($radius, 2);
    }
}

// 创建 Circle 的新实例
$c = new Circle();

// 修改属性
$c->radius = 5;

// 使用一个方法
echo 'The area of the circle is ' . $c->calcArea(5);
?>
```

如果你运行此代码，你会看到类似以下内容：

```
The area of the circle is 78.539816339745
```

查看代码，你会看到从定义类`Circle`开始。然后，你添加了实例化对象的代码：

```php
// 创建 Circle 的新实例
$c = new Circle();
```

最后，你将`$radius`属性更改为值`5`，并计算了给定半径为`5`的圆的面积：

```php
// 修改属性
$c->radius = 5;

// 使用一个方法
echo 'The area of the circle is ' . $c->calcArea($c->radius);
```

仔细观察前面那段代码，你可能注意到了你在半径属性使用方式上有些笨拙。你显式地设置了半径属性，但随后又将该属性重新作为`calcArea`方法的参数的显式值使用。由于对象内部知道半径属性，因此没有理由显式地将它提供给`calcArea()`方法。为了消除提供半径参数的要求，并使用对象自己的内部半径属性，你需要一种方法来访问它。`PHP`为我们提供了一个名为`$this`的引用来实现这样的目标。使用特别命名的变量`$this`就像引用一个实例化的对象，但`$this`引用的是包含它的对象。

修改`Circle`类，如下所示：

```php
<?php

class Circle
{
    public $radius;

    public function calcArea()
    {
        return pi() * pow($this->radius,  2);
    }
}

// 创建 Circle 的新实例
$c = new Circle();

// 修改属性
$c->radius = 5;

// 使用一个方法
echo 'The area of the circle is ' . $c->calcArea();
?>
```

运行代码将产生与上一个例子完全相同的结果——唯一的变化发生在你使用`calcArea()`方法的方式上。由于你在方法内部引用了`Circle`对象的半径属性，因此你不再需要函数定义和方法调用中的参数。

### 可见性

`PHP5`面向对象模型的一个新特性是能够为所有类属性和方法指定可见性级别。使用这些新的可见性关键字，你可以向外部代码隐藏类的某些部分，并公开你希望所有人都能访问的其他功能。`PHP5`提供三个用于类的可见性级别：`public`（公共）、`private`（私有）和`protected`（受保护）。

`public`可见性意味着属性或方法可供所有希望访问它的外部代码使用。如果未指定方法的可见性，则默认为`public`可见性。

将类成员指定为`private`意味着该属性或方法仅在所属的类定义内部可见。同一类中的所有其他方法都可以访问该私有成员，但该特定类之外的任何代码都不能访问。

## 第 2 章

最后，`protected`关键字指定该属性或方法仅在定义类内部，以及继承自该定义类的其他类中可用。关于扩展和继承类的讨论将在本章后续部分进行。

> 在`PHP5`下重用`PHP4`类时，务必记住：使用`var`关键字定义属性（例如`var $propertyName`）将被视为`public`（公开）属性，并且会发出`E_STRICT`警告。

为类成员指定可见性非常简单，只需在属性或方法声明前添加适当的前缀即可。在你之前定义的`Circle`类中，所有类成员都被定义为`public`。现在，你将要改变其中一些旧的类成员为`private`，并添加一些新的方法。

```php
<?php
class Circle
{
    private $center = array('x' => 0, 'y' => 0);
    private $radius = 1;

    public function setRadius($radius)
    {
        $this->radius = $radius;
    }
    public function setCenter($x, $y)
    {
        $this->center['x'] = $x;
        $this->center['y'] = $y;
    }
    public function calcArea()
    {
        return pi() * pow($this->radius, 2);
    }
}
?>
```
