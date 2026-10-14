

有很多常见的数组操作。诸如删除数组、确定其大小、排序等，在脚本编写中有许多应用。

## 输出数组的全部内容

下标 * 和 @ 可用于访问数组中的每个元素。与位置参数一样，@ 记法是两者中更有用的记法。以下是演示：

```
[me@linuxbox ~]$ animals=("a dog" "a cat" "a fish")
[me@linuxbox ~]$ for i in ${animals[*]}; do echo $i; done
a
dog
a
cat
a
fish
[me@linuxbox ~]$ for i in ${animals[@]}; do echo $i; done
a
dog
a
cat
a
fish
[me@linuxbox ~]$ for i in "${animals[*]}"; do echo $i; done
a dog a cat a fish
[me@linuxbox ~]$ for i in "${animals[@]}"; do echo $i; done
a dog
a cat
a fish
```

我们创建数组 animals 并为其分配三个由两个词组成的字符串。然后我们执行四个循环来观察词分割对数组内容的影响。记法 ${animals[*]} 和 ${animals[@]} 的行为在未加引号时是相同的。* 记法会产生一个包含数组内容的单个词，而 @ 记法会产生三个由两个词组成的字符串，这与数组的“真实”内容相匹配。

## 确定数组元素的数量

使用参数扩展，我们可以以与查找字符串长度类似的方式确定数组中的元素数量。以下是一个示例：

```
[me@linuxbox ~]$ a[100]=foo
[me@linuxbox ~]$ echo ${#a[@]}  # number of array elements
1
[me@linuxbox ~]$ echo ${#a[100]}  # length of element 100
3
```

我们创建数组 a 并将字符串 foo 分配给元素 100。接下来，我们使用参数扩展来检查数组的长度，使用 @ 记法。最后，我们查看元素 100 的长度，其中包含字符串 foo。有趣的是，虽然我们将字符串分配给了元素 100，但 bash 报告数组中只有一个元素。这与某些其他语言的行为不同，在那些语言中，数组中未使用的元素（元素 0–99）会被初始化为空值并计入总数。在 bash 中，数组元素只有在被赋予值时才存在，无论其下标如何。

## 查找数组使用的下标

由于 bash 允许数组在下标分配上存在“空隙”，因此有时需要确定哪些元素实际存在。这可以通过使用以下形式的<|message|> 参数扩展来完成：

```
${!array[*]}
${!array[@]}
```

其中 array 是数组变量的名称。与使用 * 和 @ 的其他扩展一样，用引号括起来的 @ 形式是最有用的，因为它会扩展为单独的词。

```
[me@linuxbox ~]$ foo=([2]=a [4]=b [6]=c)
[me@linuxbox ~]$ for i in "${foo[@]}"; do echo $i; done
a
b
c
[me@linuxbox ~]$ for i in "${!foo[@]}"; do echo $i; done
2
```

## 向数组末尾添加元素

如果我们需要向数组末尾追加值，仅知道数组中的元素数量是没有帮助的，因为 * 和 @ 记法返回的值并不能告诉我们当前使用的最大数组索引。幸运的是，shell 为我们提供了解决方案。通过使用 += 赋值运算符，我们可以自动向数组末尾追加值。在这里，我们将三个值分配给数组 foo，然后再追加三个值：

```
[me@linuxbox ~]$ foo=(a b c)
[me@linuxbox ~]$ echo ${foo[@]}
a b c
[me@linuxbox ~]$ foo+=(d e f)
[me@linuxbox ~]$ echo ${foo[@]}
a b c d e f
```

## 排序数组

与电子表格一样，通常需要对数据列中的值进行排序。shell 没有直接的方法来执行此操作，但通过一点编码并不难做到。

```
#!/bin/bash

# array-sort: Sort an array

a=(f e d c b a)

echo "Original array: ${a[@]}"
a_sorted=($(for i in "${a[@]}"; do echo $i; done | sort))
echo "Sorted array:  ${a_sorted[@]}"
```

执行脚本时，会产生以下输出：

```
[me@linuxbox ~]$ array-sort
Original array: f e d c b a
Sorted array:   a b c d e f
```

脚本通过使用巧妙的命令替换将原始数组（a）的内容复制到第二个数组（a_sorted）来工作。这种基本技术可以通过更改管道的设计来对数组执行许多种操作。

## 删除数组

要删除数组，请使用 unset 命令。

```
[me@linuxbox ~]$ foo=(a b c d e f)
[me@linuxbox ~]$ echo ${foo[@]}
a b c d e f
[me@linuxbox ~]$ unset foo
[me@linuxbox ~]$ echo ${foo[@]}

[me@linuxbox ~]$
```

unset 也可用于删除单个数组元素。

```
[me@linuxbox ~]$ foo=(a b c d e f)
[me@linuxbox ~]$ echo ${foo[@]}
a b c d e f
[me@linuxbox ~]$ unset 'foo[2]'
[me@linuxbox ~]$ echo ${foo[@]}
a b d e f
```

在此示例中，我们删除了数组的第三个元素，下标为 2。记住，数组从下标零开始，而不是一！另请注意，数组元素必须加引号以防止 shell 执行路径名扩展。

有趣的是，将空值赋给数组并不会清空其内容。

```
[me@linuxbox ~]$ foo=(a b c d e f)
[me@linuxbox ~]$ foo=
[me@linuxbox ~]$ echo ${foo[@]}
b c d e f
```

对数组变量的任何不带下标的引用都指的是数组的零号元素。

