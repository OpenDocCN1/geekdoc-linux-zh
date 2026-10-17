
前面的 `while` 循环以及 `empty()`、`top()` 和 `pop()` 函数，对对象栈的作用与对简单整数值的作用相同。只需更改栈对象名称，即可显示并移除所有 `TCoordinate` 对象。

## 队列

STL 中有两种类型的队列容器。一种基于 `list`，另一种基于 `deque`。两种类型的队列提供相同的操作；只有底层数据结构可以选择。在大多数情况下，`list` 是存储大对象和大量对象的更好选择；否则，`deque` 可能更快。队列是一种先进先出（FIFO）的数据结构，其工作方式就像在邮局前排队一样。除非程序作弊，否则对象只能在队尾进入，并从队首离开。

队列基于双端队列（`deque`，即双端队列）而非反过来，这可能看起来有些反直觉，但这是经典的构造方式。队列在内部构造上与双端队列相同，但插入和删除操作受到更多限制。

队列常用于调度应用程序——例如，按收到顺序路由呼叫者的电话消息系统，或按任务到来顺序分配作业的工作调度器。存储在队列中的对象必须支持小于和相等比较运算符。除了满足这些要求之外，你可以在 STL 队列中存储任何类型的数据。

以下各节中的编程示例取自随书 CD-ROM 的 `src/24` 目录中的 `queue.cpp` 文件。

### 声明队列

声明队列的方式与声明栈类似。根据你希望如何实现队列容器，包含 `queue` 头文件以及 `list` 或 `deque` 头文件：

```
#include <queue>
#include <list>
#include <deque>
```

将三个头文件都包含进来，尝试两种底层数据结构，看看哪种效果最好。

要创建队列容器，需要指定要存储的数据对象类型，以及用作底层数据结构的容器类型（`list` 或 `deque`）：

```
queue<TCoordinate, list<TCoordinate> > suzyQueue;
```

这将为 `TCoordinate` 对象创建一个容器 `suzyQueue`（`TCoordinate` 声明在本章前面介绍的 `coordinate.h` 头文件中），并使用 `list` 模板作为底层数据结构。为了让程序更清晰，最好为这种数据结构创建一个 `typedef` 名称：

```
typedef queue<TCoordinate, list<TCoordinate> > TQueue;
```

如果想改用 `deque`，只需将 `list` 改为 `deque`。使用 `TQueue` `typedef` 名称，创建队列容器就是一件简单的事了，本例中名为 `suzyQueue`：

```
TQueue suzyQueue;
```

### 使用队列

调用 `push()` 成员函数将对象插入队列。由于所有对象都必须从队列尾部进入，这是向这种容器中插入数据的唯一方式。

```
for (int i = 1; i < 10; i++)
    suzyQueue.push(TCoordinate(i, i * 10));
```

这个 `for` 循环压入了九个 `TCoordinate` 对象，这些对象使用索引 `i` 和 `i` 乘以 10 的值进行初始化。与大多数容器一样，你可以调用 `size()` 来统计队列中对象的数量：

```
cout << "Number of objects = " << suzyQueue.size() << endl;
```

调用 `front()` 函数来检查队首对象。这个对象将在程序下次调用 `pop()` 时被移除：

```
cout << "First object inserted: " << suzyQueue.front() << endl;
```

> 某些早期版本的 STL 将 `front()` 函数称为 `top()`。

尽管在严格的经典队列中是不允许的，但 STL 数据结构允许使用 `back()` 函数检查队列的队尾。下面的语句显示了最近插入的对象：

```
cout << "Last object inserted : " << suzyQueue.back() << endl;
```

调用 `empty()` 来判断队列是否没有对象。将 `empty()`、`front()` 和 `pop()` 函数组合起来，可以显示并弹出队列中的所有对象，如下面的 `while` 循环所示，该循环还调用 `size()` 为每个显示的对象编号：

