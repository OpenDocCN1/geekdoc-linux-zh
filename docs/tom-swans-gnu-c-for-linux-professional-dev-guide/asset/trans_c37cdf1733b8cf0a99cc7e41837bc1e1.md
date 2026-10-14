

鉴于 colors1 等于集合 {Orange, Red} 且 colors4 等于 {Blue, Indigo, Orange, Red, Violet}，程序将集合 {Blue, Indigo, Violet} 插入到 colors7 中。在这种情况下，无论源集合迭代器的顺序如何，结果集合都相同。

当不方便预先确定结果集合的大小时，可以使用插入迭代器与任何集合算法一起使用。例如，使用如下语句定义一个空的字符串集合和一个插入对象：

```
TSet colorsX;
insert_iterator<TSet> ins(colorsX, colorsX.begin());
```

这使得 colorsX 成为一个空的字符串集合。使用为与容器相同的类实例化的 STL insert_iterator 模板。该对象在此命名为 ins，是使用容器名称（colorsX）和插入开始的位置构造的——此处为空容器的开头。如果目标容器不为空，这可以是另一个迭代器，例如定义为在中间或末尾开始插入。使用示例程序中演示的 ins 插入迭代器对象：

```
set_union(
colors1.begin(), colors1.end(),
colors3.begin(), colors3.end(), ins);
```

这会找到两个集合 colors1 和 colors3 的并集，并将结果存放在插入迭代器对象 ins 所指定的位置。

## ITERATIVE ALGORITHMS

- Algorithm: for_each()
- Sample program: for-ex.cpp

for_each() 算法对定义范围内的对象执行任意操作。使用此算法为容器中的值调用你自己的函数。for_each() 算法定义如下：

```
Function for_each(
InputIterator first, InputIterator last, Function f)
```

与往常一样，两个迭代器定义了要对算法调用函数 f() 的对象范围。这里的 Function 是一个模板占位符，定义了你想要调用的函数类型。这意味着 for_each() 返回你的函数返回的任何值——void、引用、指针或对象，任何适当的值。

> Note
> STL 的过去版本将 for_each() 定义为返回 void。较新版本更通用，并且因为它也可以返回 void，所以与早期形式兼容。

唯一严格的规则是指定的函数不得通过添加或删除对象来更改容器，这会改变迭代器参数的含义。虽然你可以使用 for_each() 与常用函数一起使用，但更可能的是你会创建一个重载 operator() 的类——函数调用运算符。这允许表达式“调用”一个对象，就好像它是一个函数一样，从而提供以编程方式实现高度复杂操作的方法。为了演示如何以这种方式使用 for_each()，示例程序创建了一个名为 array 的整数数据向量：

```
int data[5] = { 2, 4, 6, 9, 10 };
vector<int> array(data, data + 5);
```

我们想要对 array 容器中的所有值执行某些操作。为了展示如何为此使用类模板，示例程序从 STL 的 unary_function 类派生出类 Times：

```
template <class T>
class Times: private unary_function<T, void>
{
    T multiplier;
public:
    Times(const T& m): multiplier(m) { }
    void operator()(const T& arg)
    { cout << setw(4) << arg * multiplier << endl; }
};
```

你可以像这里所示那样私有继承 unary_function 类，也可以使用 protected 或 public 访问说明符。只需要两项：一个用于尚未指定的类型 T 的参数化构造函数和一个重载的 operator() 函数。在这里，示例程序将参数与保存在 Times 对象中的乘数相乘并显示该值。

要使用 Times 类，使用一个值构造它，在此示例中该值乘以 array 容器中的每个值：

```
Times<int> t10(10);
```

要对每个值执行操作，调用 for_each()，传递要为其调用 Times 对象重载的 operator() 函数的对象范围：

```
for_each(array.begin(), array.end(), t10);
```

由于重载的类运算符在相乘时显示每个值，因此此简单语句也显示了结果值，如使用以下命令编译和运行程序时所见：

```
$ g++ for-ex.cpp
$ ./a.out
...
array * 10
  20
  40
  60
  90
 100
```

