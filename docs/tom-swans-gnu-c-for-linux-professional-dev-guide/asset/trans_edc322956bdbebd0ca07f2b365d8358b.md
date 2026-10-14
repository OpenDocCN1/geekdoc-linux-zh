
合并算法有两种形式。一种是将一个数据结构中的对象与另一个数据结构中的对象合并，并将结果存放到第三个容器中。另一种是在同一个容器内合并对象。我们来看第二种，也就是更易于使用的 `inplace_merge()` 算法，其定义如下：

```
void inplace_merge(
BidirectionalIterator first,
BidirectionalIterator middle,
BidirectionalIterator last [, Compare comp ])
```

第一个和最后一个迭代器指定了合并对象的目标范围。`middle` 迭代器指定了合并时源对象的起始位置。你可以选择传入一个二元（双参数）函数，当某个对象值小于另一个时返回 `true`。

为了演示就地合并，示例程序使用以下语句定义了一个容器：

```
int d1[9] = { 2, 4, 6, 8, 1, 3, 5, 7, 9 };
list<int> list1(d1, d1 + 9);
```

这将 list1 设置为所示序列——1 到 9 范围内先是四个偶数，然后是五个奇数。调用 `find()` 可以定位列表中第一个奇数值（1）：

```
list<int>::iterator middle = find(
list1.begin(), list1.end(), 1);
```

程序使用以下语句将得到的 middle 迭代器以及合并的目标范围（整个容器）传入：

```
inplace_merge(list1.begin(), middle, list1.end());
```

结果是同一列表中的值被合并，产生序列 1, 2, ..., 9。

要将两个序列合并到第三个序列中，可使用稍微复杂一些的 `merge()` 算法，其定义如下：

```
OutputIterator merge(
InputIterator1 first1, InputIterator1 last1,
InputIterator2 first2, InputIterator2 last2,
OutputIterator result [, Compare comp ])
```

前四个迭代器定义了要合并的两个容器中对象的范围。result 迭代器是目标容器中的起始位置。为了演示该算法的用法，示例程序定义了两个列表，一个包含偶数值，另一个包含奇数值：

```
int d2[4] = { 2, 4, 6, 8 };
int d3[5] = { 1, 3, 5, 7, 9 };
list<int> list2(d2, d2 + 4);
list<int> list3(d3, d3 + 5);
```

程序还定义了第三个列表来保存合并后的数据。请确保创建的数据结构足够大以容纳结果，或者能够自动扩展。在本例中，示例程序创建了一个整数列表容器，其大小等于两个源列表的大小之和，并将新列表中的所有值初始化为零：

```
list<int> list4(list2.size() + list3.size(), 0);
```

随后，程序按下述方式调用 `merge()`，将 list2 和 list3 合并，并将结果保存到 list4 中：

```
merge(list2.begin(), list2.end(),
list3.begin(), list3.end(), list4.begin());
```

前两个迭代器定义了 list2 中元素的范围。类似地，接下来的两个迭代器定义了 list3 中元素的范围。最后一个参数指定了目标容器中的起始位置，此处是 list4 的开头。执行此语句后，list4 包含序列 1, 2, ..., 9。容器 list2 和 list3 保持不变。

> 注意
> 合并是一种稳定操作。这意味着合并后，任何重复对象在容器中都保持其原有的相对顺序。

## 集合算法

算法：

- set_union()
- set_intersection()
- set_difference()
- set_symmetric_difference()
- includes()

示例程序：

```
set-ex.cpp
```

如第24章“构建标准容器”中“集合与多重集合”一节所述，set 容器并不提供 union、intersection 等运算符。这是因为 set 仅仅是对象的有序容器——它们并不是数学意义上的集合。为了提供通常应用于这类数据集合的逻辑运算，STL 提供了适用于任何有序数据集合的通用算法。你可以在 set 容器中使用这些算法，也可以在 vector、list 以及任何其数据对象可按某种逻辑顺序维护的容器中使用它们。

四个基本的集合算法是 set_union()、set_intersection()、set_difference() 和 set_symmetric_difference()。它们都采用与这里为 set_union() 所示的相同的一般形式，定义如下：

```
OutputIterator set_union(
InputIterator1 first1, InputIterator1 last1,
InputIterator2 first2, InputIterator2 last2,
OutputIterator result [, Compare comp ])
```

