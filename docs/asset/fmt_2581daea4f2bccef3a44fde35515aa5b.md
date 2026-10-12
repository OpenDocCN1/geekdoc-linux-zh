
### 说明

- 1 声明了 `House` 类。
- 2 `new` 方法是一个构造函数。该对象是一个空的匿名哈希。对象的键/值对，即属性或特征，将稍后分配。被 `$ref` 引用的对象被祝福进 `House` 类。
- 3 定义了实例方法 `set_props`。
- 4 第一个参数是对 `House` 对象的引用。它从 `@_` 数组中移出并赋给 `$object`。引用的名称可以是 `$his` 或 `$self`。这并不重要。
- 5 第二个参数从 `@_` 数组中移出。它是一个数组引用。
- 6 引用 `$val_ptr` 被解引用，以获取传递给该方法的值列表。
- 7 传递给方法的值现在被分配给对象。
- 8 定义了用于从对象中检索值的实例方法。
- 9 打印哈希中选中的值。
- 10 内置的 `ref` 函数，当给定一个对象作为参数时，返回创建该对象的类名。
- 11 由于对象是哈希的引用，我们对其进行解引用，`%$self`，以获取其键/值对。该类的使用者随后将模块加载到其程序中。
- 13 调用构造函数 `new()` 返回一个新祝福的房子对象。

## 命名参数和数据检查

目前为止的所有示例都使用了 *House* 对象。在下一个示例中，我们将创建一个 *Employee* 对象。*Employee* 构造函数将接收用作员工属性的参数。如果构造函数方法期望按顺序传入姓名、地址和薪资，那么如果参数以错误的顺序发送，就会导致地址被赋值给姓名，或姓名被赋值给薪资等问题。防止这种情况的一种方法是在调用方法时以哈希形式传递参数。这样，当方法作为参数接收它们时，它们将以键/值对的形式存在。（当然，拼写预期的键不正确可能会成为问题。）以下示例展示了如何使用命名参数。

### 示例 14.7

```perl
# User of Employee.pm--See Example 14.8 for module

use Employee;

use warnings;

use strict;

my ($name, $extension, $address, $basepay, $employee); # Declare my variables

print "Enter the employee's name. ";

chomp ($name=<STDIN>);

print "Enter the employee's phone extension. ";

chomp ($extension=<STDIN>);

print "Enter the employee's address. ";

chomp ($address=<STDIN>);

print "Enter the employee's basepay. ";

chomp ($basepay=<STDIN>);

# Passing arguments as a hash

$employee = Employee->new( "Name"=>$name,
                          "Address"=>$address,
                          "Extension"=>$extension,
                          "PayCheck"=>$basepay,
                        );

print "\nThe statistics for $name are: \n";

$employee->get_stats;
```

#### （输出）

```text
Enter the employee's name. Daniel Savage
Enter the employee's phone extension. 2534
Enter the employee's address. 599 Mission Ave, Somewhere, CA
Enter the employee's basepay. 2200
The statistics for Daniel Savage are:
Address = 599 Mission Ave, Somewhere, CA
PayCheck = 2200
IdNum = Employee Id not provided!
Extension = 2534
Name = Daniel Savage
```

### 说明

- 1. 此程序将使用 `Employee.pm` 模块。
- 2. 对于可能的错误将发出 `warnings`，并且 `strict` pragma 将跟踪全局变量、未定义变量、裸词等。
- 3. 创建了一个作用域私有变量列表。
- 4. 程序用户将被要求提供传递给 `Employee` 模块的信息。
- 5. 调用构造函数以将参数作为键/值对传递；也就是说，在 `Employee` 模块中，一个哈希被传递给构造函数。返回的对象引用被赋给 `$employee`。
- 6. 调用实例方法 `get_stats` 来显示员工的属性。

在下一个示例中，让我们看看模块如何处理其命名参数。

### 示例 14.8

```perl
# Module Employee.pm—See Example 14.7 to use this module.

package Employee;

use Carp;

sub new {
    my $class = shift;
    my ($params) = @_; # Receiving the hash that was passed
    my $ref = {
        "Name" => $params{"Name"} || croak("No name assigned"),
        "Extension" => $params{"Extension"},
        "Address" => $params{"Address"},
        "PayCheck" => $params{"PayCheck"} || croak("No pay assigned"),
        ((defined $params{"_IdNum"}) ? ("_IdNum" => $params{"_IdNum"}) : croak("Employee's id was not provided!\n"))
    };
    return bless($ref, $class);
}

sub get_stats {
    my $self = shift;
    foreach my $key (keys %$self) {
        print $key, " = ", $self->{$key}, "\n";
    }
    print "\n";
}
```
