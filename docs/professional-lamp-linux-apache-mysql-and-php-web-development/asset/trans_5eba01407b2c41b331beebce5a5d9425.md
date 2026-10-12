
## 第 2 章

### __call

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

### __get 和 __set

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

### __sleep

当你使用 PHP 类来存储必须在页面之间或长时间段内持久存在的数据时，你可以使用你最喜爱的持久化方法（文件、数据库、会话变量或 cookie）来存储对象，但对象必须首先做好准备。

当你重新读取要存储的对象数据时，请使用 `serialize()` 函数。`serialize()` 函数接受任何复杂数据结构并将其转换为字符串，可以使用你的选择方法存储该字符串。相反，要检索你的持久化数据，请使用 `unserialize()` 函数。`unserialize()` 函数接受你的序列化字符串并将其转换回原来的复杂结构。

为了给开发人员在处理对象序列化时提供更大的灵活性，提供了 `__sleep` 和 `__wakeup` 魔术方法。

如果在类中定义了 `__sleep` 魔术方法，它会在对象被序列化之前自动调用。该方法对于关闭数据库连接和清理对象资源非常有用。

`__sleep` 方法还可以返回一个包含要序列化的名称或对象值的数组，这在处理大型对象时非常有用。只有必要的数据会被序列化，而其他数据可以被忽略。

### __wakeup

`__wakeup` 魔术方法执行与 `__sleep` 方法完全相反的操作。当调用 `unserialize()` 时，会自动调用 `__wakeup`，这对于重置对象值、恢复连接以及其他初始化任务很有帮助。

看一下 `__sleep` 和 `__wakeup` 的简单示例。这个示例需要两个文件。第一个文件，你将其创建为 page1.php：

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

第二个文件，你将其命名为 page2.php：

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

将第一个文件 page1.php 加载到浏览器中，你应该看到类似于图 2.1 的内容。

![](img/fd2e7361878181c2b12e30301ff3e182_66_0.png)

**图 2.1**

点击链接，你将进入 page2.php，在那里你应该看到类似于图 2.2 的内容。

![](img/fd2e7361878181c2b12e30301ff3e182_67_0.png)

**图 2.2**

在第一个文件 page1.php 中，你开始会话，以便将对象存储在会话变量中；然后继续创建圆的类定义：

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

        return array('radius', 'origin');
    }

    public function __wakeup()
    {
        echo 'good morning!';
    }
}
```

注意，你在这里创建了 `__sleep` 和 `__wakeup` 两个函数。在这种情况下创建 `__wakeup` 方法并不是必需的，但如果你后来将类定义移动到一个包含文件中，你只需要剪切和粘贴即可。还要注意，你在 `__sleep` 中返回一个字符串数组。这些字符串与 `Circle` 中的属性名称匹配，并告诉序列化函数你要序列化对象的哪些部分，并忽略其他部分。

然后你继续实例化圆对象，更改其中一些值，将其序列化为会话变量，最后提供一个链接前往 `page2.php`：

```php
$c = new Circle();
$c->radius = 5;
$c->origin['x'] = 3;
$c->origin['y'] = 4;

echo 'Preparing to sleep....';

$_SESSION['c'] = serialize($c);

echo '<br /><a href="page2.php">Wake the object</a>';
?>
```

查看 `page2.php`，你再次以启动会话的调用开始，并使用与前一个页面相同的类定义。在反序列化对象时，在调用 `unserialize()` 函数之前，该对象的类定义 *必须* 存在，无论是直接在文件中输入，还是通过 include 或 require 语句包含。

深入 `page2.php` 的核心部分，你从在前一个页面设置的会话变量中反序列化数据，并将新创建对象的一些属性输出到屏幕上：

```php
echo 'Rise and shine....';

$c = unserialize($_SESSION['c']);

echo '<br />The contents of our Circle object are:<br />';
echo 'Radius: ' . $c->radius . '<br />';
echo 'Origin: (' . $c->origin['x'] . ', ' . $c->origin['y'] . ')';
?>
```

### __toString

可以内置到类中的最后一个魔术方法是 `__toString`。你可以猜到，`__toString` 返回一个自定义字符串值，该值在对象被转换为字符串时自动使用。请查看以下示例：

```php
<?php

class Circle
{
    public function __toString()
    {
        return "Automatic string value for Circle";
    }
}

$c = new Circle();
echo "The value of \$c is: ";
echo $c;
?>
```

执行此代码将产生以下结果：

> The value of $c is: Automatic string value for Circle

在这个示例中，你添加了 `__toString()` 魔术方法，并在使用它时，在对象被输出到屏幕时提供了值。注意，你并没有简单地在该 echo 语句中将对象连接到字符串的末尾，也没有将其包含在双引号字符串内。

如果你只是在一个 echo 语句中将对象与其他字符串一起包含会发生什么？请查看以下代码（更改部分已突出显示）：

```php
<?php

class Circle
{
    public function __toString()
    {
        return "Automatic string value for Circle";
    }
}

$c = new Circle();
echo "The value of \$c is: " . $c;
?>
```

当你运行此代码时，你会看到以下内容：

> The value of $c is: Object id #1

这肯定不是你预期的结果！它没有返回 `__toString()` 方法的值，而是返回了 `$c` 的对象 id——这与如果你没有定义 `__toString()` 所看到的完全相同。`__toString()` 魔术方法只有在直接用于 `echo` 或 `print` 时才会被调用——如果存在任何其他字符串或强制类型转换，将返回对象 id。

