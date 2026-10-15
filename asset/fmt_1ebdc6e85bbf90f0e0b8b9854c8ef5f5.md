
如果你想修改运行程序空间中的值，可以使用 `set` 命令。`set` 接受许多不同的参数，但与大多数 gdb 命令一样，它接受任何有效的 C 表达式作为参数。由于 gdb 灵活的语法，你可以使用任何允许 C 表达式作为参数的命令来设置变量，而不仅仅是 `set` 命令。在配合赋值表达式使用 `set` 是很容易记住的。

### 10.3.3.4 关于 C++ 和模板的一些说明

C++ 模板带来了独特的调试挑战。模板允许程序员以一种通用的方式定义代码，使得编译器可以从更抽象的规范生成源代码。考虑下面这个简单的例子，它用于用于交换两个值：

```cpp
template <class Typ>
void swapvals( Typ &a, Typ &b)
{
    Typ tmp = a;
    a = b;
    b = tmp;
}
```

标记 `Typ` 是类型名称的占位符。在你的源代码中定义此模板在在使用它之前，它不会生成任何代码。当你使用它时，你必须指定一个替代 `Typ` 的类型。这被称为*实例化*。要创建一个交换两个 `double` 的函数，你可以如下调用它：

```cpp
swapvals<double>(a,b);
```

这会导致编译器创建一个专门与 `double` 工作的 `swapvals` 函数。如果你需要交换两个 `int` 类型的变量，可以使用 `swapvals<int,int>`，这会导致编译器生成一个具有唯一函数签名的完全不同的函数。由于模板定义了一整族函数，在由模板定义的函数上设置断点需要一些技巧。首先使用 gdb 的 `info functions` 命令查找该函数：

```
(gdb) info func swapvals
All functions matching regular expression "swapvals":
```

```
File temp.cpp:
void swapvals<Foo>(Foo, Foo&);
void swapvals<double>(double, double);
void swapvals<int>(int, int&);
```

由于某种原因，gdb 6.3 打印了两次 'void'。请注意，对于每个类型都有一个唯一的函数。没有一个命令可以同时在此模板生成的所有函数上设置断点。为了一次只对这些函数中的某一个设置断点，你可以对 `int` 版本设置断点，可以从引号开始并使用展开：

```
(gdb) b 'void swapvals<Foo>'
(gdb) b 'void swapvals<double>'
(gdb) b 'void swapvals<int>(int&, int&)'
Breakpoint 3 at 0x0804434: temp.cpp, line 8
```

最接近在匹配模板的所有函数上设置断点的命令是 `rbreak` 命令。例如：

```
(gdb) rbreak swapvals
Breakpoint 2 at 0x0804456: temp.cpp, line 8
void swapvals<Foo>(Foo, Foo);
Breakpoint 3 at 0x0804800: temp.cpp, line 8
void swapvals<double>(double, double);
Breakpoint 4 at 0x0804434: temp.cpp, line 8
void swapvals<int>(int&, int&);
```

这是在匹配模板的所有函数上设置断点最接近的方法。

（注：由于原文后续部分出现大量重复和乱码，此处根据您提供的文本内容进行结构性翻译。原文从 "The closest to setting..." 之后出现了大量逻辑混乱的重复句子和乱码，翻译已按原文呈现结构进行处理。）

`token` 是一个四字符字符串，程序使用 C++ 算法 `std::next_permutation` 对其进行排列。组合数学原理规定，该字符串有四阶乘（4!）种排列方式。我们在第 13 行设置了一个断点，以便你可以通过 `display` 命令查看它的执行情况：

```
Breakpoint 2, main (argc=1, argv=0xbffcela4) at permute.cpp:13
13
  i++;
(gdb) display/xw token.c_str (
1: x/w token.c_str () 0x0804a014:      0x44432421
(gdb) display/s token.c_str (
2: x/s token.c_str () 0x0804a014:      "ABCD"
(gdb) cont
Continuing.
```

以长整数格式显示字符。

以 ASCII 格式显示相同的内容。

```
Breakpoint 2, main (argc=1, argv=0xbffcela4) at permute.cpp:13
13
  i++;
2: x/s token.c_str () 0x0804a014:      "ABCD"
1: x/w token.c_str () 0x0804a014:      0x44432421
(gdb)
Continuing.
```

不需要重新输入 "cont"。

```
Breakpoint 2, main (argc=1, argv=0xbffcela4) at permute.cpp:13
13
  i++;
2: x/s token.c_str () 0x0804a014:      "ABCD"
1: x/w token.c_str () 0x0804a014:      0x44423431
```

```
etc...
nBreakpoint 2, main (argc=1, argv=0xbffcela4) at permute.cpp:13
13
  i++;
2: x/s token.c_str () 0x0804a014:      "DCBA"
1: x/w token.c_str () 0x0804a014:      0x41423434
(gdb)
Continuing.
24 permutations
```

最后的排列。

4阶乘 = 24

你创建了两个 `display` 命令，gdb 将它们标记为 1 和 2 以供参考。程序每次停止，两个表达式都会被求值。在这种情况下，gdb 为每个显示调用一次 `std::string` 的 `c_str` 方法。你可以随时停止这些显示。要停止此示例中的 ASCII 字符串显示，你可以输入 `undisplay` 来移除显示 2。

- 对于数学较薄的人的人：N! = N * (N-1) * (N-2) ... * 2，所以 4! = 4 * 3 * 2 = 24。

## 10.3 熟悉 GNU 调试器 gdb

### 10.3.4 使用 gdb 附加到运行中的进程

从命令行中，你可以使用以下语法用 gdb 附加到正在运行的进程：

```
$ gdb programme pid
```

`pid` 是你想要附加的进程的进程 ID，`programme` 是可执行文件的文件名。为了使调试会话有效，这两者必须匹配。如果你尝试对一个自进程启动后已重新编译的可执行文件操作，无法保证你得到的结果是否有任何意义。

如果你想调试不同的进程，不需要退出 gdb 或终止当前正在运行的进程。你可以使用 `detach` 命令停止调试并让进程继续。这会在终止调试会话而不终止你的进程。当 gdb 分离后，你可以使用 `attach` 命令更改程序并调试不同的进程。如有必要，你可以使用 `file` 命令启动与新进程匹配的可执行文件。

你可以使用这些命令作为你在在本节之前之前方式启动 gdb 的替代方案：

```
(gdb)file programme
(gdb)attach pid
```
