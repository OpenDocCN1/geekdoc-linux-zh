
## 示例 C.4（续）

```perl
6   $h1->price(50000); # Throws an exception/readonly
7   $h1->set_price(50000); # Call 'set_price'
8   $h2->color("yellow");   # set values
    $h2->owner("Mr. Trump");
    $h2->set_price(1000000);

9   say "The price is ", $h1->price;
    # Use 'price' as an accessor method (getter)
    say "The owner is ", $h1->owner;
    say "The color is ", $h1->color, "\n";
10  print Dumper($h1,$h2);
```

（输出）
Has a color
The price is 50000
The owner is B of A
The color is yellow
$VAR1 = bless( {
    'owner' => 'B of A',
    'color' => 'yellow',
    'price' => 50000
  }, 'House2' );
$VAR2 = bless( {
    'owner' => 'Mr. Trump',
    'color' => 'yellow',
    'price' => 1000000
  }, 'House2' );

### C.3.3 Moose 类型

如前文 Moose 示例所示，当声明属性时，可以使用 Moose 的 `isa` 选项将属性与某种类型关联，例如 `Str`（字符串）、`Int`（整数）、`HashRef`（哈希引用）或 `Bool`（布尔值）等等。摘自 Moose 文档，以下是类型列表：

- Any
    - Item
    - Bool
    - Undef
    - Defined
    - Value
        - Num
        - Int
        - Str
        - ClassName
        - Ref
        - ScalarRef
        - ArrayRef
        - HashRef
        - CodeRef
        - RegexRef
        - GlobRef
        - FileHandle
        - Object
        - Role

由于 Moose 拥有自己的属性类型系统，它还可以检查参数；例如，如果你的属性接受 `ArrayRef` 类型，当你不遵守此约束时，Moose 将抛出异常。参数检查功能使得确保获取有效数据变得更加容易。请参阅 *Moose::Manual::Types* 以获取完整的类型列表及其用法。

让我们使用类型约束来修改 *House* 示例。这次，房屋对象可能有多个所有者。*owners* 属性的类型将是 `ArrayRef`，即指向一个匿名数组的引用，其中的元素（所有者）是字符串。

### 示例 C.5

```perl
use v5.16;
package House;    # Create the class
use Moose;
                # Define attributes for the House class
has 'color' => (
    is => 'rw',
    isa => 'Str',
);
has 'owners' => (
    is => 'rw',
    isa => 'ArrayRef[Str]',    # Type is an array reference
    required => 1,    # Must be provided to constructor
);
has 'price' => (
    is => 'ro',
    isa => 'Num',
    writer => '_set_price'
);
sub _set_price {
    my $self = shift;
    my $price = shift;
    $self->price($price);
}
1;
```

### 解释

1.  声明包 *House*。
2.  加载 *Moose*。它将创建类和属性。
3.  *'color'* 属性是读/写的，且类型为 *Str*（字符串）。
4.  *'owners'* 属性也是读/写的。
5.  分配给 *'owners'* 属性的值必须是一个数组引用，其中数组中的每个元素都必须是 *Str* 类型。如果你尝试向 *'owners'* 属性分配非数组引用的值，Moose 会抛出诸如以下的异常：

    ```
    # Attribute 'owners' does not pass the type constraint because:
    Validation failed for 'ArrayRef[Str]' with value Mr. Trump at /usr/
    local/ActivePerl-5.16        /lib/Moose/Meta/Attribute.pm line 1274.
    ```

6.  通常所有属性都是可选的。当将 *required* 属性设置为 1 时，Moose 表示在调用构造函数时必须提供 *'owners'* 属性，但没有指定其值应该是什么。
7.  通过使用 *reader* 和 *writer* 属性选项，你可以显式地指定用于读取和写入属性值的方法名称。由于 *'price'* 属性是只读的，我们无法直接设置价格。如果你想用它来设置价格值，你需要调用第 8 行定义的 *\_\_set\_price* 方法作为 *writer* 方法。前导下划线表示这是一个私有方法，即使它可以从类外部调用。
8.  定义 *\_\_set\_price* 方法。尽管 *'price'* 属性被定义为只读访问器，但我们可以通过使用此方法将其视为写入访问器。

