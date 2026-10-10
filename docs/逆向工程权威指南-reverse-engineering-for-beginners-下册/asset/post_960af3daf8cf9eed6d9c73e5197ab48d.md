
```assembly
029FC14   00E0103A   RETURN to fib2.00E103A from fib2.00E100
029FC18   00000008   1st argument: a
029FC1C   0000000D   2nd argument: b
029FC20   00000014   3rd argument: limit
029FC24   0000000D   "next" variable
029FC28   029F2C8   saved EBP register
029FC2C   00E0103A   RETURN to fib2.00E103A from fib2.00E100
029FC30   00000005   1st argument: a
029FC34   00000008   2nd argument: b
029FC38   00000014   3rd argument: limit
029FC3C   00000008   "next" variable
029FC40   029F2C8   saved EBP register
029FC44   00E0103A   RETURN to fib2.00E103A from fib2.00E100
029FC48   00000003   1st argument: a
029FC4C   00000005   2nd argument: b
029FC50   00000014   3rd argument: limit
029FC54   00000005   "next" variable
029FC58   029F2C0   saved EBP register
029FC5C   00E0103A   RETURN to fib2.00E103A from fib2.00E100
029FC60   00000002   1st argument: a
029FC64   00000003   2nd argument: b
029FC68   00000014   3rd argument: limit
029FC6C   00000003   "next" variable
029FC70   029F2C8   saved EBP register
029FC74   00E0103A   RETURN to fib2.00E103A from fib2.00E100
029FC78   00000001   1st argument: a
029FC7C   00000002   2nd argument: b             | prepared in fib() for next fib()
029FC80   00000014   3rd argument: limit
029FC84   00000002   "next" variable
029FC88   029F2C8   saved EBP register
029FC8C   00E0106C   RETURN to fib2.00E106C from fib2.00E100
029FC90   00000001   1st argument: a
029FC94   00000001   2nd argument: b             | prepared in main() for fib()
029FC98   00000014   3rd argument: limit
029FC9C   029F2E00   saved EBP register
029FCA0   00E011E0   RETURN to fib2.00E110 from fib2.00E100
029FCA4   00000001   main() 1st argument: argc
029FCA8   000812C8   main() 2nd argument: argc | prepared in CRT for main()
029FCAC   00082940   main() 3rd argument: envp
```

这里我们看到：递归函数在每次调用期间都会计算并传递下一个调用所需的函数参数。

## 36.3 总结

递归函数看起来很方便而已。从技术上讲，递归函数在栈方面的开销过大，因性能不怎么理想。注重性能的应用程序，应当避免递归函数。

笔者曾经尝试写过一个递归二叉树、搜索特定结点的应用程序。把它写成递归函数的时候，整个程序确实清爽又有条理性。但是每次函数调用都要进行赋值、回调，这使得递归函数比其他类型的函数慢了许多倍。

另外，部分PL[3]编译器对递归调用采取“尾部调用”的优化方法，以减轻堆栈的各种开销。

- [1] 在OllyDB中，可以选择多项指令，再使用Ctrl+C组合键把它们复制到剪贴板。本例就是这样的。
- [2] 也就是自己调用自己。
- [3] PL: Program Language (编程语言)。LISP、Python、Lua等语言能够进行尾调用。详情参阅https://en.wikipedia.org/Tail_call。

## 第37章 CRC32计算的例子

本章介绍一个基于查询实现的CRC32校验程序：

```c
/* By Bob Jenkins, 2006, Public Domain */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef unsigned long ub4;
unsigned char ub1;

static const ub4 crctab[256] = {
    0x00000000, 0x77703096, 0xee0e612c, 0x990951ba, 0x07dc4190, 0x706a4f8f, 0xe963a535, 0x9e6495a0,
    0xedbb3a4, 0x97d64c8, 0xeb7b2d07, 0x90bf1d91, 0x1405c4f, 0x663d6d, 0x0fa0f3d6, 0x0x8d80df5,
    0x73b52c, 0x4c69105, 0xd56041e, 0xa2677172, 0x3c03e4d1, 0xd20d85fd, 0xa50ab56b, 0x355a8fa,
    0xa2298bc, 0xbbbc9c, 0xacb940, 0x32d86ce, 0x45dfc75, 0xdcd60cf, 0xabd1d359, 0x26930ac,
    0x51de003a, 0xc875180, 0xbbfd066, 0x21b4f45, 0x56b3c42, 0xcfba959, 0xb8bda50f, 0x2802b9e,
    0xf5f5808, 0xc60cd9b2, 0xb10e92e, 0xf2f67c7, 0x5864c11, 0xc1611dab, 0xb6662d3d, 0x76dc4190,
    0x01db7106, 0x98d22bc, 0xedf5102a, 0x71b18589, 0x06b6b51f, 0xf9fe4a5, 0xe8b8d433, 0x78079a2,
    0x00f0934, 0x9609a88e, 0xe10e918, 0x7f6a0dbb, 0x0863d2d2, 0x9164977, 0x6635011, 0x66b6b514,
    0xc1c6c612, 0x856530d8, 0x2f6200a4, 0x6c0695ed, 0x01b0a57b, 0x8208f4c1, 0xf50fc457, 0x65b0d9c6,
    0x12b7e950, 0x88beaea, 0xfc988b7, 0x62dd1ddf, 0x15da2449, 0x8cd37cf3, 0xf8bd4c65, 0x04b26158,
    0x33ab551e, 0xa3bc0074, 0xd4db30e2, 0x4adfa541, 0x03d8d957, 0x04ad1d6c, 0xd3d6f4b8, 0x4369e9a6,
    0x346ed9fc, 0xad678846, 0xda6b8b0, 0x4404273, 0x33031de, 0xaa0a4c, 0xd0d0cc9, 0x5005731,
    0x702721a4, 0xebe0110, 0xc9c208, 0x5768b52, 0xe26f853, 0xb966d40, 0xe6c4f9, 0x05def90,
    0x299c98, 0xb0d982, 0xc7d7a84, 0x59b33d7, 0xeb4b04, 0x7f8b7c, 0xc0ba6c4, 0xd288b2,
    0x693d20, 0x5a7314, 0x0b61e2, 0x0d3b6e, 0x7f47d2, 0x9ead5743, 0x99d277a, 0x04db261,
    0x7333113, 0xe363012, 0xe440f08, 0xa9464b3,, 00066a3,,00000000,000000000,000000000,,