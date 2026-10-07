
示例中，`Cat`类继承了`Animal`类的`$name`属性和`eat`方法。它也有自己的方法`meow`。

### 常量

常量是定义后无法更改的变量。在 PHP 中，使用`const`关键字定义常量。

```php
class Config {
    const PI = 3.14159;
}
echo Config::PI;
```

### 静态属性与方法

静态属性和方法属于类本身而不是实例。使用`::`运算符访问它们。

```php
class Counter {
    public static $count = 0;
    public static function increment() {
        self::$count++;
    }
}
Counter::increment();
echo Counter::count;
```

### 接口

接口用于定义类必须实现的方法。它本身不包含任何代码。

```php
interface Shape {
    public function draw();
}
class Circle implements Shape {
    public function draw() {
        return "Drawing a circle.";
    }
}
class Square implements Shape {
    public function draw() {
        return "Drawing a square.";
    }
}
$circle = new Circle();
echo $circle->draw();
$square = new Square();
echo $square->draw();
```

### 抽象类

抽象类是无法实例类。它可以包含抽象方法，这些方法必须由任何子类实现。

```php
abstract class Animal {
    abstract public function makeSound();
    public function sleep() {
        return "Zzz...";
    }
}
class Dog extends Animal {
    public function makeSound() {
        return "Woof!";
    }
}
$dog = new Dog();
echo $dog->makeSound();
echo $dog->sleep();
```

### 特性

特性是单继承层次结构中代码重用的机制。由于 PHP 不支持多重继承，特性非常有用。

```php
trait Flyable {
    public function fly() {
        return "I'm flying!";
    }
}
class Bird {
    use Flyable;
}
class Airplane {
    use Flyable;
}
$bird = new Bird();
echo $bird->fly();
$plane = new Airplane();
echo $plane->fly();
```

嗯，这听起来很不错且符合逻辑——但这些是你已经处理过很多次的简单类型。当 PHP 处理类时，情况变得完全不同（且不符合逻辑了）：

```php
class my_class
{
    var $var1, $var2, $var3;
}
$my_object = new my_class;
```

`$my_object->var1 = 1;`
`$my_object->var2 = 2;`
`$my_object->var3 = 3;`

`$new_object = $my_object;`

`$new_object->var1 = 3;`
`$new_object->var2 = 2;`
`$new_object->var3 = 1;`

```php
print("My object goes $my_object->var1, $my_object->var2, =$my_object->var3!<br>");
print("New object goes $new_object->var1, $new_object->var2, =$new_object->var3!<br>");
```

你认为输出会是什么？脚本首先声明了一个类，创建了它的实例，并为它的三个属性赋值。在此之后，它创建了指向该对象的新引用，重新分配了它的属性，然后通过使用两个引用打印出每个属性。记住，只有一个实例。图 2.7 显示了结果。

![](img/eddeabf7128be657d5f7345abdc760ac_60_0.png)

图 2.7 PHP 创建了副本而不是引用。

# 第 2 章 高级语法

如果你现在并不感到惊讶，那你要么已经非常熟悉 PHP，要么还没有对对象进行足够的思考。PHP 创建了一个副本即`my_class`的新实例，而不是仅仅是一个新引用！这不是期望的行为，因为`new`运算符本应该在内存中创建一个`my_class`的实例，并返回它的引用。因此，当赋值给另一个变量时，应该只复制引用，让原始数据保持不变——这类似于文件系统的链接，允许通过文件系统上的不同位置访问数据。PHP 的这种行为——创建被引用数据的副本而非仅仅是引用——听起来可能并不重要；然而，稍后你就会发现它实际上会产生影响。

注意：在你写作时，PHP 3.0 和 PHP 4.0 使用拷贝语法。与核心开发人员的对话透露，计划是将默认行为更改为使用引用语法，但这种更改会导致向后兼容性的丢失。在 4.1 版本中计划了一个可能的更改——如果此处包含的信息对所有未来版本都将失效。

PHP 3.0 没有实现完善的垃圾回收。每当你向变量写入内容时，系统都会分配新空间而不是重用旧空间。`unset()`可以在一定程度上解决这个问题——尽管它没有释放内存，但将其标记为可重用——然而，在一段时间后，长期运行脚本将确保你使用（例如）`mysql_free_result()`释放数据库结果，对所有不再包含有用信息的变量使用`unset()`。在脚本终止之前，没有任何内存会被释放！

例如，一个树形结构。构建树节点的类看起来像这样：

```php
class tree_node
{
    var $left_child, $right_child;
    var $value;
}
```

