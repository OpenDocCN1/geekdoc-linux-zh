
`cd`

```
(gdb) printf "%x\n", (unsigned char) tmpPtr[2]
```

`ab`

```
(gdb) printf "%x\n", (unsigned char) tmpPtr[3]
```

`89`

```
(gdb) printf "%x\n", (unsigned char) tmpPtr[4]
```

`67`

```
(gdb) printf "%x\n", (unsigned char) tmpPtr[5]
```

`45`

```
(gdb) printf "%x\n", (unsigned char) tmpPtr[6]
```

`23`

```
(gdb) printf "%x\n", (unsigned char) tmpPtr[7]
```

`1`

在 GDB 会话中，我们通过 `set tmpPtr = &i64` 将字符指针设置为 64 位变量的地址。由于该指针是字符指针，我们可以将其作为字符数组来查找 64 位值 `i64` 的每个字节。字符数组的每个索引（例如 `tmpPtr[3]`）都按顺序显示 64 位值在内存中存储的另一个字节。从此处的 GDB 输出可以发现，64 位值 `0x0123456789abcdef` 实际上在内存中被存储为 `0xefcdab9786543210`。换句话说，字节序完全反转了。

> 注意：只有在查看大小为字（words）或更多字节的数据时，才需要进行字节反转。单个字节总是按照预期显示。

## 6.10 与 C++ 协作

C++ 是 C 的超集，包含了许多新概念，例如带有构造函数和析构函数的类、内联函数和异常。虽然完整列表超出了本章的范围，但我们将概述其中的一些区别以及如何在 GDB 中处理这些差异。

### 6.10.1 全局构造函数和析构函数

有几种方法处理全局构造函数和析构函数。构造函数作为对象初始化的一部分运行。这可能在 `main()` 函数被调用之前发生。析构函数在对象销毁时运行，这可能发生在 `main()` 函数退出之后。如果你知道构造函数或析构函数的名称，可以在它们中设置断点。但如果你不知道可执行文件或库具有哪些构造函数或析构函数呢？

有一组相对简单的步骤可以寻找全局构造函数和析构函数。下面的示例展示了这些步骤。考虑一个拥有类并定义了该类的全局对象的简单程序。例如，以下代码片段：

```cpp
#include <stdio.h>

class myClass {
    int myVar;
    myClass() {
        myVar = 5;
    }
};

myClass myObj;
```

对象 `myObj` 被实例化时，构造函数将执行该对象的任何初始化。现在我们假设不知道该对象，将在 GDB 中寻找它。第一步是反汇编 `init` 函数。该函数在库加载或程序首次执行时运行。

```
(gdb) disassemble _init
Dump of assembler code for function _init:
0x08048300 <init> push %ebp
0x08048301 <init+1> mov %esp,%ebp
0x08048303 <init+3> sub $0x8,%esp
0x08048306 <init+6> call 0x08043b4<call_start>
0x0804830b <init+9> nop
0x0804830c <init+12> call 0x08043f0<call_frame>
0x08048311 <init+17> call 0x0804550<_do_global_aux>
0x08048316 <init+22> leave
0x08048317 <init+23> ret
```

在我们的反汇代码中，可以清楚地看到调用了 `do_global_aux`。现在反汇编该函数：

```
(gdb) disassemble do_global_aux
Dump of assembler code for function do_global_aux:
0x08048550 <do_global_aux> push %ebp
0x08048551 <do_global_aux+1> mov %esp,%ebp
0x08048553 <do_global_aux+3> push $0x8
0x08048554 <do_global_aux+4> push $0x8
0x08048555 <do_global_aux+5> mov 0x0497fc,%eax
0x0804855a <do_global_aux+10> cmp $0xffffff,%eax
0x0804855d <do_global_aux+13> mov 0x0497fc,%ebx
0x08048562 <do_global_aux+18> je 0x080457c<_do_global_aux+44>
0x08048564 <do_global_aux+20> lea 0x00(%esi),esi
0x0804856a <do_global_aux+26> lea 0x00(%edi),edi
0x08048570 <do_global_aux+32> sub $0x4,%eax
0x08048573 <do_global_aux+35> call *%eax
0x08048575 <do_global_aux+37> mov (%ebx),eax
0x08048577 <do_global_aux+39> cmp $0xffffffff,%eax
0x0804857a <do_global_aux+42> jne *%eax
0x0804857c <do_global_aux+44> pop %eax
0x0804857d <do_global_aux+45> pop %ebx
0x0804857e <do_global_aux+46> pop %ebp
0x0804857f <do_global_aux+47> ret
End of assembler dump.
```

之前的反汇列表显示了 `call *%eax`。它获取 EAX 寄存器的值，将其视为地址，解引用该地址并调用存储在该地址的函数。从上面的代码可以看到 EAX 被通过 `mov 0x80497fc,%eax` 设置。让我们看看该地址的内容：

```
(gdb) x/40x 0x080497fc
0x080497fc <_CTOR_LIST_+4>: 0x084851e 0x00000000 0xffffffff 0x00000000
0x080480c <JCR_LIST_>: 0x00000000 0x08049718 0x00000000 0x00000000
0x080481c <GLOBAL_OFFSET_TABLE_+12>: 0x0804832e 0x0804833e 0x0804834e 0x00000000
0x080482c <completed.1>: 0x00000000 0x00000000 0x00000000
0x080483c Cannot access memory at address 0x080483c
```

该地址比名为 `_CTOR_LIST_` 的变量多四个字节（我们从文中得知是 `_CTOR_LIST_+4`）。在该地址有一个值 `0x084851e`，根据之前的反汇代码，这是在解引用 EAX 后被调用的值。让我们看看该地址的内容：

```
(gdb) dis 0x0804851e
dump of assembler code for GLOBAL_I_Myobj2:
0x0804851e <GLOBAL_I_Myobj2+0> pop %ebp
0x0804851f <GLOBAL_I_Myobj2+1> mov %esp,%ebp
0x08048521 <GLOBAL_I_Myobj2+3> sub $0x8,%esp
0x08048524 <GLOBAL_I_Myobj2+6> sub $0x8,%esp
0x08048527 <GLOBAL_I_Myobj2+9> push $0xfff
0x0804852c <GLOBAL_I_Myobj2+14> push $0x1
0x0804852e <GLOBAL_I_Myobj2+16> call 0x08044d8<static_initialization_and_destruction_0>
0x08048533 <GLOBAL_I_Myobj2+21> leave
0x08048536 <GLOBAL_I_Myobj2+24> add $0x10,%esp
0x08048537 <GLOBAL_I_Myobj2+25> ret
End of assembler dump.
```

这是我们在之前的源代码中看到的对象的全局构造函数。`_CTOR_LIST_` 变量存储了全局构造函数的列表

## 6.10 与 C++一起

对于可执行文件或共享库，我们使用 GDB 中的 `info variables` 命令来查找所有的全局构造列表：

```
(gdb) info variables __CTOR_LIST_
```
