
> 在 PHP5 下复用 PHP4 类时，务必牢记：使用 `var` 关键字定义的属性（例如 `var $propertyName`）将被视为 `public`，并且会发出 `E_STRICT` 警告。

为类成员指定可见性非常简单，只需在属性或方法声明前添加适当的前缀即可。在你之前定义的 `Circle` 类中，所有类成员都被定义为 `public`。现在，你将把一些旧的类成员更改为 `private`，并添加一些新方法。

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

你不再将属性保留为 `public`，而是将它们改为 `private`，并创建了函数来设置它们的值。在这种简单情况下，这样做可能有点过度，但如果你扩展应用程序，设置函数可以在设置内部值之前对数据进行复杂计算。这种分离还可以通过在允许内部数据更改之前验证外部提供的值，从而为私有成员增加一层保护。

你可以使用以下代码来使用你修改后的类：

```php
$c = new Circle();
$c->setCenter(0,0);
$c->setRadius(10);

echo "圆的面积是 " . $c->calcArea() . "\n";

// 尝试访问私有属性
echo "radius 的私有值是 " . $c->radius;
?>
```

如果你运行这段代码，你会看到类似以下内容：

> 圆的面积是 314.15926535898

> Fatal error: 无法访问私有属性 `Circle::$radius`，位于 `/www/plamp/ch02/02-002.php` 第 31 行

如你所见，这与你之前使用 `Circle` 的情况没有太大不同。但由于 `public`/`private` 的指定，你现在必须使用方法来访问 `$center` 和 `$radius` 属性，而不能直接访问这些属性。注意最后尝试直接访问私有成员时发生的情况——会发生致命错误。

## 构造函数和析构函数

在处理类的某些情况下，你可能希望有一种在对象创建时自动执行操作的方式。你可能想要初始化对象参数或自动调用类方法。也许你希望对象检查本地环境以确认必要资源可用，甚至建立初始连接。PHP 为这类情况提供了构造函数。

构造函数不过是一个具有特殊名称的方法，当对象实例化时会自动被调用。在 PHP5 中，要实现构造函数，你只需要实现一个名为 `__construct` 的方法即可。例如：

```php
<?php
class Circle
{
    public function __construct()
    {
        // 在对象创建时执行操作
        echo "正在创建圆对象。\n";
    }
}
$c = new Circle();
?>
```

当你执行这段代码时，你会看到以下内容：

> 正在创建圆对象。

正如预期的那样，定义在构造方法内部的代码在对象实例化时自动执行了。

> 你仍然可以在 PHP5 中使用 PHP4 风格的构造函数（与类同名方法），但新式的 `__construct` 方法更受推荐。

像标准方法和函数一样，构造函数也可以处理参数。要向构造函数传递参数，你需要在创建对象时将它们包含在括号内，如下所示：

### 第 2 章

```php
<?php
class Circle
{
    public $radius;

    public function __construct($r)
    {
        // 在对象创建时执行操作
        echo "正在创建圆对象。\n";

        $this->radius = $r;
    }
}

$c = new Circle(10);
?>
```

在这个例子中，你只是在创建对象时提供了一个半径参数——本例中为 10——构造函数会自动解释它，进而在实例化时设置圆的半径。

现在，你已经掌握了在对象创建时执行操作的方法，接下来看看如何在对象销毁时执行额外操作。PHP5 现在包含一个在对象销毁时被调用的特殊方法，逻辑上被称为析构函数。当对象的所有引用被移除，或者在你的代码中被手动销毁时，对象的析构函数会被调用。析构函数通常用于各种清理任务，例如关闭数据库连接和释放文件句柄。要创建析构函数，请向你的类添加一个方法，并将其命名为 `__destruct`：

```php
<?php
class Circle
{
    public function __construct()
    {
        // 在对象创建时执行操作
        echo "正在创建圆对象。\n";
    }

    public function __destruct()
    {
        // 在对象销毁时执行操作
        echo "正在销毁圆对象。\n";
    }
}

$c = new Circle();

// 销毁圆对象
unset($c);
?>
```

运行这段代码会得到：

> 正在创建圆对象。

> 正在销毁圆对象。

注意，你无需执行任何操作就能看到析构函数内部放置的消息。这是因为 PHP 在脚本执行结束时会自动清理所有对象引用，从而自动调用对象的析构函数。

最后一件需要记住的事情是，与可以有参数的构造函数不同，析构函数不能有任何参数。

## static 关键字

有时在使用面向对象编程时，你可能需要访问类的方法，而不必创建一个完整的对象。为了满足这一需求，PHP5 提供了 `static` 关键字。这是 PHP5 中新引入的，`static` 关键字允许在不实例化类的情况下使用类属性和方法。要使类成员变为静态，只需在可见性和属性或方法定义之间添加 `static` 关键字，如下所示：

```php
<?php

class Circle
{
    public static function calcArea($r)
    {
        return pi() * pow($r, 2);
    }
}
?>
```

要使用新创建的静态属性，你只需使用类名，后跟两个冒号，然后是属性名称或方法调用：

```php
$r = 5;
echo "给定半径为 " . $r .
     "，圆的面积为 " . Circle::calcArea($r);
```

在浏览器中运行这段代码将产生类似以下结果：

> 给定半径为 5，圆的面积为 78.539816339745

然而，使用静态方法存在一些限制。静态方法不能使用 `$this` 更改或访问对象变量或方法；它们只能直接访问类中其他静态属性和方法。

为了访问同一类内的其他静态变量，你可以使用 `self` 关键字，结合双冒号使用。使用 `self::` 类似于使用 `$this`，但它仅适用于静态成员。如果你希望修改 `Circle` 类以使用静态方法和属性，你可能会执行类似以下操作：

### 第 2 章

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
echo "Our statically accessed circle has a radius of " .
       Circle::getRadius() . "\n";
?>
```

快速运行 PHP5 引擎将产生以下结果：

    我们静态访问的圆的半径为 5。

## 类常量

随着 PHP5 中改进的对象模型，PHP 引入了类常量的概念。类常量类似于普通的 PHP 常量，但只能在类的定义内部使用。与标准 PHP 常量一样，它们的值只能设置一次，且必须是一个标量值——一个简单的数字或字符串——任何试图将常量设置为函数结果的尝试都会导致错误。

在使用类常量时，请记住它们的访问方式类似于静态成员——要访问类常量，必须使用双冒号 `::` 语法。要定义类常量，请在常量名称前使用 `const` 关键字，如下所示：
