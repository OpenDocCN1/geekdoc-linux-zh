
`loc_8:`                               # CODE XREF:
`my_memcpy+1C`
`; 将地址 $t0 处的无符号加载到 $v1：`
```
    lbu $v1, 0($t0)
```
`; 增加计数器 (i):`
```
    addiu $v0, $1
```
`; 将字节存储到 $a3`
```
    sb $v1, 0($a3)
```

```assembly
loc_14:                               # CODE XREF: my_memcpy
; 检查 $v0 中的计数器 (i) 是否仍小于第三个函数参数
("cnt" 在 $a2):
    sltu $v1, $v0, $a2
; 构造源块中字节的地址：
    addiu $t0, $a1, $v0
; $t0 = $a1+$v0 ; src+
; 如果仍小于“cnt”则跳转到循环体
    bnez $v1, loc_8
; 构造目标块中字节的地址 ($a3 = \$a0+\$v0 =
    addiu $a3, $a0, $v0 ; branch delay slot
; 如果触发 BNEZ 则结束：
    jr $ra
    nop $at, zero ; branch delay slot, GOP
```

这里介绍的两个指针寄存器分别是`LBU (Load Byte Unsigned)`和`SB (Store Byte)`。在两个平台上，所有的MIPS寄存器都是32位寄存器。在两个平台上，我们无法像x86那样对寄存器的低位进行操作。因此在处理单字节字符操作时，我们都是访问整个32位寄存器。`LB`指令加载带符号的数据并清除寄存器的其他位。由于有符号位的问题，所以在处理有符号的数据的时候通常要使用`LB (Load Byte)`指令把单字节的有符号数据扩展为等值的32位数据、再存储在寄存器中。`SB`指令的作用是把寄存器的低8位数据存储到内存里。

## 14.2 量化技术

- 25.1.2节详细介绍GCC的优化编译方式基于量化技术(Vectorization)的。

## 14.3 总结

当循环变量从2增到9时，循环语句对应的汇编代码如下：

指令清单14.15 x86

```assembly
mov [counter], 2 ; 初始化
jmp check
body:
  ; 循环体
  ; 执行某些操作
  ; 在本地栈中使用计数器
  add [counter], 1 ; 增
check:
  cmp [counter], 9
  jne body
```

如果没有开启编译器的优化功能，那么循环变量的增操作可能对应3条汇编指令。

指令清单14.16 x86

```assembly
MOV [counter], 2 ; 初始化
JMP check
body:
  ; 循环体
  ; 执行某些操作
  ; 在本地栈中使用计数器
  MOV REG, [counter] ; 增
  INC REG
  MOV [counter], REG
check:
  CMP [counter], 9
  JLE body
```

当循环体短时，编译器可能给循环变量分配用的寄存器。

指令清单14.17 x86

```assembly
MOV EBX, 2 ; 初始化
JMP check
body:
  ; 循环体
  ; 执行某些操作
  ; 在 EBX 中计数计数，但不修改它
  INC EBX ; 增
check:
  CMP EBX, 9
  JLE body
```

编译器还可能调部分的顺序。

指令清单14.18 x86

```assembly
MOV [counter], 2 ; 初始化
JMP label_check
label_increment:
ADD [counter], 1 ; 增
label_check:
CMP [counter], 10
JGE exit
; 循环体
  ; 执行某些操作
  ; 在本地栈中使用计数器
JMP label_increment
```

通常情况下，程序应当判断循环条件是否满足，但是在编译器优化的情况下，它可能会交换循环体和判断语句的顺序。下面这个就是一个典型的例子。

指令清单14.19 x86

```assembly
MOV REG, 2 ; 初始化
body:
  ; 循环体
  ; 执行某些操作
  ; 在 REG 中计数计数，但不修改它
  INC REG; 增
  CMP REG, 10
JL body
```

编译器不会使用`LOOP`指令。如果某代码带有`LOOP`指令，那么应当认为它是手写的汇编程序。

指令清单14.20 x86

```assembly
; 从10数到1
MOV ECX, 10
body:
  ; 循环体
  ; 执行某些操作
  ; 在 ECX 中计数计数，但不修改它!
LOOP body
```

ARM平台的R4寄存器专门存储循环变量。

指令清单14.21 ARM

```assembly
MOV R4, 2 ; 初始化
B check
body:
```
```assembly
; 循环体
  ; 执行某些操作
  ; 在 R4 中计数计数，但不修改它!
ADD R4,R4, #1; 增
check:
CMP R4, #10
BLT body
```

## 14.4 练习题

### 14.4.1 题目：现在的编译器不再使用LOOP指令了？

### 14.4.2 题目：使用熟悉的操作系统和编译器14.1节的样本程序，然后修改它的程序，使循环变量从6增加20。

### 14.4.3 题目：描述代码的功能。

### 14.4.4 题目：描述下面代码的功能：

```
bne $s0, $s1, loc_30
or $at, $zero
llw $ra, 0x28+var_4($sp)
llw $s2, 0x28+var_8_C($sp)
llw $s1, 0x28+var_C($sp)
llw $s0, 0x28+var_10($sp)
jr $ra
addiu $sp, 0x28
LCO:    .ascii  "%s\n"<0>      # 数据交叉引用: main+20
```

请参阅 Dre07，以及 Int14 第 3.4.1.7 节。

[2] 如果您感兴趣，可以到作者的网站上下载。
`http://yurichev.com/tracer-en.html`。

# 第15章 C语言字符串函数

## 15.1 strlen()

本章介绍循环控制语句的具体应用。通常，`strlen` 函数通过 `while()` 循环语句实现。参照 MSVC 标准库对 `strlen()` 函数的定义，我们讨论上述程序：

```
int my_strlen (const char * str)
{
    const char *eos = str;
    while(*eos++ );
    return(eos - str - 1);
}
```

```
int main()
{
    // test
    return my_strlen("hello!");
}
```

### 15.1.1 x86

使用 MSVC 2010 编译上述程序可得到：

```
_eos = -4          ; size = 4
_str$ = 8          ; size = 4
_strlen PROC
    push    ebp
    mov     ebp, esp
    push    ecx
    mov     eax, DWORD PTR _str$[ebp]; 将指针指向字符串
mov    DWORD PTR $eos[ebp], eax; 指向局部变量 eos
$LN2_strlen:
mov    ecx, DWORD PTR $eos[ebp]; ECX=eos
ret
    ; 从 ECX 中的地址读取 8 位字节，并将其作为符号扩展的
    ; 32 位值存入 EDX
movsx   edx, BYTE PTR [ecx]
mov    eax, DWORD PTR $eos[ebp]; EAX=eos
add    eax, 1; ; ECX++
mov    DWORD PTR $eos[ebp], eax; EAX 还原为
test   edx, edx
je     SHORT $LN1_strlen; ; EDX == 0 ? 如果是，则结束循环
jmp    SHORT $LN2_strlen; ; 继续循环
$LN1_strlen:
    ; 计算两个指针之间的差
mov    eax, DWORD PTR $eos[ebp]
sub    eax, DWORD PTR _str[ebp]
sub    eax, 1; ; 减 1 并返回结果
mov    esp, ebp
pop    ebp
xor    edx, edx
$strlen_
```
