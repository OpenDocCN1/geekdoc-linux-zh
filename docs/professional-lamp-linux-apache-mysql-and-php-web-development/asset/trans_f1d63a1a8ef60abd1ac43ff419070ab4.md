
## PHP5 OOP

仔细观察前面的代码片段，你可能会注意到在使用 `radius` 属性时有一些不太顺手的之处。你显式地设置了 `radius` 属性，然后又将该属性作为 `calcArea` 方法参数的显式值复用。既然对象内部已经知道 `radius` 属性，那么就没有理由再向 `calcArea()` 方法显式提供它。为了消除提供 `radius` 参数的要求并改用对象内部的 `radius` 属性，你需要一个方法来访问它。PHP 为我们提供了一个名为 `$this` 的引用来实现这一目标。使用这个特殊命名的变量 `$this` 就如同引用一个已实例化的对象，但 `$this` 引用的是包含它的那个对象。

修改 `Circle` 类，如下所示：

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

// 创建一个新的 Circle 实例
$c = new Circle();

// 修改属性
$c->radius = 5;

// 使用方法
echo 'The area of the circle is ' . $c->calcArea();

?>
```

运行这段代码将产生与之前示例完全相同的结果——唯一的改变在于你使用 `calcArea()` 方式。由于你在方法内部引用了 `Circle` 对象的 `radius` 属性，因此不再需要在函数定义和方法调用中包含该参数。

### 可见性

PHP5 OOP 模型的新特性之一，就是能够为所有类属性和方法指定可见性级别。使用这些新的可见性关键字，你可以将类的某些部分对外部代码隐藏，同时暴露你希望对所有代码开放访问的其他功能。PHP5 提供了三种在类中使用的可见性级别：`public`、`private` 和 `protected`。

`public` 可见性意味着属性或方法对所有希望访问它的其他代码都可用。如果未指定方法的可见性，则默认为 `public`。

将类成员指定为 `private` 意味着该属性或方法仅在所属的类定义内部可见。同一类中的所有其他方法都可以访问私有成员，但该特定类外部的任何代码都不能。

最后，*protected* 关键字指定属性或方法仅在定义类以及任何扩展或继承自定义类的其他类中可用。章节的后半部分将讨论类的扩展和继承。

> 在 PHP5 下重用 PHP4 类时，重要的是要记住，使用 var 关键字定义的属性（例如 var $propertyName）将被视为 public，并且会发出 E_STRICT 警告。

为类成员指定可见性很容易，只需在属性或方法声明前加上相应的前缀即可。在之前定义的 Circle 类中，所有类成员都被定义为 public。现在你将把一些旧的类成员更改为 private，并添加一些新方法。

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
```

没有将属性保持为 public，而是将它们更改为 private，并创建函数来设置它们的值。在像这样简单的情境下，这样做可能有点过度，但如果扩展应用程序，set 函数可以在设置内部值之前对数据执行复杂计算。这种分离还可以通过在允许内部数据更改之前验证外部提供的值，从而为私有成员增加一层保护。

你可以使用以下代码来使用你修改后的类：

```php
$c = new Circle();
$c->setCenter(0, 0);
$c->setRadius(10);

echo "The area of the circle is " . $c->calcArea() . "\n";

// 尝试访问私有属性
echo "The private value of radius is " . $c->radius;
?>
```

如果你运行这段代码，你会看到类似以下的输出：

```
The area of the circle is 314.15926535898
Fatal error: Cannot access private property Circle::$radius in /www/plamp/ch02/02-002.php on line 31
```

如你所见，这与你之前使用 `Circle` 的方式并没有太大不同，但由于 public/private 的指定，你现在必须使用方法来访问 `$center` 和 `$radius` 属性，而不是直接访问这些属性。注意在末尾尝试直接访问私有成员时发生的情况——会引发一个致命错误。

### 构造器和析构器

在处理类的一些情况下，你可能希望有一种方式在对象创建时自动执行操作。你可能想要初始化对象参数或自动调用类方法。也许你希望对象检查本地环境以确认必要的资源可用，或者甚至建立初始连接。对于这些情况，PHP 提供了 `constructors`（构造器）。

构造器不过是一个特殊命名的方法，在对象实例化时自动调用。在 `PHP5` 中，要实现构造器，你只需实现一个名为 `__construct` 的方法即可。例如：

```php
<?php
class Circle
{
    public function __construct()
    {
        // 在对象创建时执行操作
        echo "A circle object is being created.\n";
    }
}

$c = new Circle();
?>
```

执行这段代码时，你会看到以下内容：

```
A circle object is being created.
```

正如预期，定义在构造器方法内部的代码在对象实例化时自动执行了。

> 你仍然可以使用 PHP4 风格的构造器（与类同名方法）在 `PHP5` 中，但新式的 `__construct` 方法更受推荐。

像标准方法和函数一样，构造器也可以处理参数。为了向构造器传递参数，你在创建对象时将其包含在括号内，如下所示：

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

在这个例子中，你只是在创建对象时简单地提供了一个半径参数——本例中为 10——构造器会自动解析它，进而在实例化时设置圆的半径。

既然你已经有了一种在对象创建时执行操作的方法，接下来我们将看一种在对象销毁时执行额外操作的方式。PHP5 现在包含一个在对象销毁时调用的特殊方法，逻辑上称为析构器（destructor）。当移除对对象的所有引用，或在代码中手动销毁对象时，对象的析构器会被调用。析构器通常用于各种清理任务，例如关闭数据库连接和释放文件句柄。要创建析构器，请向你的类添加一个方法，并将其命名为 `__destruct`：

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

// 销毁 circle 对象
unset($c);
?>
```

运行这段代码将得到：

```
A circle object is being created.
A circle object is being destroyed.
```

注意，你看到析构器内部放置的消息，而无需做任何额外操作。这是因为 PHP 在脚本执行结束时自动清理对对象的所有引用，从而自动调用对象的析构器。

最后需要记住的一点是，与可以有参数的构造器不同，析构器不能有参数。

## Static 关键字

有时在使用面向对象编程时，你可能需要访问类的方法，但不需要创建一个完整的对象。为了满足这一需求，PHP5 提供了 `static` 关键字。`static` 关键字是 PHP5 的新功能，它允许在不实例化类的情况下使类属性和方法可用。要使类成员静态化，只需在可见性和属性或方法定义之间加上 `static` 关键字，如下所示：

```php
<?php

class Circle
{
  public static function calcArea($r)
  {
    return pi() * pow($r, 2);
  }
}
```

要使用新创建的静态属性，你只需使用类名，后跟两个冒号，然后是属性名或方法调用：

```php
$r = 5;
echo "Given a radius of " . $r .
     ", a circle has the area " . Circle::calcArea($r);
?>
```

在浏览器中运行这段代码会产生类似以下的结果：

> Given a radius of 5, a circle has the area 78.539816339745

然而，使用静态方法有一些限制。静态方法不能通过 `$this->` 更改或访问对象变量或方法；它们只能直接访问类中的其他静态属性和方法。

为了在同一类中访问其他静态变量，你可以使用 `self` 关键字，配合双冒号使用。使用 `self::` 类似于 `$this->`，但它仅用于静态成员。如果你想修改 `Circle` 类以使用静态方法和属性，你可能可以做一些类似于以下的事情：

