
从生成器函数 `func` 创建上下文器的装饰器。使用此装饰器的方法如下：

```python
@contextmanager
def foo(args):
    statements
    try:
        yield value
    except Exception as e:
        error handling (if any)
    statements
```

调用 `foo(args)` 时，它返回一个上下文管理器。`yield` 返回的值传递给 `with` 语句。如果在语句内部抛出异常，将被处理。此装饰器的示例可见第 5 章。

### nested(mgr1, mgr2, ..., mgrN)

调用多个上下文管理器的函数。它返回一个包含后续管理器的组。

### closing(object)

创建一个上下文管理器，在离开语句体时自动执行 `object.close()`。语句的返回值与 `object` 相同。

## functools

`functools` 模块包含用于创建高阶函数、函数式编程和装饰器的函数和装饰器。

### partial(func, *args, **kwargs)

创建一个类似函数的对象 `partial`，调用时会带位置参数和关键字参数调用 `func`。额外的位置参数将添加到 `args` 的末尾，关键字参数将合并到 `kwargs` 中并覆盖之前定义的值（如果有）。`partial()` 的典型用法是在需要大量调用许多参数相同的函数时。

```python
from functools import partial
button=Button(root, fg="black",font="white",size=12)
b1=button(text="Ok") # 带 text=Ok 和上面 partial() 提供的所有参数调用 Button()
b2=button(text="Cancel")
b3=button(text="Restart")
```

创建对象的实例 `p` 有以下属性：

| Item | 描述 |
|---|---|
| `p.func` | 调用 `p` 时调用的函数。 |
| `p.args` | 调用 `p` 时传递的位置参数元组。额外的位置参数将连接到该值的末尾。 |
| `p.keywords` | 调用 `p` 时传递的关键字参数字典。额外的关键字参数将合并到此字典中。 |

在使用 `partial` 对象作为普通函数的替代品时要小心。结果与普通函数并不完全相同。例如，如果你在类定义中使用 `partial()`，它的行为类似于静态方法，而不是实例方法。

### reduce(function, items, [initial])

将函数累积地应用于可迭代项 `items` 并返回单个值。函数必须接受两个参数，并首次应用于 `items` 的前两个元素。此结果与随后的 `items` 元素以相同的方式逐一结合，直到 items 中的所有元素都被处理完毕。`initial` 是可选的起始值，用于第一次计算以及当 `items` 为空时。

空。此函数与 Python 2 中内置的 `reduce()` 函数相同。为了未来的兼容性，请使用此版本。

### update_wrapper(wrapper, wrapped [, assigned [, updated]])

这是一个编写装饰器时非常有用的工具函数。它将被包装函数的属性复制到包装器函数中，使得被包装的函数看起来像原始函数。`assigned` 是要复制的属性名称元组，默认设置为 `('__name__', '__module__', '__doc__')`。`updated` 是包含字典函数名称元组，你希望在包装器中合并这些函数的值。默认情况下，它是元组 `('__dict__')`。

### wraps(function [, assigned [, updated]])

装饰器对对其作用的函数执行与 `update_wrapper()` 相同的任务。`assigned` 和 `updated` 具有相同含义。该装饰器的典型用法是编写其他装饰器。例如：

```python
from functools import wraps
def debug(func):
    @wraps(func)
    def wrapped(*args, **kwargs):
        print('Calling %s' % func.__name__)
        r = func(*args, **kwargs)
        print('Done calling %s' % func.__name__)
    return r
```

```python
@debug
def add(x,y):
    return x+y
```

另请：
第 6 章，“函数与函数式编程。”

# heapq

`heapq` 模块使用堆实现了优先级队列。堆简单来说是有序元素的列表，其中施加了堆条件。具体而言，对于所有的 n（从 n=0 开始），`heap[n] <= heap[2*n+1]` 且 `heap[n] <= heap[2*n+2]`。`heap[0]` 始终包含最小项。

### heapify(x)

将列表 `x` 原地转换为堆。

### heappop(heap)

返回并移除堆中的最小项，同时保持堆条件。
如果堆为空，则抛出 `IndexError`。

### heappush(heap, item)

将 `item` 添加到堆中，同时保持堆条件。

### heapppop(heap, item)

在单次操作中将 `item` 添加到堆并移除堆中的最小项。
这比分别调用 `heappush()` 和 `heappop()` 更高效。

### heapreplace(heap, item)

返回并移除堆中的最小项。同时添加一个新项。在此过程中保持堆结构。此函数比顺序调用 `heappop()` 和 `heappush()` 更高效。此外，返回值是在添加新项之前获取的。返回值可能比 `item` 大。如果堆为空，则抛出 `IndexError`。

### merge(s1, s2, ...)

创建一个迭代器，将已排序的可迭代对象 `s1`、`s2` 等合并成一个单一有序序列。此函数不会消耗输入，而是返回一个能够增量处理数据的迭代器。

### nlargest(n, iterable, [key])

创建一个包含 `iterable` 中 n 个最大项的列表。最大的项出现在返回列表的第一个。`key` 是一个可选函数，它接受单个输入参数并为 `iterable` 中的每个项计算键。

### nsmallest(n, iterable, [key])

创建一个包含 `iterable` 中 n 个最小项的列表。最小的项出现在返回列表的第一个。`key` 是可选函数。

> 注意 堆队列的理论和实现可以在大多数算法书中找到。

# itertools

`itertools` 模块包含用于创建高效迭代器的函数，用于以各种方式遍历数据。该模块中的所有函数都返回迭代器，可以与 `for` 语句以及涉及迭代器的生成器和生成器表达式的其他函数配合。

### chain(iter1, iter2, ..., iterN)

给定一组迭代器（`iter1`, ..., `iterN`），该函数创建一个链接所有迭代器的新迭代器。返回的迭代器从 `iter1` 开始产生项，直到其耗尽。接着产生 `iter2` 中的项。持续持续，直到 `iterN` 中的所有项都耗尽。

### chain.from_iterable(iterable)

`chain` 的替代方案，其中 `iterable` 是一个产生可迭代对象序列的可迭代对象。此操作的结果与以下生成器代码片段相同：

```python
for it in iterables:
    for x in it:
        yield x
```