```
while (!suzyQueue.empty()) {
    cout << suzyQueue.size() << " : ";
    cout << suzyQueue.front() << endl;
    suzyQueue.pop();
}
```

这个循环会完全清空队列。编译并运行测试程序，可以看到循环的输出（此处为节省篇幅已缩减）：

```
$ g++ queue.cpp
$ ./a.out
Creating queue of TCoordinate objects
Number of objects == 9
...
9 : x == 1; y == 10
8 : x == 2; y == 20
...
1 : x == 9; y == 90
Number of objects == 0
Queue is empty
```

## 优先队列

优先队列类似于栈或队列，但它始终按关键顺序维护对象。此外，无论插入顺序如何，最关键的对象都会先于不太关键的对象从容器中移除。这种容器非常适合需要确保关键任务获得优先权的调度程序和关键路径程序。

关键性是通过将小于运算符应用于元素对，或由用户提供的比较函数对象来确定的。每次在优先级队列中插入或删除对象时，都会使关键对象（即通过比较找到的那些对象）移动到队列的前端。

有两种优先级队列。一种基于 `vector`；另一种由 `deque` 构建。通常，`vector` 优先级队列比 `deque` 优先级队列更快，但内存效率较低。

优先级队列在任何需要对数据进行优先级排序的应用程序中都很有用。一个好的例子是待办事项列表，其中优先级较低的项目（1-清洁烤箱，2-清扫车库）没有那些数值较高的项目（8-兑现薪水支票，9-给妈妈打电话）那么关键。你可以按任意顺序将对象插入优先级队列。对象根据其优先级从队列中取出。下面是一个待办事项列表程序的示例（参见“创建待办事项列表优先级队列”），但首先，让我们研究一下这个有用的 STL 容器的基本知识。

> 注意
> 以下各节中的示例程序来自 CD-ROM 上 `src/c24` 目录中的 `pqueue.cpp` 文件。

### 声明优先级队列

要创建优先级队列，请包含 `queue` 和 `vector` 或 `deque` 头文件：

```
#include <queue>
#include <vector>
```

与其他相对复杂的数据结构一样，通常最好为实例化的优先级队列类定义一个名称。例如，下面的语句指定 `TPQueue` 是一个可以存储整数值的 `priority_queue` 类的名称：

```
typedef priority_queue<int, vector<int>, less<int> > TPQueue;
```

`priority_queue` 的底层数据结构是 `vector`，它使用 `less` 函数对象来维护对象的顺序。使用 `less` 会使具有较大值的条目获得较高的优先级。如果希望优先处理具有较小值的条目，请将 `less` 改为 `greater`。使用 `typedef` 名称，下面的代码构造了一个名为 `pQueue` 的 `priority_queue` 容器：

```
TPQueue pQueue;
```

### 使用优先级队列

使用优先级队列的方式与普通队列相同。例如，下面的循环使用标准 C 库的 `random()` 函数将随机选择的整数值插入 `pQueue` 容器：

```
for (int i = 0; i < 10; i++)
    pQueue.push(random() % 1000);
```

与大多数容器一样，`size()` 报告 `priority_queue` 中的对象数量：

```
cout << "Number of insertions == " << pQueue.size() << endl;
```

尽管对象是随机插入的，弹出它们时会移除优先级较高的对象——在本例中，即具有较高值的对象。下面的循环在从 `priority_queue` 中移除所有对象时显示它们：

```
while (!pQueue.empty()) {
    cout << pQueue.top() << " ";
    pQueue.pop();
}
```

> 注意
> `top()` 函数是为优先级队列定义的，但普通队列将其称为 `front()`，这是 STL 中一个虽小却令人烦恼的差异。

编译并运行测试程序将显示它按从高到低的顺序输出其随机整数值：

```
$ g++ pqueue.cpp
$ ./a.out
Pushing random integers into priority queue
Number of insertions == 10
Displaying and popping objects
975 974 642 624 584 368 317 238 113 73
```
