

```cpp
} else {
    owners--;
    return new TData(s);
}
```

你可以用几乎相同的编程方法处理其他类型的数据，只需做少量改动。如果所指数据不是数组，就去掉 `delete[]` 中的方括号。此外，还需做必要的操作来复制所指信息。这里，程序调用 `strlen()` 和 `strcpy()` 来复制 `cp` 所指的字符串。其余代码在处理任何类型的数据时都不需要改动。在 else 子句中，`owners` 被递减，并使用参数 `s` 所指的新数据构造出一个 `TData` 对象的克隆。

另外两个 `TData` 成员函数是可选的，这里仅为测试目的提供。你可能需要某种方式来访问 `TData` 类中的数据。在本例中，`GetString()` 只是简单地返回私有指针 `cp`。返回值和函数都必须是 `const`，因为对所指数据的所有更改都必须通过 `TData` 的 `PutData()` 函数进行，以保持复制对象的完整性：

```cpp
const char *GetString() const
{
    return cp;
}
```

还提供了一个你可能要删除的函数。它返回所有者的数量，供后面的测试程序使用，该程序会在屏幕上显示如图 21.1 和 21.2 所示的对象关系：

```cpp
int NumberOfOwners()
{
    return owners;
}
```

接下来在 cow.h 头文件中是 `TContain` 类，它在 `TData` 类提供的引用计数和写时复制方法上做了最后的完善。因为 `TData` 的所有成员都是私有的，只有 `TContain` 才能创建和使用 `TData` 对象，并且通过这种方式，所有 `TData` 对象的副本都被安全地封装在 `TContain` 对象中。清单 21.2 显示了 cow.h 文件的其余部分。

## LISTING 21.2　COW.H (PARTIAL)

```cpp
// A class that stores a pointer to a TData object and
// provides for safe copying of TContain objects. This
// class is implemented in cow.cpp.

class TContain {
private:
    TData * tp_data;
public:
    TContain(const char *arg);          // Constructor
    TContain(const TContain &copy);     // Copy constructor
    ~TContain();                        // Destructor
```

*continues*

## LISTING 21.2 CONTINUED

```cpp
void operator=(const TContain &copy);  // Assignment operator
const char *GetString() const;        // Returns object data
void PutNewData(const char *s);        // Member function

// For test purposes only
//
int NumTDataOwners() {
    return tp_data->NumberOfOwners();
}
};
```

TContain 是一个看起来更正常的类。在程序层面，要存储引用计数的数据，语句会创建 TContain 对象。在 TContain 内部，函数使用 TData 成员来实现引用计数和写时复制方法。类私有的是指向 TData 对象的指针，声明为
TData * tp_data;

除了数据成员外，TContain 类还声明了针对所讨论数据类型（本例中为 C 风格字符串）的构造函数、拷贝构造函数、析构函数、重载的赋值运算符() 函数，以及两个用于检索和更改对象数据的函数——GetString() 和 PutNewData()。你可以随意命名这两个函数。最后，严格用于测试目的，TContain 有一个内联函数 NumTDataOwners()，你可以在生产代码中将其删除。其他成员是实现引用计数和写时复制方法的最低要求。清单 21.3，cow.cpp，展示了 TContain 成员的实现。

## LISTING 21.3 COW.CPP

```cpp
#include "cow.h"     // Need TData and TContain classes

// Constructor
//
TContain::TContain(const char *arg)
{
    tp_data = new TData(arg);
}

// Copy constructor
//
TContain::TContain(const TContain &copy)
{
    tp_data = copy.tp_data->GetCopy();
}

// Destructor
//
TContain::~TContain()
{
    if (tp_data->DeleteCopy() <= 1)
```

```cpp
 delete tp_data;
}

// Assignment operator
//
void TContain::operator=(const TContain &copy)
{
    if (this == &copy) return;          // Can't copy self
    if (tp_data->DeleteCopy() <= 1)     // Delete TData object if
        delete tp_data;                 // any and if in use
    tp_data = copy.tp_data->GetCopy();  // Get TData copy
}

// Return pointer to object's data
//
const char *TContain::GetString() const
{
    return tp_data->GetString();
}

// Assign new data to TContain object
//
void TContain::PutNewData(const char *s)
{
    tp_data = tp_data->PutData(s);
}
```

在你自己的程序中，你应该能够使用 TContain 类中列出的成员函数，而几乎不需要或不需要任何改动。类构造函数创建一个新的 TData 对象，并将其地址赋给 TContain 类的 tp_data 指针：

`tp_data = new TData(arg);`

拷贝构造函数专门编写为调用 TData 类的 GetCopy() 成员函数：

`tp_data = copy.tp_data->GetCopy();`

在内部，这会将 copy.tp_data 分配给目标对象中的 tp_data，导致两个 TContain 对象中的指针都指向同一个 TData 对象。然而，该对象的 owners 变量会由 GetCopy() 递增（参见例如图 21.1 中的对象 E 和 F）。

当程序销毁一个 TContain 对象时，它必须检查它所拥有的 TData 对象是否被其他 TContain 对象拥有。如果是，则该 TData 对象不得被干扰。这是等式中的引用计数部分，由 TContain 析构函数实现：

`if (tp_data->DeleteCopy() <= 1)`
`    delete tp_data;`

只有当调用 TData::DeleteCopy() 返回的值小于或等于 1 时，tp_data 才会真正被删除。这保留了 TData 对象，如果它被其他 TContain 对象拥有。

