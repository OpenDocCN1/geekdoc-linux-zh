
The string contains one MT two MT three MT four MT five

`D:\>Perl\book>`

这个编程示例演示了 `join` 函数与我们在本节中介绍的其他数组函数结合使用。现在，让我们继续到本节的最后一个函数。

`split` 函数用于将字符串“分割”为列表，这与 `join` 函数的作用相反。`split` 的语法为：

```perl
@array = split("separator", $string);
```

`split` 函数在字符串中搜索分隔符并创建一个新数组。这里有一个使用 `split` 的编程示例：

```perl
#!/usr/bin/perl

$string = "one two three four";

print "The original string contains $string\n\n";

@array = split(" ", $string);

print "The array contains @array\n";
```

## 第 4 模块：列表、数组与哈希 147

上一行代码从哈希中检索与键键位置对应的一个元素。除了可以检索元素外，你还可以使用以下语法添加新元素。

```perl
$hash($key) = $value;
```

上一行代码在现有的哈希中创建一个新元素，如果该哈希尚不存在，它还会创建一个新的哈希。这里有一个简单的编程示例，演示了如何以几种不同的方式创建哈希：

```perl
#!usr/bin/perl

$hash = (a, 1, b, 2, c, 3, d, 4);

$value = $hash(a);

print "The value stored under the key is $value \n\n";

$value1 = $hash(c);

print "The value stored under the c key is $value1 \n\n";

$hash1(e) = 5;

print "The value stored under the e key is $hash1(e) \n";

$value2 = $hash1(e);

print "The value stored under the newly created e key is $value2 \n\n";

$hash2(f) = 6;

print "The value stored under the f key is $hash2(f) \n\n";

$value3 = $hash2(f);

print "The value stored in the new hash is $value3 \n\n";
```

上一个编程示例的输出见下所示。

![](img/2070407c4a70134aab89572f10d21e60_170_0.png)

## Perl：初学者指南

你可能已经从上一个示例注意到我们并没有一次性打印第一个哈希的所有内容。你不能简单地将哈希变量名放在双引号内让它插值其内容。如果你想查看哈希的所有内容，通过将哈希赋值给数组并打印该数组可以轻松实现。以下几行代码向屏幕打印了上一个示例中使用的 `%hash` 变量的键和值：

```perl
@array = %hash;

print "The keys and elements stored in %hash are @array \n";
```

### 注意

当你将哈希赋值给数组变量时，元素的顺序并不一定是正确的。如果必须这样做，请记住这一点。此外，哈希名称 `%hash` 被作为字符串的一部分打印出来，因为它在双引号内不被视为变量名。

现在你已经了解了如何在哈希中创建和存储值，你需要学习几个应该大有用场的哈希函数。我们讨论的第一个函数是 `keys` 函数，它可以用于选择哈希中存储的所有键，并将它们存储在数组变量中。一旦存储了键列表，你就可以更轻松地遍历哈希了。以下是 `keys` 函数的语法：

```perl
keys(%hash);
```

如果你想将键的列表存储在数组变量中，可以使用以下行代码：

```perl
@array = keys(%hash);
```

现在你已经接触了 `keys` 函数，这里有一个演示其某些用途的编程示例：

## 第 4 模块：列表、数组与哈希

这是一个遍历整个哈希并打印其所有键和值的循环。

创建了一个包含四个元素的哈希

```perl
#!/usr/bin/perl

%hash1 = (a, 1, b, 2, c, 3, 4);

@array1 = keys(%hash1);

print "The keys in the hash variable are @array1 \n";

foreach $key (keys(%hash1)) {

    print "The current key is $key \n";

    print "The corresponding value is $hash1{$key} \n";

}

if ($hash1) {

    print "The Hash contains at least one element \n";

}

else {

    print "The Hash is empty \n";

}
```

这个 if-if-else 结构判断了哈希是否为空。

上一个编程示例的输出见下所示。

![](img/2070407c4a70134aab89572f10d21e60_172_0.png)

# 150 Perl：初学者指南

我们涵盖的下一个函数与 `keys` 函数密切相关。`values` 函数返回的不是哈希的键，而是它的哈希的值。以下是 `values` 函数的语法：

```perl
values(%hash);
```

如果你想将值的列表存储在数组变量中，可以使用以下行代码：

```perl
@array = values(%hash);
```

尽管你可以使用此函数从哈希中获取值，它可能对你没有用，因为你无法获得相应键的列表。键是哈希的基础组成部分，正是它们的存在使得哈希变得如此有用。如果你不知道哪些键与元素对应，并且可以不需要它们，那么你可能应该使用数组而不是哈希。以下编程示例演示了 `values` 函数的使用：

| 创建了一个包含四个元素的哈希 | 哈希中的所有值都存储在数组变量 @array1 中 |
| :--- | :--- |
| !/usr/bin/perl | %hash1 = (a, 1, b, 2, c, 3, 4); |
| @array1 = keys(%hash1); | print "The keys in the hash variable are @array1 \n"; |
| foreach $key (keys(%hash1)) { | print "The current key is $key \n"; |
| print "The corresponding value is $hash1{$key} \n"; | } |
| if ($hash1) { | print "The Hash contains at least one element \n"; |
| else { | print "The Hash is empty \n"; } |
| 这个 if-if-else 结构判断了哈希是否为空 | |

## 第 4 模块：列表、数组与哈希 174

上一个编程示例的输出见下所示。

![](img/2070407c4a70134aab89572f10d21e60_172_0.png)

我们涵盖的下一个函数与 `keys` 函数密切相关。`values` 函数返回的不是哈希的键，而是它的哈希的值。以下是 `values` 函数的语法：

```perl
values(%hash);
```

如果你想将值的列表存储在数组变量中，可以使用以下行代码：

```perl
@array = values(%hash);
```

尽管你可以使用此函数从哈希中获取值，它可能对你没有用，因为你无法获得相应键的列表。键是哈希的基础组成部分，正是它们的存在使得哈希变得如此有用。如果你不知道哪些键与元素对应，并且可以不需要它们，那么你可能使用数组而不是哈希。以下编程示例演示了 `values` 函数的使用：

我们涵盖的下一个函数是 `delete` 函数，它应该大有用场，因为你知道如何创建和向哈希添加元素，但不知道如何删除。`each` 函数是从哈希中获取所有值和键的快捷方法。不需要先存储所有键，然后逐个遍历获取所有值，`each` 从哈希开始检索键值对，并在每次调用时自动递增，直到到达哈希结束。该函数的语法如下：

```perl
delete(%hash);
```

这里有一个使用 `each` 打印哈希所有键和元素的编程示例：

```perl
#!usr/bin/perl

hash1 = (a, 1, b, 2, c, 3, d, 4);

while (@values = each(%hash1)) {

    print "The key/value pair is @values \n"
}
```
