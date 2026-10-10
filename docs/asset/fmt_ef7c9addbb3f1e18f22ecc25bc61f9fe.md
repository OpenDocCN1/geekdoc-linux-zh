
```c
#include <stdio.h>
void print_square(int val);
int main()
{
    int num = 5;
    print_square(num);
}
void print_square(int val)
{
    printf("\nThe square is %d\n", val);
}
```

## 函数返回值

除了接受参数，函数还可以返回值。这意味着你可以让函数调用成为算术运算和赋值的一部分。例如，假设有一个函数 `triple(int)`。它被设计为返回一个 `int` 并将其乘以三。你可以这样使用函数调用：

```c
y = triple(x);
```

函数接收 `x` 的值，将其三倍，然后返回该值。前面的语句将返回值存储在变量 `y` 中。`triple()` 函数可能如下：

```c
int triple(int num)
{
  return (num * 3);
}
```

该函数被定义为 `int` 函数。这意味着它返回一个 `int` 值。你可以在程序中任何预期 `int` 的地方调用此函数。该函数接收单个参数，该参数也是 `int`。在该函数中，参数存储在变量 `num` 中。下一个示例程序演示了该函数：

```c
#include <stdio.h>
int triple(int num);
int main()
{
  int x = 6, y;
  y = triple(x);
  printf("%d tripled is %d.\n", x, y);
}
int triple(int num)
{
  return (num * 3);
}
```

程序的输出是：

6 tripled is 18.

# C 语言编程简介 523

程序的输出如下：

```
[stephen@localhost ~] ./func3
6 tripled is 18.
```

尝试“动手实践项目 10–4”来创建接受参数并返回值的函数。

# 在 C 中处理文件

文件是连续的数据流。它们通常存储在磁盘上。许多文件操作是顺序的，这意味着它们从文件的开始一直到文件的末尾进行工作。当文件被打开时，你正在操作的是文件的开头。每当向文件读取或写入一个字节时，你在文件中的当前位置就会向前移动一个字节。

# 文件指针

C 的输入输出被设计为使用文件指针，文件指针指向一个包含文件信息的预定义结构。该结构模板在 `stdio.h` 中。在使用 I/O 包时，你必须声明一个文件指针。以下是一个示例：

```
FILE *fp;
```

这将 `fp` 声明为文件指针。它被用于各种文件访问函数。

# 打开和关闭文件

在使用文件之前，必须先打开它。用于打开文件的库函数是 `fopen()`，在下面的示例中：

```
fp = fopen("myfile.dat", "r");
```

`fopen()` 函数接受两个参数：文件名和访问模式。此示例打开了一个名为 `myfile.dat` 的文件。"r" 表示以只读模式打开文件。

接下来的语句使用 "w" 访问模式进行写入：

```
fp = fopen("myfile.dat", "w");
```

`fopen()` 函数返回一个文件指针。如果无法打开文件，它将返回一个 `NULL` 指针（指向地址 0 的指针）。下面的代码是你可以测试文件是否打开的一种方法：

```c
if ((fp = fopen("myfile.dat", "r"))==NULL)
{
    printf("Error opening myfile.dat\n");
}
```

打开文件的相反操作是关闭文件。当文件被关闭时，它的缓冲区会被刷新，确保所有数据都已正确写入文件中。`fclose()` 函数用于关闭由 `fopen` 打开的文件。这里是一个示例：

```
fclose(fp);
```

# 第 10 章使用 C 和 C++ 开发 UNIX/Linux 应用程序

# 执行文件输入/输出

C 提供了许多用于读写写文件的函数。在本章中，你将重点关注两个：`fgets` 和 `fputc`。这两个函数 `fgets()` 和 `fputc()` 执行对文件的字符输入/输出。以下是 `fgets()` 的一个示例：

```
ch = fgetc(fp);
```

`fgets()` 从文件中读取单个字符并指向它。该字符是从当前位置读取的。字符输出通过 `fputc()` 执行，如如下示例所示：

```
fputc(ch, fp);
```

在例示例中，存储在 `ch` 中的字符被写入到由 `fp` 指引的文件的当前位置。

# 测试文件末尾

使用 `feof()` 函数来确定在输入操作期间是否遇到了文件结束标记符，如接下来的示例所示：

```c
if (feof(fp))
    fclose(fp);
```

如果遇到了文件结束标记符，`feof()` 函数返回非零值。否则，它返回零。

现在你已经对 C 语言的文件操作有了基本了解，准备好在“动手实践项目 10-5”中练习编写一个执行文件输入/输出的程序。

# 使用 make 工具维护程序源文件

你可能经常处理包含许多源代码文件的程序。例如，你在“动手实践项目 10-4”中创建的绝对程序可以分为两个文件。以下是 `absolute.c` 程序的代码。

```c
#include <stdio.h>
int absolute(int num);
int main()
{
    int x = -12, y;
    y = absolute(x);
    printf("The absolute value of %d is %d\n", x, y);
}
int absolute(int num)
{
    if (num < 0)
        return (-num);
    else
        return (num);
}
```

# C 语言编程简介 525

如果你将此程序分成两个文件，一个文件可以包含 `main()` 函数，另一个文件可以包含 `absolute()` 函数。一个名为 `abs_func.c` 的文件可以如下：

```c
int absolute(int num)
{
    if (num < 0)
        return (-num);
    else
        return (num);
}
```

第二个名为 `abs_main.c` 的文件可能包含以下代码行：

```c
#include <stdio.h>
int absolute(int num);
int main()
{
    int x = -12, y;
    y = absolute(x);
    printf("The absolute value of %d is %d\n", x, y);
}
```

创建两个文件的优点是你可以将代码分解为更小、更容易理解的模块，这些模块可以与其他模块组合。在示例中，两个文件可以被编译并链接成一个可执行程序。尝试“动手实践项目 10-4”来练习这种编程技术。

当你开发如 `absolute.c` 这样的多模块程序并进行更改时，你必须重复编译程序。然而，通过 `make`，你就不需要手动执行这些命令了。`make` 会根据时间戳自动决定哪些文件需要重新编译。这种方法在处理大型项目时非常有用。尝试“动手实践项目 10-4”来练习这种编程技术。

# 调试你的程序

C 语言程序员的典型错误包括使用错误的语法，例如忘记用分号结束语句。或者，由于你在 C 程序中键入几乎所有内容都是小写的，你的程序可能会出现大小写敏感错误。如果你在 `print` 命令中漏掉一个引号，你可能会在屏幕上看到如下示例：

```
simple.c:10: unterminated string or character constant
simple.c:10: possible real start of unterminated constant
simple.c:4: missing terminating " character
simple.c:5: error: syntax error before ')' token
```

编译器产生的错误数量通常比它在代码中发现的实际错误数量多。编译器会报告错误行以及任何受错误影响的周围行：

> 记住，每当你修改（修正或添加文本）程序源文件时，你都必须重新编译程序以创建一个新的可执行程序。

要纠正程序中的语法错误，请遵循以下步骤：

1. 写下每个错误的行行号和简要描述。
2. 编辑你的源文件，将光标移动到编译器报告的第一行号。
3. 在源文件中纠正错误，然后将光标移动到下一行号。大多数编辑器会显示当前行号，帮助你定位文件中的特定行。
4. 纠正错误后，保存并重新编译文件。
