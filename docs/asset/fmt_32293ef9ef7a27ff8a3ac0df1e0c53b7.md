
这意味着即使你不预计会有其他人查看你的代码，也必须对代码进行注释。在你交付代码的六个月后，你将用一个完全陌生人的眼光来读它，并困惑于自己竟然能写出如此复杂且扭曲的代码，并指望会有除灾难以外的后果。

## 异常

在 C++ 中，异常是一个对象，它从发生问题的代码区域传递到准备处理该问题的代码部分。异常的类型决定了哪部分代码将处理该问题，而抛出的对象内容（如果有）可以用于向用户提供反馈。

异常背后的基本思想非常简单：

- 资源的实际分配（例如，内存的分配或文件的锁定）通常在程序的非常低层完成。
- 当操作失败、无法分配内存或无法锁定文件时，采取的逻辑通常位于程序的高层，即与用户交互的代码部分。
- 异常为分配资源的代码到可以处理错误条件的代码提供了一条直接的路径。如果存在中间函数层，它们将获得清理内存分配的机会，但并不要求包含仅用于传递错误状态的代码。

## 异常是如何使用的

`try` 块是为了包裹可能出现问题的代码区域。例如：

```
try
{
  SomeDangerousFunction();
}
```

`catch` 块处理 `try` 块中抛出的异常。例如：

```
try
{
  SomeDangerousFunction();
}
catch(OutOfMemory)
{
  // take some actions
}
catch(FileNotFound)
{
  // take other action
}
```

## 异常与错误处理

使用异常的基本步骤是：

1. 识别程序中开始执行可能引发异常的操作区域，并将它们放入 `try` 块中。
2. 创建 `catch` 块以便在抛出异常时捕获它们、清理分配的内存，并适当通知用户。列表 20.1 展示了 `try` 块和 `catch` 块的使用。

异常是用于传输问题信息的对象。

`try` 块是一个由大括号包围的，在其中可能会抛出异常。

`catch` 块是紧随 `try` 块之后的块，在其中处理异常。

当异常被抛出（或引发）时，控制权将转移到紧随当前 `try` 块之后的 `catch` 块。

> 某些旧版本的编译器（如 GNU 2.7.2 版本）不支持异常。然而，异常是 ANSI C++ 标准的一部分，不过每个编译器厂商的最新版本都完全支持原生异常。你将无法编译或运行本课程中的练习。不过，最好的做法是通读整个课程，并在升级编译器后返回学习这些材料。请使用光盘上的编译器版本（2.9.5）来运行这些示例。

## 列表 20.1 抛出异常

```cpp
56:          for (int i = 0; i<itsSize; i++)
57:              pType[i] = rhs[i];
58:      }
59:
60:      int& Array::operator[](int offset)
61:      {
62:          if (offset < 0 || offset >= itsSize)
63:              throw XBoundary();
64:          return pType[offset];
65:      }
66:
      const int& Array[](int offset) const
67:      {
68:          if (offset < 0 || offset >= itsSize)
69:              throw XBoundary();
70:          return pType[offset];
71:      }
72:
73:      friend ostream&operator<<(ostream& os, const Array& a)
74:      {
75:          os << "Array size: " << a.itsSize;
76:          return os;
77:      }
78:  };
79:
80:  int main()
81:  {
82:      Array intArray(10);
83:      try
84:      {
85:          for (int i = 0; i < 15; i++)
86:              intArray[i] = i;
87:              cout << "Array index: " << i << endl;
88:      }
89:      catch (XBoundary e)
90:      {
91:          cout << "Caught exception: index out of range!" << endl;
92:      }
93:      return 0;
94:  }
```

在尝试确定块的位置时，请查看分配内存或使用资源的地方。其他需要检查的还有越界错误、非法输入等。

# 捕获异常

捕获异常的工作如下：当异常被抛出时，会检查调用栈。调用栈是程序的一个部分调用另一个函数时创建的函数调用列表。

调用栈跟踪执行路径。如果 `main()` 调用函数 `Animal::GetFavoriteFood()`，而 `GetFavoriteFood()` 调用 `Animal::LookupPreferences()`，后者又调用 `fstream::operator>>()`，那么所有这些都在调用栈上。递归函数可能会在调用栈上出现多次。

