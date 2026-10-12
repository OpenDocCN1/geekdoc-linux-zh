
```php
interface GeometricOperations
{
    public function getOrigin();
}

interface TwoDimensionalOperations
{
    public function calculateArea();
}

class Circle implements TwoDimensionalOperations, GeometricOperations
{
    // Implement the required methods
    public function getOrigin()
    {
        // Circle->getOrigin() implementation
    }
    public function calculateArea()
    {
        // Circle->calculateArea() implementation
    }
}
```

使用继承和多个接口，结合继承的接口，你可以使用简单的构建模块构建非常复杂且强大的应用程序。

## 魔术方法

为了帮助简化面向对象编程的使用，PHP5 提供了一些所谓的“魔术方法”。这些魔术方法是所有类的特殊命名方法，会在特定场景下自动调用。

到目前为止，你在本章中已经看到了两个魔术方法，`__construct` 和 `__destruct`。它们分别在对象被实例化或被销毁时调用。PHP5 包含一些你可以实现的魔术方法，为你的类提供特殊功能。三个魔术方法——`__call`、`__get` 和 `__set`——都允许你访问对象中未明确定义的方法和属性。第六个，`__toString()`，定义当对象直接用作字符串时发生什么。

## 第 2 章

### `__call`

魔术方法 `__call` 允许你在对象上调用未定义的方法时提供操作或返回值。`__call` 魔术方法可用于模拟方法重载，甚至可以在对象上调用未定义方法时提供平滑的错误处理。`__call` 接收两个参数：未定义方法的名称以及传递给该未定义方法的参数数组。

示例如下：

```php
<?php

class Circle
{
    public function __call($m, $a)
    {
        echo "The method " . $m . " was called.\n" .
             "The arguments were as follows:\n";
        print_r($a);
    }
}

$c = new Circle();
$c->undefinedmethod(1, 'a', 2, 'b');
?>
```

当你运行这段代码时，你将看到类似以下的内容：

```
The method undefinedmethod was called.
The arguments were as follows:
Array
(
    [0] => 1
    [1] => a
    [2] => 2
    [3] => b
)
```

在这里，你定义了一个 `__call` 函数来处理对 `undefinedmethod` 方法的调用。正如预期的那样，它接收了逗号分隔的参数列表，并将其转换为数组，这些数组被 `$a` 参数捕获。

### `__get` 和 `__set`

魔术方法 `__get` 和 `__set` 允许你指定自定义函数，用于存储和检索类中尚未定义的属性中的数据。

`__get` 接收一个参数，即属性的名称，而 `__set` 需要两个：属性的名称和新值。

```php
<?php
class Circle
{
    public function __get($p)
    {
        return $this->$p;
    }

    public function __set($p, $v)
    {
        $this->$p = $v;
    }
}

$c = new Circle();
$c->nonexistent = 5;
echo "The value of our nonexistent property: " . $c->nonexistent;
?>
```

当你执行上述代码时，PHP 会立即识别出类中不存在名为 "nonexistent" 的属性。由于指定的属性不存在，因此调用了 `__set()` 方法，该方法将值分配给新创建的类的属性，从而允许你看到以下内容：

我们不存在属性的值: 5

在这个例子中，你创建了魔术方法 `__get` 和 `__set` 来处理任何未定义的属性访问，并随后使用了一个名为 `nonexistent` 的未定义属性。

## `__sleep`

当你使用 PHP 类存储需要在页面之间或较长时间内持久化的数据时，你可以使用你最喜爱的持久化方法（文件、数据库、会话变量或 Cookie）来存储对象，但对象必须首先进行准备。

当你重新读取要存储的对象数据时，使用 `serialize()` 函数。`serialize()` 函数接受任何复杂的数据结构，并将其转换为可以用你选择的方法存储的字符串。相反，要检索你持久化的数据，请使用 `unserialize()` 函数。`unserialize()` 函数接受你的序列化字符串，并将其转换回原来的复杂结构。

为了给开发者在处理对象序列化时提供更多的灵活性，提供了 `__sleep` 和 `__wakeup` 魔术方法。

如果在类中定义了 `__sleep` 魔术方法，它会在对象被序列化之前自动调用。该方法对于关闭数据库连接和清理对象资源非常有用。

`__sleep` 方法还可以返回一个包含要序列化的对象值名称的数组，这在处理大型对象时很有用。只有必要的数据会被序列化，而其他数据则被忽略。

## `__wakeup`

`__wakeup` 魔术方法执行与 `__sleep` 方法完全相反的操作。当调用 `unserialize()` 时，会自动调用 `__wakeup`，这对于重置对象值、恢复连接以及其他初始化任务非常有用。

看看这个关于 `__sleep` 和 `__wakeup` 的简单示例。这个示例需要两个文件。第一个文件，你将创建为 `page1.php`：

```php
<?php
session_start();

class Circle
{
    public $radius;

    public $origin = array('x'=>0, 'y'=>0);

    public function __sleep()
    {
        echo 'zzzzz';

        return array('radius','origin');
    }

    public function __wakeup()
    {
        echo 'good morning!';
    }
}

$c = new Circle();
$c->radius = 5;
$c->origin['x'] = 3;
$c->origin['y'] = 4;

echo 'Preparing to sleep.....';
$_SESSION['c'] = serialize($c);
echo '<br /><a href="page2.php">Wake the object</a>';
?>
```

你将第二个文件命名为 `page2.php`：

```php
<?php
session_start();

class Circle
{
    public $radius;

    public $origin = array('x'=>0, 'y'=>0);

    public function __sleep()
    {
        echo 'zzzzz';

        return array('radius','origin');
    }

    public function __wakeup()
    {
        echo 'good morning!';
    }

    echo 'Rise and shine......';

    $c = unserialize($_SESSION['c']);

    echo '<br />The contents of our Circle object are:<br />' ;
    echo 'Radius: ' . $c->radius . '<br />' ;
    echo 'Origin: ( ' . $c->origin['x'] . ', ' . $c->origin['y'] . ' )' ;
?>
```

在浏览器中加载第一个页面 `page1.php`，你应该看到类似图 2.1 的内容。

![](img/cacdd24f2926f10ee3219256ad732604_66_0.png)

点击链接，你将被引导到 `page2.php`，在那里你应该看到类似图 2.2 的内容。
