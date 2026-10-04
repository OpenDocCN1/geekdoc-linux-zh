在Linux 2.6内核的编译选项中，设定了寄存器选项“mregparm=3”。

这个选项决定，编译器首先通过EAX、EDX和ECX寄存器传递函数所需的3个参数，再通过传递剩余的参数。如果，参数的总数不足3，它只会用到部分通用寄存器。

在Ubuntu里Linux Kernel 2.6.31，并用“make vlinux”指令编译，然后使用IDA打开程序，查找函数do_fil_open()。这个函数的开头部分大体是这样的：

# 指令清单19.6 do_fil_open() (Linux kernel 2.6.31)

```
do_fil_open:

    push    ebp
    mov     ebp, esp
    push    edi
    push    esi
    push    ebx
    mov     ebx, ecx
    add     ebx, 1
    sub     esp, [ebp+arg_4] ; acc_mode (5th arg)
    test    bl, 3
    mov     [var_80], eax; dfd (1th arg)
    mov     [var_7C], edx; pathname (2th arg)
    mov     [var_78], ecx; open_flag (3rd arg)
    jnz     short loc_C01EF684
    mov     ebx, ecx ; ebx <= open_flag
```

函数参数个数，就把3个寄存器里的参数值存储在里。若非如此，之后程序就会出现寄存器内存不可用的资源紧张问题。

我们再来看do_fil_open()函数的另外一段代码：

# 指令清单19.7 do_fil_open() (Linux kernel 2.6.31)

```
loc_C01EF6B4:

    test    bl, 40h ; CODE XREF: do_fil_open+4F
    jnz     loc_C01EF810 ; O_CREAT
    mov     edi, ebx
    shr     edi, 11h
    xor     edi, 1
    and     edi, 1
    test    ebx, 10000h
    jz      short loc_C01EF6D3
    or      edi, 2
```