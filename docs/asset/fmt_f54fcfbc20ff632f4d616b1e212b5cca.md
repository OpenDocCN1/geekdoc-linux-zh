
该 SQL 查询将从包含信息的表中选择 `car_type`、`car_color` 和 `car_speed`。查询结果通过 `mysql_fetch_row()` 获取，该函数以数组形式返回值。`car_type` 将位于索引 0，`car_color` 索引 1，`car_speed` 位于索引 2。从左到右读取，这些值将按值赋值给 `list()` 语句中提供的参数。

因此，你将得到以下赋值：

### 列表参数 SQL 字段

| `$car_type` | `car_type` (数组索引 0) |
| `$car_color` | `car_color` (数组索引 1) |
| `$car_speed` | `car_speed` (数组索引 2) |

当你想要将一组值拆分为单个变量时，`list()` 语句非常有用——这在数据库编程中经常发生。但注意，`list()` 只能作为左值（lvalue），不能作为右值（rvalue）——你不能使用 `list()` 来交换一组变量。例如，以下语句不起：
`list($var1,$var2) = list($var2,$var1);`

`each()` 语句通常与 `list()` 语句结合使用。`each()` 遍历数组并以键值对的形式返回每个元素。这是通过“遍历”输入数组实现的。PHP 为每个数组分配了一个内部指针。该指针指向数组的第一个元素。每次调用 `each()` 都会返回内部指针指向的元素；该指针会递增。

## 数组函数 35

键值对的返回格式是一个包含四个元素的数组，键分别为 "0"、1"、key" 和 "value"。这意味着它既可以作为索引数组，也可以作为关联数组使用。数组的索引部分（键为 "0" 和 "1"）包含源元素在索引 0 处的键；值可以在索引 1 找到。可以使用数组的关联部分访问相同的信息。（实际上，将数组分为关联部分和索引部分是不正确的，因为索引数组只是关联数组的特殊形式——从理论上说，它们是不同的，但在 PHP实践中是相同的。详情请参见后文。）源元素的键包含在 "key" 中，值包含在 "value" 中。例如：`$my_array = array("Element 1", "Element 2", "Element 3");`

这将创建一个包含以下内容的数组：

- Element 1
- Element 2
- Element 3

为了更好地理解 `each()` 背后的原理，为此数组创建一个更详细的列表是有用的：

| 键 (Key) | 值 (Value) |
| 0 | Element 1 |
| 1 | Element 2 |
| 2 | Element 3 |

这是数组 `$my_array` 中包含的所有键值对的列表。现在我们对它使用 `each()`：

```php
list($key, $value) = each($my_array);
```

第一次调用 `each()` 返回第一个包含 `$my_array` 中第一个键值对的四元素数组。注意，由于我们只给 `list()` 运算符提供了两个参数，只有四元素数组中的值可以被赋值：这些是 "0"、第一个键以及来自 `$my_array` 的第一个值元素 "Element 1"。

以下代码列出了数组的内容：

```php
$my_array = array("Element 1", "Element 2", "Element 3");

while(list($key, $value) = each($my_array)) {
    print("Key: $key, Value: $value<br>");
}
```

该脚本产生的输出如图 2.1 所示。

## 36 第 2 章 高级语法

![](img/eddeabf7128be657d5f7345abdc760ac_53_0.png)

图 2.1 使用 each() 的数组列出。

你也可以使用 `each()` 来显示 `each()` 返回的元素：

```php
$my_array = array("Element 1", "Element 2", "Element 3");

while($four_element_array = each($my_array)) {
    while(list($key, $value) = each($four_element_array)) {
        print("Key $key, Value $value<br>");
    }
}
```

这将产生如图 2.2 所示的结果。

![](img/eddeabf7128be657d5f7345abdc760ac_53_1.png)

图 2.2 each() 的返回值。

你可以在输出中清晰地看到条目 1, value, 0，且 0 和 1 像“key”和“value”一样配合使用。注意每对代表源数组的一个条目。

在索引数组上使用 `each()` 初看起来可能并不合理，因为数组的元素

## 54 数组函数 37

在索引数组上使用 `each()` 初看起来可能并不合理，因为数组的元素

## 数组函数 37

在索引数组上使用 `each()` 初看起来可能并不合理，因为数组的元素

| 键/索引 (Key/Index) | 值 (Value) |
| 0 | Landon |
| 3 | Graeme |
| 4 | Tobias |
| 10 | Till |

在索引数组上使用 `each()` 初看起来可能并不合理，因为数组的元素

### 错误报告

在索引数组上使用 `each()` 初看起来可能并不合理，因为数组的元素

## 第 55 章 高级语法

在索引数组上使用 `each()` 初看起来可能并不合理，因为数组的元素

## 数组函数 39

此函数使 PHP 的内部指针移动数组的第一个元素，该元素的值也是 `reset()` 的返回值。

以下脚本在两个不同的循环中两次访问同一个数组，两者都使用了 `each()`：

```php
$my_array = array("Landon" => 1, "Graeme" => 2, "Tobias" => 3, "Till" => 4);
```

