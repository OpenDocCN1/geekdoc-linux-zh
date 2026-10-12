
字符串类将 UNIX shell 类型的字符串运算符添加到 C++ 语言中，以及大量的额外运算符。表 27.4 列出了字符串类可用的许多运算符。

**表 27.4. 字符串类运算符。**

| 运算符 | 含义 |
| :------- | :------- |
| `str1 == str2` | 如果 `str1` 等于 `str2`，则返回 `TRUE` |
| `str1 != str2` | 如果 `str1` 不等于 `str2`，则返回 `TRUE` |
| `str1 < str2` | 如果 `str1` 小于 `str2`，则返回 `TRUE` |
| `str1 <= str2` | 如果 `str1` 小于或等于 `str2`，则返回 `TRUE` |
| `str1 > str2` | 如果 `str1` 大于 `str2`，则返回 `TRUE` |
| `str1 >= str2` | 如果 `str1` 大于或等于 `str2`，则返回 `TRUE` |
| `compare(str1, str2)` | 在不考虑字符大小区别的比较 `str1` 和 `str2` |
| `str3 = str1 + str2` | 将 `str1` 与 `str2` 连接的结果存储在 `str3` 中 |

字符串类还提供许多其他运算符，用于执行不同类型的字符串比较、连接以及子字符串提取和操作。

### 随机数

GCC C++ 类库中提供了类，允许你生成几种不同类型的随机数。用于生成这些数字的类是 `Random` 类和 `RNG` 类。

### 数据收集

类库提供了两种执行数据收集和分析功能的类。这两个类是 `SampleStatistic` 和 `SampleHistogram`。`SampleStatistic` 类提供了一种收集样本的方法，并提供了许多可以对收集的数据进行计算的统计功能。可执行的计算包括均值、方差、标准差、最小值和最大值。

`SampleHistogram` 类派生自 `SampleStatistic` 类，并支持按分桶区间收集和显示样本。

### 链表

GNU C++ 库支持两种类型的链表：由 `SLLlist` 类实现的单向链表，以及由 `DLLlist` 类实现的双向链表。这两种类型的链表都支持所有标准的链表操作。这些类支持的操作摘要如表 27.5 所示。

**表 27.5. 列表运算符。**

| 运算符 | 描述 |
| :--- | :--- |
| `list.empty()` | 如果 `list` 为空，则返回 `TRUE` |
| `list.length()` | 返回 `list` 中的元素数量 |
| `list.prepend(a)` | 将 `a` 放在 `list` 的前面 |
| `list.append(a)` | 将 `a` 放在 `list` 的末尾 |
| `list.join(list2)` | 将 `list2` 附加到 `list`，在此过程中销毁 `list2` |
| `a = list.front()` | 返回指向存储在 `list` 头部的元素的指针 |
| `a = list.rear()` | 返回指向存储在 `list` 末尾的元素的指针 |
| `a = list.remove_front()` | 删除并返回存储在 `list` 前面的元素 |
| `list.del_front()` | 删除第一个元素而不返回它 |
| `list.clear()` | 删除 `list` 中的所有项目 |
| `list.ins_after(i, a)` | 在 `list` 中的位置 `i` 之后插入 `a` |
| `list.del_after(i)` | 删除 `list` 中位置 `i` 之后的元素 |

双向链表还支持表 27.6 中列出的操作。

**表 27.6. 双向列表运算符。**

| 运算符 | 描述 |
| :--- | :--- |
| `a = list.remove_rear()` | 删除并返回存储在 `list` 末尾的元素 |
| `list.del_rear()` | 删除最后一个元素，而不返回它 |
| `list.ins_before(i, a)` | 在 `list` 中的位置 `i` 之前插入 `a` |
| `list.del(i, dir)` | 删除当前位置的元素，然后如果 `dir` 为正，则向前移动一个位置；如果 `dir` 为 0 或负数，则向后移动一个位置 |

## Plex 类

Plex 类是行为类似于数组但功能更强大的类。Plex 类具有以下特性：

- 它们具有任意上下界索引。
- 它们可以在下界和上界两个方向上动态扩展。
- 元素可以通过索引访问。与典型的数组不同，边界检查是在运行时执行的。
- 只有那些被专门初始化或添加的元素才可以被访问。