当然，只是一个简单的树节点，但它包含了我们需要的一切：指向左子节点的链接和指向右子节点的链接，以及一个包含该节点内容的变量。我们将构建一个简单的树：

```php
$root_node = new tree_node;
$left_node = new tree_node;
$right_node = new tree_node;
```

```php
$root_node->value = 1;
$left_node->value = 2;
$right_node->value = 3;
```

```php
$root_node->left_child = $left_node;
$root_node->right_child = $right_node;
```

这段代码简单地构建了一个有一个根节点和两个子节点的树，并为它们每一个分配了不同的值。可以通过这样的函数完成树遍历：

```php
function traverse_tree($start_node)
{
    $node = $start_node;
    print('Value is $node->value<br>');
    print('Traversing left tree:<br>');
    traverse_tree($node->left);
    print('Traversing right tree:<br>');
    traverse_tree($node->right);
}
```

暂忘记这个递归函数永远不会返回，因为我们的树没有设置停止标记（函数不知道哪个节点实际上有子节点，哪个节点没有），让我们来看看它是工作的以及 PHP 将如何处理它。

关键点已经出现在第一行，即`$node`正在被赋值。作为参数的`$start_node`包含了起始节点的实例，而赋值给`$node`将创建它的一个副本。对于一个仅仅递归遍历树并打印节点内容的函数来说，其副本与并不重要，但当你计划在某处更改树时，这可能非常重要。

现在假设你想写一个函数向树的最左侧叶子节点添加一个新节点。没问题——只需写一个计算叶子节点的递归函数即可。

## PHP 与 OOP

对于不同的 PHP 版本，我们仍然持怀疑态度。我们听过双方的意见——一方坚持对象是垃圾，不应该在像 PHP 这样的语言中使用；另一方则在 3.0 中认为对象优于任何过程化方法。对于那些只使用过程化的人来说，对象似乎是一个最好不要触碰的野兽；对于 OOP 派来说，“PP”（过程化的人者）是白痴。这几乎像是一场宗教战争。每当我们提到这个话题，很快就会引发无休止且不安的讨论。

我们诚实地认为两个极端都是错误的。忽视特性绝不是明智之举，在不考虑缺点的情况下使用特性同样不如此。我们不喜欢说这是一个个人偏好的问题，因为技术不应该是这样的。我们的建议是：消除你可能有的任何偏见——尤其是他人的偏见——然后客观地判断对你的项目最好的方案。

### 类: 3.0

数据：不要使用类来实现需要指针的复杂数据结构（如树）。如果必须，将类的使用限制在数据收集而非数据管理上。代码：仅使用类来构建不受拷贝影响的 API。

### 类: 4.0

类在 PHP 4.0 中得到了改进，但我们仍然持怀疑态度。

### 实现类

尽管有优劣，类是一项重要的语言元素，而且似乎一直存在 PHP 类实现的需求。

PHP 中的类实现非常简单。你将从其他语言中熟悉大部分的关键字：

```php
class shopping_cart
{
    var $item_list;
    function pick($item, $quantity)
    {
        $this->item_list[$item] += $quantity;
```

## 48 第 2 章 高级语法

```php
function drop($item, $quantity)
{
    if($this->item_list[$item] > $quantity)
        $this->item_list[$item] -= $quantity;
    else
        $this->item_list[$item] = 0;
}
```

这段代码定义了`shopping_cart`类，包含成员`$item_list`、`pick()`和`drop()`。注意，这里没有区分公共（public）和私有（private）成员的方法。在 PHP 中，一切默认都是公共的——这意味着你可以从外部无限制地访问类的所有属性和成员函数。这个简单的类实现了一个某种购物车（如名所示），包含一个使用关联数组`$item_list`的变量来存储购物车内容，以及两个函数`pick()`和`drop()`，用于添加和移除物品。成员函数的声明方式与普通函数一样，不同之处它们是在类定义内部实现的。类属性（类内部的变量）使用`var`关键字定义。

> 注意：在 PHP 中，无法将类的声明和实现分开。你必须直接在类声明中实现所有函数。

### 访问对象

成员函数可以通过“旧”的语法`instance->member()`或“新”的语法`instance::member()`来调用。同样，属性通过`instance->property`或`instance::property`访问。后者形式对于调用父类的构造函数或访问未位于当前对象中的其他成员特别有用（关于该主题将在后文的“继承”章节中详细介绍）。

```php
class extended_cart extends shopping_cart
{
    function extended_cart()
    {
        shopping_cart::shopping_cart("Mousepad", 1);
    }
    function query($item)
    {
        return($this->item_list[$item]);
    }
}
```

