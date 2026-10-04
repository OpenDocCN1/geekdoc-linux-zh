

## 指令清单18.49 非优化 Keil 6/2013 (ARM模式)

```assembly
f PROC
RSB r1,r1,LSL #4
ADD r0,r0,LSL #6
ADD r1,r0,r2,LSL #3
LDM r1,{r0,r1}
BX
ENDP
```

## 指令清单18.50 非优化 Keil 6/2013 (Thumb模式)

```assembly
f PROC
MOVS r3,0xf
LSLS r3,r3,#6
MULS r1,r3,r1
ADDS r0,r1,r0
LSLS r1,r2,#3
ADDS r1,r0,r1
LDM r1,{r0,r1}
BX
ENDP
```

## 指令清单18.51 优化 GCC 4.9 (ARM64)

```assembly
f:
sxtw x1, w1
add x0, x0, x2, sxtw 3
lsl x2, x1, 10
sub x1, x2, x1, lsl 6
ldr d0,[x0,x1]
ret
```

## 指令清单18.52 优化 GCC 4.4.5 (MIPS)(IDA)

```assembly
f:
sll $v0, $al, 10
sll $al, 6
subu $al, $v0, $al
addu $al, $a0, $al
sll $a2, 3
addu $al, $a2
lcwl $f0, 4($al)
or $at, Szero
lcwl $f1, 0($al)
jr $ra
or $at, $zero
```

## 18.9.4 题目4

请描述下列代码的作用。

请判断数据组的维度。

## 指令清单18.53 优化 MSVC 2010

```assembly
array$ = 8
xS$ = 12
yS$ = 16
z$ = 20
PROC
mov eax, DWORD PTR _xS$[esp-4]
mov edx, DWORD PTR _yS$[esp-4]
mov ecx, eax
shl ecx, 4
sub ecx, eax
lea eax, DWORD PTR [edx+ecx*]
mov ecx, DWORD PTR _array$[esp-4]
mov eax, DWORD PTR [eax+ecx*]
shl eax, 4
add eax, DWORD PTR _z$[esp-4]
mov eax, DWORD PTR [ecx+eax*]
ret
0
ENDP
```

## 指令清单18.54 非优化 Keil 6/2013 (ARM模式)

```assembly
PROC
RSB r1,r1,r1,LSL #4
ADD r1,r1,r1,LSL #2
ADD r0,r0,r1,LSL #8
ADD r1,r2,r2,LSL #2
ADD r0,r0,r1,LSL #6
LDR r0,[r0,r3,LSL #2]
BX
ENDP
```

## 指令清单18.55 非优化 Keil 6/2013 (Thumb模式)

```assembly
PUSH {r4,lr}
MMOVS r4,#0x4b
LSLS r4,r4,#8
MULS r1,r1,r0
ADDS r0,r1,r0
MMOVS r1,#0xff
ADDS r1,#0x41
MULS r2,r1
ADDS r0,r0,r2
LSLS r1,r3,#2
LDR r0,[r0,r1]
POP {r4,pc}
ENDP
```

## 指令清单18.56 优化 GCC 4.9 (ARM64)

f:
```assembly
sxtw x2, w2
mov w4, 19200
add x2, x2, x2, lsl 2
smull x1, w1, w4
lsl x2, x2, 4
add x3, x2, x3, sxtw
add x0, x0, x3, lsl 2
ldr w0, [x0,x1]
ret
```

## 指令清单18.57 优化 GCC 4.4.5 (MIPS)(IDA)

f:
```assembly
sll $v0, $al, 10
sll $al, 8
addu $al1, $v0
sll $v0, $a2, 6
sll $a2, 4
addu $a2, $v0
sll $v0, $al, 4
ubu $al, $v0, $al
addu $a2, $a3
addu $al1, $a0, $al
sll $a2, 2
addu $al1, $a2
lw $v0, 0($al)
jr $ra
or $at, $zero
```

## 18.9.5 题目代码的作用。

请描述下列代码的作用。

## 指令清单18.58 优化 MSVC 2012 /GS-

COMM _tbl:DWORD:064H
tv759 = -4 ;size=4

