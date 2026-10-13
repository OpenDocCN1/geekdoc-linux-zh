
### if 语句

你可以使用 `if` 语句测试一个表达式，并且仅当表达式不为零时执行语句。`if` 语句采用以下形式：

```
if ( expression ) statement
```

`if` 之后的语句仅在括号中的表达式求值为非零值时执行。该语句通常是复合语句。以下是一个示例：

```c
if(mem_left < threshold)
{
    Message("Low on memory! Close some windows.\n");
}
```

### if-else 语句

`if-else` 语句是 `if` 语句与 `else` 子句结合的一种形式。语句的语法为

```
if ( expression )
    statement_1
else
    statement_2
```

其中如果括号内的表达式不为零，则执行 `statement_1`。否则，执行 `statement_2`。以下示例使用 `if` 和 `else` 选择两个变量中较小的一个：

```c
if ( a <= b)
    smaller = a;
else
    smaller = b;
```

### 空语句

空语句由单个分号表示，不执行任何操作。当所有处理都在循环表达式中完成而不是在循环体中完成时，你在循环中使用空语句。例如，要定位标记字符串末尾的零字节，可以使用以下语句：

```c
char str[80] = "Test";
int i;
for (i=0; str[i] != '\0'; i++)
    ; /* Null statement */
```

### return 语句

`return` 语句停止执行当前函数并将控制返回给调用函数。语法是

```
return expression;
```

其中表达式的值作为函数的值返回。对于不返回值 的函数，使用以下方式不带表达式的 `return` 语句：

```
return;
```

### switch 语句

`switch` 语句根据表达式的值执行多分支。它具有以下语法：

```
switch (expression)
{
    case value1:
        statement_1
        break;
    case value2:
```
`statement_2`
`break;`
`.`
`.`
`default:`
    `statement_default`
}
```

如果 `switch` 测试的表达式求值为 `value1`，则执行 `statement_1`。如果表达式等于 `value2`，则执行 `statement_2`。将值与每个 `case` 标签进行比较，并执行与匹配标签对应的语句。如果值与任何 `case` 标签都不匹配，则执行 `default` 标签后面的块 `statement_default`。每个语句都以 `break` 语句结束，将一个 `case` 标签的代码与另一个 `case` 标签的代码分隔开。以下是根据名为 `command` 的整数变量的值调用不同例程的 `switch` 语句：

```
switch (command)
{
    case 'q':
        quit_app();
    case 'c':
        connect();
        break;
    case 's':
        set_params();
        break;
    case '?':
    case 'H':
        print_help();
        break;
    default:
        printf("Unknown command!\n");
}
```

## while 语句

`while` 语句用于以下形式

```
while (expression) statement
```

其中语句执行直到表达式求值为 0。`while` 语句在每次执行语句之前评估表达式。因此，`while` 循环执行语句零次或多次。以下是用于将一个数组复制到另一个数组的 `while` 语句：

```
i = length;
while (i >= 0) /* Copy one array to another */
{
    array2[i] = array1[i];
    i--;
}
```

## 函数

函数是一组声明和语句。因此，函数是 C 程序的构建块。每个 C 程序至少有一个函数——`main` 函数，C 程序的执行从这里开始。C 库主要包含函数，尽管其中也包含相当多的宏。

## 函数原型

在 C 中，你必须在使用函数之前声明它。函数声明告诉编译器函数返回的值的类型以及它接受的参数的数量和类型。将函数声明为完整的函数原型，显示返回类型以及参数列表。C 库中的 `calloc` 函数返回一个 `void` 指针并接受两个参数，每个参数的类型都是 `size_t`，这是一种无符号整数类型，其大小足以容纳 `sizeof` 运算符的值。因此 `calloc` 的函数原型如下：

```
void *calloc(size_t, size_t);
```

该原型显示了参数列表中每个参数的类型。你也可以为每个参数包含一个标识符。在这种情况下，你将按如下方式编写原型：

```
void *calloc(size_t num_elements, size_t elem_size);
```

这里原型看起来与函数定义的第一行完全一样，只是你没有定义函数，而是在行尾加上分号结束。参数使用合适的名称时，这种原型的形式可以提供大量关于函数使用的信息。例如，只看一下 `calloc` 的原型就应该能告诉你它的第一个参数是要分配的元素数量，第二个参数是每个元素的大小。

调用函数时可能犯的错误，例如传递错误数量的参数（当函数接受固定数量的参数时）或向函数传递错误类型的参数。

## void 类型

当一个函数既不返回任何内容也不接受任何参数时该怎么办？为处理这些情况，C 提供了 `void` 类型，它可用于声明不返回任何内容的函数以及描述可以指向任何类型数据的指针。例如，你可以使用 `void` 返回类型声明一个不返回任何内容的函数，如 `exit`：

```
void exit(int status);
```

另一方面，如果一个函数不接受任何形式参数，其参数列表由 `void` 表示：

```
FILE *tmpfile(void);
```

`void` 指针对于处理内存块的函数很有用。例如，当你从内存分配例程 `malloc` 请求一定数量的字节时，你可以使用这些位置存储适合该空间的任何数据。在这种情况下，已分配内存块的第一个位置的地址作为 `void` 指针返回。因此，`malloc` 的原型写成如下：

```
void *malloc(size_t numbytes);
```

## 具有可变数量参数的函数

如果一个函数接受可变数量的参数，你可以使用省略号 `...` 代替参数列表来表示这一点；但是，你必须在省略号之前提供至少一个参数。`stdio.h` 头文件中定义的 `printf` 系列函数就是此类函数的良好示例。这些函数的原型如下：

```
int fprintf(FILE *stream, const char *format, ...);
int printf(const char *format, ...);
int sprintf(char *buffer, const char *format, ...);
```

## C 库

ANSI 和 ISO 对 C 的标准定义了 C 的所有方面——语言、预处理器和库。库中函数的原型以及所有必要的数据结构和预处理器常量都在一组标准头文件中定义。表 2-4 列出了标准头文件，包括其内容摘要。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_788_0.png)

如果你要在 C 中编写应用程序，你必须熟悉许多标准库，因为 C 的大部分编程能力都在于此。如果你正在编写图形应用程序，你还必须学习其他库，例如 The GIMP 工具包。

## 表 2-4 C 中的标准头文件

| 头文件 | 用途 |
|---|---|
| `<assert.h>` | 定义 `assert` 宏。用于程序诊断。 |
| `<ctype.h>` | 声明用于分类和转换字符的函数。 |
| `<errno.h>` | 定义错误条件的宏、`EDOM` 和 `ERANGE`，以及整数变量 `errno`，库函数在其中返回错误代码。 |
| `<float.h>` | 定义可存储在浮点类型中的值的范围。 |
| `<iso646.h>` | 定义了一些宏，在用非英语语言编写 C 程序时很有帮助，这些语言可能将字符组合如 `&` 和 `~` 用于其他目的。 |
| `<limits.h>` | 定义所有整数数据类型的限制值。 |
| `<locale.h>` | 声明 `lconv` 结构以及使 C 程序适应特定区域设置所需的函数。 |
| `<math.h>` | 声明常见的数学函数和 `HUGE_VAL` 宏。 |
