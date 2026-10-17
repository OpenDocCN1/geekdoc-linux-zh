
`vector<int> array(data, data + 10);`

该程序演示了 `remove()` 的一个怪癖。调用 `remove()` 并将搜索参数设为 `6`

```
remove(array.begin(), array.end(), 6);
```

会删除该值但不会调整 resulting 数组。因此，容器现在具有值
`1 2 3 4 5 7 8 9 10 10`

容器末尾重复的 `10` 是 `remove()` 删除值 `6` 并将其他值上移一位的结果。然而，最终值也需要擦除。通过改为按如下方式调用 `remove()` 并将结果迭代器保存在变量中来完成此操作：

```
vector<int>::iterator start =
remove(array.begin(), array.end(), 6);
```

迭代器 `start` 是容器类导出的迭代器类型。为了清理最终容器，将 `remove()` 返回的迭代器以及定义范围末尾的第二个迭代器（通常是容器的末尾）传递给容器的 `erase()` 函数：

```
array.erase(start, array.end());
```

现在数组正确地包含九个值。另一方面，也许你不想擦除剩余的值。在这种情况下，你可以将其设为零：
`*start = 0;`

> Tip
> 请记住，`remove()` 仅影响目标值，而不影响容器中的其他值。从容器中删除对象后通常需要对剩余值进行后续操作，但这始终是可选的。

## 条件删除

**算法：**

- `remove_if()`
- `remove_copy()`
- `remove_copy_if()`

**示例程序：**

- `remov-ex.cpp`

STL 提供了三种 `remove()` 算法的变体。`remove_if()` 算法删除满足条件的数值。该算法定义如下：

```
ForwardIterator remove_if(
  ForwardIterator first, ForwardIterator last,
  Predicate pred)
```

参数与 `remove()` 相同，但谓词函数对象决定是否对特定值执行操作。通常，谓词是一个派生自 STL `unary_function` 模板的类。包含 `<functional>` 头文件，然后按示例程序所示设计你的类：

```
template<class T>
class is_even: public unary_function<T, bool>
{
  public:
    bool operator()(const T& x){
      return (x % 2) == 0; }
};
```

该类不必是模板。如果知道容器中数据的类型，可将 `T` 改为该类型。例如，在本例中可将 `T` 改为 `int`。新的类 `is_even` 只需要一个元素——重载的 `operator()` 函数。该函数根据对常量引用参数 `x` 应用的某些条件返回 `bool` `true` 或 `false` 值。在本例中，我将函数编程为当 `x` 为偶数时返回 `true`。

要将谓词类应用于容器中的值，请将该类的对象传递给 `remove_if()` 算法。例如，以下语句从数组容器中删除所有偶数值：

```
start = remove_if(array.begin(), array.end(), is_even<int>());
```

这里，同样保存了 resulting 迭代器，以便后续操作可以擦除容器中剩余的值。使用数组中的值（1 到 10，不包括 6），前述语句在 `array` 中留下以下值：

```
1 3 5 7 9 7 8 9 10
```

最后四个值是删除原始数组中四个偶数值后留下的残留值。为了清理结果，使用保存的迭代器调用容器的 `erase()` 函数：

```
array.erase(start, array.end());
```

现在数组只包含奇数值：

```
1 3 5 7 9
```

### 提示

> 不必测试 `remove_if()` 返回的迭代器是否等于尾后值。将该值传递给 `erase()` 不会造成损害，实际上什么也不做。

另外两种删除算法 `remove_copy()` 和 `remove_copy_if()` 与 `remove()` 和 `remove_if()` 工作方式相同，但将结果存放在目标容器中。原始容器中的对象不受影响。`remove_copy()` 算法定义如下：

```
OutputIterator remove_copy(
InputIterator first, InputIterator last,
OutputIterator result, const T& value)
```

两个迭代器定义了搜索值的对象范围，常量引用 `T` 指定要删除的值。第三个迭代器 `result` 指定算法复制剩余值到的容器中的起始位置。`remove_copy_if()` 算法类似地定义如下：

```
OutputIterator remove_copy_if(
InputIterator first, InputIterator last,
OutputIterator result, Predicate pred)
```

唯一的区别是谓词对象决定哪些对象符合删除条件。谓词对象通常是如 `is_even` 的类，派生自 STL 的 `unary_function` 模板，如前一节所述。

为演示如何使用 `remove_copy()`，示例程序定义了两个 `vector` 容器：

```
vector<int> invec(data, data + 10);
vector<int> outvec(invec.size(), 0);
```

`invec` 向量初始化为 `1, 2, ..., 10` 的序列。`outvec` 向量与 `invec` 相同大小，但其值初始化为零。要创建除去值 `8` 的新向量，按如下方式调用 `remove_copy()`：

```
start = remove_copy(
invec.begin(), invec.end(), outvec.begin(), 8);
```

resulting `outvec` 容器现在包含除去 `8` 的值序列：

```
1 2 3 4 5 6 7 9 10 0
```

然而，尾随的零再次需要后续的擦除：

```
outvec.erase(start, outvec.end());
```

调用 `remove_copy_if()` 并配合谓词函数对象来确定是否应删除某个值。为演示，示例程序构造了一个整数向量 `oddballs`，其大小与 `invec` 相同（仍保存序列 `1, 2, ..., 10`），初始化为零。

```
vector<int> oddballs(invec.size(), 0);
```

调用 `remove_copy_if()` 并使用以下参数可将所有奇数值移除到 `oddballs` 中，而不会以任何方式干扰 `inVec`：

```
start = remove_copy_if(inVec.begin(), inVec.end(),
    oddballs.begin(), is_even<int>());
```

要额外删除目标向量中未使用的值，程序调用 `erase()`，并传递算法返回的迭代器和容器的 `end()` 值：

```
oddballs.erase(start, oddballs.end());
```

之后，`oddballs` 向量包含序列

`1 3 5 7 9`

## REMOVING UNIQUE VALUES

算法：

- `unique()`
- `unique_copy()`

示例程序：

`uniq-ex.cpp`

调用 `unique()` 算法可从容器中删除所有重复值。该算法与 `remove()` 类似，它不会清理被移除时移动后留下的值。通常你会调用 `erase()` 来丢弃这些剩余值，但这始终是可选的。`unique()` 算法定义如下：

```
ForwardIterator unique(
    ForwardIterator first, ForwardIterator last)
```

只需向 `unique()` 传递两个迭代器，算法就会删除所有重复值。为了演示，示例程序定义了一个整数向量并用重复值填充它：

```
vector<int> array;
...
for (int i = 1; i < 9; i++)
    for (int j = 1; j <= i; j++)
        array.push_back(i);
```

resulting 向量包含这些值：

`1 2 2 3 3 3 4 4 4 4 5 5 5 5 5 6 6 6 6 6 6`
`7 7 7 7 7 7 7 8 8 8 8 8 8 8 8`

要删除重复项，程序调用 `unique()`。这必须随后跟随 `erase()` 以清理算法在每次移除时将值向上移动后留下的向量值：
