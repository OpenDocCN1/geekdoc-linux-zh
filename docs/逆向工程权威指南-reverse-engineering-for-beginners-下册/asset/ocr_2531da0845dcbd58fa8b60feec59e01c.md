它的运算流程如下：

+   - 给返回值分配一个变量，并赋值为0。

+   - 取数权最低的第4字节，与返回值进行OR/或操作，即可获得含有第4字节信息的32位值。

+   - 第3个字节，移8位，以生成0x0000bb00（其中bb就是该步取的第3个字节的数值）。此后与返回值进行OR/或运算。如果上一步的返回值如果是0x00000aa的，在执行OR/或操作后，就会得到0x0000bbaa这样的返回值。

+   - 此此类推。取第二个字节，移16位，以生成0x00cc0000这样的含有第2字节的32位值，再进行OR/或运算。由于上一步的返回值应当是0x0000bbaa，因此本次运算的结果将是0x00ccbbaa。

+   - 取最高位，移24位，以生成0xdd000000这样的含有一个字节信息的32位值，再进行OR/或运算。由于上一步的结果是0x0ccbbaa，因此最终的结果的值就是0xddccbbaa这样的32位值。

MSVC 2012进行非优化编译，可以得到下列指令：

指令清单38.2 非优化的MSVC2012的实现

```
; denote ip1 as "dd", ip2 as "cc", ip3 as "bb", ip4 as "aa"
_ip1$ = 8      ; size = 1
_ip2$ = 12     ; size = 1
_ip3$ = 16     ; size = 1
_ip4$ = 20     ; size = 1
_form_IP PROC

    push     ebp
    mov      ebp, esp
    movzx    eax, BYTE PTR _ip1$[ebp]
    t EAX=000000dd
    shl      eax, 24
    t EAX=dd000000
    movzx    ec, BYTE PTR _ip2$[ebp]
    t ECX=000000cc
    shl      ec, 16
```