定义了四种不同类型的 Plex：`FPlex`、`XPlex`、`RPlex` 和 `MPlex`。`FPlex` 是一种只能在其声明的边界内缩小或增长的 Plex。`XPlex` 可以在任何方向上动态增长，没有任何限制。`RPlex` 与 `XPlex` 几乎相同，但它具有更好的索引功能。最后，`MPlex` 与 `RPlex` 相同，只不过它允许元素被逻辑删除和恢复。

表 27.7 列出了适用于所有四种 Plex 的部分有效操作。

### 表 27.7. 为 Plex 定义的操作。

| 操作 | 描述 |
| :--- | :--- |
| `Plex b(a)` | 将 Plex `a` 的副本分配给 Plex `b` |
| `b = a` | 将 Plex `a` 复制到 `b` |
| `a.length()` | 返回 `a` 中的元素数量 |
| `a.empty()` | 如果 `a` 没有元素，则返回 `TRUE` |
| `a.full()` | 如果 `a` 已满，则返回 `TRUE` |
| `a.clear()` | 从 `a` 中删除所有元素 |
| `a.append(b)` | 将 Plex `b` 追加到 `a` 的高位部分 |
| `a.prepend(b)` | 将 Plex `b` 前置到 `a` 的低位部分 |
| `a.fill(z)` | 将 `a` 中的所有元素设置为等于 `z` |
| `a.valid(i)` | 如果 `i` 是 `a` 的有效索引，则返回 `TRUE` |
| `a.low_element()` | 返回指向 `a` 中最低位置元素的指针 |
| `a.high_element()` | 返回指向 `a` 中最高位置元素的指针 |

Plex 是一个非常有用的类，GNU C++ 类库中的许多其他类都是基于它构建的。`Stack`、`Queue` 和 `Linked list` 类型中的一些是构建在 `Plex` 类之上的。

## 堆栈

`Stacks` 类实现了标准的后进先出（LIFO）堆栈。GNU C++ 类库提供了三种不同的堆栈实现：`VStack`、`XPStack` 和 `SLStack`。`VStack` 是固定大小的堆栈，这意味着你在最初创建它时必须指定堆栈大小的上限。`XPStack` 和 `SLStack` 都是动态大小的堆栈，它们以略有不同的方式实现。

表 27.8 列出了可以应用于 `Stacks` 类的操作。

### 表 27.8. 堆栈类运算符。

| 运算符 | 描述 |
| :--- | :--- |
| `Stack st` | 声明 `st` 为一个堆栈 |
| `Stack st(sz)` | 声明 `st` 为一个大小为 `sz` 的堆栈 |
| `st.empty()` | 如果堆栈为空，则返回 `TRUE` |
| `st.full()` | 如果堆栈已满，则返回 `TRUE` |
| `st.length()` | 返回堆栈中的元素数量 |
| `st.push(x)` | 将元素 `x` 放入堆栈顶部 |
| `x = st.pop()` | 从堆栈中移除并返回顶部元素 |
| `st.top()` | 返回指向堆栈中顶部元素的指针 |
| `st.del_top()` | 从堆栈中删除顶部元素，但不返回该元素 |
| `st.clear()` | 从堆栈中删除所有元素 |

## 队列

`Queue` 类实现了标准的先进先出（FIFO）队列。GNU C++ 类库提供了三种不同类型的 `queue`：`VQueue`、`XPQueue` 和 `SLQueue`。`VQueue` 是固定大小的队列，因此你在最初创建这种类型的队列时必须指定大小上限。`XPQueue` 和 `SLQueue` 都是动态大小的队列，因此不需要上限。`Queue` 类支持的操作列于表 27.9。

### 表 27.9. 队列类运算符。

| 运算符 | 描述 |
| :--- | :--- |
| `Queue q` | 声明 `q` 为一个队列 |
| `Queue q(sz)` | 声明 `q` 为一个大小为 `sz` 的队列 |
| `q.empty()` | 如果 `q` 为空，则返回 `TRUE` |
| `q.full()` | 如果 `q` 已满，则返回 `TRUE` |
| `q.length()` | 返回 `q` 中的元素数量 |
| `q.enq(x)` | 将元素 `x` 添加到 `q` |
| `x = q.deq()` | 从 `q` 中移除并返回一个元素 |