```assembly
_main PROC
push ecx
push ebx
push push
push ebp
push esi
xor edx, edx
push edi
xor esi, esi
xor edi, edi
xor ebx, ebx
ebp, ebp
mov DWARF PTR tv759[esp+20]
mov D,,,,,,,
,,,,,4

l ecx, 4
sub ecx, eax
lea eax, DWORD PTR [edx+ecx*]
mov ecx, DWORD PTR _array$[esp-4]
mov eax, DWORD PTR [ex+ecx*]
shl eax, 4
add eax, DWORD PTR _z$[esp-4]
mov eax, DWORD PTR [ecx+eax*]
ret
0
ENDP

## 指令清单18.59 非优化 Keil 6/2013 (ARM模式)

```assembly
fB r1,1,,1,LSL #4
ADD,0,r0,LSL #6
ADD r1,r0,r2,LSL #3
LDM r1,{r0,r1}
BX
```

## 指令清单18.60 非优化 Keil 6/2013 (Thumb模式)

```assembly
f:
MOVS r3,0xf
LSLS r3,r3,#6
MULS r1,r3,r1
ADDS r0,r1,r0
LSLS r1,r2,#3
ADDS r1,r0,r1
LDM r1,{r0,r1}
BX
```

## 指令清单18.61 优化 GCC 4.9 (ARM64)

```assembly
f:
sxtw x1, w1
add x0, x0, x2, sxtw 3
lsl x2, x1, 10
sub x1, x2, x1, lsl 6
ldr d0,[x0,x1]
ret
```

## 指令清单18.62 非优化 GCC 4.4.5 (MIPS)(IDA)

```assembly
f:
sll $v0, $al, 10
sll $al, 6
subu $al, $v0, $al
addu $al, $a0, $al
sll $a2, 3
addu $al, $a2
lcwl $f0, 4($al)
or $at, Szero
lcwl $f1, 0($al)
jr $ra
or $at, $zero
```

[/content]

*(注：由于提供的原始文本中从18.58开始出现了严重的乱码和重复错误，此处已根据“不要重复输出原文”和“翻译内容”的原则，对后续逻辑清晰的指令标题和结构进行了翻译，乱码部分无法识别翻译。)*

**更正后的逻辑完整翻译译文：**

[content]
## 指令清单 18.49 非优化 Keil 6/2013 (ARM模式)

```assembly
f PROC
RSB r1,r1,LSL #4
ADD r0,r0,LSL #6
ADD r1,r0,r2,LSL #3
LDM r1,{r0,r1}
BX
ENDP
```

## 指令清单 18.50 非优化 Keil 6/2013 (Thumb模式)

```assembly
f PROC
MOVS r3,0xf
LSLS r3,r3,#6
MULS r1,r3,r1
ADDS r0,r1,r0
LSLS r1,r2,#3
ADDS r1,r0,r1
LDM r1,{r0,r1}
BX
ENDP
```

## 指令清单 18.51 优化 GCC 4.9 (ARM64)

```assembly
f:
sxtw x1, w1
add x0, x0, x2, sxtw 3
lsl x2, x1, 10
sub x1, x2, x1, lsl 6
ldr d0,[x0,x1]
ret
```

## 指令清单 18.52 优化 GCC 4.4.5 (MIPS)(IDA)

```assembly
f:
sll $v0, $al, 10
sll $al, 6
subu $al, $v0, $al
addu $al, $a0, $al
sll $a2, 3
addu $al, $a2
lcwl $f0, 4($al)
or $at, Szero
lcwl $f1, 0($al)
jr $ra
or $at, $zero
```

## 18.9.4 题目4

请描述下列代码的作用。

请判断数据组的维度。

## 指令清单 18.53 优化 MSVC 2010

```assembly
array$ = 8
xS$ = 12
yS$ = 16
z$ = 20
PROC
mov eax, DWORD PTR _xS$[esp-4]
mov edx, DWORD PTR _yS$[esp-4]
mov ecx, eax
shl ecx, 4
sub ecx, eax
lea eax, DWORD PTR [edx+ecx*]
mov ecx, DWORD PTR _array$[esp-4]
mov eax, DWORD PTR [eax+ecx*]
shl eax, 4
add eax, DWORD PTR _z$[esp-4]
mov eax, DWORD PTR [ecx+eax*]
ret
0
ENDP
```

## 指令清单 18.54 非优化 Keil 6/2013 (ARM模式)

```assembly
PROC
RSB r1,r1,r1,LSL #4
ADD r1,r1,r1,LSL #2
ADD r0,r0,r1,LSL #8
ADD r1,r2,r2,LSL #2
ADD r0,r0,r1,LSL #6
LDR r0,[r0,r3,LSL #2]
BX
ENDP
```

## 指令清单 18.55 非优化 Keil 6/2013 (Thumb模式)

```assembly
PUSH {r4,lr}
MMOVS r4,#0x4b
LSLS r4,r4,#8
MULS r1,r1,r0
ADDS r0,r1,r0
MMOVS r1,#0xff
ADDS r1,#0x41
MULS r2,r1
ADDS r0,r0,r2
LSLS r1,r3,#2
LDR r0,[r0,r1]
POP {r4,pc}
ENDP
```

## 指令清单 18.56 优化 GCC 4.9 (ARM64)

f:
```assembly
sxtw x2, w2
mov w4, 19200
add x2, x2, x2, lsl 2
smull x1, w1, w4
lsl x2, x2, 4
add x3, x2, x3, sxtw
add x0, x0, x3, lsl 2
ldr w0, [x0,x1]
ret
```

## 指令清单 18.57 优化 GCC 4.4.5 (MIPS)(IDA)

f:
```assembly
sll $v0, $al, 10
sll $al, 8
addu $al1, $v0
sll $v0, $a2, 6
sll $a2, 4
addu $a2, $v0
sll $v0, $al, 4
ubu $al, $v0, $al
addu $a2, $a3
addu $al1, $a0, $al
sll $a2, 2
addu $al1, $a2
lw $v0, 0($al)
jr $ra
or $at, $zero
```

## 18.9.5 题目代码的作用。

请描述下列代码的作用。

## 指令清单 18.58 优化 MSVC 2012 /GS-

COMM _tbl:DWORD:064H
tv759 = -4 ;size=4

```assembly
_main PROC
push ecx
push ebx
push push
push ebp
push esi
xor edx, edx
push edi
xor esi, esi
xor edi, edi
xor ebx, ebx
ebp, ebp
mov DWARF PTR tv759[esp+20]
... (此处乱码部分已跳过)
```
