
```
add esp, 8
mov ecx, eax
cmp edx, esi
jl SHORT LL3@form_netma
$LN9@form_netma:
    pop esi
    mov eax, ecx
    pop ebx
    ret
form_netmask ENDP
```

set_bit()函数的功能十分单一。它将输入值左移既定的比特，接着将位移运算的结果与输入值进行或OR运算。而在form_mask()函数通过循环语句重复调用set_bit()函数，帮助循环控制变量netmask_bits设置子掩码数值为1的各个比特位。

## 38.5 总结

上述程序的结果如下：

```
netmask=255.255.255.0
network address=10.1.2.0
netmask=255.0.0.0
network address=10.0.0.0
netmask=255.255.255.128
network address=10.1.2.0
netmask=255.255.255.192
network address=10.1.2.64
```

- [1] CIDR是Classless Inter-Domain Routing的缩写，即无类域间路由
- [2] 可用地址数字空间-2。

## 第39章 循环：几个迭代

多数循环语句只有有一个迭代器。但是在汇编层面，一个迭代器可能对应多个数据实体。

下面所示的是一个简单的例子。

```c
#include <stdio.h>

void f(int *al, int *a2, size_t cnt)
{
    size_t i;

    // copy from one array to another in some weird scheme
    for (i=0; i<cnt; i++)
        al[i*3]=a2[i*7];
}
```

我们可以看到，每次迭代都有两次乘法运算，是很耗费时间的操作。不能优化一下呢？答案是肯定的。如果仔细看程序代码，就会发现这个程序的矩阵的参数是跳跃的，我们可以比较容易地不用乘法就把它计算出来。

### 39.1 三个迭代器

指令序列39.1 采用MSVC 2013 x64优化的代码

```assembly
f               PROC
    ; RDX=al
    ; RCX=a2
    ; R8=cnt

    test    r8, r8      ; cnt==0? exit then
je SHORT $LN1@f
pad 11

$LL3@f:
mov eax, DWORD PTR [rdx]
lea rcx, QWORD PTR [rcx+12]
lea rdx, QWORD PTR [rdx+28]
mov DWORD PTR [rcx-12], eax
dec r8
jne SHORT $LL3@f

$LN1@f:
ret 0
ENDP
```

这里有三个迭代变量，它们是cnt变量和两个序列参数（索引下标）。序列参数每次迭代都增加12或者28（其实就是采用加法替换源程序中的乘法）。因此我们可以采用C/C++语言写代码如下：

```c
#include <stdio.h>

void f(int *al, int *a2, size_t cnt)
{
    size_t i;
    size_t idx1=0; idx2=0;

    // copy from one array to another in some weird scheme
    for (i=0; i<cnt; i++)
    {
        al[idx1]=a2[idx2];
        idx1+=3;
        idx2+=7;
    }
}
```

这个程序在每次迭代更新3个迭代参数，而不是1个。另外，编译器实现了两个乘法操作。

### 39.2 两个迭代器

GCC 4.9可以做得更好，只有两个参数。

指令清单39.2 采用GCC 4.9 x64优化

```assembly
; RDI=al
; RSI=a2
; RDX=cnt
f:
    test rdx, rdx ; cnt=0? exit then
    je .L1
    ; calculate last element address in "a2" and leave it in RDX
    lea rax, [0+rdx*4]
    ; RAX=RDX*cnt*4
    sal rdx, 5
    ; RDX<<5=cnt*32
    sub rdx, rax
    ; RDX-RAX=cnt*32-cnt*4=cnt*28
    add rsi
    ; RDX+RSI=a2+cnt*28
.L3:
    mov eax, DWORD PTR [rsi]
    add esi, 28
    add rdi, 12
    mov DWORD PTR [rdi-12], eax
    cmp rsi, rdx
    jne .L3

.L1:
rep ret
```