```php
print("<h2>没有 reset() 的循环</h2>");
```

```php
print("<h3>第一次循环</h3>");
```

```php
for($i = 0; $i < 2; $i++) {
    list($key, $value) = each($my_array);
    print("$Key $key, Value $value<br>");
}
```

```php
print("<h3>第二次循环</h3>");
```

```php
for($i = 0; $i < 2; $i++) {
    list($key, $value) = each($my_array);
    print("$Key $key, Value $value<br>");
}
```

如图 2.5 所示，第二次循环*不会再次从第一个元素开始*；它将从第一次循环停止的地方继续。这是由于 PHP 的内部数组指针没有重置导致的。对脚本进行微小的修改会产生不同的结果（见图 2.6）：

```php
$my_array = array("Landon" => 1, "Graeme" => 2, "Tobias" => 3, "Till" => 4);
```

```php
print("<h2>带有 reset() 的循环</h2>");
```

```php
print("<h3>第一次循环</h3>");
```

```php
for($i = 0; $i < 2; $i++) {
    list($key, $value) = each($my_array);
    print("$Key $key, Value $value<br>");
}
```

```php
print("<h3>调用 reset()</h3>");
```

```php
reset($my_array);
```

```php
print("<h3>第二次循环</h3>");
```

```php
for($i = 0; $i < 2; $i++) {
    list($key, $value) = each($my_array);
    print("$Key $key, Value $value<br>");
}
```

# 第 2 章 高级语法

![](img/eddeabf7128be657d5f7345abdc760ac_57_0.png)

图 2.5：没有 reset() 的循环

![](img/eddeabf7128be657d5f7345abdc760ac_57_1.png)

图 2.6：带有 reset() 的循环

以下脚本在两个不同的循环中两次访问同一个数组，两者都使用了 `each()`：

如图 2.5 所示，第二次循环*不会再次从第一个元素开始*；它将从第一次循环停止的地方继续。这是由于 PHP 的内部数组指针没有重置导致的。对脚本进行微小的修改会产生不同的结果（见图 2.6）：

## 面向对象编程 vs 过程式编程

在 90 年代，面向对象编程（OOP）成为了一种流行的编写代码方式。在此之前，大多数程序员使用过程式编程。在过程式编程中，数据存储在变量并在函数之间传递。而在 OOP 中，数据封装在对象内部，这使得代码更安全且更容易维护。

另一个区别是 OOP 中的继承，它允许类从另一个类继承属性和方法。在过程式编程中，没有继承的概念，如果需要相似的功能，必须复制代码。OOP 还支持多态，允许将不同的对象被视为同一个基类的实例。总的来说，对于大型复杂的项目，OOP 被认为更好，因为它允许代码重用。然而，过程式编程对于小型任务。

### 类与对象

类是对象的蓝图。它定义了对象将拥有的属性和方法。对象是类的实例。

```php
class Dog {
    public $name;
    public $breed;
    public function __construct($name, $breed) {
        $this->name = $name;
        $this->breed = $breed;
    }
    public function bark() {
        return $this->name . " says woof!";
    }
}
$myDog = new Dog("Buddy", "Golden Retriever");
echo $myDog->bark();
```

示例中，`Dog` 类有两个属性 `$name` 和 `$breed`，以及两个方法 `__construct` 和 `bark`。`__construct` 方法是在创建新对象时调用的特殊方法。`bark` 方法返回一个狗叫的字符串。

### 属性与方法

属性是属于对象的变量。方法是属于对象的函数。你可以使用 `->` 运算符访问和修改属性。

```php
class Car {
    public $color;
    public $model;
    public function setColor($color) {
        $this->color = $color;
    }
    public function getColor() {
        return $this->color;
    }
}
$myCar = new Car();
$myCar->setColor("red");
echo $myCar->getColor();
```

示例中，`Car` 类有两个属性 `$color` 和 `$model`，两个方法 `setColor` 和 `getColor`。`setColor` 方法设置 `$color` 属性的值，`getColor` 方法返回 `$color` 属性的值。

### 方法：构造函数与析构函数

构造函数是在创建新对象时调用的特殊方法。析构函数是在对象销毁时调用的特殊方法。

```php
class User {
    public $name;
    public function __construct($name) {
        $this->name = $name;
        echo "Object created for user: $this->name\n";
    }
    public function __destruct() {
        echo "Object destroyed for user: $this->name\n";
    }
}
$user = new User("Alice");
unset($user);
```

示例中，当创建 `User` 对象时执行 `__construct` 方法，当使用 `unset()` 销毁对象时执行 `__destruct` 方法。

### 继承

允许一个类从另一个类继承属性和方法。基类被称为父类，派生类被称为子类。

```php
class Animal {
    public $name;
    public function eat() {
        return "$this->name is eating.";
    }
}
class Cat extends Animal {
    public function meow() {
        return "$this->name says meow!";
    }
}
$cat = new Cat();
$cat->name = "Whiskers";
echo $cat->eat();
echo $cat->meow();
```
