
在本章中，我们将探索 PHP 面向对象编程的核心概念以及如何实现它们。我们将学习类、对象、继承、接口以及其他强大的功能。在本章结束时，你将为使用 PHP 构建面向对象的应用程序奠定坚实的基础。

属性定义的第二部分 `property_name` 仅仅是你想要让该属性拥有的名称。

例如，假设你想创建一个名为 `Circle` 的类。你可能想要有一个公共属性来存储半径，如下所示：

```php
class Circle {
    public $radius;
}
```

此外，你可以在定义中为该属性指定一个初始值。假设你想将 `Circle` 的初始半径设置为 10；你可以执行以下操作：

```php
class Circle {
    public $radius = 10;
}
```

那么，每当创建一个 `Circle` 对象时，它将从 10 的初始半径开始。

# 方法

你已经创建了属性来存储对象内部的数据，现在你需要一种处理这些数据的方法。为了执行这些操作，你将在类内部创建函数，这些函数被称为方法。

在 PHP 中定义方法与在代码的其他地方创建标准函数非常相似：

```php
visibility function function_name(parameters) {
    // 方法实现在这里
}
```

与属性定义类似，方法的定义需要一个可见性组件。除了可见性前缀外，方法的定义方式与标准 PHP 函数完全相同——只需使用 `function` 关键字，后跟函数名以及括号内可选的参数列表。

再次使用 `Circle` 示例，你将添加一个方法来计算圆面积：

```php
class Circle {
    public $radius;

    public function calcArea($radius) {
        return pi() * pow($radius, 2);
    }
}
```

你创建了一个方法 `calcArea()`，它接收一个参数 `$radius` 并返回给定半径的圆的面积。

现在你已经创建了这些属性和方法，你需要一种方法来实际使用这些属性和方法。这就是“实例化”。

# 第 2 章

## 使用类：实例

为了访问类的属性和方法，你首先需要实例化，或者说创建一个该类的实例。当一个类被实例化时，它会返回该类类型的独立对象，供你使用。在 PHP5 中，使用 `new` 关键字创建对象实例，如下：

```php
$c = new Circle();
```

一旦创建了对象，就可以使用“箭头”运算符（紧跟连字符后的大于号）来访问各个属性和方法，如下代码所示：

```php
<?php
class Circle {
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

// 使用方法
echo 'The area of the circle is ' . $c->calcArea(5);
?>
```

如果你运行这段代码，你将看到类似下面的内容：

> The area of the circle is 78.539816339745

观察代码，你会发现你首先定义了 `Circle` 类。然后，你添加了实例化对象的代码：

```php
// 创建 Circle 的新实例
$c = new Circle();
```

最后，你将 `$radius` 属性的值改为 5，并计算了半径为 5 时的圆的面积：

```php
// 修改属性
$c->radius = 5;

// 使用方法
echo 'The area of the circle is ' . $c->calcArea($c->radius);
```

## PHP 5 OOP

仔细观察之前的代码，你可能注意到你使用 `radius` 属性的方式有点别扭。你显式地设置了 `radius` 属性，但随后将其作为 `calcArea` 方法参数的显式值。由于对象内部已经知道 `radius` 属性，没有理由将其传递给 `calcArea()` 方法。为了移除提供半径参数并使用对象自身 `radius` 属性的需求，你需要一个方法来访问它。PHP 为我们提供了名为 `$this` 的引用来实现这一目标。使用特定变量 `$this` 就像引用一个实例化的对象，`$this` 指向它所包含的对象。

如下所示修改类结构：

```php
<?php

class Circle
{
    public $radius;

    public function calcArea()
    {
        return pi() * pow($this->radius, 2);
    }
}

// 创建 Circle 的新实例
$c = new Circle();

// 修改属性
$c->radius = 5;

// 使用方法
echo 'The area of the circle is ' . $c->calcArea();

?>
```

运行这段代码将得到与之前示例完全相同的结果——唯一的变化在于你使用 `calcArea()` 方法的方式。由于你在方法内部引用了 `Circle` 对象的 `radius` 属性，你不再需要在函数定义和方法调用中需要该参数。

## 可见性

