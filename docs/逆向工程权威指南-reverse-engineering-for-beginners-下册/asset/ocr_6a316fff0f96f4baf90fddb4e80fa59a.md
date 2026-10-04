# 第49章 不正确的反汇编代码

在实际工程中，反汇编工程师们经常遇到一些不正确的反汇编
代码。我们来看看如何处理。

#  49.1 x86环境下的从一开始错误的反汇编

与opcode等长的ARM以及MIPS指令集（它们每个指令的opcode无非
就是2个字节或4个字节长度）不同，x86架构下的指令长度不尽相同。因
此，若从x86程序的中间开始解析指令，无论什么分析工具都会分析出
错误的结果。

比如如下:

```
add         [ebp-31F7Bh], cl
dec         dword ptr [ecx-3277Bh]
dec         dword ptr [ebp-2CF7Bh]
inc         dword ptr [ebx-7A7633Ch]
fdiv        st(4), st
db          0FFh
dec         dword ptr [ecx-21F7Bh]
dec         dword ptr [ecx-22373Bh]
dec         dword ptr [ecx-2276Bh]
dec         dword ptr [ecx-22B63Bh]
dec         dword ptr [ecx-22F4Bh]
dec         dword ptr [ecx-23343Bh]
jump        dword ptr [ecx-74Bh]
xchg        eax, ebp
clc
std
db          0FFh
db          0FFh
```