
`print "$key: $self->{$key}\n";`

};

(The Script)

# User of the class; another program

`use House;`

# my $house1 = new House("Tom Savage", 250000);

# Invoking constructor--two ways.

`my $house1 = House->new("Tom Savage", 250000);`

`my $house2 = House->new("Devin Quigley", 55000);`

# Two objects have been created

`$house1->display_object();`

`$house2->display_object();`

`print "$house1, $house2\n";`

## 说明

- 1 声明了包 `House`。（此时，程序尚未提供任何描述该类功能或使用方法的说明。解释如何使用某个类的文档被称为公共接口。有关如何以 Perl 方式记录模块说明的指令，请参见第 14.5 节“纯旧式文档——模块文档”。）
- 2 类方法 `new` 被定义为一个构造函数。
- 3 传递给类方法的第一个参数是该类（包）的名称。
- 4 “实例变量”是从 `@_` 数组的剩余部分创建的。
- 5 一个匿名哈希的地址被赋给引用 `$ref`。键是硬编码的，值来自实例变量。
- 6 引用 `$ref` 指向的“东西”被祝福（`bless`）进该类，成为新的对象。
- 7 当调用该方法时，引用 `$ref` 的值将被返回。子例程 `display_object` 是一个实例方法。它在这个类中定义。
- 传递给实例方法的第一个参数是对对象的引用。
- 8 `foreach` 循环与 `keys` 函数一起使用，从被 `$self` 引用的哈希（对象）中获取键，并在循环块中打印键和值。
- 9 类的使用者将 `House.pm` 加载到其命名空间中。
- 10 调用 `new` 方法时传递了三个参数：`House`、`Tom Savage` 和 `250000`。第一个参数是类的名称。虽然你看不到它，但 Perl 会隐式地将其发送给构造函数。接下来的两个参数由类的使用者显式发送。这里唯一的限制是 `Owner` 值是第一个参数，而 `Price` 值是第二个参数。没有错误检查。该示例仅展示了如何向构造函数传递参数。返回一个新 `House` 对象的引用，并将其赋给 `$house1`，这是一个哈希引用。
- 11 再次调用 `new` 方法，但使用不同的参数 `Devin Quigley` 和 `55000`。返回给 `$house2` 的值是另一个对象的引用。`new` 方法已被用于创建两个 `House` 对象。你可以创建任意多的对象。如第 14 行的输出所示，它们都将具有独特的地址。由于这些对象在构造函数中被祝福，Perl 知道这些对象属于 `House` 类。
- 12 调用实例方法来显示由 `$house1` 引用的对象数据。
- 13 再次调用实例方法，但用于显示由 `$house2` 引用的对象数据。
- 14 打印两个对象的地址。你可以看到这些地址已被标记为属于 `House` 类。

### 向实例方法传递参数。

实例方法的第一个参数始终是对对象的引用。在被调用的方法中，这个值通常从 `@_` 数组中移出（`shift`）并存储在名为 `$self` 或 `This` 的变量中，尽管变量叫什么名字并不重要。然后，其余参数像在任何普通子例程中那样进行处理。

以下示例演示了一个在被调用时发送额外参数的实例方法。

## 示例 14.6

```perl
#!/bin/perl

# Program to demonstrate passing arguments to an instance method.

# In this example, a pointer to an array is passed.

1  package House;  # Class

use warnings;

sub new{  # Constructor

    my $class = shift;

    my $ref = {};  # Define properties later

    return bless ($ref, $class);

}

3  sub set_props{  # Instance methods

4  my $object = shift;  # Pointer to object

5  my $val_ptr=shift;  # Receive another pointer

6  my ($owner,$price,$style) = @{$val_ptr};  # Create a slice

7  $object->{"Owner"}=$owner;

    $object->{"Price"}=$price;

    $object->{"Style"}=$style;

}

8  sub get_owner{

    my $self=shift;

    return $self->{"Owner"};

}

sub get_price{

    my $self=shift;

    return $self->{"Price"};

}

sub get_address{

    my $self=shift;

    return $self->{"Address"};

}

9  sub display_props{

    my $self = shift;

10 print "Properties for the ", ref($self), " are:\n";

11 foreach my $key (keys %{$self}){  # Dereference hash ref

        my $value = $self->{$key};

        printf "%-10s %-10s\n", $key, $value;

    }  # Don't forget this!

}

# (The Script)

12 use House;

use warnings;

use strict;
```

## 14.2 Perl 类、对象和方法——与真实世界建立联系

### 示例 14.6（续）

```perl
13 my $h1 = House->new();

14 my $h1->set_props( { "Unity Bank", "12 Main St.", "150000" } );

   $h1->display_props();

   my $h2 = House->new();

15 $h2->set_props( { "Pierre Dupont", "150000", "Pacific Ridge" });

   $h2->display_props();
```

#### （输出）

```text
Owner Unity Bank
Address 12 Main St.
Price 150000
Owner Pierre Dupont
Address 10 Pacific Ridge
Price 150000
```
