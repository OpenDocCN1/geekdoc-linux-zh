
第一行是标准的，但第二行引入了 `$this` 变量。类的每个实例都有自己的一组变量，因此 PHP 使用 `$this` 变量来指代调用了该函数的那个对象。如果你调用 `$concorde->brake()`，那么 `$this` 就是 `$concorde`；如果你调用 `$viper->brake()`，那么 `$this` 就是 `$viper`。

设置对象变量的方式非常具体。你不要使用 `$name = ...` 或 `$this->$name = ...`——前者设置了一个名为 `$name` 的新局部变量，而后者查找局部变量 `name` 的值并将其用作变量变量。也就是说，如果 `$name` 是 `wombat`，它会设置 `$this->$wombat`。请记住，除非你想使用变量变量，否则 PHP 变量永远只有一个美元符号！

设置好变量后，我们可以修改其他两个函数以打印名称，从而区分不同的汽车。最终脚本如列表 31.10 所示。

### 列表 31.10 通过名称区分的多辆汽车

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

虽然拥有一个设置汽车名称的函数很有帮助，但显然每辆汽车都需要一个名称。与其使用 `setName()` 来设置名称的初始值，不如只在因某种原因需要重命名汽车时才使用它更合理。相反，因为所有汽车都需要一个名称，我们可以强制用户在创建汽车时传入名称。

这是通过 *构造函数* 完成的，这是一个魔法函数，PHP 在创建任何类的对象时都会调用它。如果你没有构造函数，比如我们当前的脚本，PHP 会跳过这一步。构造函数用于设置对象的初始值。例如，如果你正在创建一个 `Human` 对象，它可能会将年龄设置为 0（刚出生），将生日设置为今天，等等。

因为构造函数是一个魔法函数（注意：*魔法函数* 是描述构造函数及其同类函数的实际术语），你必须为它使用固定的名称：`__construct()`。注意开头的两个下划线，这是魔法函数的明确标志。

如果我们想在创建对象时设置汽车名称，构造函数应该如下所示（将此放在 `public $name` 行之后）：

```php
public function __construct($name) {
    $this->name = $name;
}
```

如果我们将其添加到汽车类中，保存脚本并尝试运行，我们会看到 PHP 现在输出警告，指出我们没有为两辆汽车提供初始名称。构造函数有效地替代了我们在此处使用的 `setName()` 函数；因此，我们可以将底部的整块代码重写为：

```php
$viper = new car("Viper");
$concorde = new car("Concorde");
$viper->changeGear(1);
$viper->changeGear(2);
$concorde->brake();
```

与构造函数一起出现的是 *析构函数*，它在对象的另一端起作用，并在你的对象被销毁时调用。对象销毁可以是显式的（你使用 `unset()` 函数）或隐式的（脚本结束）。无论哪种情况，PHP 都会为你调用 `__destruct()` 函数，你可以随心所欲地使用它，例如关闭你在构造函数中打开的任何文件句柄。

我们可以通过在 `__construct()` 函数下方添加以下代码来修改我们的汽车类以包含一个析构函数：

```php
public function __destruct() {
    echo "Car ${this->name} going to the scrap heap...\n";
}
```

保存你的脚本并再次运行它；在 PHP 清理对象时，你应该会在脚本末尾看到每个汽车对象的析构函数被调用。

## 类的继承

PHP 允许你使用一个类作为另一个类的基础，这就是所谓的*类继承*。目前我们有一个汽车类，但如果我们要添加一个卡车类和一个公共汽车类呢？我们可以简单地复制 `changeGear()` 和 `brake()` 方法到每个类中，但这会使维护变得更加困难。例如，如果我们稍后在 `brake()` 方法中发现了 bug，我们将需要记住在其他多个地方更改它。相反，我们应该创建一个名为 `vehicle` 的类，包含所有这些共享功能，然后让 `car`、`truck` 和 `bus` 类都从 `vehicle` 继承。

当一个类继承自另一个类时，它会带来所有声明为 public 的变量和函数，迄今为止所有的都是 public。我们可以通过在类定义中使用 `extends` 关键字来从 `vehicle` 类继承 `car` 类，如下所示：

```php
class car extends vehicle {
```

然后，通过修改 `car` 类为 `vehicle` 类，我们可以扩展所有三个类，如清单 31.11 中所示的完整脚本。

### 清单 31.11 多个车辆，全部为子类

```php
<?php
class vehicle {
    public $name;

    public function __construct($name) {
        $this->name = $name;
    }

    public function __destruct() {
        echo "$this->name going to the scrap heap...\n";
    }

    public function setName($newname) {
        $this->name = $newname;
        echo "Name changed to $newname\n";
    }

    public function brake() {
        echo "$this->name is braking...\n";
    }

    public function changeGear($gear) {
        echo "$this->name is changing gear to $gear\n";
    }
}

class car extends vehicle { }
class truck extends vehicle { }
class bus extends vehicle { }

$viper_var = new car("Viper");
$caterpillar_var = new truck("Caterpillar");
$viper_var->changeGear(1);
$caterpillar_var->brake();
?>
```

由于 `car`、`truck` 和 `bus` 的类定义都是空的，除了名称不同外，它们与 `vehicle` 类完全相同。然而，将它们分开意味着我们可以添加单独的功能，例如为公共汽车添加 `setFare()` 函数。

尽管我们一次只能从一个类继承，但你可以从被继承的类继承。也就是说，我们的 `car` 类从 `vehicle` 继承，但我们可以创建新的类，这些类反过来从 `car` 继承。有各种术语用来描述继承，其中最常见的是父/子关系。在我们的例子中，`car` 是 `vehicle` 的子类，或者换一种说法，`vehicle` 是 `car` 的父类。如果我们进一步用诸如 `coupe` 或 `sedan` 这样的类扩展 `car`，那么 `vehicle` 将是 `coupe` 的祖类。

另一个常用的词是*子类化*。因此，`car` 是 `vehicle` 的子类，`coupe` 是 `car` 的子类，等等。子类的对立面是超类。在这种情况下，`vehicle` 是 `car` 的超类。

## 访问修饰符

PHP 面向对象编程的内容远不止本文所能涵盖的范围，但访问修饰符对于完整理解至关重要，因此绝对不能省略。
