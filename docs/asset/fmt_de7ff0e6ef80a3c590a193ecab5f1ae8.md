
`tp_data = new TData(arg);`

// Copy constructor

//

`TContain::TContain(const TContain &copy)`

{

`tp_data = copy.tp_data->GetCopy();`

}

// Destructor

//

`TContain::~TContain()`

{

`if (tp_data->DeleteCopy() <= 1)`

```cpp
 delete tp_data;
```
}

// Assignment operator

//

`void TContain::operator=(const TContain &copy)`

{

`if (this == &copy) return;`          // Can't copy self

`if (tp_data->DeleteCopy() <= 1)`     // Delete TData object if

`delete tp_data;`                 // any and if in use

`tp_data = copy.tp_data->GetCopy();`  // Get TData copy

}

// Return pointer to object's data

//

`const char *TContain::GetString() const`

{

`return tp_data->GetString();`

}

// Assign new data to TContain object

//

`void TContain::PutNewData(const char *s)`

{

`tp_data = tp_data->PutData(s);`

}

在你自己的程序中，你应该能够使用 `TContain` 类中列出的成员函数，而几乎不需要或不需要任何改动。类构造函数创建一个新的 `TData` 对象，并将其地址赋给 `TContain` 类的 `tp_data` 指针：

`tp_data = new TData(arg);`

拷贝构造函数专门编写为调用 `TData` 类的 `GetCopy()` 成员函数：

`tp_data = copy.tp_data->GetCopy();`

在内部，这会将 `copy.tp_data` 分配给目标对象中的 `tp_data`，导致两个 `TContain` 对象中的指针都指向同一个 `TData` 对象。然而，该对象的 `owners` 变量会由 `GetCopy()` 递增（参见例如图 21.1 中的对象 E 和 F）。

当程序销毁一个 `TContain` 对象时，它必须检查它所拥有的 `TData` 对象是否被其他 `TContain` 对象拥有。如果是，则该 `TData` 对象不得被干扰。这是等式中的引用计数部分，由 `TContain` 析构函数实现：

`if (tp_data->DeleteCopy() <= 1)`
`delete tp_data;`

只有当调用 `TData::DeleteCopy()` 返回的值小于或等于 1 时，`tp_data` 才会真正被删除。这保留了 `TData` 对象，如果它被其他 `TContain` 对象拥有。

重载的 `operator=()` 赋值函数需要更多的编程。
`TContain` 使用以下语句实现此函数：
`if (this == &copy) return;`
`if (tp_data->DeleteCopy() <= 1)`
`delete tp_data;`
`tp_data = copy.tp_data->GetCopy();`

你在这本书中已经多次看到第一步。它忽略了将对象复制给自身的任何请求。第二条语句使用了与 `TContain` 析构函数中相同的代码。只有在调用 `DeleteCopy()` 表明它不被其他 `TContain` 对象拥有时，才会删除所指向的 `TData` 对象。最后，`GetCopy()` 创建了正在被复制的 `TData` 对象的副本。然而，正如所解释的，调用 `GetCopy()` 只是递增 `TData` 对象的拥有者计数，因此不会复制数据。

函数 `PutData()` 仅通过调用 `TData` 的 `PutData()` 成员函数简单地实现了写时复制方法：
`tp_data = tp_data->PutData(s);`

这会导致 `TData` 对象被复制，并将新数据插入该副本中。如果原始副本只有一个拥有者，则会被删除。最后在 `TContain` 类中，函数 `GetString()` 提供了访问 `TData` 对象中数据的方式。你的程序也需要类似的函数，但你可以为其命名不同。

有了 `cow.cpp` 模块和头文件，实现引用计数和写时复制方法所需的所有元素都已就位。列表 21.4，`cowdemo.cpp`，测试了 `TData` 和 `TContain` 类。为了节省篇幅，我在此删除了程序中除少数几个之外的所有测试。我还删除了仅暂停等待你按 Enter 并显示对象数据以查看测试结果的本地函数。完整的源文件当然在 CD-ROM 上的文件中。

## LISTING 21.4 COWDEMO.CPP

```cpp
#include <iostream.h>

#include "cow.h"    // Copy-on-write classes
#define BUFSIZE 256

char buffer[BUFSIZE];  // Temporary input buffer

// Local function prototypes
//

void pause(const char *s);
void show(const char *s, TContain *tp);
void show_objects();

// Pointers to test TContain objects
//

TContain *A, *B, *C, *D, *E, *F;
int main()
{
    pause("1: Construct object A*");
```

```
A = new TContain("aaaa");
show_objects();

pause('2: Construct object B from existing object A');
B = new TContain(*A);
show_objects();

pause('3: Construct object C from existing object B');
C = new TContain(*B);
show_objects();

pause('4: Change data in object B');
B->PutNewData("bbbb");
show_objects();

pause('9: Create new object F from B');
F = new TContain(*B);
show_objects();

...
pause('99: Delete object C');
delete C; C = NULL;
show_objects();

return 0;
}
```

输入以下命令来编译和运行 `cow.cpp` 模块和 `cowdemo.cpp` 测试程序：

```
$ g++ -c cow.cpp
$ g++ cowdemo.cpp cow.o
$ ./a.out
```

按 Enter 运行每个测试，并观察结果。 （你可能想同时查看程序源代码的副本，以查看产生每个测试结果的语句。）前四个测试演示了引用计数和写时复制方法。前两个测试构造了两个 `TContain` 对象 `A` 和 `B`，它们具有相同的 `TData` 对象。测试 3 然后执行以下语句：

```
C = new TContain(*B);
```

这调用 `TContain` 拷贝构造函数来复制 `B`。屏幕上，你可以看到测试的结果：

```
3: Construct object C from existing object B
object A
string ...........: aaaa
num data owners....: 3
object B
string ...........: aaaa
num data owners....: 3
object C
string ...........: aaaa
num data owners....: 3
```

现在有三个 `TContain` 对象 `A`、`B` 和 `C`。每个都拥有相同的 `TData` 对象。该对象的引用计数等于 3，表明有三个对象拥有字符串 `"aaaa"`，但内存中只有一个该字符串的副本。前面列出的测试表明引用计数技术方面正在工作。为了测试写时复制方法，测试 4 使用以下语句更改对象 `B` 中的数据：

```
B->PutNewData("bbbb");
```

测试 4 的结果显示当三个对象之一的数据被更改时会发生什么：

```
4: Change data in object B
object A
```
