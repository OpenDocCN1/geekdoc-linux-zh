# 18. 9.1 题目1

请描述下述代码的功能。

```
指令清单18.38 MSVC 2010+/01

a$ = 8      ; size = 4
b$ = 12     ; size = 4
c$ = 16     ; size = 4
?s@YAXPAN00@ PROC; s, COMAT
mov     eax, DWORD PTR_b$[esp-4]
mov     ecx, DWORD PTR_$a$[esp-4]
mov     edx, DWORD PTR_$c$[esp-4]
push    esi
push    edi
sub     ecx, eax
sub     edx, eax
mov     edx, 200    ; 000000c8H
$LL6s:
push    100      ; 00000064H
pop     esi
$LL3@s:
fld     WORD PTR [ecx+e]
fadd    WORD PTR [eax]
fstp    WORD PTR [edx+e]
add     eax, 8
dec     esi
jne     SHORT $LL3@s
dec     edi
jne     SHORT $LL6@s
pop     esi
pop     esi
ret
?s@YAXPAN00@Z ENDP      ; s
```

/01 代码minimize_size，即生成最小长度的程序。

通过Keil 5.03 (启用选项-03) 编译而得到的ARM代码如下所示。

```
指令清单18.39 Optimizing Keil 6/2013 (ARM mode)

PUSH    {r4-r12,lr}
MOV     r9,r2
MOV     r10,r1
MOV     r11,r0
MOV     r15,#0
|L0.20:
ADD     r0,r5,LSL #3
ADD     r0,r0,r5,LSL #4
```