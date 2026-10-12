
有关使用 Moose 处理异常的更多信息，请参见：`Moose::Manual::Exceptions` at `cpan.org`。

- 6. 我们可以显式指定用于读取和写入的方法。在这个例子中，我们将访问器设置为公开可读，但不可写。如果用户想要设置或更改价格，他将必须调用为该属性提供的 `_set_price` 方法。
- 7. 这是在 `price` 属性中定义为 `writer` 的 `_set_price` 方法。此方法让我们可以更改或设置价格。
- 8. 如前所述，Moose 并不强制你将属性用作访问器。你可以像使用 Moose 之前那样创建自己的访问器方法。请记住，在底层，Moose 只是 Perl 5 OO。在这个被注释掉的片段中，我们希望传入属性信息到 `set_props`，而不是使用在定义属性时由 Moose 创建的访问器。这样做，我们忽略了访问器。由于我们没有 `get_props` 方法，我们将使用 `price`、`owner` 和 `color` 作为访问器方法。

下一个示例展示了用户如何使用示例 C.3 中定义的 `House` 模块。

#### 示例 C.4

```perl
# (User of the House module)

#!/usr/bin/env perl

# 1

use House;

use Data::Dumper;

use v5.16;

# 2

my $h1 = House->new() ;  # Call constructor

my $h2 = House->new() ;

# 3

$h1->color('yellow') ;   # Use 'color' as an accessor

# 4

print "Has a color \n" if $h1->has_color == 1 ;

                         # use predicate method

# 5

$h1->owner("B of A") ;
```

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

由于 Moose 拥有自己的属性类型系统，它还可以检查参数；例如，如果你的属性接受 `ArrayRef` 类型，当你不遵守此约束时，Moose 将抛出异常。参数检查功能使得确保获取有效数据变得更加容易。请参阅 `Moose::Manual::Types` 以获取完整的类型列表及其用法。

让我们使用类型约束来修改 `House` 示例。这次，房屋对象可能有多个所有者。`owners` 属性的类型将是 `ArrayRef`，即指向一个匿名数组的引用，其中的元素（所有者）是字符串。

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

1. 声明包 `House`。
2. 加载 `Moose`。它将创建类和属性。
3. `'color'` 属性是读/写的，且类型为 `Str`（字符串）。
4. `'owners'` 属性也是读/写的。
5. 分配给 `'owners'` 属性的值必须是一个数组引用，其中数组中的每个元素都必须是 `Str` 类型。如果你尝试向 `'owners'` 属性分配非数组引用的值，Moose 会抛出诸如以下的异常：

```
# Attribute 'owners' does not pass the type constraint because:

Validation failed for 'ArrayRef[Str]' with value Mr. Trump at /usr/
local/ActivePerl-5.16        /lib/Moose/Meta/Attribute.pm line 1274.
```

6. 通常所有属性都是可选的。当将 `required` 属性设置为 1 时，Moose 表示在调用构造函数时必须提供 `'owners'` 属性，但没有指定其值应该是什么。
7. 通过使用 `reader` 和 `writer` 属性选项，你可以显式地指定用于读取和写入属性值的方法名称。由于 `'price'` 属性是只读的，我们无法直接设置价格。如果你想用它来设置价格值，你需要调用第 8 行定义的 `__set_price` 方法作为 `writer` 方法。前导下划线表示这是一个私有方法，即使它可以从类外部调用。
8. 定义 `__set_price` 方法。尽管 `'price'` 属性被定义为只读访问器，但我们可以通过使用此方法将其视为写入访问器。

示例 C.6 展示了 `House` 模块的使用者，`house.pl`。

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
```
