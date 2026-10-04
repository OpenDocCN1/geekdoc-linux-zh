```
void printing_function(int i)
{
    printf("f%%d\n", i);
}

int main()
{
    int i;
    for (i=2; i<10; i++)
        printing_function(i);
    return 0;
}
```

使用MSVC 2010编译上述程序，可得到如下所示的指令：

#  指令清单14.1 MSVC 2010

```
_i = -4
_main PROC
    push ebp
    mov ebp, esp
    push ecx
    mov DWORD PTR _i$[ebp], 2    ;  初始化
    jmp SHORT $LN3@
$LN2main:
    mov eax, DWORD PTR _i$[ebp], 10  ; 循环语句：
    add eax, 1                  ; i增1
    mov DWORD PTR _i$[ebp], eax
$LN3main:
    cmp DWORD PTR _i$[ebp], 10   ; 判断是否满足循环条件
    jge SHORT $LN1@             ; 如果i=10 则终止循环语句
    mov ecx, DWORD PTR _i$[ebp]  ; 循环体：call f(i)
    push ecx
    call _printing_function
    add esp, 4
    jmp SHORT $LN2@             ; 跳到循环开始处
$LN1main:
    xor eax, eax                ; 循环结束
    mov ebp, ebx
    pop ebp
    ret 0
_main ENDP
```

上面的汇编代码可以说是中规中矩的。


使用GCC 4.4.1（未开启优化选项）编译上述程序，可得到如下汇编指令：

#  指令清单14.2 GCC 4.4.1