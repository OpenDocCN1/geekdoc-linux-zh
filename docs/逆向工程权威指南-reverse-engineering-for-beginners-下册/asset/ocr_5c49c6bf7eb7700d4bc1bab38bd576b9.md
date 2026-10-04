```
; int _cdecl main()
_main proc ptr -4
var_4= dword ptr -4
argc= dword ptr 8
argv= dword ptr 0Ch
envp= dword ptr 10h

push    ebp
mov     ebp, esp
push    ecx
push    offset Format ; "Enter X:\n"
call    ds:printf
add     esp, 4
lea     eax, [ebp-var_4]
push     eax
push     offset aD ; "%d"
call    ds:scanf
add     esp, 8
cmp     eax, 1
jnz    short error
```

![](bbox=[0.3485, 0.4015, 0.6515, 0.4835])

图7.8 IDA 解耦模式下的收缩操作

这种解耦模式非常实用。逆工程工作经验不多的人，可以使用这种方式大幅度的减少他需要处理的信息量。

# 7.3.3 MSVC: x86+OllyDbg

我们使用OllyDbg调试刚才的程序，在 scanf()刚才返回的值的情况下强制其继续运行余的指令。

在把变量的地址传递给scanf() 的时候，变量处于未初始化状态，其值应当随机的噪声数据。如图7.9所示，变量x的值为0x6E494714。