异常沿着调用栈向上传递给每个闭合块。随着栈的回溯，栈上局部对象的析构函数会被调用，对象会被销毁。

每个 `try` 块后面跟着一个或多个 `catch` 语句。如果异常匹配其中一个 `catch` 语句，则认为通过执行该语句处理了异常。如果它不匹配任何项，则继续进行栈的回溯。

如果异常一直到达程序的开头（`main()`）且未被捕获，则会调用内置处理器来终止程序。

注意的是，栈的回溯是单行道。随着它的进行，栈会被回溯，栈上的对象会被销毁。没有回头路：异常被处理后，程序将从处理该异常的 `catch` 语句的 `try` 块之后继续执行。

因此，在列表 20.1 中，执行将在第 101 行继续，即处理 `xboundary` 异常的 `catch` 语句 `try` 块之后的第一行。记住，当异常发生时，程序流将在 `catch` 块之后继续，而不是抛出异常的点。

# 多个 catch 规格

多个条件可能导致异常。在这种情况下，`catch` 语句可以一个接一个排列，就像 `switch` 语句中的条件一样。`default` 语句等价于“捕获所有”语句，用 `catch(...)` 表示。列表 20.2 展示了多个异常条件。

# 异常与错误处理

输入列表 20.2 多重异常

```cpp
1: #include <iostream.h>
2: // Listing 20.2: multiple exceptions
3: const int DefaultSize = 10;
4: 
5: class Array
6: {
7:     public:
8:     // constructors
9:     Array(int size = DefaultSize);
10:    Array(const Array& rhs);
11:    ~Array() { delete [] ptype; }
12: 
13:    // operators
14:    Array& operator=(const Array&);
15:    int& operator[](int offset);
16:    const int& operator[](int offset) const;
17: 
18:    // accessors
19:    int GetItsSize() const { return itsSize; }
20: 
21:    // friend function
22:    friend ostream& operator<<(ostream, const Array&);
23: 
24:    // define the exception classes
25:    class xBoundary {};
26:    class xTooBig {};
27:    class xToSmall {};
28:    class xZero {};
29:    class xNegative {};
30:    private:
31:        int *ptype;
32:        int itsSize;
33:    };
34: 
35:    int& Array::operator[](int offset)
36:    {
37:        int size = GetItsSize();
38:        if (offset >= 0 && offset < GetItsSize())
39:            return ptype[offset];
40:        throw xBoundary();
41:        return ptype[0]; // appease MFC
42:    }
43: 
44: const int& Array::operator[](int offset) const
45:    {
46:        int mysize = GetItsSize();
47:        if (offset >= 0 && offset < GetItsSize())
48:            return ptype[offset];
49:    
50:    throw xBoundary();
51:
52:        return pType[0];  // appease MFC
53:    }
54:
55:
56:    Array::Array(int size):
57:        itsSize(size)
58:    {
59:        if (size == 0)
60:            throw xZero();
61:        if (size < 10)
62:            throw xTooSmall();
63:        if (size > 30000)
64:            throw xTooBig();
65:        if (size < 1)
66:            throw xNegative();
67:
68:        pType = new int[size];
69:        for (int i = 0; i<size; i++)
70:            pType[i] = 0;
71:    }
72:
73:
74:
75:    int main()
76:    {
77:
78:        try
79:        {
80:            Array(0);
81:            for (int j = 0; j < 100; j++)
82:            {
83:                intArray[j] = j;
84:                cout << "intArray[" << j << "] okay...\n";
85:            }
86:        }
87:        catch (Array::xBoundary)
88:        {
89:            cout << "Unable to process your input!\n";
90:        }
91:        catch (Array::xTooBig)
92:        {
93:            cout << "This array is too big...\n";
94:        }
95:
96:        catch (Array::xTooSmall)
97:        {
98:            cout << "This array is too small...\n";
99:        }
100: catch (Array::xZero)
101:   cout << "You asked for an array of objects!\n";
102: }
103: catch (...)
104: {
105:   cout << "Something wrong!\n";
106: }
107: cout << "Done.\n";
108: return 0;
109: }
```
