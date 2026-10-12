

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

我们已经看到 public 函数和变量会被子类继承。public 函数和变量的另一个特性是它们可以被类外的代码访问。我们在代码主体中调用 `brake()` 和 `changeGear()` 函数。

而不是 public 函数，我们可以使用 private 函数，它们与 public 函数的所有行为相反。如果 `brake()` 函数被声明为 private，它就不能像示例中那样被调用，因为 private 函数只能在另一个类函数内部调用。类似地，private 变量只能在类函数内部设置。在继承时，private 变量对新引入的子类函数不可访问。在我们的例子中，`$name` 是 public；将其改为 private 仍然允许 `car` 函数通过 `setName()` 更改名称，因为 `setName()` 是 `vehicle` 函数，而不是 `car` 函数。

第三种选择是 `protected`，它是 `private` 的稍宽松版本。`protected` 在所有方面都像 `private` 一样工作，除了 `inheriting`（继承）。`protected` 变量可被子类引入的函数访问。

面向对象编程的基本原则之一是*封装*。类应该被封装，以便外部的程序员不需要了解其内部如何工作。如果你有一个实现了 `setName()` 函数的类，使用它的程序员只需要知道它接受哪些参数及其返回值是什么。虽然我们可以直接去掉 `setName()` 函数，告诉程序员直接更改 `$name` 变量，但这迫使他们必须拥有关于对象如何工作的显式知识。

以下是可以添加到 `vehicle` 类的函数列表，并附有必要的访问方式和说明：

- `accelerate()`—Public（公开）。
- `setspeed()`—Private/protected（私有/受保护），因为程序员不应能够任意定义汽车的速度。相反，他们应该使用 `accelerate()` 或 `decelerate()`。
- `soundHorn()`—Public（公开）。
- `crash()`—Public（公开），因为这是发生在汽车上的外部事件，触发其他事件。
- `inflateAirbag()`—Private/protected（私有/受保护），因为这只应该作为其他事情的结果发生——例如，某人调用 `crash()`。

如果情况恶化，你根本无法理解 `private`、`protected` 和 `public`（即使在你购买了一本全面的 PHP 书籍之后），你可以简单地将你的所有函数和变量声明为 `public`。这不是首选，但它有效。

## 处理 HTML 表单

鉴于 PHP 的主要角色是处理网页，你可能会想知道为什么这一节被放在章节的这么后面。这是因为处理 HTML 表单对于 PHP 至关重要，以至于它基本上是自动完成的。

考虑这个表单：

```html
<form method="POST" action="thispage.php">
User ID: <input type="text" name="UserID" /> <br />
Password: <input type="password" name="Password" /> <br />
<input type="submit" />
</form>
```

当访问者点击提交时，`thispage.php` 再次被调用，这次 PHP 拥有 `$_REQUEST` 数组中的变量。给定该脚本，如果用户输入 `12345` 和 `frosties` 作为她的用户 ID 和密码，PHP 会为你提供设置为 `12345` 的 `$_REQUEST['UserID']` 和设置为 `frosties` 的 `$_REQUEST['Password']`。请注意，使用 HTTP post 非常重要，除非你特别想要 GET。POST 允许你发送更多的数据，并阻止人们篡改你的 URL 以尝试查找你脚本中的漏洞。

就这样吗？几乎吧。这告诉你如何检索用户数据，但你应该确保对其进行清理，以防用户试图将 HTML 或 JavaScript 混入你的数据库，伪装成你认为无害的内容。PHP 提供了 `strip_tags()` 函数用于此目的。它接受一个字符串并返回相同的字符串，但移除了所有 HTML 标签。

## 数据库

PHP 能够轻松用于创建动态、数据库驱动的网站，对许多人来说，这是使用它的关键原因。PHP 的标准构建版本支持 MySQL、PostgreSQL、SQLite、Oracle、MS SQL Server、ODBC 以及几种其他流行的数据库，因此你肯定会找到适合你数据的东西。

如果你想的话，你可以学习 PHP 支持的每种数据库的所有个别连接和操作函数，但一个更聪明的想法是使用 PEAR::DB。**PEAR::DB** 是 PHP 支持的数据库之上的抽象层，这意味着你只需编写一次代码，并且——通过最小的更改——它可以在每个数据库服务器上工作。

PEAR 是 PHP 的脚本库，包含用于常见问题的众多工具和预写解决方案。**PEAR::DB** 可能是 PEAR 项目中最流行的部分，但值得查看 PEAR 网站，看看是否有其他吸引你注意的内容。

### 介绍 PEAR::DB

要基本使用 PEAR::DB，你需要了解如何连接数据库、运行 SQL 查询以及处理结果。这不是 SQL 教程，所以我们假设你已经熟悉该语言。为了本教程的目的，我们还假设你正在使用一个名为 **dentists** 的数据库和一个名为 **patients** 的表，该表包含以下字段：

- **ID**—主键，自动递增的整数，用于存储每个患者唯一的编号
- **Name**—用于存储患者姓名的 varchar(255) 字段
- **Age**—整数
- **Sex**—男性为 1，女性为 2
- **Occupation**—用于存储患者职业的 varchar(255) 字段

同样，为了本教程的目的，我们将使用 IP 地址为 **10.0.0.1** 的数据库服务器，运行 MySQL，用户名为 **fedora**，密码为 **ai#65z**。你需要用自己的详细信息替换这些细节——使用 **localhost** 连接本地服务器。

