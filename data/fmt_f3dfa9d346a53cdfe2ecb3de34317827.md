
... 省略号用于函数原型的形式参数列表中，以表示可变数量的参数或不同类型 的参数。

为了说明一些常用运算符，请考虑以下简短程序：

```c
main()
{
  int a;
  int b;
  int c;
  a = 5;        /*Assign a value of 5 to variable 'a'*/
  b = a/2;      /*Assign the value of 'a' divided by two to variable 'b'*/
  c = b * 2;    /*Assign the value of 'b' multiplied by two to variable 'c'*/

  if (a == c)    /* Test if 'a' holds the same value as 'c' */
    puts("Variable 'a' is an even number");
  else
    puts("Variable 'a' is an odd number");
}
```

通常，当递增变量的值时，你会写类似以下内容：

```c
x = x + 1
```

C 还提供增量运算符 `++`，因此你可以写成：

```c
x++
```

同样，你可以使用 `--` 递减变量的值，如下所示：

```c
x--
```

所有其他数学运算符都可以以相同方式使用；因此，在 C 程序中，你可以写成简写形式：

| 常规写法 | C 简写 |
|---|---|
| `x = x + 1` | `x++` |
| `x = x - 1` | `x--` |
| `x = x * 2` | `x *= 2` |
| `x = x / y` | `x /= y` |
| `x = x % 5` | `x %= 5` |

# 函数

函数是构成 C 程序的源代码过程。它们遵循以下一般形式：

```c
return_type function_name(parameter_list)
{
	statements
}
```

`return_type` 指定函数将返回的数据类型：`char`、`int`、`double`、`void` 等。C 函数内的代码对其他任何 C 函数都是不可见的；不能从一个函数跳到另一个函数的中间，尽管函数可以调用其他函数。此外，函数不能在其他函数内部定义，只能定义在源模块中。

参数可以通过值或通过引用传递给函数。如果参数通过值传递，则只有参数的当前值的副本被传递给函数。然而，通过引用传递的参数是指向实际参数的指针，该指针随后可以被函数修改。以下示例将两个参数通过值传递给函数 `funca()`，该函数尝试修改传递给它的变量的值。然后，它将相同的两个参数通过引用传递给 `funcb()`，后者也尝试修改它们的值：

```c
#include <stdio.h>
int funca(int x, int y)
{
/* This function receives two parameters by value, x and y */
x = x * 2;
y = y * 2;

printf("\nValue of x in funca() %d value of y in funca() %d",x,y);

return(x);
}

int funcb(int *x, int *y)
{
/* This function receives two parameters by reference, x and y */

*x = *x * 2;
*y = *y * 2;

printf("\nValue of x in funcb() %d value of y in funca() %d",*x, *y);

return(*x);
}

main()
{
int x;
int y;
int z;

x = 5;
y = 7;

z = funca(x,y);
z = funcb(&x,&y);

printf("\nValue of x %d value of y %d value of z %d",x,y,z);
}
```

在这里，`funcb()` 不改变其接收的参数的值；相反，它改变接收的指针所指向的内存地址中的内容。虽然 `funca()` 从函数 `main()` 接收变量 `x` 和 `y` 的值，但 `funcb()` 从函数 `main()` 接收变量 `x` 和 `y` 的内存地址。

# 向函数传递数组

以下程序将一个数组传递给函数 `funca()`，该函数初始化数组元素：

```c
#include <stdio.h>

void funca(int x[])
{
int n;
    for(n = 0; n < 100; n++)
        x[n] = n;
    }

main()
{
    int array[100];
    int counter;

    funca(array);

    for(counter = 0; counter < 100; counter++)
        printf ("\nValue of element %d is %d",counter,array[counter]);
}
```

`funca()` 的参数 `int x[]` 被声明为任意长度的数组。之所以有效，是因为编译器将数组参数的起始地址传递给函数，而不是各个元素的值。这当然意味着函数可以改变数组元素的值。为了防止函数改变值，你可以将参数指定为 `const` 类型：

```c
func(const int x[])
{
```

这将导致在尝试向数组写入值的行处产生编译器错误。然而，将参数指定为 `const` 并不能保护该参数免受间接赋值的影响，如下面的程序所示：

```c
#include <stdio.h>

int func(const int x[])
{
    int *ptr;
    int n;

/*  This line gives a 'suspicious pointer conversion warning' */
/*  because x is a const pointer, and ptr is not */
    ptr = x;

    for(n = 0; n < 100; n++)
    {
        *ptr = n;
        ptr++;
    }
}

main()
{
    int array[100];
    int counter;

    func(array);
    for (counter = 0; counter < 100; counter++)
        printf ("\nValue of element %d is %d",counter,array[counter]);
}
```

# 向 main() 传递参数

C 允许在程序开始执行时通过两个参数 `*argc*` 和 `*argv[]*` 从操作系统向程序传递参数，如下所示：

```c
#include <stdio.h>

main(int argc, char *argv[ ])
{
    int n;
    for (n = 0; n < argc; n++)
        printf ("\nParameter %d equals %s",n,argv[n]);
}
```

参数 `*argc*` 保存传递给程序的参数数量；而数组 `*argv[]*` 保存每个传递参数的地址；`*argv[0]*` 始终是程序名称。此功能在需要访问系统文件的应用程序中可以得到很好的利用。考虑以下场景：一个简单的数据库应用程序将其数据存储在一个名为 `*data.dat*` 的单个文件中。需要创建该应用程序，使其可以存储在使用软盘或硬盘上的任何目录中，并且既可以从宿主目录内部执行，也可以通过 DOS 搜索路径执行。为了正确工作，应用程序必须始终知道在哪里找到数据文件 `*data.dat*`。这可以通过假设数据文件与可执行模块位于同一目录来解决，这是加诸操作员的一个并不不合理的限制。以下代码片段说明了应用程序如何应用此算法以始终能够定位所需的系统文件：

```c
#include <string.h>

char system_file_name[160];

void main(int argc,char *argv[ ])
{
    char *data_file = "DATA.DAT";
    char *p;

    strcpy(system_file_name,argv[0]);
    p = strstr(system_file_name,".EXE");
    if (p == NULL)
    {
        /* The executable is a .COM file */
        p = strstr(system_file_name,".COM");
    }

    /* Now back track to the last '\' character in the file name */
    while (*(p - 1) != '\\')
        p--;
}
```

235
