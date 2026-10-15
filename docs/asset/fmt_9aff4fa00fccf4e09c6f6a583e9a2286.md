
```asm
MOVS        R0,#8

STR         R0, [SP,#0x64+var_54]

MOVS        R0,#0A

STR         R0, [SP,#0x64+var_50]

MOVS R0, #0xC

STR R0, [SP,#0x64+var_4C]

MOVS R0, #0xE

STR R0, [SP,#0x64+var_48]

MOVS R0, #0x10

STR R0, [SP,#0x64+var_44]

MOVS R0, #0x12

STR R0, [SP,#0x64+var_40]

MOVS R0, #0x14

STR R0, [SP,#0x64+var_3C]

MOVS R0, #0x16

STR R0, [SP,#0x64+var_38]

MOVS R0, #0x18

STR R0, [SP,#0x64+var_34]

MOVS R0, #0x10

STR R0, [SP,#0x64+var_30]

MOVS R0, #0x1C

STR R0, [SP,#0x64+var_2C]

MOVS R0, #0x1E

STR R0, [SP,#0x64+var_28]

MOVS R0, #0x20

STR R0, [SP,#0x64+var_24]

MOVS R0, #0x22

STR R0, [SP,#0x64+var_20]

MOVS R0, #0x24

STR R0, [SP,#0x64+var_1C]

MOVS R0, #0x26

STR R0, [SP,#0x64+var_18]

MOV R0, 0xFDA ;"a[%d]=d"

MOV R5, SP

DS R6, #4

ADD R4, PC

B loc_2FC

; second loop

loc_2F4

ADDS R0, R5, #1

LDR.W R2, [R6, R5, LSL#2]

MOV R5, R0

loc_2FC

MOV R0, R4

MOV R1, R5

BLX _printf

CMP R5, #0x13

BNE loc_2F4

LDR.W R0, [R8]

LDR R1, [SP,#0x64+canary]

CMP R0, R1

ITTT

MOVEQ R0, #0

ADDEQ SP, SP,#0x54
```

## 18.5.6 数组溢出

本例参数的取值是0~11。如果输入值为12，会发生什么？虽然查询里没有对应的值，但是程序还是会计算地址。如果其他函数访问这种越界地址，那么在读取字符串时可能会溢出崩溃。

输入值为12会发生什么情况？程序将返回数据组首地址之后的第13个元素。我们一起来看看CPU是如何处理“13”个元素的那个64位值的：

## 指令清单18.16 IDA 中的可执行文件

```
off_140011000      dq offset qword_140011060    ; 数据交叉引用;
.text:000000140001003

      dq offset areruary_1      ; "February"
      dq offset aMarch_1       ; "March"
      dq offset aApril_1       ; "April"
      dq offset aMay_1         ; "May"
      dq offset aJune_1        ; "June"
      dq offset aJuly_1        ; "July"
      dq offset aAugust_1      ; "August"
      dq offset aSeptember_1  ; "September"
      dq offset aOctober_1    ; "October"
      dq offset aNovember_1   ; "November"
      dq offset aDecember_1   ; "December"

qword_140011060  dq 797261756E614AH    ; 数据交叉引用;
sub_140011020+4                .data:off_140011000
.data:0000000014001008

      aFebruary_1 db 'February',0  ; 数据交叉引用;
      align 4
      a_1 db 'March',0      ; 数据交叉引用;
      .data:0000000014001010
```

那个地址是097261756E44。如果某个函数用字符串指针访问这个地址，整个程序多半会崩溃。毕竟这个值是一个有效的地址：

## 数组溢出保护

如果指调用函数的用户确保参数不错范围，那么这个程序就会慢了。在编程领域，成熟的应用程序应当具备“早期失败（Fail Early）”或“快速失败（Fail-Fast）”能力：C/C++ `assertions` 就是手段之一。我们可以修改程序，验证输入参数是否范围内：

## 指令清单18.17 添加的 `assert()`

```cpp
const char* get_month_checked (int month)
{
    assert(month<12);
    return month[month];
}
```

只要在函数启动时用参数有效性的 `assert()` 函数，当输入值在区间之外时，程序将进行。

## 指令清单18.18 MSVC 2013 优化

```
3143 DB    'm',0, 'o',0, 'n',0, 't',0, 'h',0,., 
            DB    'c',0
3144 DB    'm',0, 'o',0, 'n',0, 't',0, 'h',0, '<',
            DB    '1',0, '2',0
month$ =48
get_month1_checked PROC
$LN5:
push     rbx
sub      rsp, 32
mov      rbx, ecx
cmp      ebx, 12
jil      SHORT OFFSET:$LN3@get_month1
lea      rdx, OFFSET FLAT:$3143
lea      rcx, OFFSET FLAT:$3144
mov      rbx, 29
call     _inert
$LN3@get_month1:
lea      rcx, OFFSET FLAT:month1
mov      rax, QWORD PTR [rcx+8]
add      rsp, 32
pop      rbx
ret
get_month1_checked ENDP
```

严格地说，`assert()` 只能算表达式不能算函数。它对条件表达式进行判断，然后把行号和文件名传递另一个函数，由后者提供。在可执行程序里，我们可以看到文件名和条件表达式，以及 `assert()` 在源文件行号。所有编译器在编译 `assert` 时的处理机制基本相同。本文演示 GCC 的编译结果：

## 指令清单18.19 GCC 4.9 优化

```
.LC1:      .string "month.c"
.LC2:      .string "month<12"
get_month1_checked:
cmp      edi, 12
jg       .L6
movsx    rdi, edi
mov      rax, QWORD PTR [0+rdi*8]
ret
.L6:
push     rax
mov      ecx, OFFSET FLAT:PRETTY_FUNCTION__243
mov      esi, OFFSET FLAT:.LC1
mov      edi, OFFSET FLAT:.LC2
call     __assert
.PRETTY_FUNCTION__243: .string "get_month_checked"
```
