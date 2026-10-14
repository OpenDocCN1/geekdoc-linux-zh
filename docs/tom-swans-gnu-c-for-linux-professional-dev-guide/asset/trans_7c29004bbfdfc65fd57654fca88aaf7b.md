

在为容器对象的默认大小指定了 `DEFAULT_SIZE` 常量后，头文件声明了三项内容。首先是一个不完整类声明，形式如下：

```
class TObject;
```

这指明符号 `TObject` 是一个类，但其类体尚未确定。它允许程序像这样的类确实存在一样使用该符号。例如，在本例中，我们需要两种指针类型，由接下来的两行声明：

```
typedef TObject * PTObject;
typedef PTObject * PPTObject;
```

第一行将 `PTObject` 声明为类型 `TObject *`（指向 `TObject` 的指针）。第二行将 `PPTObject` 声明为类型 `PTObject *`（指向 `TObject` 指针的指针）。我喜欢加入这类类型定义，以便更轻松地声明指针和数组。

## 虚析构函数

接下来在 `container.h` 中（参见清单 15.1）是 `TObject` 的类声明。它表明 `TObject` 拥有三个公有虚成员函数。由于从来不会创建 `TObject` 抽象类的对象，因此它没有构造函数。然而，为了支持删除从 `TObject` 派生的类的对象，该类声明了一个虚析构函数：

```
virtual ~TObject() { };
```

虚析构函数以保留字 `virtual` 开头，后跟函数名（始终是 `~` 字符加上类名）。析构函数不能声明参数。它们可以执行语句，但在本例中，我们只需要一个占位符，用于派生类中的未来析构函数，因此该析构函数的函数体为空。

注意，这并不是一个以 `=0` 结尾的纯虚函数。你可以声明纯虚析构函数；不过，我想展示纯虚函数与普通虚函数声明之间的区别。如前所述，纯虚函数不需要实现——它纯粹是一个占位符，期望由派生类提供。普通虚函数（如 `TObject` 析构函数）需要实现，即使实现只是一个什么都不做的空语句块。两类虚函数的作用类似——它们提供了 C++ 根据对象类型调用特定函数的机制。

## 纯虚函数

清单 15.1 中的 `TObject` 类还声明了两个纯虚函数：`Compare()` 和 `Display()`：

```
virtual int Compare(PTObject p) = 0;
virtual void Display() = 0;
```

使用纯虚函数，我们说 `TObject` 是一个具有比较两个由 `TObject` 派生的类的对象的能力的类。正如后面的示例所示，这些类会提供实际的 `Compare()` 函数。

然而，即使在这样的类存在之前，编译器也允许语句调用虚函数 `TObject::Compare()`，尽管它仅仅是一个占位符，不包含任何实际代码。在运行时，会根据所涉及对象的类型调用实际的 `Compare()`——这一行为的技术术语称为后期绑定（late binding）。通过这一过程，语句与 `Compare()` 等函数的实际绑定（或称链接）发生在运行时，而不像普通 C 或 C++ 函数那样发生在编译期间。

`TObject` 声明了第二个纯虚函数 `Display()`。这里同样，期望派生类实现实际的函数，C++ 会根据所涉及对象的类型来调用它。后面的示例将演示如何从 `TObject` 派生一个类并完成其纯虚函数。不过，我们先来看看容器类。

## TCONTAINER 类

清单 15.2 显示了 `container.h` 头文件的其余部分以及 `TContainer` 类的声明。

```
LISTING 15.2 CONTAINER.H (PARTIAL)
class TContainer {
private:
    int size;        // Capacity of objects array
    int count;       // Number of objects in array
    PPTObject objects; // Array of TObject pointers
protected:
    void Quicksort(int left, int right);
public:
    TContainer(int n = DEFAULT_SIZE); // Constructor
    ~TContainer();                    // Destructor
    //
    // Inline member functions
    //
    bool IsFull() const { return (count >= size); }
    int GetSize() const { return size; }
    int GetCount() const { return count; }
    //
    // Other public member functions
    //
    void PutObject(PTObject pto);
    void ShowAllObjects(const char *msg);
    void Sort();
};
```

像大多数设计良好的类一样，`TContainer` 将其所有数据成员声明为私有。在本例中，有三个变量：

```
int size;
int count;
PPTObject objects;
```