示例 C.6 展示了 *House* 模块的使用者，*house.pl*。

### 示例 C.6

```perl
#!/usr/bin/env perl
use Data::Dumper;
use strict;
use warnings;
1 my $h1 = House->new('owners'=>[ "Mrs. A", "Mr. B" ]);
2 my $h2 = House->new('owners'=>[ ]);  # Define values later
3 my $h3 = House->new('owners'=> "Mr. Trump");
4 $h1->color('red');
   $h1->_set_price(125000);
5 $h2->owners(['Mr. Trump', 'Mr. Mellon', 'CityBank']);
   $h2->color('blue');
   $h2->_set_price(5000000);

say "The price is ", $h1->price;
6 say "The owners are ", join(' ', @{$h1->owners});
say "The color is ", $h1->color;
say "The price is ", $h2->price;
```

### 示例 C.6（续）

```perl
7  say "The owners are ", join(", ", @{$h2->{owners}});
   say "The color is", $h2->{color};
8  #print $h1->dump;
9  print Dumper($h1,$h2);
```

（输出）
The owners are Mrs. A, Mr. B
The color is red
The price is 5000000
The owners are Mr. Trump, Mr. Mellon, CityBank
The color is blue
$VAR1 = bless ( {
              'color' => 'red',
              'owners' => [
                  'Mrs. A',
                  'Mr. B'
              ],
              'price' => 125000
            }, 'House' );
$VAR2 = bless ( {
              'color' => 'blue',
              'owners' => [
                  'Mr. Trump',
                  'Mr. Mellon',
                  'CityBank'
              ],
              'price' => 5000000
            }, 'House' );

### 解释

1.  调用构造函数时传入参数，包括属性名（owners）及其值（所需的 ArrayRef 及其字符串值）。（注意：构造函数本身要求你发送哈希或哈希引用作为参数。）
2.  调用构造函数时传入所需的 ArrayRef，这次没有值。稍后会对它们进行赋值。只要构造函数接收到 *required* 类型，即指向匿名数组的引用，这就没问题。
3.  这一行抛出了异常，因为 Moose 尝试验证参数，但该参数未通过类型约束；也就是说，'owners' 属性的值不是 ArrayRef 类型。
4.  'color' 属性被用作 setter，为房屋对象的颜色分配值。
5.  现在我们正在使用 'owners' 属性作为访问器方法。请注意，开启 *required* 后，我们必须向构造函数发送一个 arrayref，但我们可以稍后分配值，如此处所示。
6, 7. 'owners' 属性用于访问（获取）第一和第二栋房屋的数值；即解引用方法返回的指向匿名数组的引用。

### 解释（续）

8. Moose 通过其 `dump` 方法提供了 `Data::Dumper` 的自有版本。
9. `Data::Dumper` 模块对于展示这些房屋对象的输出与非 Moose 程序相同非常有帮助。你可以看到对象被 bless 为哈希引用到 `House` 类中，并且所有属性及其值都如预期显示。

### C.3.4 使用 Moose 和扩展的示例

修改和扩展 Moose 可以通过自行添加扩展或使用已编写好的扩展来完成。一些最流行的 Moose 扩展可以在 `Moose::Manual::MooX` 中找到。下一个示例展示了如何使用其中两个扩展：`MooX::Declare` 和 `MooX::ClassAttributes`。

### 示例 C.7

```perl
(The Student Module)
# Student.pm
# Written by Daniel Holmes

use Moose;
1 use List::MoreUtils;

2 use MooX::Declare;

class Student {
  use MooX::ClassAttribute; # Include Moose extensions
  class has student_count => (
    is      => 'rw',
    isa     => "Int",
    default => 0,
  );
  6 has 'name' => (
    is      => 'rw',
    isa     => 'Str',
    required => 1,
  );
  7 has 'major' => (
    is      => 'rw',
    isa     => 'Str',
    default => "",
  );
  8 has 'courses' => (
    is      => 'rw',
    9   isa     => 'ArrayRef[Str]',
    10  default => sub { [] },
    11  traits  => ['Array'],
```

