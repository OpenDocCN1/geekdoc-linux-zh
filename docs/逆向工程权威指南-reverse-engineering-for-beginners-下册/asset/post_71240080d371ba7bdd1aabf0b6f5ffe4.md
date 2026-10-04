
```
if size eq 13
    ; jump .+D; .npad 7; .npad 4
    DB OEBH, 0BH, 0DH, 8DH, 0A4H, 24H, 00H, 00H, 00H
00H, 8DH, 64H, 24H, 00H
else
    if size eq 14
        ; jump .+E; .npad 7; .npad 5
        DB OEBH, 0CH, 0DH, 8DH, 0A4H, 24H, 00H, 00H, 00H
00H, 05H, 00H, 00H, 00H, 00H
    else
        if size eq 15
            ; jump .+F; .npad 6
            DB OEBH, 0DH, 8DH, 0A4H, 24H, 00H, 00H, 00H
00H, 8DH, 9BH, 00H, 00H, 00H, 00H
        else
            %out error: unsupported npad size
            .err
        endif
    endif
    endif
endif
endif
endif
endif
endif
endif
endif
endif
endm
```

# 第89章 修改可执行文件

## 89.1 文本字符串

除了那些经过加密存储的字符串以外，我们可以使用任何一种hex editor直接编辑C字符串。即使那些不了解机器码和可执行文件体格式的人，也可以。修改后的字符串，其长度不得大于原来字符串的长度，否则可能覆盖其他的数据。在MS-DOS盛行的时代，人们普遍使用这种方式直接用汇编转换中的外文字。在20世纪80年代和90年代的前苏联，这种技术十分流行。所以，那个时代也出现了各种灵精的超短编写：预定长度的字符串存储空间可能容纳不完整的译文，即使编译器翻译人员不够压缩译文的长度。

在修改Delphi程序的字符串时，还要调整字符串的长度。

## 89.2 x86修改指令

修改可执行文件中汇编指令的方式有以下几种：

- 禁用某些指令。此时只需要0x90 (NOP)替换相应的汇编指令即可。

- 禁用条件跳转指令。在修改74 xx (JZ)这样的条件跳转指令时，我们可以直接把跳转指令的2个字节替换为两个0x90 (NOP)，也可以把第二个字节（jump offset）替换为0，即把偏移量固定为0。

- 强制程序进行跳转。有些时候，我们需要把条件跳转替换为跳转指令，强制其进行跳转。此时，把opcode的第一个字符替换为JMP的0xEB即可。

- 禁用函数。只要把函数的第一个指令替换为RET (0xC3)，那么它就不会运行。只要程序的调用约定不是stdcall（第64章第2节），用这种修改方法就不会会有问题的。在修改stdcall约定的函数时，修改人要首先注意函数参数的数量（可以查阅函数的RET指令），然后使用带有16字节的RETN (0xC2) 指令替换函数的第一个指令。

- 某些情况下，被用的函数必须返回0或1。此时可使用“MOV EAX, 0”或“MOV EAX, 1”进行处理。直接使用这两条指令的opcode进行替换，你就会发现其opcode长度不够。这种情况下可以使用XOR EAX, EAX (0x31C0两个字符)或XOR EAX/INC EAX (0x31C00x40三个字符)进行替换。

很多软件采用了防修改的技术。这个功能通常由“读取可执行文件代码”和“校验(checksum校验)”两个步骤分步实现。也就是说，要实现修改机制，程序首先要读取（加载到内存里的）程序文件。我们可以设置断点，解析其读取内存函数的具体地址。

tracer工具可以满足这种调试需要。它具有BP（内存断点）功能。

在修改程序时，不要修改PE执行文件的relocs（参考本书的68.2.6节）。Windows的加载程序会新的代码覆盖这部分代码。如果使用Hiew打开执行程序，会发现这部分代码以灰色显示（请参考图7.12）。万不可得的时候，您可以使用跳转指令通过reloc，否则就要编辑relocs的数据表。

