

执行前面的代码时，PHP 会立即识别出该类中不存在名为 'nonexistent' 的属性。由于命名属性不存在，`__set()` 方法会被调用，随后将值赋给新创建的类属性，从而你可以看到以下内容：

> 我们不存在的属性值：5

在这个示例中，你创建了魔术方法 `__get` 和 `__set` 来处理任何未定义的属性访问，并接着使用了一个名为 `nonexistent` 的未定义属性。

## __sleep

当你使用 PHP 类来存储需要在页面之间或长时间段内持久保存的数据时，你可以使用你喜欢的持久化方法（文件、数据库、会话变量或 Cookie）来存储对象，但对象必须首先准备好。

当你重新读取要存储的对象数据时，请使用 `serialize()` 函数。`serialize()` 函数接受任何复杂的数据结构并将其转换为字符串，该字符串可以使用你选择的方法进行存储。相反地，若要取回你持久化的数据，请使用 `unserialize()` 函数。`unserialize()` 函数接受你的序列化字符串并将其转换回原来的复杂结构。

为了给开发人员在处理对象序列化时提供更大的灵活性，提供了 `__sleep` 和 `__wakeup` 魔术方法。

如果在类中定义了 `__sleep` 魔术方法，它会在对象被序列化之前自动调用。该方法对于关闭数据库连接和清理对象资源极其有用。

`__sleep` 方法还可以返回一个包含要序列化的属性名称或对象值的数组，这在处理大型对象时非常有用。只有必要的数据会被序列化，而其他数据可以被忽略。

## __wakeup

`__wakeup` 魔术方法执行与 `__sleep` 方法完全相反的操作。当调用 `unserialize()` 时，`__wakeup` 会被自动调用，这对于重置对象值、恢复连接以及其他初始化任务很有帮助。

下面来看一个简单的 `__sleep` 和 `__wakeup` 实际运行的示例。这个示例需要两个文件。第一个文件，你将创建为 `page1.php`：

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

第二个文件命名为 `page2.php`：

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

    echo 'Rise and shine....';
    $C = unserialize($_SESSION['c']);

    echo '<br />The contents of our Circle object are:<br />';
    echo 'Radius: ' . $C->radius . '<br />'; 
    echo 'Origin: (' . $C->origin['x'] . ',' . $C->origin['y'] . ')';
?>
```

在浏览器中加载第一个页面 page1.php，你应该会看到类似于图 2.1 的内容。

![](img/ab27c6ac898db1f934d39fa127b14657_66_0.png)

点击链接，你会被导向 page2.php，在那里你应该会看到类似于图 2.2 的内容。

![](img/ab27c6ac898db1f934d39fa127b14657_67_0.png)

在第一个文件 page1.php 中，你启动了会话以便将对象存储在会话变量中；然后继续创建圆类的类定义：

```php
<?php
session_start();

class Circle
{
    public $radius;
    public $origin = array('x'=>0, 'y'=>0);

    public function __sleep()
    {
        echo 'zzzz';
        return array('radius','origin');
    }

    public function __wakeup()
    {
        echo 'good morning!';
    }
}
```

请注意，你在这里同时创建了 `__sleep` 和 `__wakeup` 的函数。在这种情况下创建 `__wakeup` 方法并不是必须的，但如果你稍后将类定义移动到一个*include*文件中，你所要做的只是剪切和粘贴。还要注意，你在 `__sleep` 中返回了一个字符串数组。这些字符串与 Circle 内部的属性名称相匹配，告诉序列化函数你希望序列化对象的哪些部分，并忽略其他所有部分。

然后你继续实例化圆对象，更改其部分值，将其序列化为会话变量，最后提供一个链接前往 *page2.php*：

```php
$c = new Circle();
$c->radius = 5;
$c->origin['x'] = 3;
$c->origin['y'] = 4;

echo 'Preparing to sleep.....';

$_SESSION['c'] = serialize($c);

echo '<br /><a href="page2.php">Wake the object</a>';
?>
```

查看 *page2.php*，你再次以启动会话的调用开始，并拥有与前一页相同的类定义。在反序列化对象时，该对象的类定义*必须*在调用 *unserialize()* 函数之前存在，无论是直接输入在文件本身中，还是通过 *include* 或 *require* 语句包含进来。

进入 *page2.php* 的核心内容，你从前一页设置的会话变量中反序列化数据，并将一些新重建对象的属性回显到屏幕上：

```php
echo 'Rise and shine.....';

$c = unserialize($_SESSION['c']);

echo '<br />The contents of our Circle object are:<br />';
echo 'Radius: ' . $c->radius . '<br />';
echo 'Origin: (' . $c->origin['x'] . ', ' . $c->origin['y'] . ' )';
?>
```

## __toString

可以构建到类中的最后一个魔术方法是 `__toString`。正如你可能猜测的那样，`__toString` 返回一个自定义的字符串值，当对象被转换为字符串时会自动使用该值。请看以下示例：

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
echo "The value of $c is: ";
echo $c;
?>
```

执行这段代码时，会产生以下结果：

> The value of $c is: Automatic string value for Circle

在这个示例中，你添加了 `__toString()` 魔术方法，并在对象被回显到屏幕时使用它来提供值。请注意，在之前的 echo 语句中，你并没有简单地将对象拼接到字符串的末尾，也没有将其包含在双引号字符串内部。

如果你简单地将对象与另一个字符串包含在同一个 echo 语句中，究竟会发生什么？请看以下代码（更改部分已高亮显示）：

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
echo "The value of $c is: " . $c;
?>
```

运行这段代码时，你会看到以下内容：

> The value of $c is: Object id #1

这绝对不是你所期望的！它没有返回 `__toString()` 方法的值，而是返回了 $c 的对象 id — 与你未定义 `toString()` 时看到的效果完全一样。`__toString()` 魔术方法仅在与 echo 或 print 直接配合使用时才会被调用 — 如果存在其他字符串或强制转换，则会返回对象 id。

## 摘要

正如你所见，PHP5 为你的项目带来了改进得多的对象模型。无论你决定坚持面向过程的编程，偶尔尝试一下面向对象编程（OOP），完全投身于 OOP 路线，还是在两者之间找到一条路径，希望本章中你看到的一些内容能让你继续开始使用 PHP5 的新 OOP 构建你自己的系统。

从这里开始，你将离开 OOP，进入 PHP 语言中一些较深奥的角落。你可能已经知道数组在 PHP 中有多强大，但你可能并不清楚 PHP 有多少函数可以让你利用这种力量。一旦你掌握了这些，我们将向你介绍流（streams）的概念，这将让你可以使用一组通用的函数来处理网络资源和本地文件。

