

我经常编写诸如 copyops.cpp 这样的测试程序，其中包含的函数除了向标准输出写入字符串之外什么也不做。这提供了每个函数被调用时何时被调用的有用跟踪，如以下示例运行所示。输入以下两个命令即可查看程序输出：
$ g++ copyops.cpp
$ ./a.out
Inside default constructor
Inside copy constructor
Inside copy constructor
Inside operator=() member function

程序声明了一个类 TAnyClass，它具有默认构造函数、拷贝构造函数和 operator=() 成员函数。main() 函数使用以下语句创建并复制对象：
TAnyClass t1;
TAnyClass t2 = t1;
TAnyClass t3(t2);
t1 = t3;

每个语句在屏幕上产生一行文本。第一个语句通过调用 TAnyClass() 默认构造函数构造对象 t1。第二个语句将 t1 的副本作为新对象 t2 构造。这会调用 TAnyClass() 拷贝构造函数。第三个语句将 t2 的副本作为对象 t3 构造，也会调用拷贝构造函数。第四个语句将已存在的对象 t3 分配给另一个对象 t1。由于这两个对象已经存在，因此不会调用任何构造函数。然而，由于 TAnyClass 实现了 operator=() 函数，C++ 会调用它来处理赋值。

前面的代码仅演示了拷贝构造函数和 operator=() 成员函数的形式。利用这些工具，现在可以创建一个安全的 TPrompt 类，该类可安全地复制类对象。清单 13.4，prompt2.cpp，展示了 resulting 程序。

## LISTING 13.4 PROMPT2.CPP

```
#include <iostream.h>
#include <string.h>  // Need strlen(), strcpy()

// A class that prompts users to enter a string, and also
// provides for safe copying

class TPrompt {
private:
    char * tp_string;  // Addresses the string input
public:
    TPrompt(const char *prompt);        // Constructor
    TPrompt(const TPrompt &copy);       // Copy constructor
    ~TPrompt();                         // Destructor
    void operator=(const TPrompt &copy); // Assignment operator
    const char *GetString();            // Returns user input
};

int main()
{
```
```
// Use the class to construct a local object
TPrompt prompt1("Prompt #1: ");
cout << "You entered " << prompt1.GetString() << endl;

// Construct another object
TPrompt prompt2("Prompt #2: ");
cout << "You entered " << prompt2.GetString() << endl;

// Test copy constructor
TPrompt prompt3(prompt2);
cout << "Prompt 3 " << prompt3.GetString() << endl;

// Test operator=() function
prompt1 = prompt3;
cout << "Prompt 1   " << prompt1.GetString() << endl;

return 0;
}

// Constructor
TPrompt::TPrompt(const char *prompt)
{
    const int buf_size = 128;        // Size of input buffer
    char *temp = new char[buf_size]; // Create input buffer
    cout << prompt;                  // Prompt user for input
    cin.getline(temp, buf_size);     // Read input from user
    tp_string = new char[strlen(temp) + 1]; // Create string
    strcpy(tp_string, temp);         // Copy buffer to result
    delete[] temp;                   // Delete the buffer
}

// Copy constructor
TPrompt::TPrompt(const TPrompt &copy)
{
    tp_string = new char[strlen(copy.tp_string) + 1];
    strcpy(tp_string, copy.tp_string);
}

// Destructor
TPrompt::~TPrompt()
{
    delete[] tp_string;   // Delete dynamic memory
}

// Assignment operator
void TPrompt::operator=(const TPrompt &copy)
{
    if (this == &copy) return;       // Avoid copying self to self
    delete[] tp_string;              // Delete old data
    tp_string = new char[strlen(copy.tp_string) + 1];
    strcpy(tp_string, copy.tp_string);
}

// Member function
const char *TPrompt::GetString()
{
    return tp_string;
}
```

修订后的 `TPrompt` 类声明了拷贝构造函数和 `operator=()` 成员函数，二者共同安全地处理 `TPrompt` 对象的复制。该类的拷贝构造函数使用 new `operator`、`strlen()` 和 `strcpy()` 函数来创建由 `copy.tp_string` 指向的动态字符串的副本：

```cpp
tp_string = new char[strlen(copy.tp_string) + 1];
strcpy(tp_string, copy.tp_string);
```

在拷贝构造函数内部，copy 参数引用正在被复制的源 `TPrompt` 对象。每个对象——正在被复制的对象和正在构造的新对象——都有一个 `tp_string` 指针。使用 `strlen()` 和 `strcpy()`，前面的语句确保每个对象都指向动态内存的新副本。

> **Note**
> 
> C 程序员可能会使用单个 `strcpy()` 语句来复制字符串，但由于它没有使用 C++ `new` 运算符来分配内存，因此需要调用 `free()` 来释放已分配的内存。为了使用 `new` 和 `delete` 进行内存管理，我使用了两个语句来执行字符串复制。

以下这样的语句会调用拷贝构造函数：

```
TPrompt prompt3(prompt2);  // calls copy constructor
```

`prompt2` 对象，即正在被复制的对象，按引用传递给拷贝构造函数的 copy 参数。拷贝构造函数进而将 `copy.tp_string` 传递给 `strlen()` 和 `strcpy()` 以分配内存并复制字符串。由于内存中现在有两个等价的字符串，当 `prompt3` 和 `prompt2` 超出作用域时，`TPrompt` 析构函数会删除它们的指针。由于这两个指针指向不同的内存块，因此不会发生段错误。

同样，`TPrompt::operator=()` 函数处理一个 `TPrompt` 对象向另一个对象的赋值。该函数类似于拷贝构造函数，但由于两个对象已经存在，因此该函数的语句需要执行一些额外的任务：

```
if (this == &copy) return;   // Avoid copying self to self
delete[] tp_string;           // Delete old data
tp_string = new char[strlen(copy.tp_string) + 1];
strcpy(tp_string, copy.tp_string);
```

这是一个需要 `this` 指针的情况。正如你可能回忆的那样，this 指向调用构造函数、成员函数或析构函数的对象。在本例中，`this` 指向赋值运算符左侧的对象——换句话说，就是正在被赋值的目标对象。在前面的代码片段中，`if` 语句测试程序是否将同一个对象赋给自身——这无疑是一个愚蠢的错误，但在包含数百个甚至更多在内存中飞速运行的对象的复杂程序中，这确实是可能的。在这种情况下，`operator=()` 函数简单地返回，因为如果两个对象相同，就没有需要复制的内容。

如果两个对象不同，该函数会删除目标对象 `tp_string` 指针所指向的任何现有内存。该指针即将从

