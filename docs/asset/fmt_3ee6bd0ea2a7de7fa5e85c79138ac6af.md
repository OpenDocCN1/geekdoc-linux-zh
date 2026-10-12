
### 解释

- 1. `feature` 模块允许你像使用 `print` 函数一样使用 `say` 函数，不同之处在于它会在输出字符串末尾添加换行符，并且可能节省一点时间。
- 2. 我们将使用 `Data::Dumper` 模块对数组的数组进行美化打印。
- 3. 通过设置 `Data::Dumper` 的 `indent` 值，输出将把 `matrix` 显示为一行，而不是在每一行后添加换行符。默认的 `indent` 值为 1。
- 4. `@matrix` 是一个命名数组，由三个元素组成，即对三个数组的引用；也就是说，这是一个数组引用数组。
- 5. 打印这三个引用。
- 6. 打印指向第一行的引用。
- 7. `@` 符号用于解除第一行的引用。花括号用于块处理 `$matrix[0]`，在这个例子中不是必需的，但在更复杂的表达式中将是必需的。
- 8. 使用中缀箭头运算符来解除引用并访问第一行的值。
- 9. 当两个索引值相邻时，可以省略中缀箭头运算符。
- 10. `Dumper` 函数接受 `@matrix` 的引用并美化打印其值。

## 指向列表列表的引用

在以下示例中，一个引用指向一个匿名的列表列表。注意，在这个例子中，`$matrix` 是指向方括号中匿名数组的引用，而在前面的例子中，`@matrix` 是使用括号包含其值的命名数组。这一区别很重要，因为使用 `/` 而本应使用 `()`（或反之）是一个常见错误。

### 示例 12.7

```perl
(The Script)

  use warnings;

  use strict;

  # 指向二维数组的引用

1  my $matrix = [

       [ 0, 2, 4 ],

       [ 4, 1, 32 ],

       [ 12, 15, 17 ]

     ];

2  print "Row 3 column 2 is $matrix->[2]->[1].\n";

3  print "Dereferencing with two loops.\n";

4  for(my $x=0; $x<3; $x++){ 

5    for(my $y=0;$y<3;$y++){ 

6      print "$matrix->[$x]->[$y] ";

     }

   }

  print "\n";

7  print "Dereferencing with one loop.\n";

8  for(my $i=0; $i < 3; $i++){

9    print "@{$matrix->[$i]}\n";

  }
```

**(输出)**

```
2  Row 3 column 2 is 15.

3  Dereferencing with two loops.

   0  2  4

   4  1  32

   12 15 17

7  Dereferencing with one loop.

   0 2 4

   4 1 32

   12 15 17
```

## 12.1 什么是引用？

387

### 解释

- 1 引用（指针）`$matrix` 被赋值为三个匿名数组的匿名数组，即二维（列表的列表）。
- 2 使用箭头运算符访问数组的第一个元素。相邻的下标括号之间隐含了箭头，因此不需要显式写出。它可以写成 `$matrix->[2][1]`。
- 4 进入外层 `for` 循环。这将遍历数组的行。
- 5 进入内层 `for` 循环。此循环遍历数组的列。
- 6 通过引用（指针）打印二维数组的每个元素。
- 8 这次，只使用一个 `for` 循环来打印矩阵的内容。
- 9 使用块格式解除引用的引用。打印每个列表的所有元素。

**哈希数组**。列表可以包含哈希或指向哈希的引用。在示例 12.8 中，一个引用被赋值为包含两个匿名哈希引用的匿名数组。

### 示例 12.8

```perl
use Data::Dumper;

use warnings;

use strict;

my $petref = [ { "name" => "Rover",

"type" => "dog",

"owner" => "Mr. Jones",

},

{ "name" => "Sylvester",

"type" => "cat",

"owner" => "Mrs. Black",

}

];

print "the first pet's name is $petref->[0]->{name}.\n";

print "Printing an array of hashes.\n";

for my $i (0..2){

foreach my $key (keys @{$petref->[$i]}) {

print "$key - $petref->[$i]->{$key}\n";

}

print "\n";

}

print "Adding a hash to the array.\n";

push @$petref, {"owner"=>"Mrs. Crow",

"name"=>"Tweety",

"type"=>"bird",

};

print Dumper $petref;
```

**(输出)**

```
4   The first pet's name is Rover.

    Printing an array of hashes.

7   owner -- Mr. Jones

    name -- Rover

    type -- dog

    owner -- Mrs. Black

    name -- Sylvester

    type -- cat

Adding a hash to the array.

$VAR1 = [

    {

        'owner' => 'Mr. Jones',

        'name' => 'Rover',

        'type' => 'dog'

    },

    {

        'owner' => 'Mrs. Black',

        'name' => 'Sylvester',

        'type' => 'cat'

    },

    {

        'owner' => 'Mrs. Crow',

        'name' => 'Tweety',

        'type' => 'bird'

    }

];
```

### 解释

- 1   引用 `$petref` 被赋值为一个包含两个匿名哈希引用的匿名数组的地址。
- 2   这是第二个列表元素，一个带有其键/值对的匿名哈希引用。
      这是匿名数组的结束右方括号。
- 3   引用 `$petref` 用于解除列表引用，首先通过选择数组的零元素，然后使用箭头运算符选择哈希中的键。
      显示与键 `name` 关联的值。
- 6   进入 `for` 循环，使用 `$i` 代表数组中的索引值来遍历列表。数组的每个元素都是一个匿名哈希。
- 7, 8   进入 `foreach` 循环。它遍历来自匿名哈希的每个键，`name, type, owner`。每次循环，键 `$Key` 及其值 `$petref`->{$i}->{$key} 都会被打印。
- 9   一个新的匿名哈希引用被推送到数组的末尾。使用内置的 `push` 函数作用于 `@{$petref}`。
- 10  `Data::Dumper` 模块中的 `Dumper` 函数显示哈希数组。

## 哈希中的哈希

一个哈希（hash）可能包含另一个哈希，或者一组哈希引用。在示例 12.9 中，一个引用被分配了一个由两个键组成的匿名哈希引用，每个键都关联着一个值，而这些值恰好又是另一个哈希引用（包含其自身的键/值对）。

### 示例 12.9

```perl
use Data::Dumper;

use strict;

use warnings;

# 包含匿名哈希的哈希引用。

1 my $hashref = {

2   Math => {

3     "Anna" => 100,    # 键

4     "Hao" => 95,      # 值

5     "Rita" => 85,

6   },

7   Science => {

8     "Sam" => 78,      # 键

9     "Lou" => 100,     # 值

10    "Vijay" => 98,

11  },

12 };

13 print "Anna got $hashref->{Math}->{Anna} on the Math test.\n";

14 $hashref->{Science}->{Lou} = 90;

15 print "Lou's grade was changed to $hashref->{Science}->{Lou}.\n";

16 print "The nested hash of Math students and grades is: ";
```
