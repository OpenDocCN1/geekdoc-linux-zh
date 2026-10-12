
## 面向对象

在 PHP 5 之前，PHP 的面向对象功能充其量只是语法糖——它看起来不错，但只是一种花哨的操作方式，并没有带来任何优势。然而，从 v5 开始，在恰当的使用者手中，面向对象（OOP）已成为一种强大的工具。因此，如果你花时间彻底学习它，你的代码将会受益。

如果你之前使用过 Java，那么在 PHP 中你会感觉很熟悉，因为 Java 中的几乎所有特性在 PHP 中都有，且实现方式非常相似。本章面向没有面向对象编程（OOP）知识的读者，因此如果你已经有经验，本章的许多内容对你来说只是复习。

### 面向对象简介

*面向对象编程* 是一种将代码中的实体表达为类和对象的系统。*类* 是实体的定义。例如，你可能会定义一个汽车类或一个铅笔类。*对象* 是类的实例。例如，使用你的汽车类，你可以创建 10 个汽车对象。在定义汽车类时，你可以为它提供存储汽车相关变量的属性（如颜色、型号等），以及汽车特定的功能（如 *brake()*、*changeGear()* 等）。当你创建一个汽车的实例时，该对象将获得一组独立的变量和函数，这些不与其他汽车共享。

使用 *class* 关键字和函数及变量列表来定义类。然后，你可以使用 *new* 运算符创建该类的实例，它会返回类中的一个新对象。在 PHP 中，这看起来是这样的：

```php
<?php
class car {
    public function brake() {
        echo "Car is braking...\n";
    }

    public function changeGear($gear) {
        echo "Car is changing gear to $gear\n";
    }
}
?>
```

这里我们有一个汽车类，包含两个函数：`brake()` 和 `changeGear()`。请注意函数的书写方式：第一个字母小写，后续单词的首字母大写。这被称为 *驼峰式命名法*（camel caps）或 *首字母大写式命名法*（studly caps），它只是一种有助于提高可读性的编码约定。

其次，请注意 `function` 关键字前面的 `public` 一词。PHP 实现了一套完整的 PPP（公有、私有、受保护）系统，这意味着你拥有私有函数和变量、公有函数和变量、以及受保护函数和变量。它们各自有不同的作用，你需要牢固掌握它们之间的区别才能理解 OOP（我们在“访问修饰符”一节中对此进行了讨论）。

接下来，我们需要创建该汽车的一个实例来使用其功能：

```php
$viper = new car; 
$viper->changeGear(1); 
$viper->changeGear(2); 
$viper->brake();
```

这将输出以下内容：

```
Car is changing gear to 1
Car is changing gear to 2
Car is braking...
```

### 对象变量与 $this

考虑以下代码：

```php
$viper = new car; 
$concorde = new car; 
$viper->changeGear(1); 
$viper->changeGear(2); 
$concorde->brake();
```

虽然代码看起来很不同，但输出是完全相同的，因为我们目前无法区分不同的汽车。我们需要创建一个函数 `setName()`，为每辆汽车赋予一个名称。这意味着我们需要将名称存储在汽车内部，并在调用其他函数时打印它。

向类中添加变量很简单——在 `class car` 行下方添加这一行：

```php
public $name;
```

同样，请注意这里有 `public`；否则你可以忽略它。将这个 `setName()` 函数放在 `$name` 行下方：

```php
public function setName($newname) { 
  $this->name = $newname; 
  echo "Car name changed to $newname\n"; 
}
```

第一行是标准的，但第二行引入了 $this 变量。类的每个实例都有自己的一组变量，因此 PHP 使用 $this 变量来指代调用了该函数的那个对象。如果你调用 $concorde->brake()，那么 $this 就是 $concorde；如果你调用 $viper->brake()，那么 $this 就是 $viper。

设置对象变量的方式非常具体。你不要使用 $name = ... 或 $this->$name = ...——前者设置了一个名为 $name 的新局部变量，而后者查找局部变量 name 的值并将其用作变量变量。也就是说，如果 $name 是 wombat，它会设置 $this->$wombat。请记住，除非你想使用变量变量，否则 PHP 变量永远只有一个美元符号！

设置好变量后，我们可以修改其他两个函数以打印名称，从而区分不同的汽车。最终脚本如列表 31.10 所示。

#### 列表 31.10 通过名称区分的多辆汽车

```php
<?php
class car {
    public $name;

    public function setName($newname) {
        $this->name = $newname;
        echo "Car name changed to $newname\n";
    }

    public function brake() {
        echo "Car $this->name is braking...\n";
    }

    public function changeGear($gear) {
        echo "Car $this->name is changing gear to $gear\n";
    }
}

$viper = new car;
$concorde = new car;
$viper->setName("Viper");
$concorde->setName("Concorde");
$viper->changeGear(1);
$viper->changeGear(2);
$concorde->brake();
?>
```

这一次，输出能够区分不同的汽车了。

### 构造函数与析构函数

虽然拥有一个设置汽车名称的函数很有帮助，但显然每辆汽车都需要一个名称。与其使用 setName() 来设置名称的初始值，不如只在因某种原因需要重命名汽车时才使用它更合理。相反，因为所有汽车都需要一个名称，我们可以强制用户在创建汽车时传入名称。

这是通过 *构造函数* 完成的，这是一个魔法函数，PHP 在创建任何类的对象时都会调用它。如果你没有构造函数，比如我们当前的脚本，PHP 会跳过这一步。构造函数用于设置对象的初始值。例如，如果你正在创建一个 Human 对象，它可能会将年龄设置为 0（刚出生），将生日设置为今天，等等。

因为构造函数是一个魔法函数（注意：*魔法函数* 是描述构造函数及其同类函数的实际术语），你必须为它使用固定的名称：`__construct()`。注意开头的两个下划线，这是魔法函数的明确标志。

如果我们想在创建对象时设置汽车名称，构造函数应该如下所示（将此放在 `public $name` 行之后）：

```php
public function __construct($name) {
    $this->name = $name;
}
```

如果我们将其添加到汽车类中，保存脚本并尝试运行，我们会看到 PHP 现在输出警告，指出我们没有为两辆汽车提供初始名称。构造函数有效地替代了我们在此处使用的 setName() 函数；因此，我们可以将底部的整块代码重写为：

```php
$viper = new car("Viper");
$concorde = new car("Concorde");
$viper->changeGear(1);
$viper->changeGear(2);
$concorde->brake();
```

与构造函数一起出现的是 *析构函数*，它在对象的另一端起作用，并在你的对象被销毁时调用。对象销毁可以是显式的（你使用 unset() 函数）或隐式的（脚本结束）。无论哪种情况，PHP 都会为你调用 `__destruct()` 函数，你可以随心所欲地使用它，例如关闭你在构造函数中打开的任何文件句柄。

我们可以通过在 `__construct()` 函数下方添加以下代码来修改我们的汽车类以包含一个析构函数：

```php
public function __destruct() {
    echo "Car ${this->name} going to the scrap heap...\n";
}
```