# 第90章 编译器内部函数

编译器内部函数 (compiler intrinsic) 是与特定编译器有关的函数，并非非常特殊的库函数。在编译库函数时，编译器会调用 (call) 这个函数；而在编译内部函数时，编译器使用对应的机器码进行直接译。内部函数通常是与特定CPU指令集相关的伪函数。

例如，C/C++语言并没有循环移位指令，许多CPU硬件支持这种指令。为了方便程序员使用这种指令，MSVC输出了相关的伪函数 _rotl() 和 _rotr()。在编译这两个函数时，编译器会直接使用x86指令集中ROL/ROR指令的opcode进行替换。

此外，为了方便程序代码调用SSE指令，MSVC还推出了一些内部函数。

如需查询所有的MSVC内部函数，请查询MSDN网站：http://msdn.microsoft.com/en-us/library/26td21ds.aspx

# 第91章 编译器短板

Intel C++编译器在Linux x86平台上 有时候生成两个连续的JZ指令。实际上第二条JZ指令不会执行、没有实际意义。

指令清单91.1

```
.text
08114CF1               loc_8114CF1: CODE XREF: __PGOSF539_kldimem+89A
.text
08114CF1                               ;__PGOSF539_kldimem+394
.text
08114CF1 8B 45 08               eax, [ebp+arg_0]
.text
08114CF4 0F 86 14   movzx edx, byte ptr [edi+14h]
.text
0811A2AF F6 C2 01   test dl, 1
.text
0811A2B2 75 3E       jnz short loc_8112F2
.text
0811A2B4 83 E0 01   and eax, 1
.text
0811A2B7 74 1F       jz short loc_811AD8
.text
0811A2B9 74 37       jz short loc_8112F2
.text
0811A2BB 6A 00       push 0
.text
0811A2BD FF 71 08   push dwordptr [ecx+8]
.text
0811A2C0 E8 5F FE FF FF call len2nbytes
```

上述文件中，另有一处这种问题。指令清单91.2 from the same code

```
.text
0811A2A5   loc_811A2A5: ; CODE XREF: kdiSerLengths+11C
.text
0811A2A5               ;kdiSerLengths+1C1
.text
0811A2A5 8B 7D 08   mov edi, [ebp+arg_0]
.text
0811A2A8 8B 7F 10   mov edi, [edi+10h]
.text
0811A2A8 AF 06 57 14   movzx edx, byte ptr [edi+14h]
.text
0811A2AF F6 C2 01   test dl, 1
.text
0811A2B2 75 3E       jnz short loc_8112F2
.text
0811A2B4 83 E0 01   and eax, 1
.text
0811A2B7 74 1F       jz short loc_811AD8
.text
0811A2B9 74 37       jz short loc_8112F2
.text
0811A2BB 6A 00       push 0
.text
0811A2BD FF 71 08   push dwordptr [ecx+8]
.text
0811A2C0 E8 5F FE FF FF call len2nbytes
```

这些问题属于编译器的bug。但是它们生成的程序将不会受到该bug的影响，所以可以被测试人员遗掉了。本书的19.2.4节、39.3节、47.7节、18.7节、12.4.1节、19.5.2节中都演示了这种问题。

本文演示了这些编译器问题，以证明编译器确实可能出现我们意想不到的奇怪行为。如果遇到了这种现象，读者就不必费尽力地去调试“编译器为什么会生成这种诡异代码”。

# 第92章 OpenMP

