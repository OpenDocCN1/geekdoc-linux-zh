```
3   push    ebp
4   mov     ebp, esp
5   sub     esp, 16
6   mov     BYTE PTR _tmp$[ebp], 1    ; set field a
7   mov     DWORD PTR _tmp$[ebp+4], 2   ; set field b
8   mov     BYTE PTR _tmp$[ebp+8], 3   ; set field c
9   mov     DWORD PTR _tmp$[ebp+12], 4  ; set field d
10  sub     esp, 16                      ; allocate place for
11  temporary structure
12  mov     eax, esp
13  mov     ecx, DWORD PTR _tmp$[ebp]      ; copy our structure to the
14  temporary one
15  mov     DWORD PTR [eax], ecx
16  mov     edx, DWORD PTR _tmp$[eax+4]
17  mov     DWORD PTR [eax+4], edx
18  mov     ecx, DWORD PTR _tmp$[ebp+8]
19  mov     DWORD PTR [eax+8], ecx
20  mov     edx, DWORD PTR _tmp$[ebp+12]
21  mov     DWORD PTR [eax+12], edx
22  call    f
23  add     esp, 16
24  xor     eax, eax
25  mov     esp, ebp
26  pop     ebp
27  ret     0
28  _main  ENDP
29  s$ = 8                              ; size = 16
30  ?f@@YUS@@@Z PROC                   ; f
31  push    ebp
32  mov     ebp, esp
33  mov     eax, DWORD PTR _s$[12]
34  push    eax
35  movsx   ecx, BYTE PTR _s$[8]
36  push    eax
37  mov     edx, DWORD PTR _s$[ebp+4]
38  push    edx
39  movsx   eax, BYTE PTR _s$[ebp]
40  push    eax
41  push    OFFSET $SSG3842
42  call    _printf
43  add     esp, 20
44  pop     ebp
45  ret     0
46  ?f@@YUS@@@Z ENDP                   ; f
47  _TEXT   ENDS
```

虽然我们在代码里一次性分配了结构体tmp，但是依次给它的四个字段赋值
值，但是可执行程序的指令不同：它将结构的指针赋值到临时地址
（第10行指令分配的空间里），然后通过临时的中间变量给结构体的四个值
赋值临时结构体（第12~19行的指令），还把指针复制传给f()调用）。