这里没有计数器变量counter了，是因为GCC编译器认为它没有必要。a2的最后一个参数在循环开始前就已经计算好了（很容易，其实就是cnt乘以7）。而且循环的结束条件也不复复杂：第二个索引指针达到那个预先计算出来的临界值时，循环就会随之终止即可。

其中涉及一些特殊的加/减/位移等算法代替乘法运算的知识，感兴趣的读者可以参本书第16.1节。

上述汇编代码与述C/C++程序对应：

```c
#include <stdio.h>

void f(int *al, int *a2, size_t cnt)
{
    size_t i;
    size_t idx1=0; idx2=0;
    size_t last_idx2=cnt*7;

    // copy from one array to another in some weird scheme
    for (;);
    {
        al[idx1]=a2[idx2];
        idx1+=3;
        idx2+=7;
        if (idx2==last_idx2)
           break;
    }
}
```

ARM64下的GCC(Linaro) 4.9采用了不同的编译方法。它是计算的数组a1的最后一个索引值，而不是像上面的程序那样数组a2为边界条件。当然，程序的功能最终还是一样的。

## 指令清单39.3 ARM64下的GCC(Linaro) 4.9

```assembly
X0=al
X1=a2
X2=cnt
f:
   cbz x2, .L1      ; cnt==0? exit then
   ; calculate last element of "a1" array
   add x3, x0, x2, LSL #2  ; x3=a1+cnt*4
   lsl x4, x2, #5         ; x4=cnt*32
   sub x4, x4, x3         ; x4=cnt*32-cnt*4=cnt*28
   add x1, x1, x4         ; x1=a2+cnt*28
.L3:
   ldr w0, [x1], #4      ; load 32-bit word from a2 (post-increment)
   str w0, [x0], #12     ; store 32-bit word at a1+12
   add x0, x0, #12       ; a1=a1+12
   bne.ne .L3
.L1:
   ret
```

MIPS下的GCC 4.5差异如此。

## 指令清单39.4 MIPS(IDA)下的GCC 4.5

```assembly
$a0=al
$a1=a2
$a2=cnt
f:
   beq $a2, $zero, loc_24  ; cnt==0? exit then
   ; initialize counter (i) at 0
   move $t0, $zero
loc_8:
   ; load 32-bit word from a2
   lw $t1, 0($a1)
   ; increment counter (i)
   addi $t0, $t0, 1
   ; check for i < cnt
   slt $t2, $t0, $a2
   bne $t2, loc_8
   ; store 32-bit word at a0
   sw $t1, 0($a0)
   ; update pointers
   addi $a0, $a0, 12
   addi $a1, $a1, 4
loc_24:
   jr $ra
```

## 39.3 Intel C++ 2011 实例

编译器的优化有时非常奇怪。但是无论它们采用了什么方式，程序的功能必须忠于源程序。

指令清单39.5 Intel C++ 2011 (x64) 优化

```assembly
f PROC
    ; RDX=al
    ; RCX=a2
    ; R8=cnt
B1.0:
    test r8, r8      ; cnt==0? exit then
    jz loc_24
B1.1:
    mov r10, r8
    mov r9, rcx
    shl r10, 4
    lea rax, QWORD PTR [r8*4]
    sub r9, rdx
    sub r10, rax
    cmp r9, r10
    jge just_copy2
B1.2:
    cmp r8, 6
    jbe just_copy
B1.3:
    cmp rcx, rdx
    jbe .B1.5
B1.4:
    mov r10, r8
    mov r9, rcx
    shl r10, 4
    ... (rest of logic follows similar logic)
B1.5:
    cmp rdx, rcx
    jbe just_copy
B1.6:
    mov r9, rdx
    lea rax, QWORD PTR [r8*8]
    sub r9, rcx
    lea r10, QWORD PTR [rax+r8*4]
```

## 40章 达夫装置

达夫装置(Duff's Device)是一种综合了多种语句的循环展开技术，可大幅度地减少代码的分支总数。这种循环展开巧妙地利用了switch语句的滑梯(fallthrough)效果。