PHP5 OOP 的新功能之一是能够为所有属性和方法设置可见性级别。通过这些可见性关键字，你可以向外部代码隐藏类的某些部分，并暴露你希望所有人访问的功能。PHP5 提供了三种可见性级别供类使用：`public`（公共）、`private`（私有）、`protected`（保护）。

`public` 可见性意味着属性或方法对所有想要访问它的代码可用。如果没有为方法指定可见性，它默认为 `public` 可见。

将类成员指定为 `private` 会使该属性或方法仅在所属的类定义内部可见。该类中的所有其他方法都可以访问它。

最后，`protected` 关键字指定属性或方法仅在定义类以及任何继承自该类的类可用。继承和扩展将在稍后的章节讨论。

在 PHP5 中复用 PHP4 类时，重要的是使用 `var` 关键字定义的属性（如 `$propertyname`）将被视为 `public`，并会发出 `E_STRICT` 警告。

为类成员指定可见性只需在属性或方法声明前加上适当的前缀。在你之前定义的类中，所有类成员都定义为 `public`。现在你要将一些旧类成员改为 `private`，并添加一些新方法。

```php
<?php
class Circle {
    private $center = array('x' => 0, 'y' => 0);
    private $radius = 1;

    public function setRadius($radius) {
        // 由于此处 OCR 损坏，此代码是推断的
        $this->radius = $radius;
    }

    public function setCenter($x, $y) {
        $this->center['x'] = $x;
        $this->center['y'] = $y;
    }

    public function calcArea() {
        return pi() * pow($this->radius, 2);
    }
}
?>
```

## 构造函数与析构函数

```php
<?php

class Circle
{
    public $radius;

    public function __construct($r)
    {
        // 在对象创建时执行操作
        echo "A circle object is being created.\n";

        $this->radius = $r;
    }
}

$c = new Circle(10);
?>
```

在这个示例中，你在创建对象时简单地提供了一个半径参数——在本例中为 10——该参数会被构造函数自动解析，从而在实例化时设置圆的半径。

既然你已经了解了在对象销毁时执行操作的方法，现在你将查看在对象销毁时执行额外操作的方法。PHP 现在包含一个在对象销毁时调用的特殊方法，逻辑上它被称为**析构函数**。当对象的所有引用都被移除，或者在代码中手动销毁对象时，对象的析构函数就会被调用。析构函数通常用于清理任务，例如关闭数据库连接和释放文件句柄。要创建一个析构函数，请向类添加一个方法并将其命名为 `__destruct()`：

```php
<?php

class Circle
{
    public function __construct()
    {
        // 在对象创建时执行操作
        echo "A circle object is being created.\n";
    }

    public function __destruct()
    {
        // 在对象销毁时执行操作
        echo "A circle object is being destroyed.\n";
    }
}

$c = new Circle();

// 销毁圆对象
unset($c);
?>
```

运行这段代码将得到：

- A circle object is being created.
- A circle object is being destroyed.

注意看你看到放置在析构函数内部的消息，而无需进行任何手动操作。这是因为 PHP 在脚本执行结束时会自动清理所有对象的引用，从而自动调用对象的析构函数。

需要记住的一点是，与带有参数的构造函数不同，析构函数不能有任何参数。

## Static 关键字

有时在进行面向对象编程时，你可能需要访问类的方法，而无需创建一个完整的对象。为了满足这一需求，PHP5 引入了 `static` 关键字。对于初接触 PHP5 的学者，`static` 关键字允许在不实例化类的情况下使用类属性和方法。要使类成员变为静态，只需在可见性范围与属性或方法定义之间添加 `static` 关键字，如下：

```php
class Circle {
    public static function calcArea($r) {
        return pi() * pow($r, 2);
    }
}
```

使用新创建的静态属性，只需使用类名后跟两个冒号，然后是属性名或方法调用：

```php
$r = 5;
echo "Given a radius of " . $r .
", a circle has the area " . Circle::calcArea($r);
```

在浏览器中运行这段代码将产生类似下面的结果：

> Given a radius of 5, a circle has the area 78.53981633975

然而，静态方法也有一些局限性。静态方法不能通过 `$this->` 修改或访问对象变量或方法；它们只能直接访问类中的其他静态属性和方法。

