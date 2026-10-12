
```perl
package House; # House class

use warnings;

use strict;

sub new{ # The constructor method

    my $class=$shift;

    my $house_obj={

        "Owner"=>"Planet Bank", # Properties/attributes

        "Color"=>"Beige",

        "Payment"=>undef,

    };

    return bless($house_obj, $class); # The blessing creates the object

}

sub set_owner{ # Instance/Access methods

    my $self=$shift;

}

sub set_color{

    my $self=$shift;

    $self->{"Color"}=$shift;

}

sub get_payment{

    my $self=$shift;

    my $payment=$shift;

    $self->{"Payment"}=$payment unless $payment < 0;

}

sub get_owner{ # Retrieve data from the object

    my $self=$shift;

    return $self->{Owner};

}

#----------------End of Class definition-----------------------

# User of the Class

use Data::Dumper; # We'll look at the structure of the object

my $house1=House->new(); # Make a new house object and get back

# its address

my $house2=House->new(); # Make another house object

$house2->set_owner("Mr. T"); # Change the default owner of the

# second house

$house2->set_payment("2000"); # Set the payment of the second house

print "The owner of my first house is ", $house1->get_owner(),"\n", # Retrieve data from the first house.

print Dumper($house1,$house2); # Look at the content of the

# house objects
```

## 示例 14.1（续）

```perl
(Output)

The owner of my first house is Planet Bank

$VAR1 = bless( {

  'Owner' => 'Planet Bank',

  'Payment' => undef,

  'Color' => 'Beige'

}, 'House' );

$VAR2 = bless( {

  'Owner' => 'Mr. T',

  'Payment' => 2000,

  'Color' => 'Beige'

}, 'House' );
```

# Perl 包即类。

Perl 包充当类。没有名为*class*的保留字，但在面向对象的 Perl 中，包通常被称为类。类通常存储在一个*pm*模块中，类名与模块名相同（去掉*.pm*扩展名）。如果你想*区分*这两个术语，那么类就是包含称为方法的特殊子程序的包，这些方法用于创建和操作对象。Perl 类通常由以下部分组成：

- 1. 描述对象的数据。
- 2. 使用 `bless` 函数创建对象的构造器方法。
- 3. 称为“方法”的特殊子程序，它们知道如何创建、访问、操作和销毁对象。

与其他面向对象语言不同，Perl 中没有*private*、*public*或*protected*等特殊 Perl 关键字。Perl 的包机制构成了存储数据和子程序（称为方法）的类。*my* 函数使变量具有词法作用域，而 *bless* 函数保证对象创建时知道它属于哪个类。总之，对象是指向匿名哈希、数组、标量或子程序的引用，并通过称为方法的特殊函数进行操作，这些方法通过引用访问对象。

# Perl 类。

由于类实际上只是一个包，因此它有自己独立的符号表，一个类中的全局数据或例程可以被另一个类访问。

与其他语言不同，Perl 不会严格监控模块内的公共/私有边界。为了保持数据私有，可以使用几种技术（见本章稍后的第 14.3 节，“匿名子程序、闭包和隐私性”）。

![](img/8556abcb353c0991f12099420ec28735_483_0.png)

## 14.2.3 Perl 对象

**引用。** 首先，Perl 中的对象通过使用引用来创建。你可能需要回顾第 12 章，“这个工作需要引用吗？”如果你不清楚如何使用引用。简而言之，引用是一个持有某个变量地址的标量。引用也可以指向没有名称的数据类型，称为**匿名变量**。例如，这里有一个名为 `$ref` 的引用，指向由两个键值对组成的匿名哈希：

```perl
my $ref=["Owner"=>"Tom", "Price"=>"25000"];
```

要访问匿名哈希中的值，可以使用箭头运算符解引用（去引用）引用（指针）`$ref`，如下所示：

```perl
$ref->{"Owner"}
```

要创建 Perl 对象，首先创建一个引用。该引用通常指向一个匿名哈希（尽管它也可以被分配为数组或标量的地址，甚至是一个子程序）。该哈希将包含对象的数据成员和属性。

**祝福（Blessing）。** 被引用的内存地址（称为**被引用对象**）必须经过“祝福”才能将其转换为 Perl 对象；换句话说，被引用对象必须知道它属于哪个包。这是通过创建引用，然后将（被引用的对象）祝福到某个包中来实现的。将祝福视为创建一种新的数据类型，即对象。

```perl
my $ref= (Owner=>"Tom", Price=>250000); # 属性 Owner, Price
bless($ref, "House"); # 将引用标记为属于 House
return $ref; # 返回指向该对象的引用给调用者
```

`bless` 函数接受一个或两个参数。第一个参数*始终*是一个引用，第二个可选参数是类（包）的名称。`bless` 函数标记被引用的对象（称为被引用对象）。它创建一个内部指针来跟踪该对象（被引用对象）属于哪个包。该对象是（通常是一个哈希）被祝福到类（包）中的东西。如果*package* 未作为第二个参数列出，`bless` 函数假设当前包。

`bless` 函数返回指向已祝福对象的引用。在图 14.2 中，显示了祝福之前和之后的对象地址。请注意，祝福之后，地址被标记为类名，在本例中为 *House*。

![](img/8556abcb353c0991f12099420ec28735_484_0.png)

### 图 14.2 祝福前后的地址。

由于祝福将对象与特定的包（类）关联起来，Perl 将始终知道对象属于哪个包，从而消除了使用我们在过程化模块中使用的 `::` 语法的需求。一个对象可以被祝福到一个类，然后*重新祝福*到另一个类，依此类推，但一个对象一次只能属于一个类。一旦对象被祝福，你就不必使用 `@EXPORT_OK` 或 `@EXPORT` 数组导出符号。事实上，作为一个一般规则，如果模块试图面向对象，那么什么也不导出。

## 14.2.4 方法是 Perl 子程序

**定义。** 方法是处理对象的子程序。例如，它用于创建对象，存储或修改对象中的数据，从对象中检索数据等。它是属于类的特殊子程序，其第一个参数将是以下之一：

- 1. 类（包）名称
- 2. 对象的引用

这个第一个参数由 Perl 隐式发送。即使你可能在没有参数的情况下调用方法，Perl 也会自动发送一个，即包名或对象引用。否则，它看起来与其他子程序无异。在示例 14.1 中，我们创建了两个房屋对象。创建对象的方法被称为 `new`（尽管它可以称为任何名称），并且如下所示，当方法被调用时，它前面跟着类名 `House`，然后是一个箭头，`House->new()`。Perl 会自动将箭头左边的内容发送到方法。因此在这种情况下，`new()` 方法将自动获取一个参数，即 `House`，即类名。

- 1. Perl 隐式地将类名称发送到 `new()` 方法

![](img/8556abcb353c0991f12099420ec28735_485_0.png)

```perl
$house1 = House->new(); # 创建一个新的房屋对象并获取其地址
$house2 = House->new(); # 创建另一个房屋对象
```
