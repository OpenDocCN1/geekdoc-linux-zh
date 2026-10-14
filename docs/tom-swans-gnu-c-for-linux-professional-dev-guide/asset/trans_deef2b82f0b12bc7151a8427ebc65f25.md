

这就到达了类层次结构中的最低层。你可以继续发出 *next* 和 *step* 命令来进一步跟踪代码，并检查该对象初始化过程中的每个层级。但你已经探索完毕，输入一个 *continue* 命令（你可以将其缩写为 *cont*）来将程序运行到完成，然后输入 *q* 退出：

```
```text
(gdb) cont
Continuing.

(gdb) q
```
```

## INSPECTING OBJECT DATA MEMBERS

使用调试器，你可以深入查看一个对象以检查其数据成员的值。要尝试此操作，请重新加载 tlabel.cpp 程序：

```
```text
$ gdb --silent tlabel
(gdb)
```
```

如本章及前几章所述，为安全的对象拷贝提供支持是 C++ 面向对象编程中不可或缺的事实。为了检查测试程序是如何做到这一点的，在将一个对象复制到另一个对象的语句处设置断点：

```
```cpp
dest_object = test;
```
```

输入以下命令来设置断点（在我这里是在第 29 行）：

```
```text
(gdb) b 29
Breakpoint 1 at 0x80488b7: file tlabel.cpp, line 29.
```
```

接下来，运行程序直到断点。你应该在最后一条输出行看到赋值语句：

```
```text
(gdb) run
Starting program: /src/c14/tlabel
Breakpoint 1, main () at tlabel.cpp:29
29 dest_object = test;
```
```

使用 *print* 命令在赋值语句执行之前检查 *dest_object* 的数据成员：

```
```text
(gdb) print dest_object
$1 = {<TColor> = {<TCoordinate> = {tc_x = 0, tc_y = 0},
tc_color = UNKNOWN,
  static colorname = 0x8049f00, tl_label = 0x0}
```
```

调试器为 dest_object 分配了一个伪名称 $1，你可以在其他命令中使用它。在输出中，大括号根据其类层次结构对对象进行分段，但这种风格乍一看可能有点令人困惑。最内层的大括号表示 TCoordinate 部分的 tc_x 和 tc_y 数据成员被设置为零。在下一个更高层级，TColor 类的 tc_color 数据成员被设置为 UNKNOWN。最后，在 dest_object 的层级，tl_label 等于 NULL（0x0）。这种格式需要一些适应，但它不仅显示了对象的数据成员值，还显示了其类组织。

为了在为其分配另一个值后检查 0x8049f00 的值，并以此方式调查类拷贝构造函数和 operator=() 函数的完整性，发出一个 next 命令：

```
(gdb) next
30 display("Object after copy", dest_object);
```

再次打印 dest_object 的值以将其数据成员与之前列出的进行比较：

```
```text
(gdb) print dest_object
$2 = {<TColor> = {<TCoordinate> = {tc_x = 100, tc_y = 200},
tc_color = RED,
static colornames = 0x8049f00},
tl_label = 0x804a538 "Test Label"}
```

我稍微重新排列了行以适应本页。它们显示每个数据成员都已被赋予一个值。为了将这些值与源对象进行比较，你可以输入 print test（此处未显示）。

检查对象数据成员的另一种有用方法是发出 display 命令。这会让调试器在程序每次暂停时——例如在断点处或在 next 命令之后——显示一个或多个对象。如果你正在跟随操作，输入以下命令（如果你退出了，重新加载 label，在第 30 行设置断点，运行程序，并重新发出 display 命令）：

```
(gdb) display dest_object.tl_label
1: dest_object.tl_label = 0x804a538 "Test Label"
```

调试器在程序每次停止时显示对象的 tl_label 数据成员的值。要看到此效果，发出一个 next 命令：

```
(gdb) next
Object after copy
x == 100; y == 200; color = Red (1); Test Label
32 return 0;
1: dest_object.tl_label = 0x804a538 "Test Label"
```

命令行之后的输出前两行来自程序本身。最后两行来自 GNU 调试器。第 32 行显示下一个要执行的语句。最后是 tl_label 数据成员的值，显示字符串值及其在内存中的地址。顺便说一下，一些其他调试器将 display 表达式称为“监视”或“监视表达式。”

Tip
输入不带参数的 display 以查看当前所有显示的表达式列表。要清除显示列表，输入 undisplay，并在提示“Delete all auto-display expressions?”时回答 yes。

## CALLING MEMBER FUNCTIONS

在调试特定的成员函数时，调用它脱离上下文可能很有用。这在大型程序中尤其有帮助，当仅仅为了调用一个函数而逐步执行到某条语句很不方便时。

