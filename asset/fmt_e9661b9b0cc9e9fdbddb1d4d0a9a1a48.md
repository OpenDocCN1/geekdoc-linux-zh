
```
toupper PROC
MOVS    r1,r0
SUBS    r1,#0x61
CMP     r1,#0x19
BHI     |L0.14
SUBS    r0,r0,#0x20
LLS     r0,r0,#24
LRS     r0,r0,#24
|L0.14|
BX     lr
ENDP
```

## 48.2.1 ARM64的GCC

# 指令清单48.7 ARM64的非优化GCC 4

```assembly
toupper:
    sub     sp, sp,#16
    strb    w0,[rsp,15]
    ldrb    w0,96
    bls     .L2
    ldrb    w0,[rsp,15]
    cmp     w0,122
    bhi     .L2
    ret
```

```
ldrb  w0, [sp,15]
sub    w0, w0, #32
uxtb  w0, w0
b             .L3
```

```
.L2:
  ldrb  w0, [sp,15]
.L3:
  add    sp, sp, 16
  ret
```

## 清单48.8 ARM64下的优化GCC 4.9

```
toupper:
  uxtb  w0, w0
  sub    w1, w0, #97
  uxtb  w1, w1
  cmp    w1, 25
  bhi    .L2
  sub    w0, w0, #32
  uxtb  w0, w0
```

```
.L2:
  ret
```

## 48.3 总结

本章演示的优化技术已经十分常见的编译器优化技术。逆向工程分析人员会频繁遇到这种类型的汇编指令。

- [1] 然而，如果小心翼翼的话，还有一些编译器即使不优化的办法，也能输出正确的结果。

## 第49章 不正确的反汇编代码

在实际工程中，反汇编工程师们经常遇到一些不正确的反汇编代码。我们来看看如何处理。

## 49.1 x86环境下的从一开始错误的反汇编

与`opcode`等长的ARM以及MIPS指令集（它们每个指令的`opcode`无非就是2个字节或4个字节长度）不同，x86架构下的指令长度不尽相同。因此，若从x86程序的中间开始解析指令，无论什么分析工具都会分析出错误的结果。

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

```
mov    word ptr [ebp-214h], cs; <- 反汇编器终于
在这里找到了正确的轨道
mov    word ptr [ebp-238h], ds
mov    word ptr [ebp-23Ch], es
mov    word ptr [ebp-240h], fs
mov    word ptr [ebp-244h], gs
push
pop     dword ptr [ebp-210h]
mov    eax, [ebp+4]
mov    [ebp-218h], eax
lea    eax, [ebp+4]
mov    [ebp-20Ch], eax
mov    dword ptr [ebp-2D0h], 10001h
mov    eax, [eax-4]
mov    [ebp-21Ch], eax
mov    eax, [ebp+0Ch]
mov    [ebp-320h], eax
mov    eax, [ebp+10h]
mov    [ebp-31Ch], eax
mov    eax, [ebp+4]
mov    [ebp-314h], eax
call   ds:DebuggerPresent
mov    edi, eax
lea    eax, [ebp-328h]
push   eax
call   sub_047663
pop    ecx
test   eax, eax
jnz   short loc 402D7B
```

这里我们可以看到，解析出来的前几条指令毫不无理。但是后来反汇编工具逐渐上了正轨。

## 49.2 随机噪音，怎么看起来像反汇编指令？

简单来说，我们可以从以下三点来判断，一段程序是由随机代码组成的还是正常的程序段：

- 不寻常的指令集合。一般来说，x86最常见的指令是`PUSH`、`MOV`、`CALL`等。如果遇到了大类杂染式的稀有指令大排盘（浮点运算`FPU`指令、输入输出`IN/OUT`指令和很少见的一些系统指令混在一起），多数情况就是反汇编过程出了问题。
- 又大像是随机数的数值、偏移量以及即时数。
- 转移指令的偏移量不逻辑，经常跳转到其他代码块的中间。

## 指令清单49.1 x86模式下的随机数噪声

```
mov     bl, 0Ch
mov     ecx, 0D38558Dh
mov     eax, ds:2C869A86h
mov     db, 67h
mov     dl, 0Ch
insb
mov
push    eax
xor     [edx-53h], ah
fcom   qword ptr [edi-45EF72h]
pop     esp
pop     ss
in     eax, dx
dec     ebx
push    esp
lds     esp, [esi-41h]
ret
ret ptr ptr ptr [eax], cl
mov     cl, 9Ch
mov     ch, 0DFh
push    cs
insb
mov     esi, 0D9C65Dh
imul    ebp, [ecx],66h
push
sal     dword ptr [ebp-64h], cl
sub     eax,0AC3D64h
out     8Ch, eax
pop     ss
[eax], ebx
aas
jxch   cl, [ebx+4+14Eh]
jec  short near ptr_58+1
xor     al, 0Ch
inc     edx
db     36h
push    a
stosb
test    [ebx], ebx
```

pop      eax

stosb

loc_58; 代码交叉引用:0000004A

test     [esi], eax

inc      ebp

das

db       64h

pop      ecx

das

hlt

pop      edx

out      0Bh, al

push     ebx

cd

out      dx, al

sub     al, 0Ah

sti

out      d

add      dword ptr [ecx],96FCBBh

and      eax,0E3EE4h

inc      esp

stosd

push     ecx

in      al, 0CBh

mov      esi, 659185h

## 指令清单49.2 x86-64的随机噪声

```
lea      esi, [rax+4*3558D9]
loc_AF3: 代码交叉引用:000000000B6
cl      byte ptr [rsi*8+29BB], 1
lea      ecx, cs:FFFFFA67F
mov      al, 96h
mov      ah, CE0
push          rsp
                ptr
esi
db       2Fh
pop      rsp
db       64h
ret     0E93h
```

cmp      ah, [rax+4Ah]

movzx   rsi, dword ptr [rbp-25h]

push     4Ah

movzx   rdi, dword ptr [rdi+8*8]
