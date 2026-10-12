
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

结合继承和多个接口，以及继承的接口，您可以使用简单的构建块构建一些非常复杂且功能强大的应用程序。

## 魔术方法

为了在使用面向对象编程时使事情变得更加容易，PHP5 提供了一些所谓的“魔术方法”。这些魔术方法是所有类中特殊命名的方法，在特定场景中会被自动调用。

到目前为止，本章中您已经看到两个魔术方法，`__construct` 和 `__destruct`。它们分别在对象被实例化或销毁时被调用。PHP5 包含一些您可以实现的魔术方法，为您的类提供特殊功能。三个魔术方法—— `__call`、`__get` 和 `__set`——都允许您访问对象中未显式定义的方法或属性。第六个，`__toString()`，定义了当对象直接用作字符串时发生的事情。

## 第 2 章

### `__call`

魔术方法 `__call` 允许你在对象调用未定义方法时提供动作或返回值。`__call` 魔术方法可用于模拟方法重载，甚至可以在对象调用未定义方法时提供平滑的错误处理。`__call` 接受两个参数：方法名称以及传递给未定义方法的参数数组。例如：

```php
<?php

class Circle
{
    public function __call($m, $a)
    {
        echo "The method " . $m . " was called.\n".
             "The arguments were as follows:\n";
        print_r($a);
    }
}

$c = new Circle();
$c->undefinedmethod(1, 'a', 2, 'b');
?>
```

当你运行此代码时，你会看到类似以下内容：

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

在这里，你定义了一个 `__call` 函数来处理对 `undefinedmethod` 方法的调用。正如预期的那样，它接收逗号分隔的参数列表，并将其转换为数组，该数组被存储在 `$a` 参数中。

### `__get` 和 `__set`

魔术方法 `__get` 和 `__set` 允许你指定自定义函数来存储和检索类中尚未定义的属性中的数据。

`__get` 接受一个参数，即属性名称，而 `__set` 需要两个参数：属性名称和新值。

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
$c->nonexistant = 5;
echo "The value of our nonexistant property: " . $c->nonexistant;
?>
```

当你执行上述代码时，PHP 会立即识别出类中不存在名为 'nonexistant' 的属性。由于该命名属性不存在，`__set()` 方法被调用，然后将值赋给类中新创建的属性，从而允许你看到以下内容：

```
The value of our nonexistant property: 5
```

在这个示例中，你创建了魔术方法 `__get` 和 `__set` 来处理任何未定义属性的访问，并继续使用了名为 `nonexistant` 的未定义属性。

### `__sleep`

当你使用 PHP 类来存储必须在页面之间或长时间段内持久存在的数据时，你可以使用你最喜爱的持久化方法（文件、数据库、会话变量或 cookie）来存储对象，但对象必须首先做好准备。

当你重新读取要存储的对象数据时，请使用 `serialize()` 函数。`serialize()` 函数接受任何复杂数据结构并将其转换为字符串，可以使用你的选择方法存储该字符串。相反，要检索你的持久化数据，请使用 `unserialize()` 函数。`unserialize()` 函数接受你的序列化字符串并将其转换回原来的复杂结构。

为了给开发人员在处理对象序列化时提供更大的灵活性，提供了 `__sleep` 和 `__wakeup` 魔术方法。

如果在类中定义了 `__sleep` 魔术方法，它会在对象被序列化之前自动调用。该方法对于关闭数据库连接和清理对象资源非常有用。

`__sleep` 方法还可以返回一个包含要序列化的名称或对象值的数组，这在处理大型对象时非常有用。只有必要的数据会被序列化，而其他数据可以被忽略。

### `__wakeup`

`__wakeup` 魔术方法执行与 `__sleep` 方法完全相反的操作。当调用 `unserialize()` 时，会自动调用 `__wakeup`，这对于重置对象值、恢复连接以及其他初始化任务很有帮助。

看一下 `__sleep` 和 `__wakeup` 的简单示例。这个示例需要两个文件。第一个文件，你将其创建为 `page1.php`：

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

第二个文件，你将其命名为 `page2.php`：

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

    echo 'Rise and shine.....';

    $c = unserialize($_SESSION['c']);

    echo '<br />The contents of our Circle object are:<br />';
    echo 'Radius: ' . $c->radius . '<br />';
    echo 'Origin: (' . $c->origin['x'] . ',' . $c->origin['y'] . ')';
?>
```

将第一个文件 `page1.php` 加载到浏览器中，你应该看到类似于图 2.1 的内容。

![](img/fd2e7361878181c2b12e30301ff3e182_66_0.png)

**图 2.1**

点击链接，你将进入 `page2.php`，在那里你应该看到类似于图 2.2 的内容。
