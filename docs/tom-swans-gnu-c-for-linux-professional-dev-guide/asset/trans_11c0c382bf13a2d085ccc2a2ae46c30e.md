

短整型和长整型实际上分别是 short int 和 long int 的缩写。你可以使用这些未缩写的名称来声明变量，如下所示：

```
short int shorter;
long int longer;
```

但下面的声明是等价的，而且更常见：

```
short shorter;
long longer;
```

你可以将 unsigned 和 signed 与 short 和 long int 声明结合使用。例如，下面的语句声明了两个 unsigned 变量，类型分别为 short int 和 long int：

```
unsigned short int short_n_sweet;
unsigned long int long_n_tall;
```

## Constants As Macros

常量是一个程序在运行时无法更改的对象或其他值。在 C++（以及 ANSI C）中，有两种类型的常量——由宏定义的常量和作为数据对象定义的常量。最简单的常量是由 #define 指令创建的宏。例如，这定义了一个名为 MAXIMUM 等于 100 的常量：

```
#define MAXIMUM 100
```

像 MAXIMUM 这样的符号被称为宏，因为 C++ 预处理器会在符号出现的地方将其替换为其关联的值（但字符串或注释内部除外）。按照惯例，以这种方式定义的常量都写成全大写，但这不是必需的。

定义 MAXIMUM 之类的常量的最重要原因是为了避免在程序源代码中散布字面值。例如，即使 MAXIMUM 在一百个不同的地方使用，修改 #define 指令即可更改其关联的值。命名良好的常量也使程序的源代码更易于理解。

你可以在其值（100）合适的地方使用 MAXIMUM 这样的常量。所说的“值”并不是指其整数值——尽管看起来如此，MAXIMUM 并不是一个整数对象。它是字符 1、0 和 0 的符号宏表示。你可以使用如下输出语句显示 MAXIMUM

```
cout << "MAXIMUM == " << MAXIMUM << endl;
```

预处理后，该语句会被编译为好像写成这样：

```
cout << "MAXIMUM == " << 100 << endl;
```

在展开 MAXIMUM 宏时，C++ 预处理器会在编译前将字符 1、0 和 0 插入到程序文本中。

使用 #define 创建常量时，还有另外两条重要的规则需要记住。首先，切勿在指令末尾加上分号。在 GNU C++ 中，这种常见错误会产生以下警告和错误信息：

x.cpp:5: warning: missing white space after '#define MAXIMUM'
x.cpp:9: parse error before ';'

其次，请记住，使用 #define 创建的常量仅仅是对其后内容（忽略前导空白）的符号表示。如何恰当地使用常量取决于你。清单 6.2，defines.cpp，展示了使用 #define 创建的各种类型常量的几个示例。

### LISTING 6.2 DEFINES.CPP

```
#include <iostream.h>

#define CHARACTER '@'
#define STRING "I'd rather be programming!"
#define MAX_VALUE 100
#define PI 3.14159

int main()
{
cout << "CHARACTER == " << CHARACTER << endl;
cout << "STRING == " << STRING << endl;
cout << "MAX_VALUE == " << MAX_VALUE << endl;
cout << "PI == " << PI << endl;
return 0;
}
```

编译并运行 defines.cpp 会产生以下输出：

```
CHARACTER == @
STRING == I'd rather be programming!
MAX_VALUE == 100
PI == 3.14159
```

正如该程序所示，使用 #define 创建的常量可以表示任何你能输入到程序文本中的数据类型，包括字符、字符串、整数和浮点值，仅举几例。

## CONSTANTS AS OBJECTS

声明常量值的另一种方法是使用保留字 const 在对象声明前加上前缀。这告诉编译器禁止程序尝试更改常量的值。const 标识符是 C++ 的创新，但已被重新纳入 ANSI C，因此你现在可以在 C 和 C++ 程序中使用 const。

将对象声明为 const 会在它们周围形成一道屏障，防止其值在运行时被更改。如果你像这样将整数 count 声明为 const：

```
const int count = 1234;
```

编译器会拒绝以下语句：

```
count = count + 100; // ???
```

count 的初始值被锁定，后续的程序语句无法更改它。

