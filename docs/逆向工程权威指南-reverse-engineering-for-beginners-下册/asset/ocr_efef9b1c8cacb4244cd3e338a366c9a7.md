push arg3
push arg2
push arg1
call function

function:
... do something ...nret 12

此类约定在Win32的标准库文件中十分常见。然而因为Win64系统遵循调用约定的是Win64规范，所以Win64的库文件里不会出现stdcall的标志性操作指令。

以书8.1节中的函数为例。我们给其中的函数增加__stdcall限定符即可强制使用stdcall调用约定：n调用约定：

```
int __stdcall f2 (int a, int b, int c)
{
    return a*b+c;
}
```

它的编译结果与本书8.2节类相似，但是最后的指令从RET变成了RET。在遵循stdcall约定之后，指针SP就不再由调用方更新了。

这样一来，我们就可以通过函数尾部的RETN指令直观地推算出外部参数的个数。计算方法就是：N除以4。

# 指令清单64.3 MSVC 2010

```
_a$ = 8
_b$ = 12
_c$ = 16
_f2@12 PROC
    push ebp
    mov ebp, esp
    mov eax, DWORD PTR _a$[ebp]
    mov eax, DWORD PTR _b$[ebp]
    mov eax, DWORD PTR _c$[ebp]
    add eax
    pop ebp
    ret 12      ; 0x000000CH
_f2@12 ENDP

push 3
```