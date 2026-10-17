
## C.3 属性

Moose 程序的下一步是为你的对象设置属性。这些属性也称为属性（properties）或插槽（slots），是 Moose 最强大的特性之一。事实上，你可以创建一个仅由属性组成的类。这些属性与之前不使用 Moose 创建的属性不同的地方在于，这些属性可以作为访问器方法（getter 和 setter）使用。例如，如果你有一个 `Dog` 类，其中一个属性是 `name`，那么 `name` 既可以用作 setter，也可以用作 getter。

### C.3.1 has 函数

Moose 提供 `has` 函数来声明属性。在以下小片段中，*dog* 有一个 *name* 属性。*rw* 表示该属性可以作为方法来获取和设置对象的属性。你可以使用 *name* 作为写入访问器，以这种方式设置名称：

```perl
$dog->name("Fido");
```

并作为读取访问器，以这种方式获取名称：

```perl
$dog->name();
```

或者你可以简单地直接设置属性，如下所示：

```perl
$dog->{name} = "Fido";
```

并创建自己的方法来获取名称，或者为你的 setter 和 getter 使用任何组合的方法。在下面的示例中，类 `Dog` 有一个读/写 `name` 属性。

#### 示例 C.1

```perl
# (The Dog.pm Module)

package Dog;

use Moose;

has 'name' => (is => 'rw');  # Set the attribute;

---------------------------------------------------

And the user of the module:

use Dog;

my $dogref = Dog->new;     # Call default constructor

$dogref->name("Lassie"); # Use 'name' as a setter method

print "The dog's name is ", $dogref->name(), "\n";

# Use 'name' as a getter method

use Data::Dumper;

print Dumper($dogref);  # Moose blessed the object.

# (Output)

# The dog's name is Fido.

# $VAR1 = bless( {

#  'name' => 'Fido'

# }, 'Dog' );
```

属性还可以拥有默认值、类型约束、委托等。（参见 `Moose::Manual::Attributes`。）将属性用作 setter 或 getter 方法是可选的。一旦你有了对象的引用，你就可以像在非 Moose OO 程序中那样创建自己的访问器。注意，在之前的示例中，`Data::Dumper` 的输出显示 `dog` 对象被加冕为 `Dog` 类，这与非 Moose 方式中显示的样子完全一样。

### C.3.2 Moose 前后的示例

接下来的两个示例展示了 Moose 之前的程序，使用传统的 Perl OO。第二个示例使用 Moose 做同样的事情。

示例 C.2 展示了 Moose 之前的面向对象模块。

#### 示例 C.2

```perl
# (Class Without Moose)

package House;  # Class

use strict;

use warnings;

sub new {  # Constructor

    my $class = shift;

    # Set properties

    my $house = {  

        Color => undef,

        Owner => undef,

        Price => undef,

    };  # Attributes

    bless($house, $class);  # Blessing

    return $house;  # Return blessed hashref

}

sub set_props {  # method/setter

    my $obj = shift;

    my ($color, $owner, $price) = @_; # Set attributes

    $obj->{Color} = $color;

    $obj->{Owner} = $owner;

    $obj->{Price} = $price;

}

sub get_props {  # method/getter

    my $self = shift;

    my $prop = shift;

    return $self->{$prop};

}

1;
```

示例 C.3 展示了同样的示例，但这次使用 Moose。

#### 示例 C.3

```perl
# House.pm

# 1

package House;

# 2

use Moose;

# Define attributes for the House class

# 3

has 'color' => {

    is => 'rw',

    isa => 'Str',

    predicate => 'has_color',

};

# 4

has 'owner' => {

    is => 'rw',

    isa => 'Str',

};

# 5

has 'price' => {

    is => 'ro',

    isa => 'Int',

    # 6

    writer => '_set_price',

};

# 7

sub _set_price {

    my $self = shift;

    $self->{price} = shift;

}

# 8

sub _set_props { # define your own method

    my $self = shift;

    my ($color, $owner, $price) = @_;

    # $self->{color} = $color;

    # $self->{owner} = $owner;

    # $self->{price} = $price;

    # }

}
```

**说明**

- 1. `House` 类在包中定义。创建类所做的就是声明一个包并使用 Moose。
- 2. 加载 Moose 会自动开启严格模式（*warnings* 和 *strict*）。名为 `new` 的默认构造函数也会被自动添加。
- 3. 这是你为对象定义属性的地方。第一个属性是 `'color'`。此选项接受 `rw`（读/写）或 `ro`（只读）。在这个例子中，它创建一个与属性同名的读/写访问器。`'color'` 也被称为 *setter/getter* 方法。你不必将属性用作访问器方法。你可以创建自己的方法来设置或检索对象的值。`'color'` 属性也被赋予了 type => `'Str'`（是字符串）。*predicate* 方法告诉你一个属性是否已被设置，即使是 `undef` 也可以，如果已设置则返回 *true*，如果未设置则返回 *false*。下一个属性是 `'owner'`。它可以作为读/写访问器。`'owner'` 类型 `isa => 'Str'`（是字符串）。
- 5. `price` 属性是只读的。这意味着如果你尝试将其用作访问器方法，你**不能设置**价格，但你可以获取其值。这里是你尝试使用访问器直接给房子分配价格时会得到的错误：

```perl
$h1->price(5000000);
```

产生以下错误（部分输出）：

```text
Cannot assign a value to a read-only accessor at reader House::price

(defined at House.pm line 16) line 3.

        House::price('House2\HASH(0x1010025e0)', 500000) called at

        houseMooseuser line 9
```
