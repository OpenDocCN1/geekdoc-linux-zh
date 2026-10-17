
类中的变量具有不同的作用域，取决于它们如何声明。全局变量定义为外部可见的变量。静态变量可以在文件作用域内或函数内声明。静态变量在外部不可见，并以特殊方式处理。自动变量（`automatic variable`）是在函数内部声明的变量，仅在相应函数运行且未结束时在栈上可用。以下是关于如何声明三种作用域变量的简要概述（这对于理解如何在 GDB 中处理每类型非常重要）。

```
Global variable:
int foo = 6 ;
```

> 注意：你必须在最高作用域内并在任何函数之外声明变量。

Static variable:

`static int foo = 6;`

```
Automatic variable:
int function() {
  int foo = 6;
}
```

全局符号始终可以在调试器中查看，尽管你可能并不总是知道它的类型。静态变量也是始终可用的，但剥离的可执行文件或库可能不包含静态函数的名称。函数局部变量（也称为自动变量）只有在源代码用 `-g` 编译时才能进行打印。以调试模式构建提供了打印自动变量所需的两个条件：第一是类型信息；第二是自动变量的调试信息，包括它们与类型信息的链接。

考虑一个如下定义的全局变量：

```
const char *constString = "This is a constant string!";
```

对于一个未用 `-g` 编译的程序，在 GDB 中打印此内容将产生：

```
(gdb) print constString
$2 134513832
```

GDB 可以找到全局变量，但它不知道它的类型。只要它是一个基础类型（即不是结构体、类或联合体），我们仍然可以使用格式化功能正确打印它：

```
(gdb) printf "%s\n", constString
This is a constant string!
(gdb)
```

我们能够将 `constString` 作为字符串打印，因为它是一个基础类型并且是一个全局符号。局部符号不会存储在符号表中，如果不进行调试构建将无法引用它。

接下来，让我们看看如何打印静态变量。这与全局变量类似，不同之处可能有多个同名的静态变量。

考虑定义在文件级别的静态函数（即声明为 `static` 但在函数作用域之外）：

```
static int staticInt = 5 ;
```

接下来，让我们看看有多少个静态函数：

```
(gdb) info variable staticInt
All variables matching regular expression "staticInt":
1 = 5
```

因为只列出了一个，接下来让我们打印它的值：

```
(gdb) print /x staticInt
$3 = 0x5
```

自动变量不在符号表中，这意味着如果不进行调试构建就无法找到。考虑这个定义了 `b` 的简单函数：

```
int function( int a )
{
    int b = 0;
}
```

如果我们没有使用调试（即没有 `g`），GDB 将没有名称。如果使用了 `-g` 编译，GDB 就能找到变量并打印其值：

```
(gdb) break foo
Breakpoint 1 at 0x804822: file foo.C, line 30.
(gdb) run
Starting program: /home/wilding/src/Linuxbook/foo

Breakpoint 1, foo(int) (a=6) at foo.C:30
int b = 0;
(gdb) print b
No symbol "b" in current context.
```

### 6.5.3.2 打印格式

打印格式化允许用户更改变量和内存的显示方式。有时以十六进制格式打印整数更有用，而查看十进制格式也有帮助。查看变量值的基本方法（即不格式化）是使用 `print <variable_name>` 命令。

```
(gdb) print stackVar
$1 = 10
```

你可以指定想要显示的格式。例如，要以十六进制查看，请使用 `/x` 参数：

```
(gdb) /x stackVar
$2 = 0xa
```

注意变量值前面总有一个美元符号、数字和等号。这是因为 GDB 自动将打印的值赋值并存储在该命名的内部变量。GDB 将这些称为*便利变量*（convenience variables）。例如，你可以在此调试会话中重用新创建的 `$1` 进行其他计算：

```
(gdb) print $1 + 5
$3 = 15
```

# GNU 调试器 (GDB) 第 6 章

比 `print` 命令更强大的替代方案是 `printf` 命令。`printf` 命令的工作原理与标准 C 库函数的工作非常相似：

```c
(gdb) printf "The value of stackVar in hex is 0x%x\n", stackVar
The value of stackVar in hex is 0xa
```

打印数组同样简单。考虑以下数组：

```c
int list[10] = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
```

你可以完整地打印数组，也可以只打印其中一个元素：

```gdb
(gdb) print list
$2 = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
(gdb) print list[3]
$1 = 3
(gdb)
```

注意，数组索引是 C 风格的，0（零）是第一个索引值。因此，索引为 3 的元素实际上是数组的第四个元素。

在某些情况下，你可能想用 `@` 字符来模拟数组。考虑以下整数：

```c
int globInt = 5 ;
```

我们可以将此整数视为一个长度为三个元素的数组：

```gdb
(gdb) print globInt@3
$16 = {5, 5, 134514122}
```

这在处理已在堆中分配且根据 GDB 没有任何特定类型的内存时通常有用。

## 6.5.3.3 确定变量的类型

偶尔，你可能想要确定即将查看的是什么类型的变量。这在查看全局和静态变量时最有用。需要时，使用 `whatis` 命令：

```gdb
(gdb) whatis a
type = int
```

## 6.5.3.4 查看内存中的数据

如前所述，如果问题没有使用 `-g` 编译，它将不包含任何调试信息，例如变量类型信息。在这种情况下，你可能需要使用 `examine` 或 `x` 命令直接查看内存。该命令接受多个参数 —— `FMT ADDRESS`。`FMT` 是一个重复计数，后面跟着一个格式字母和一个大小字母。`ADDRESS` 指定开始显示数据的地址。以下示例将显示从 `0x08048000` 开始的 8 个 4 字节十六进制值：

```gdb
(gdb) x / 8xw 0x08048000
0x046c457f 0x00010101 0x00000000 0x00000000
0x08048010 0x00030002 0x00000001 0x08048320 0x00000034
```

GDB 构建 `x` 的输出非常有用，为了方便见，表中列出了最常用的格式代码。

| 格式描述 | 格式代码 |
|---|---|
| 1 字节 ASCII 字符 | `cb` |
| 2 字节十进制整数 | `dh` |
| 4 字节十进制整数 | `dw` |
| 1 字节十六进制数 | `xb` |
| 2 字节十六进制数 | `xh` |
| 4 字节十六进制数 | `xw` |
| 8 字节十六进制数 | `xg` |
| 字符串 | `s` |

表 6.1 GDB 格式代码。

## 6.5.3.5 格式化内存中的值

如果你在内存中有一个变量并知道它的地址，你可以使用强制类型转换以正确的格式进行打印。考虑前一个示例中定义的字符串 `constString`。这里是四种正确将此变量打印为字符串的方法。

```gdb
(gdb) print constString
$5 = 0x080485c0 "This is a constant string"
(gdb) x /s 0x080485c0
0x080485c0 <IO_std::...>: "This is a constant string"
(gdb) printf "%s", 0x080485c0
This is a constant string!
(gdb) print (char *) 0x080485c0
$6 = 0x080485c0 "This is a constant string!"
```

第一种需要包含此变量的共享库或可执行文件带有调试信息构建（使用 `-g` 编译）。如果没有这些调试信息，调试器将没有符号 `constString` 的符号。第二种方法使用 GDB 检查命令 (`x`) 配合字符串格式 (`%s`)。第三种方法使用 GDB 的 `printf` 命令配合字符串标记 (`%s`)。最后一种方法使用 GDB 中的强制类型转换功能将地址打印为特定类型。后三种方法不需要任何信息（也就是说，它们可以在没有使用 `-g` 编译的程序上运行）。
