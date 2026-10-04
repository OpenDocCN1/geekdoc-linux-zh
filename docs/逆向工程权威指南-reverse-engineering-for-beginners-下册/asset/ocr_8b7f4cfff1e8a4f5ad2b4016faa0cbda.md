```
or	 eax, ecx
; EAX=dcccbbaa
ret	 0
_form_IP ENDP
```

这个过程还可以描述为：每个字节都写入到其返回值的最低8位比特，并且每次左移一个字节，将其与返回值进行或或操作。重复四次，就能完成函数功能。

就足够了。然而遗憾的是，可能没有其他的办法来实现上述的逻辑了。正如著者所知，目前的CPU以及ISA还不能把规定位比特或字节直接复制到其他类型数据里。所以一般都是通过位移和OR或运算才能把IP地址转换为32位数据。

# 38.3 函数print_as_IP()

函数print_as_IP()实现的功能与上面函数完全相反，它将一个32位的数值切分成4字节。切分过程比较简单：只需要将输入的数值位移24位、16位、8位或者0，最低字节的0到7即可。

>  指令清单38.4 非优化版MSVC 2012

```
_a$ = 8
_print_as_IP PROC		 size = 4
push	 ebp
mov	 ebp, esp
mov	 edx, DWORD PTR _a$[ebp]
t; EAX=dcccbbaa
and	 eax, 255
t; EAX=000000aa
push	 eax
mov	 ecx, DWORD PTR _a$[ebp]
t; ECX=dcccbbaa
shr	 ecx, 8
t; ECX=00ddccbb
and	 ecx, 255
t; ECX=000000bb
push	 ecx
mov	 edx, DWORD PTR _a$[ebp]
t; EDX=dcccbbaa
shr	 edx, 16
t; EDX=0000ddcc
and	 edx, 255
```