为了访问同一个类内的静态变量，可以使用 `self` 关键字配合双冒号。使用 `self::` 类似于 `$this->`，但它仅用于静态成员。如果你想修改 `Circle` 类以使用静态方法和属性，可以采取如下操作：

```php
<?php
class Circle
{
    private static $radius;

    public static function setRadius($r)
    {
        self::$radius = $r;
    }

    public static function getRadius()
    {
        return self::$radius;
    }
}

Circle::setRadius(5);
echo "our staticially accessed circle has a radius of " . 
Circle::getRadius() . "\n";
?>
```

快速运行 PHP5 引擎将产生：

- Our staticially accessed circle has a radius of 5.

## 类常量

随着 PHP5 中对象的改进，类常量的概念也被引入了 PHP。类常量与普通的 PHP 常量相似，但它们仅在类内部可用。标准的 PHP 常量的值只能被设置一次标量值——简单的数字或字符串——任何尝试将常量设置为函数的结果都会导致错误。

使用类常量时，请记住它们在访问方式上类似于静态成员——访问类常量必须使用双冒号（`::`）语法。要定义类常量，请在常量名之前使用 `const` 关键字，如下代码所示：

```php
<?php
class Circle
{
    const pi = 3.14159265359;

    public function getPi()
    {
        return self::pi;
    }
}

echo "The value of Pi in our Circle class is " . Circle::pi . "\n";

$c = new Circle();

echo "To recap, the value of Pi in our Circle class is " . $c->getPi();
?>
```

运行这段代码将产生输出：

The value of Pi in our Circle class is 3.14159265359

To recap, the value of Pi in our Circle class is 3.14159265359

在面向对象编程（OOP）中，有几种方法可以指定一组属性供多个类使用。第一种是**继承**，它允许你定义一组属于基类的属性和方法，并可以将它们作为更具体类的构建基块。第二种是**接口**，它允许你规定一个类必须实现的方法列表。

## 继承

假设你正在创建一个代码库，用于处理不同的几何形状。你在整个章节中一直使用的 `Circle` 类可以是该库的一部分。在为不同的形状（正方形、圆形、三角形等）创建不同的类时，你可能会发现所有形状之间存在相似或完全相同的方法，导致了重复代码。这将是继承的一个良好机会。

### extends 关键字

假设所有的几何形状类都将绘制在网格上。因此，它们需要某种原点（x,y）。你可以在每个不同的类中包含一个原点，也可以使用 `extends` 关键字，通过继承在某个共享位置中定义该属性。要实现这一点，你将创建一个 `Shape` 类，它将作为你可能创建的所有几何类的父类。每个具体的形状类——无论是 `Circle`、`Square`、`Ellipse` 还是 `Star`——都拥有 `Shape` 提供的基础功能集。理解这种父子关系的简单方法是使用“是一个 A”的短语。在这个例子中，`Circle` 是一个 `Shape`，就像 `Square` 是一个 `Shape`，`Triangle` 是一个 `Shape`。

要使用你的 `Shape` 类，可以执行类似的操作：

```php
<?php
class Shape
{
    public $origin = array('x'=>0, 'y'=>0);
}

class Circle extends Shape
{
    public $radius;
}

$c = new Circle();
print_r($c->origin);
?>
```

运行这段代码将产生以下结果：

```
Array
(
    [x] => 0
    [y] => 0
)
```

### 重写属性与方法

在扩展基类时，可以重新定义父类（基类）中存在的属性和方法。例如：

```php
<?php
class Shape {
    public $origin = array('x'=>0, 'y'=>0);
}

class Circle extends Shape {
    public $origin = 'New origin';
}

$c = new Circle();
print_r($c);
?>
```

这段代码将输出：

```
Circle Object
(
    [origin] => New origin
)
```

通过在子类中重新定义基属性 `$origin`，新定义会隐藏父类的值。方法的行为方式也相同——在子类中重新定义会覆盖父类方法或多个方法的功能。例如，以下代码：

```php
<?php
class Shape {
    public $origin = array('x'=>0, 'y'=>0);
    public function getOrigin() {
        return $this->origin;
    }
}

class Circle extends Shape {
    public function getOrigin() {
        return array('x'=>1, 'y'=>1);
    }
}

$c = new Circle();
print_r($c->getOrigin());
?>
```
