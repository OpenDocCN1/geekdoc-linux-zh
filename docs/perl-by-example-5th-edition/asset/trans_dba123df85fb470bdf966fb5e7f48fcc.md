

以及 `$b`，而不是普通的 `@array`。（有关进一步讨论，请参阅第 11 章“子程序如何工作？”。）不要尝试修改 `$a` 或 `$b`，因为它们代表正在排序的值。如果你希望 Perl 根据特定的区域设置（locale）对你的数据进行排序，你的程序应包含 `use locale` 预处理指令。如需完整讨论，请参阅 `perldoc perl perllocale`。

## 格式

```
sort(SUBROUTINE LIST)
sort(LIST)
sort SUBROUTINE LIST
sort LIST
```

## 示例 3.39

（脚本）

```perl
use warnings;
# 简单的字母顺序排序
1 my @list = ("dog", "cat", "bird", "snake");
  print "原始列表: @list\n";
2 my @sorted = sort @list;
  print "ASCII 排序: @sorted\n";

# 反转的字母顺序排序
4 @sorted = reverse sort @list;
  print "反转 ASCII 排序: @sorted\n";
```

（输出）

```
Original list: dog cat bird snake
ASCII sort: bird cat dog snake
Reversed ASCII sort: snake dog cat bird
```

## 解释

-   1. `@list` 数组将包含要排序的项目列表。
-   2. `sort` 函数对各项执行字符串排序（对于当前区域设置，即字典序）。排序后的值必须赋值给另一个列表或同一列表。`sort` 函数不会改变原始列表。
-   3. 打印排序后的字符串。
-   4. 此列表按字母顺序排序，然后反转。

## 使用子程序进行 ASCII 和数字排序

你可以定义一个子程序或使用内联函数来执行自定义排序，如下面的示例所示。关于 `$a` 和 `$b` 的说明：它们是 Perl 中的特殊全局变量，供 `sort` 函数在比较值时使用。如果你需要了解所使用的运算符的更多信息，请参阅第 6 章“运算符在哪里？”。

## 5.3 数组函数

### 示例 5.40

（脚本）

```perl
use warnings;
my @list=("dog","cat","bird","snake");
print "Original list: @list\n";
# 使用子程序进行 ASCII 排序
sub asc_sort{
    $a cmp $b; # 升序排序
}
@sorted_list=sort asc_sort(@list);
print "ASCII sort: @sorted_list\n";
# 使用子程序进行数字排序
sub numeric_sort{
    $a <=> $b; # $a 和 $b 按数值比较
}
@number_sort=sort numeric_sort 10, 0, 5, 9.5, 10, 1000;
print "Numeric sort: @number_sort\n";
```

（输出）

```
Original list: dog cat bird snake
ASCII sort: bird cat dog snake
Numeric sort: 0 5 9.5 10 10 1000.
```

### 解释

-   1. `@list` 数组将包含要排序的项目列表。
-   2. 将字符串列表发送给子程序 `asc_sort()` 以进行排序。
-   3. 在按升序比较要排序的项目时，使用特殊全局变量 `$a` 和 `$b`。如果 `$a` 和 `$b` 互换（例如，`$b cmp $a`），则按降序排序。比较字符串时使用 `cmp` 运算符。
-   4. `sort` 函数将一个列表发送给用户定义的子程序 `asc_sort()`，在其中执行排序。排序后的列表将被返回并存储在 `@sorted_list` 中。
-   5. 这是一个用户定义的子程序，名为 `numeric_sort()`。特殊变量 `$a` 和 `$b` 按数值升序比较要排序的项目。如果 `$a` 和 `$b` 互换（例如，`$b <=> $a`），则按数值降序排序。比较数字时使用 `<=>` 运算符。
-   6. `sort` 函数将数字列表发送给 `numeric_sort()` 函数，并获取一个排序后的数字列表，存储在 `@number_sort` 数组中。

### 示例 5.41

（脚本）

```perl
use warnings;
# 使用块对数字进行排序
1 my @sorted_numbers = sort {$a <=> $b} (3,4,1,2);
2 print "The sorted numbers are: @sorted_numbers", "\n";
```

（输出）

```
2 The sorted numbers are: 1 2 3 4.
```

### 解释

-   1. 给 `sort` 函数提供一个块（也称为**内联子程序**），用于对作为参数传入的数字列表进行排序。使用 `<=>` 运算符与变量 `$a` 和 `$b` 一起比较数字。排序后的数字列表被返回并存储在数组 `@sorted_numbers` 中。（有关 `sort` 函数的更多信息，请参阅 <http://perldoc.perl.org/functions/sort.html>）。
-   2. 打印排序后的列表。

## 5.3.9 检查数组索引值是否存在

**`exists` 函数。** 如果数组索引（或哈希键）已定义，`exists` 函数返回 **true**；如果未定义，则返回 **false**。它最常用于测试哈希键是否存在。

## 格式

```
exists $ARRAY[index];
```

## 示例 5.42

（脚本）

