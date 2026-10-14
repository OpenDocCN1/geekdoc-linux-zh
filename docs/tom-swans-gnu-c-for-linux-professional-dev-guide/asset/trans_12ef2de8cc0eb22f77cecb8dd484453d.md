
```
{
    if (IsFull()) {
        cout << "*** Error: Container is full" << endl;
        exit(1);
    }
    objects[count] = pto;
    count++;
}
```

container.cpp 中实现的第一个函数是 `TContainer()` 构造函数。在初始化 `size` 和 `count` 私有数据成员之后，构造函数创建用于保存对象的存储机制。请仔细检查这些语句：

```
objects = new TObject*[size];
for (int i = 0; i < size; i++)
    objects[i] = NULL;
```

第一行创建一个 `TObject` 指针数组，并将结果赋给私有成员 `objects` 指针。当然也可以使用其他存储机制，但这一种足够通用，可以处理任何从 `TObject` 派生的类的对象。程序可以通过 `TObject` 指针来访问这些对象，因为在运行时，C++ 会根据对象的实际类型调用该类的虚函数。第二条语句使用 `for` 循环将 `objects` 数组中的每个 `TObject` 指针初始化为 `NULL`。在程序调用 `PutObject()` 插入对象之前，此时并不存在真正的对象。但容器已经构造完成，可以随时使用。在程序中，可以使用如下语句构造容器并插入对象：

```
TContainer box;
box.PutObject(new TMyClass(data));
```

或者，也可以使用 `new` 创建容器：

```
TContainer *pbox = new TContainer(10);
pbox->PutObject(new TMyClass(data));
```

这段假设代码假定 `TMyClass` 派生自 `TObject`。为容器指定一个计数（如 10）是可选的——如果未指定大小，容器的尺寸默认为 100。

接下来，container.cpp 中是 `TContainer` 析构函数。这里展示了虚函数的一个隐晦用法，从源代码中可能不太明显，但这是学习创建通用容器时必不可少的技术：

```
for (int i = 0; i < count; i++)
    delete objects[i];    // Delete contained objects
delete objects;        // Delete array of TObject pointers
```

`for` 循环删除数组中的每个对象。它之所以能做到这一点，是因为 `TObject` 声明了一个虚析构函数。因此，在运行时，C++ 会调用数组中对象的实际析构函数。唯一的要求是这些对象必须是从 `TObject` 派生的类的对象。在删除各个对象之后，程序会删除 `objects` 指针本身。这样，当容器本身被销毁时，所有分配的内存都会被完全释放。

## 第15章 使用虚函数编程

> **注意**
> 
> `TContainer` 析构函数包含一条输出语句，你可以通过启用该语句在运行时跟踪析构函数的调用。要启用跟踪，请在编译模块时指定 `-DDEBUG`（定义 DEBUG）选项。

最后，在 `TContainer` 实现模块的这一部分中，函数 `PutObject()` 负责将新对象插入容器。该函数首先检查容器是否已满：

```
if (IsFull()) {
    cout << "*** Error: Container is full" << endl;
    exit(1);
}
```

这指出了 `TContainer` 类的一个主要缺陷。理想情况下，如果容器已满，它应当采取措施扩展自身以容纳新数据。如果做不到这一点，它应当抛出*异常*来报告错误，而不是退出程序并显示错误消息。不过，为了使本章中提供的代码示例避免过于冗长，异常处理留到第16章“处理异常”中讨论。

如果容器未满，两个简单的语句即可插入新对象：

```
objects[count] = pto;
count++;
```

此时，`TContainer` 并不具体知道它保存的对象类型。它所知道且需要知道的只是，`PTObject` 类型的 `pto` 指向一个从 `TObject` 派生的类的对象。该函数还会递增 `count`，以跟踪容器中对象的数量。

清单15.4（container.cpp）补全了 `TContainer` 实现模块，并展示了虚 `TObject` 成员函数的其他用法。

### 清单15.4    CONTAINER.CPP（部分）

```
// Call Display() for all objects in container
void TContainer::ShowAllObjects(const char *msg)
{
    cout << msg << endl;
    cout << "Number of objects == " << count << endl;
    for (int i = 0; i < count; i++)
        objects[i]->Display();   // Calls virtual function!
    cout << endl << endl;
}

void TContainer::Quicksort(int left, int right)
{
    int i = left;
    int j = right;
    PTObject test = objects[(left + right) / 2];
    PTObject swap;
    do {
        while (objects[i]->Compare(test) < 0) i++;
```
