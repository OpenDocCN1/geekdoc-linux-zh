```
mov DWORD PTR [ecx+4], 999
mov eax, DWORD PTR _this$[ebp]
mov esp, ebp
pop ebp
ret 0
??0c@QAE@XZ END ; c::c
```

```
_this$ = -4 ; size = 4
aS$ = 8 ; size = 4
b$ = 12 ; size = 4
??0c@QAE@HH$Z PROC ; c::c,COMDAT
; _this$ = ecx
push ebp
mov ebp, esp
mov DWORD PTR _this$[ebp], ecx
mov eax, DWORD PTR _this$[ebp]
mov ecx, DWORD PTR _a$[ebp]
mov DWORD PTR [eax], ecx
mov edx, DWORD PTR _this$[ebp]
mov eax, DWORD PTR _b$[ebp]
mov DWORD PTR [ecx+4], eax
mov eax, DWORD PTR _this$[ebp]
mov esp, ebp
pop ebp
ret 8
??0c@QAE@HH$Z END ; c::c
```

构造函数本身就是一种函数，它们使用ECX寄存器存储结构体的指针，将后复制到自己的局部变量里。当然，第二步并不是必须的。

从C++的标准（IS013, P.12.1）可知，构造函数不需要返回返回值。事实上，从指令层面来看，构造函数的返回值是一个新创建的对象指针，即this指针。

现在我们来看dump().

# 指令清单51.3 MSVC

```
_this$ = -4 ; size = 4
?dump@@@QAEXXZ PROC ; c::dump,COMDAT
; _this$ = ecx
push ebp
mov ebp, esp
```