这个扩展的`extended_cart`对象包含一个构造函数，它调用父类的构造函数来正确初始化对象树的其他部分。注意，如果没有在这个构造函数中显式地调用父类构造函数，PHP 还提供了指向对象当前实例的别名。这个别名名为`this`，并允许访问实际实例化的所有成员。这对于所有自引用都是必要的；PHP 并没有在类定义内部引入新的局部作用域，请确保你在任何进行引用的地方都包含了该关键字。忘记使用它将指示 PHP 指向全局作用域，这非常容易产生错误；

### 构造函数

构造函数的定义也与普通函数一样，但它们的名称必须与类名相同。PHP 没有析构函数。构造函数可以像任何其他函数一样接受参数——可选参数（更多细节请参见后文关于变量列表的章节）。

> 注意：从 PHP 4.0 开始，构造函数只能接受标量值（字符串、整数等）作为参数，而不能接受数组或对象，这在 PHP 3.0 中是可以可能的。

要给前面的示例添加构造函数，我们可以添加一小段代码：

```php
class shopping_cart
{
  var $item_list;
  function shopping_cart($item = 'T-Shirt', $quantity = 1)
  {
    $this->pick($item, $quantity);
  }
  function pick($item, $quantity)
  {
    $this->item_list[$item] += $quantity;
  }
  function drop($item, $quantity)
  {
    if($this->item_list[$item] > $quantity)
      $this->item_list[$item] = $quantity;
    else
      $this->item_list[$item] = 0;
  }
}
```

包含在`shopping_cart::shopping_cart()`中的构造函数接受两个可选参数——如果未指定参数，在实例化时，购物车将自动“预填充”一件 T 恤。否则，它将接受所需的物品：

```php
$default_cart = new shopping_cart; // 此购物车默认将自己填充一件 T 恤
$mug_cart = new shopping_cart("Mug", 2); // 此购物车将包含两个马克杯
```

### 继承

向对象添加函数应该通过通过重载结构来重写旧代码来完成。新对象可以使用`extends`关键字继承自旧对象。如名所示：

```php
class extended_cart extends shopping_cart
{
  function query($item)
  {
    return($this->item_list[$item]);
  }
}
```

这个扩展后的`extended_cart`现在包含了来自`shopping_cart`的所有属性和成员函数，并增加了另一个函数`query()`，它允许我们检查购物车中任何给定物品的数量。

注意：`extended_cart`类没有它自己的构造函数。如果子类没有构造函数，PHP（从 4.0 版本开始）会自动调用父类的构造函数。然而，默认情况下 PHP 永远不会调用父类的构造函数。因此，如果你需要设置父对象，请确保你手动调用它的构造函数。

### 特殊 OOP 函数

PHP 提供了一些实用的函数，让处理对象变得更容易。下表描述了这些函数。

| 函数 | 描述 |
| --- | --- |
| string `get_class(object object)` | 以字符串形式返回指定对象的实例名称。 |
| bool `is_a(object object, string class)` | 判断对象是否是某个类的实例。 |
| bool `is_subclass_of(object object, string class)` | 判断对象是否为类的子类。 |
| bool `method_exists(object object, string method)` | 判断对象中是否存在该方法。 |
| bool `property_exists(object object, string property)` | 判断对象中是否存在该属性。 |

这个想法并不新。它起源于多年前，而且并不难理解。它不是在每个节点中携带一个指向内存中下一个节点的指针，而是每个节点都包含指向其链接的每个节点的数组索引。这种做法的另一个优点是，PHP 能够向你警告无效的索引，而且你只需要将包含树数组的变量赋值给另一个变量，就可以复制整棵树。此外，你还可以将整个树序列化，并将其“原封不动”保存到你想的任何地方。

为了给出更有理论性的解释：将你的程序可用的内存想象为一个巨大的数组。在物理 RAM 的情况下，元素的大小可能是字节，但每个元素的大小实际上并不重要。重要的是，指针仅仅是指向这些元素之一的数字，从而指向你放置在 RAM 中的每个结构的开头。现在，将整个过程抽象化为语言构造结构（一个“真实”数组），你在更高层级上面临着相同的情况：PHP 数组现在包含了你的“RAM”，而每个数组元素将代表一个树节点。指针变成了该数组的索引，而引用简单地通过从数组中检索正确的元素来完成。

使用数组允许你创建许多“RAM”，增加或减少它们的大小，整体丢弃它们或仅丢弃单个元素；总体来说，非常非常舒适内存管理方法。将所有内容集成到一个健壮的库中为你提供了一个很好的工具。

图 2.9 显示了树库内部如何在数组中处理树节点。
