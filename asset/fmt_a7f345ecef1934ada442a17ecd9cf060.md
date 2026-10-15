
`print "The owner of my first house is ",$house1->get_owner(),"\n";`

`print Dumper($house1,$house2);` # Take a look at the two instances

```
（输出）
我的第一栋房子的所有者是 Planet Bank
$VAR1 = bless( {
      'Owner' => 'Planet Bank',
      'Payment' => undef,
      'Color' => 'Beige',
}, 'House' );
$VAR2 = bless( {
      'Owner' => 'Mr. T',
      'Payment' => '2000',
      'Color' => 'Beige',
}, 'House' );
```

## 解释

- 1. 声明 `House` 类。
- 2. 这是构造方法，它为我们提供新房子的引用并将其“祝福”（`bless`）到该类中；也就是说，它创建了一个 `House` 类的实例。
- 3. 现在定义实例方法，以便向房子对象设置值或从中检索值。
- 4. 这是一个“获取器”（getter）方法，旨在从房子对象中检索数据。
- 5. 现在用户可以创建更多的房子对象。这是对 `new()` 构造方法的调用。第一个参数位于箭头左侧；这是类的名称。返回一个被“祝福”的房子对象的引用，并赋值给 `$house1`。
- 6. 创建另一个房子对象 `$house2`，并返回其引用。
- 7. 一旦拥有对象的实例，我们就可以访问该地址并设置值。实例方法 `set_owner()` 隐式地获取 `$house2` 作为其第一个参数，即箭头左侧的内容。获取第二栋房子的地址作为第一个参数，确保了 Perl 在正确的位置设置数据。第二个参数“Mr. T”由用户提供。这将覆盖构造函数中设置的默认值“Planet Bank”。
- 8. 现在我们使用 `get_owner()` 方法检索第一栋房子的所有者值。
- 9. `Data::Dumper` 函数显示两栋房子的值。（你可以将这些数据保存到文件中并据此重构对象。）如果设置 `$Data::Dumper::Terse=1`，则显示中会省略 `$VAR1` 和 `$VAR2` 变量。关于对象的序列化，请参阅 [http://perI.find-info.ru/perl/025/adverpl2-chap-4sect-2.html](http://perI.find-info.ru/perl/025/adverpl2-chap-4sect-2.html)。

### 14.2.5 创建面向对象的模块

在上一个示例中，所有代码都包含在单个文件的单个包中。现在是时候创建一个模块了。

图 14.4 展示了一个简单的面向对象模块及其用户界面的布局。定义类的 `.pm` 文件是一个模块。在这个例子中，`.pm` 文件是 `House.pm`。该文件包含一个包声明。该包将被称为类；因此，这是 `House` 类。通常，类名与模块名相同，只是去掉了 `.pm` 扩展名。类由子例程组成，这些子例程现在被称为方法，如前面的示例所示。示例程序中的第一个方法名为 `new`，是构造方法。它是定义和创建（构造）对象的方法。当该模块的用户调用 `new` 方法时，他们将获得一个新创建的被“祝福”的 `House` 对象的引用（房子的地址）。实例方法用于存储和检索对象中的数据。一旦用户获得了对象的引用，就会使用它来调用实例方法。

另一个小细节：当类与用户界面分离时，正如我们在第 13 章“模块化它、打包它并送到图书馆！”中创建的过程式模块那样，必须在模块末尾放置 `1;` 以返回一个真值。

模块的使用者必须使用 `use Module` 指令指定要包含的模块，该指令也在第 13 章中讨论过。设计模块的方式有很多，这只是其中一种简单的方法。

```perl
The Module Filename: House.pm

package House;  # House is the class

# The package name normally matches the filename minus the .pm extension

sub new{

    my $class = shift;     # Constructor method

                           # First argument is the name of the class

    my $house_obj = { };   # Create the reference/pointer.

    bless($house_obj, $class); # Bless the referent; Create an object

    return $house_obj;       # Return a reference to the object

}

sub set_owner{

    my $Self = shift; # Access/instance method

                      # First argument is a reference to the object

    $Self->("Owner")=shift; # Sometimes called a "setter" method

}

sub get_owner{

    my $Self = shift; # Access/instance method

                      # First argument is a reference to the object

    return $Self->("Owner"); # Sometimes called a "getter" method

}

1; # Must return a true value, or module won't load
```

```perl
The user of the Class: the Perl script, myHouse.plx

use House; # Tell Perl to load House.pm

my $house1 = House->new(); # Call class constructor.
# Get back a reference to a new house. Perl sends
# the name of the class as its first argument

my $house2 = House->new(); # Create another house object

$house1->set_owner("B of A"); # Call access method:
# Perl sends the address of the first house
# object, to method set_owner()

print "The owner of the first house is ", $house1->get_owner, "\n";
# Perl gets the object's data with the get_owner access method
```

![](img/8556abcb353c0991f12099420ec28735_494_0.png)

## 向方法传递参数

实例变量用于在创建对象时初始化对象。这样，每次创建对象时，都可以对其进行自定义。描述对象的属性可以作为参数传递给构造方法，并分配给实例变量。它们被称为**实例变量**，是因为它们在对象被创建（即实例化）时才会存在。通常使用匿名哈希（anonymous hash）或匿名数组（anonymous array）来存储实例变量。在下面的示例中，对象“拥有”或“包含”一个所有者和一个价格。

### 示例 14.3

```perl
1  (The Module: House.pm)

2  package House;

3  sub new{              # Constructor method

4      my $class = shift;

5      my ($owner, $price) = @_; # Instance variables

6      my $ref={"Owner"=>$owner,      # Instance variables to

7              "Price"=>$price,        # initialize the object

8      };

9      bless($ref, $class);

10     return $ref;

11 }

12 

13 sub display_object{ # An instance method

14     my $self = shift;      # A reference to the object is received

15     foreach $key (keys %$self){
```
