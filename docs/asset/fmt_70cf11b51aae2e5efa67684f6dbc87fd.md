
**（输出）**

Courses in Ascending Numeric Order:
101  Intro to Computer Science
102  Perl
103  PHP
200  Language arts
221  Linguistics
300  Astronomy

Courses in Descending Numeric Order:
300  Astronomy
221  Linguistics
200  Language arts
103  PHP
102  Perl
101  Intro to Computer Science

## 解释

- 1. 这是一个用户定义的子程序，名为 `desc_sort_subject`。当将其名称传递给 `sort` 函数时，该函数将用于比较传入的键。它会按数字顺序对键进行排序。
- 2. 特殊的 Perl 变量 `$a` 和 `$b` 用于比较名为 `%courses` 的哈希中键的值。`<=>` 运算符是一个数字比较运算符，会将待排序的每个键作为数字进行比较。在此前的示例中，我们按字母顺序对键进行了排序。由于 `$b` 位于 `$a` 之前，因此排序为降序。
- 3. 这同样是一个用户定义的子程序，名为 `asc_sort_subject`。此函数与第 1 行的前一个函数相同，除了它会按数字升序而非降序对哈希的键进行排序。
- 4. 在此函数中，特殊变量 `$a` 和 `$b` 的位置互换了，导致比较后的排序变为升序。
- 5. 名为 `%courses` 的哈希由键/值对定义。
- 6. `foreach` 循环将用于遍历哈希中的每个键。它从 `sort` 命令的输出接收列表。
- 7, 8. `printf` 函数格式化并打印键和排序后的值。

**按数值顺序对哈希值进行升序排序。** 要按值对哈希进行排序，也需要定义一个用户自定义函数。哈希的值由特殊变量 `$a` 和 `$b` 进行比较。如果 `$a` 位于比较运算符的左侧，则排序为升序；如果 `$b` 位于左侧，则排序为降序。`<=>` 运算符按数值比较其操作数。

## 示例 5.32

（脚本中）

```perl
use warnings;

sub asc_sort_wins {
   $wins{$a} <=> $wins{$b};
}

my %wins = (
   "Portland Panthers"    => 10,
   "Sunnyvale Sluggers"  => 12,
   "Chico Wildcats"      => 5,
   "Stevensonville Tigers" => 6,
   "Lewiston Blazers"    => 11,
   "Danville Terriers"   => 8,
);

print "\n\tWins in Ascending Numeric Order:\n\n";

foreach my $key (sort asc_sort_wins (keys %wins)) {
   printf "\t% -20s%5d\n", $key, $wins{$key};
}
```

（输出）

Wins in Ascending Numeric Order:
Chico Wildcats 5
Stevensonville Tigers 6
Danville Terriers 8
Portland Panthers 10
Lewiston Blazers 11
Sunnyvale Sluggers 12

## 解释

- 1. 这是一个用户定义的子程序，名为 `asc_sort_wins`。当将其名称传递给 `sort` 函数时，该函数将用于比较传入的哈希值。它会按数值对值进行排序。
- 2. 特殊的 Perl 变量 `$a` 和 `$b` 用于比较名为 `%wins` 的哈希的值。`<=>` 运算符是一个数字比较运算符，将比较待排序的每个值。要比较字符串，则使用 `cmp` 运算符。
- 3. 名为 `%wins` 的哈希被赋以键/值对。
- 4. `foreach` 循环遍历哈希中的每个元素。它从 `sort` 函数返回的结果接收列表。
- 5. `printf` 函数格式化并打印键和排序后的值。

**按数值顺序对哈希值进行降序排序。** 要按数值和降序对哈希值进行排序，如同前一示例那样创建用户自定义函数。但此时，`$b` 变量位于 `<=>` 数字运算符的左侧，而 `$a` 变量位于右侧。这使得 `sort` 函数按降序排序。

## 示例 5.33

（脚本中）

```perl
use warnings;

# Sorting a hash by value in descending order

sub desc_sort_wins {
  $wins{$b} <=> $wins{$a}; # Reverse $a and $b
}

my %wins = (
    "Portland Panthers"  => 10,
    "Sunnyvale Sluggers" => 12,
    "Chico Wildcats"     => 5,
    "Stevensonville Tigers"=> 6,
    "Lewiston Blazers"   => 11,
    "Danville Terriers"  => 8,
  );

print "\n\tWins in Descending Numeric Order:\n";

foreach my $key (sort desc_sort_wins(keys %wins)) {
    printf "\t% -20s%5d\n", $key, $wins{$key};
}
```

（输出）

Wins in Descending Numeric Order:
- Sunnyvale Sluggers 12
- Lewiston Blazers 11
- Portland Panthers 10
- Danville Terriers 8
- Stevensonville Tigers 6
- Chico Wildcats 5

## 解释

- 1. 这是一个用户定义的子程序，名为 `desc_sort_wins`。当将其名称传递给 `sort` 函数时，该函数将用于比较传入的哈希值。它会按数值对值进行降序排序。
- 2. 特殊的 Perl 变量 `$a` 和 `$b` 用于比较名为 `%wins` 的哈希的值。`$a` 和 `$b` 的位置决定了排序是升序还是降序。如果 `$a` 位于 `<=>` 运算符的左侧，则为数字升序排序；如果 `$b` 位于 `<=>` 运算符的左侧，则为降序排序。要比较字符串，则使用 `cmp` 运算符。
- 3. 名为 `%wins` 的哈希被赋以键/值对。
- 4. `foreach` 循环将用于遍历哈希中的每个键。它从 `sort` 函数返回的结果接收列表。
- 5. `printf` 函数格式化并打印键和排序后的值。

## 5.4 哈希（关联数组）函数

### 5.4.6 `delete` 函数

`delete` 函数从哈希中删除指定的元素。如果成功，则返回被删除的值。[^1]

[^1]: 如果删除了 `%ENV` 哈希中的某个值，环境将会改变。（参见第 137 页的“%ENV 哈希”）。

### 示例 5.34

```perl
use warnings;

my %employee = (
     "Nightwatchman" => "Joe Blow",
     "Janitor" => "Teddy Plunger",
     "Clerk" => "Sally Olivetti",
     );

my $layoff = delete $employee{"Janitor"};

print "We had to let $layoff go.\n";

print "Our remaining staff includes: \n";

while (my ($key, $value) = each %employee) {
    print "$key: $value\n";
}
```

（输出）
We had to let Teddy Plunger go.
Our remaining staff includes:
Nightwatchman: Joe Blow
Clerk: Sally Olivetti

### 解释

- 1. 定义了一个包含三个键/值对的哈希。
- 2. `delete` 函数通过指定键从指定的哈希中删除一个元素。
- 3. `Janitor` 是键。键和值都被移除。与键 `Janitor` 关联的哈希值被移除并返回。值 `Teddy Plunger` 被返回并赋给标量 `$layoff`。

### 5.4.7 exists 函数

如果哈希键（或数组索引）存在，`exists` 函数返回 true；如果不存在，则返回 false。

**格式**

```perl
exists $ASSOC_ARRAY[KEY];
```
