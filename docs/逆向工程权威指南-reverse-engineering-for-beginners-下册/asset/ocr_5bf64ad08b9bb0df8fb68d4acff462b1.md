```
limit$ = 16      ; size = 4
_fib PROC
    push   ebp
    mov    ebp, esp
    mov    eax, DWORD PTR _a$[ebp]
    add    eax, DWORD PTR _b$[ebp]
    push   eax
    push   OFFSET $SG2750 ; "%d"
    call   DWORD PTR __imp_printf
    add    esp, 8
    mov    ecx, DWORD PTR _limit$[ebp]
    push   ecx
    mov    edx, DWORD PTR _a$[ebp]
    add    edx, DWORD PTR _b$[ebp]
    push   edx
    mov    eax, DWORD PTR _b$[ebp]
    push   eax
    push   
    call   fib
    add    esp, 12
    push   ebp
    pop    
    ret    0
ENDP
```

```
_main PROC
    push   ebp
    mov    ebp, esp
    push   OFFSET $SG2753 ; "0\n\n1\n\n"
    call   DWORD PTR __imp_printf
    add    esp, 4
    push   20
    push   1
    call   fib
    add    esp, 12
    xor    eax, eax
    pop    ebp
    ret    0
ENDP
```

我们重点分析这个程序的结构。

我们在OllyDbg中加载本例的可执行程序，并跟踪到调用f()函数的那条指令，如图36.1所示。