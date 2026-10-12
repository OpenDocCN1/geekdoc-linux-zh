

## RecursiveIterator

`RecursiveIterator` 类有助于实现递归迭代，即自动重复调用函数直至满足特定条件。该类的函数可帮助你判断是否存在子迭代器，以及这些子迭代器可能是什么。

## ArrayIterator

使用 `ArrayIterator` 内置类，你可以在迭代对象的同时修改 `array` 的值和键。它允许你在每次迭代时操作数组。诸如 `append()`、`copy()` 和 `seek()` 等函数使开发者能够以超出常规数组函数集的方式处理数组。

迭代器正在不断得到改进和增强，你可以预期在 PHP 5.1 中看到一些重大变化。

## 构造方法与析构方法

在 PHP4 中，你可以通过将方法命名为与类名相同的方式，在类中立即调用该方法。在 PHP5 中，为此目的引入了一个新的“魔术方法”名称，即 `__construct()`。在类中包含此方法后，当对象创建时会自动调用它。

同样，如果在类中包含魔术方法 `__destruct()`，对象将被销毁。此方法在被调用时销毁对象。如果没有更多对对象的引用，或者到达 PHP 脚本的末尾时，`__destruct()` 方法也会被调用。

第 2 章将更深入地讨论构造方法和析构方法。

## 访问修饰符

现在，你可以使用 PHP5 新增的三个关键字来控制类成员和方法的可见性级别：`public`、`private` 和 `protected`。方法和成员被标记为 `public`、`private` 或 `protected`。

以下是关于 `private`、`protected` 和 `public` 关键字的简要总结（你可以在第 2 章阅读有关这些特性的更多内容）：

-   `Public`（公开）：这些成员和方法对整个脚本可用。它们可以在对象内部或对象外部引用。
-   `Protected`（受保护）：标识为受保护的成员或方法仅在对象内部或继承类中可用。
-   `Private`（私有）：私有方法和成员仅在对象本身内部可用，对任何继承类都不可用。

## final 关键字

`final` 关键字可与类或类内的方法一起使用。当与类一起使用时，此关键字阻止任何其他类继承该类。当与方法一起使用时，它阻止任何继承类重写该方法，从而有效确保其永久性，并保护它们不受其他程序员甚至你自己的影响。

## static 关键字

将成员或方法声明为 *static*（静态）会将其绑定到它所属的类，而不是类的任何单个对象或实例。静态成员和方法可在整个脚本中访问。

关于使用 *static* 关键字有一些重要的注意事项。首先，不要使用 `$this->varName` 语法从类内部访问变量，而应使用 `self::$varName`。在之前的示例中，你从一个不同的函数中访问了 `self::$count` 成员，但由于静态成员对类内部的一切都可用，因此仍然使用了 `self::` 语法。其次，当从类外部访问静态成员时，应使用语法 `className::$varName`。同样，当在类内部任何地方访问静态方法时，应使用 `self::methodName()`；当从类外部访问时，应使用 `className::methodName()`。

关于使用 *static* 关键字的更详细讨论将在第 2 章中进行。

## abstract 关键字

当你有一个高级类，知道它将被更具体、更低的类继承时，使用 abstract 关键字。例如，你可以如下使用抽象类和方法：

```php
<?php
    abstract class getToday {
        public $today = getdate();
        abstract function showCalendar();
    }
    class monthlyCalendar extends getToday {
        function showCalendar() {
            //显示本月的日历
        }
    }
    class dailyCalendar extends getToday {
        function showCalendar() {
            //显示今天的每日日历
        }
    }
    class yearlyCalendar extends getToday {
        function showCalendar() {
            //显示今年的日历
        }
    }
?>
```

这个抽象类基本上说“创建一个日历，但然后在子类中指定其类型”。如你所见，第一个类中的 `showCalendar()` 函数被故意留空并设为抽象，因为该类应该被扩展，并根据调用的继承类显示适当的日历。`getToday()` 类是不完整的，是抽象化的完美候选者。抽象方法（如同接口中的方法）实际上是空的，需要在子类中进一步实现。

使用抽象类时的一些规则包括：

-   如果你有抽象方法，整个类也必须定义为抽象。
-   你不能实例化抽象类。
-   你可以将一个类定义为抽象类，即使它不包含任何抽象方法。
-   实现抽象方法的继承类必须具有与其父类相同（或更弱）的可见性。

在第 2 章中，我们将更详细地讨论抽象。

## 内置方法重载函数

与 PHP4 不同，在 PHP4 中你必须使用 `overload()` 函数来强制进行重载检查，而 PHP5 原生允许你对任何不符合预期的方法或成员引用进行重载，从而有效地让你控制接下来发生的事情。新的魔术方法 `__get()`、`__set()` 和 `__call()` 用于重载，如下所示：

```php
<?php

class overload {

  function __get($property) {
    //检查属性是否存在于类中
    //如果不存在，执行我们想要执行的操作
    //例如显示错误。否则返回
    //一个值。
  }

  function __set($property, $value) {
    //检查属性是否存在于类中
    //如果存在，将其设置为传入的值
    //否则执行我们想要执行的操作，例如
    //显示错误。
  }

  function __call($method, $array_of_arguments) {
    //检查方法是否存在于类中
    //如果不存在，执行某些操作，例如将其委托给
    //包含该方法的另一个类或
    //打印错误语句。
  }
}
?>
```

第 2 章将更详细地讨论重载。

## 新函数

以下是 PHP5 中所有新函数的综合列表，不包括那些需要扩展的函数：

-   `array_combine()`: 将两个数组合并为一个，使用其中一个数组作为值，另一个数组作为键。
-   `array_diff_uassoc()`: 通过命名字典确定两个或多个数组之间的差异，并进行额外的键比较。
-   `array_udiff()`: 通过使用命名字典进行数据比较，确定两个或多个数组之间的差异。
-   `array_udiff_assoc()`: 通过使用命名字典进行数据比较，并进行额外的键比较，确定两个或多个数组之间的差异。
-   `array_udiff_uassoc()`: 通过使用命名字典进行额外的键比较，以及通过命名字典进行数据比较，确定两个或多个数组之间的差异。
-   `array_intersect()`: 通过使用命名字典进行数据比较，确定两个或多个数组之间的交集。
-   `array_intersect_assoc()`: 通过使用命名字典进行数据比较，并进行额外的键比较，确定两个或多个数组之间的交集。
-   `array_intersect_uassoc()`: 通过使用命名字典进行额外的键比较，以及通过命名字典进行数据比较，确定两个或多个数组之间的交集。
-   `array_walk_recursive()`: 对数组的每个元素递归地应用命名字典。
-   `convert_uudecode()`: 解码 uuencoded 字符串。
-   `convert_uuencode()`: 对字符串进行 uuencode 编码。
-   `curl_copy_handle()`: 复制 cURL 句柄及其所有偏好设置。
-   `date_sunrise()`: 基于给定的纬度、经度、天顶角和 GMT 偏移量返回日出时间。
-   `date_sunset()`: 基于给定的纬度、经度、天顶角和 GMT 偏移量返回日落时间。
-   `dba_key_split()`: 将字符串表示中的索引拆分为数组表示。
-   `dbase_get_header_info()`: 返回 dBase 数据库的列结构信息。