本章将以加密意义的非重复随机数nonce为例，演示OpenMP的应用方法。下面这段代码把nonce和未加密的明文进行串联（即添加），再进行非可逆加密，从而增加截载、破解密文的难度。此外，Bitcoin协议规定，在某个阶段通过nonce使用消息块的hash包含特定长度的、连续的零。这种机制又叫作“proof of system”（系统验证）(https://en.wikipedia.org/wiki/Proof_of_work)。虽然下面代码和没有直接关系，但是功能却是。它向字符串“hello, world!”添加一个数字，使得“hello, world!”包含三个以上的字节。假设劣质的区间为0~INT32最大数-1：

```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <time.h>
#include "sha512.h"

int found=0;
int32_t checked=0;
int32_t* __min;
int32_t* __max;
time_t start;

#ifdef GNUC
#define min(X,Y) ((X) < (Y) ? (X) : (Y))
#define max(X,Y) ((X) > (Y) ? (X) : (Y))
#endif

void check_nonce(int32_t nonce)
{
    uint8_t buf[32];
    struct sha512_ctx ctx;
    uint8_t res[64];

    // update
    int t=omp_get_thread_num();

    #pragma omp atomic
    #pragma omp critical
    if (__min[t]==-1)
        __min[t]=nonce;
    if (__max[t]==-1)
        __max[t]=nonce;

    __min[t]=min(__min[t], nonce);
    __max[t]=max(__max[t], nonce);

    // idle if valid found
    if (found)
        return;

    memset(buf, 0, sizeof(buf));
    sprintf(buf, "hello, world!%d", nonce);

    sha512_init_ctx(&ctx);
    sha512_process(buf, strlen(buf), &ctx);
    sha512_finish_ctx(&ctx, &res);
    if (res[0]==0 && res[1]==0 && res[2]==0)
    {
        printf("found (thread %d): %s seconds\nspent=%d\n", t, buf, time(NULL)-start);
        found=1;
    }
    #pragma omp atomic
    checked++;
}

int main() {
    int32_t i;
    int threads=omp_get_threads();
    printf("threads=%d\n", threads);
    
    __min=(int32_t*)malloc(threads*sizeof(int32_t));
    __max=(int32_t*)malloc(threads*sizeof(int32_t));
    for (i=0; i<threads; i++)
        __min[i]=__max[i]-1;

    start=time(NULL);

    #pragma omp parallel for
    for (i=0; i<INT32_MAX; i++)
        check_nonce(i);

    for (i=0; i<threads; i++)
        printf("__min[%d]=0x%08x max[%d]=0x%08x\n", i, __min[i], i, __max[i]);

    free(__min); free(__max);
}
```

函数check_nonce()有3个作用：向字符串加数字、使用SHA512算法计算字符串的hash、检查hash中有3个为0的字节。这段代码中较为重要的部分是

```
#pragma omp parallel for
for (i=0; i<INT32_MAX; i++)
    check_nonce(i);
```

这个程序并不复杂。如果没有#pragma，程序会从0开始穷到INT32的最大值（07ffffffff，即2147483647），依次调用check_nonce()函数验证。加上#pragma之后，编译器会添加特定的代码把整个区间划分为若干个区域，充分利用CPU的多核进行并行运算。我们可以通过上述指令，使用MSVC 2012编译：

```
cl openmp_example.c sha512.obj /openmp /O1/Zi/Faopenmp_example.asm
```

GCC对应的编译指令为:

```
gcc -fopenmp 2.c sha512.c -S -masm=intel
```

## 92.1 MSVC

MSVC 2012生成的主循环的指令如下所示。

指令清单92.1 MSVC

```
push        OFFSET  _main$s1
push        0
push        1
call        _vcomp_fork
add         esp, 16      ;00000010H
```

所有vcomp开启的函数都是与OpenMP相关的函数，通过vcomp*.dll进行加载。它将发起一组程序进行并行计算。具体来说，_main$s1的汇编代码如下:

```
$T1 = -8              ; size = 4
$T2 = -4              ; size = 4
_main$s1 PROC      ;COMDAT
push       ebp
mov        ebp, esp
push       ecx
push       ecx
push       esi
lea        eax, DWORD PTR $T2[ebp]
push       eax
lea        eax, DWORD PTR $T1[ebp]
push       eax
```
