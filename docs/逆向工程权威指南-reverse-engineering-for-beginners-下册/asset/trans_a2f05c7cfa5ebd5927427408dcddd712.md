
```assembly
C:\Polygon\ex3.exe

Enter X:
asdasd
You entered 1850296084...
```

图7.11 控制台窗口

1850296084是十进制值，其十六进制值就是我们刚才看到的0x6E64947114。

## 7.3.4 MSVC: x86+Hiew

下面，我们一起修改可执行文件。所谓的“修改”可执行文件，就是对其打补丁（即人们常说的“patch”）。通过打补丁的方法，我们可以强制程序在所有情况下都不进行输出。

首先，我们要启用MSVC的编译选项/MD。这样编译出来的可执行文件将把标准函数链接到MSVC*.DLL，方便我们在可执行文件的文本段落里找到main()函数。此后，我们使用Hiew工具打开可执行文件，找到text段开头的main()函数（依次使用Enter、F8、F6、Enter、Enter）。

然后会看到图7.12所示的界面。

### Hiew.ex3.exe

```assembly
C:\Polygon\ollydbg\ex3.exe
00401000: 55          push    ebp
00401001: 80DEC      mov     ebp,esp
00401003: 51          push    ecx
00401004: 68003400    push    00040300;'Enter X:' --021
00401009: FF15941000    call    printf
0040100F: 83C404      add     esp,4
00401012: 8BA4FC      lea     eax,[esp]-4
00401015: 50          push    eax
00401016: 68303400    push    00040300;'--02
0040101B: FF159C1000    call    scf
00401021: 83C404      add     esp,8
00401024: 83F801      cmp     eax,1
00401027: 7514        jnz     00401030;'--03
00401029: 89D0FC      mov     ecx,[esp]-4
0040102C: 51          push    ecx
0040102D: 68303000    push    00043010;'You entered %d...' --04
00401032: FF15943000    call    printf
00401038: 83C404      add     esp,8
0040103B: EB0E        jumps   00401048;  --05
0040103D: 68243000    push    00043024;'What you entered? Huh?' --06
00401042: FF15942000    call    printf
00401048: 83C404      add     esp,4
0040104B: 33C0        xor     eax,eax
0040104E: 89E5        mov     esp,ebp
0040104F: 50          pop     ebp
00401050: C3          ret;       ....................
00401051: 8BA05A00    mov     eax,000005A0;' ZM'
```

7.12 使用Hiew观察main()函数

Hiew能够识别并显示ASCIIZ，以null为结束字节的ASCII字符。它还能识别导入函数的名称。

如图7.13所示，将光标标记移动至00040127处（即JNZ命令所在的位置），我们使其失效，按F3，然后输入“9090”。“9090”是两个连续的NOP（No Operation，空操作）opcode。

![](img/a13a81a53f805f55074b2e5d2ec754b6_146_0.png)

图7.13 在Hiew中将JNZ替换为两条NOP指令

然后按F9（更新），将修改后的可执行文件保存到磁盘。

连续的9090是典型的修改特征，有人会觉得很美。此外还可以把这个opcode的第二个字节为零（opcode的两个字节代表jump offset），令jcc指令跳转的偏移为0，从而继续运行下一条指令。

这种修改方法可以迁移指令流。除此之外我们还可以强制程序进行跳转。我们可以把jcc对应的opcode的第一个字母替换为“EB”，不去修改第二节(offset)。这种方法把条件指令替换为了无条件跳转指令。经过这样的调整之后，本例中的可执行文件无条件显示错误信息“What you entered? Huh?”

## 7.3.5 MSVC:x64

本例使用的变量是int变量。在64位平台上，int变量还是32位。在64位系统中，访问寄存器的（低32位）时，在汇编语言中我们需要使用寄存器名称。

```assembly
DATA SEGMENT
$SG24 DB  'Enter X: ', 0AH
$SG26 DB  '%d', 0AH
$SG27 DB  'You entered %d ', 0AH
$SG29 DB  'What you entered? Huh?', 0AH
ENDS

TEXT SEGMENT
$ = 32
main  PROC
$LN5:
    sub     rsp, 56
    lea     rcx, OFFSET:$SG24 ; 'Enter X: '
    call    printf
    mov     eax, DWORD PTR [rsp]
    lea     rcx, OFFSET:$SG26 ; '%d'
    call    printf
    cmp     eax, 1
    jne     LN2@main
    mov     edx, DWORD PTR [rsp] ; 'You entered %d...'
    lea     rcx, OFFSET:$SG27
    call    printf
    jmp     LN1@main
$LN2@main:
    lea     rcx, OFFSET:$SG29 ; 'What you entered? Huh?'
    call    printf
$LN1@main:
    xor     eax, eax
    add     rsp, 56
    ret
main
ENDP
```

## 7.3.6 ARM

ARM: Optimizing Keil (Thumb mode)

```assembly
var_8      = -8

PUSH      {R3,LR}
ADR       R0,aEnter      ; "Enter X:\n"
BL        printf
MOV       R1,SP
ADR       R0,aD           ; "%d"
BL        scanf
CMP       W0, #1
BEQ       loc1E
ADR       R0,aEntered  ; "What you entered?\n"
BL        printf
POP      {R3,PC}           ; XREF: main+12
loc1E
    LDR       R1, [SP,#8]
    ADR       R0,aEnded  ; "You entered...\n"
BL        printf
```

这里见到了CMP和BEQ指令。它们都是参数比较，并设置标志位。ARM系统的指令与x86相似。BEQ是条件跳转指令（Branch if Equal），在操作数相等，ZF寄存器的值就是1，那么BEQ就会跳转到它的偏移量。它与x86指令相同。其余的指令并不理解：程序有两个分支，这两个分支终于loc1A处，通过“MOV R0,#0”指令将返回值保存在R0寄存器，然后退出。

ARM64

指令清单：Non-optimizing GCC

```assembly
LC0:
    .string "Enter X:"
LC1:
    .string "%d"
LC2:
    .string "You entered...\n"
LC3:
    .string "What you entered? Huh?"
f6:
    ; save FP and LR in stack frame;
    stp     x29, x30, [sp, -32]! ; set stack frame (FP=SP)
    add     x29, sp, #0
    ; load pointer to the "Enter X:" string:
    adrp    x0, LC0
    add     x0, x0, :lo:LC0
    puts
    ; calculate address of x in the local stack
    add     x1, x29, #28
    bl      scanf ; scanf returned result in W0.
    cmp     w0, #1
    bne     Branch If Not Equal ; if W0!=0, jump to L2 will occurred
    bne     L2 ; at moment W0=1, meaning no error
    ; load x1, [x29,28]
    ; load pointer to the "You entered...\n" string:
    adrp    x0, LC2
    add     x0, x0, :lo:LC2
    printf
```

## 7.3.7 MIPS

### 指令清单：Optimizing GCC 4.4.5 (IDA)

```assembly
.text:00406A0 main:
    var_18 = -0x18
    var_10 = -0x10
    var_4 = -4
    lui     $gp, 0x42
    addiu $sp, -0x28
    lui     $gp, 0x418960
    sw      $ra, 0x28+var_4($sp)
    sw      $gp, 0x28+var_18($sp)
    la      $t9, puts
    la      $a0, 0x40
    jalr    $t9 ; puts
    la      $a0, EnterX # "Enter X:"
    lw      $gp, 0x28+var_4($sp)
    lui     $a0, 0x42
    ...
```