```perl
use warnings;
1 my @names = qw(Tom Raul Steve Jon);
2 print "Hello $names[1]\n", if exists $names[1];
3 print "Out of range!\n", if not exists $names[5];
```

（输出）

```
2 Hello Raul
3 Out of range!
```

## 解释

-   1. 将姓名数组赋值给 `@names`。
-   2. 如果索引 *1* 已定义，`exists` 函数返回 `true`，并打印该字符串。
-   3. 如果索引 *5* 不存在（在此示例中确实不存在），则打印字符串 *Out of range!*。

## 5.3.10 反转数组

`reverse` 函数。`reverse` 函数反转列表中的元素，因此如果数值原本按降序排列，现在变为升序，反之亦然。在标量上下文中，它连接列表元素并返回一个所有字符都反转的字符串；例如，在标量上下文中，`Hello, there!` 反转为 `,erreh! olleH`。

## 格式

```
reverse (LIST)
reverse LIST
```

## 示例 5.43

（脚本）

```perl
use warnings;
my (@names, @reversed);
# 反转数组元素
1 @names=('Bob', 'Dan', 'Tom', 'Guy');
2 print @names "\n";
3 my @reversed=reverse @names, "\n";
4 print "@reversed\n";
```

（输出）

```
2 Bob Dan Tom Guy
4 Guy Tom Dan Bob
```

### 解释

-   1. 将列表值赋值给数组 `@names`。
-   2. 打印原始数组。
-   3. `reverse` 函数反转列表中的元素并返回反转后的列表。它不会改变原始数组；也就是说，数组 `@names` 未被更改。反转后的项目存储在 `@reversed` 中。
-   4. 打印反转后的数组。

## 5.4 哈希（关联数组）函数

### 5.4.1 `keys` 函数

`keys` 函数以随机顺序返回一个数组，其元素是哈希的键（另请参阅第 5.4.2 节“`values` 函数”和第 5.4.3 节“`each` 函数”）。从 Perl 5.12 开始，`keys` 还返回数组的索引值。在标量上下文中，它返回键（或索引）的数量。

### 格式

```
keys (ASSOC_ARRAY)
keys ASSOC_ARRAY
```

### 示例 5.44

（脚本）

```perl
use warnings;
my(%weekday, @daynumber, $key);
# keys 函数返回哈希的键
1 my %weekday= (
    '1'=>'Monday',
    '2'=>'Tuesday',
    '3'=>'Wednesday',
    '4'=>'Thursday',
    '5'=>'Friday',
    '6'=>'Saturday',
    '7'=>'Sunday',
);
2 my @daynumber = keys(%weekday);
3 print "@daynumber\n";
4 foreach $key ( keys(%weekday) ){print "$key ";}
print "\n";
5 foreach $key ( sort keys(%weekday) ){print "$key ";}
print "\n";
```

（输出）

```
6 4 1 3 7 2 5
6 4 1 3 7 2 5
1 2 3 4 5 6 7
```

### 解释

-   1. 将键和值赋值给哈希 `%weekday`。
-   2. `keys` 函数返回哈希中所有键的列表。在此示例中，`@daynumber` 是 `%weekday` 哈希中所有键的无序列表。
-   4. `keys` 函数返回键的列表。`foreach` 循环将遍历该键列表，每次打印一个键。
-   5. `keys` 函数返回 `%weekday` 哈希中的键列表。然后对该列表进行排序，最后 `foreach` 循环遍历排序后的键列表，每次打印一个键。

### 5.4.2 `values` 函数

`values` 函数以随机顺序返回由命名哈希的所有值组成的列表。（在 Perl 5.12 之后，它还返回数组的值。）在标量上下文中，它返回值的数量。

### 格式

```
values (ASSOC_ARRAY)
values ASSOC_ARRAY
```

### 示例 5.45

（脚本）

```perl
use warnings;

# values 函数返回哈希中的值
1 my %weekday= {
    '1'=>'Monday',
    '2'=>'Tuesday',
    '3'=>'Wednesday',
    '4'=>'Thursday',
    '5'=>'Friday',
    '6'=>'Saturday',
    '7'=>'Sunday',
};
2 foreach my $val ( values(%weekday) ){
    print "$val\n";
}
```

（输出）

```
2 Saturday Thursday Monday Wednesday Sunday Tuesday Friday
```

### 解释

-   1. 将键和值赋值给哈希 `%weekday`。
-   2. `values` 函数从哈希 `%weekday` 中返回值的列表。使用 `foreach` 遍历值列表，每次处理一个值，使用 `$val` 作为循环变量。

由于哈希以随机顺序存储，若要按赋值顺序获取哈希值，可以使用哈希切片，如下面的示例所示。

### 示例 5.46

（脚本）

```perl
use warnings;

# 使用哈希切片以顺序获取返回的值。
1 my %weekday= {
    '1'=>'Monday',
    '2'=>'Tuesday',
    '3'=>'Wednesday',
    '4'=>'Thursday',
    '5'=>'Friday',
    '6'=>'Saturday',
    '7'=>'Sunday',
};

