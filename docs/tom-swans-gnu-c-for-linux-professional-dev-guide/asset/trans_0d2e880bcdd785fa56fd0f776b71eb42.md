

TLabel 实现模块比你之前看到的要复杂一些。但一次处理一个函数——各个语句都相当简单。首先，参数化构造函数将 color、x 和 y 参数传递给其祖先类 TColor 的构造函数。这让祖先类负责初始化对象的一部分。剩下的工作就是使用字符串参数 label 来初始化对象的 t1_label 数据成员。两条语句完成了这项工作：

```
t1_label = NULL;
SetLabel(label);
```

t1_label 变量首先被设为 NULL，因为 SetLabel() 的工作方式就是这样（稍后会详细介绍）。在构造函数中以这种方式调用类自身的成员函数是完全合法的。然而，使用这种技术时必须小心，不要调用任何使用尚未初始化的数据的函数。

模块中接下来的是类的拷贝构造函数。因为其中一个数据成员是指向动态分配内存的指针，而你在前几章学到过，对于类来说，提供安全的拷贝机制以防止指针地址值被意外复制尤其重要。有趣的是，拷贝构造函数几乎与刚才讨论的参数化构造函数相同。然而，在这种情况下，初始化表达式 TColor(copy) 将 copy 传递给祖先的自动生成的拷贝构造函数。以下语句随后完成了将一个 TLabel 对象拷贝到另一个对象的任务：

```
t1_label = NULL;
SetLabel(copy.t1_label);
```

再次，t1_label 被设为 NULL，因为 SetLabel() 的工作方式就是这样。该函数将源对象（copy）中 t1_label 指针所指向的数据复制到正在构造的当前对象。

SetLabel() 函数本身需要多花一点精力来理解。它的工作很简单——将一个字符串的地址赋给类的私有 t1_label char 指针——但编程必须仔细处理任何现有数据。以下语句完成了这个任务：

```
delete[] t1_label;   // Okay if t1_label == NULL
t1_label = NULL;     // Set t1_label to NULL
if (label != NULL)   // If param not NULL...
{
    t1_label = new char[strlen(label) + 1];
    strcpy(t1_label, label); // Copy param to t1_label
}
```

首先，删除当前指向的字符串。如果 t1_label 为 NULL，删除它也不会造成伤害。为了确保 t1_label 在此时为 NULL，它随后被设为该值。这样，如果函数的 label 参数为 NULL，则对象的 t1_label 指针也等于 NULL。如果 label 不为 NULL，则两条语句为字符串创建空间并将 label 参数的字符串复制到该分配的内存中。

最后在 TLabel 类模块中是函数 operator=()。如第 13 章“创建和销毁对象”中所解释的，此函数是为安全地将一个对象复制到另一个已构造的对象而需要的。为此，`operator=()` 函数执行以下语句：

```
if (this == &copy) return;
Setxy(copy.GetX(), copy.GetY());
SetColor(copy.GetColor());
SetLabel(copy.GetLabel());
```

第一行在所有 `operator=()` 函数中都很典型——它忽略任何将同一对象复制到自身的尝试。其他三条语句通过调用继承的 `SetXY()`、`SetColor()` 和 `SetLabel()` 函数以及 `GetX()`、`GetY()`、`GetColor()` 和 `GetLabel()` 来初始化拷贝。对 `Setxy()` 和 `SetColor()` 的调用说明了声明 const 成员函数的重要性。要理解原因，请看 `operator=()` 函数的头：

```
void TLabel::operator=(const TLabel &copy)
```

copy 参数，即被复制的源对象，被声明为类型 `const TLabel &`——换句话说，是对一个常量 TLabel 对象的引用。如果 `GetX()`、`GetY()` 和 `GetColor()` 等函数未被声明为 const，则将 const 对象作为参数传递的语句会让编译器陷入困境。例如，这条语句：

```
Setxy(copy.Getx(), copy.Gety());
```

将 `GetX()` 和 `GetY()` 传递了 const 对象 copy 的 `this` 指针。因为这些函数被声明为 const，所以它们不会无意中修改对象也就没有危险。列表 14.9，tlabel.cpp，测试了已实现的 TLabel 类。该列表没有新内容，你应该能够从源代码理解编程。

### LISTING 14.9 TLABEL.CPP

```
#include <iostream.h>
#include "tlabel.h"    // Need TLabel

void display(const char *msg, TLabel &t);

int main()
{
    TLabel test("Test Label", RED, 100, 200);
    display("Test object", test);

    TLabel copy_object(test);
    display("Copy constructed object", copy_object);

    TLabel dest_object;
    display("Object before copy", dest_object);
    dest_object = test;
    display("Object after copy", dest_object);

    return 0;
}

// Display facts about object tc
void display(const char *msg, TLabel &t)
```
