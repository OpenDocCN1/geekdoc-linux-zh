```
mov    DWORD PTR $eos[ebp], eax; 指向局部变量eos
$LN2_strlen:
mov    ecx, DWORD PTR $eos[ebp]; ECX=eos
ret

    ; take 8-bit byte from address in ECX and place it as 32-bit value
to EDX with sign extension

movsx   edx, BYTE PTR [ecx]
mov    eax, DWORD PTR $eos[ebp]; EAX=eos
add    eax, 1; ; ECX++
mov    DWORD PTR $eos[ebp], eax; EAX还原为
test   edx, edx
je     SHORT $LN1_strlen; ; EDX = 0 ? yes, then finish loop
jmp    SHORT $LN2_strlen; ; continue loop
$LN1_strlen:
    ; we calculate the difference between two pointers

mov    eax, DWORD PTR $eos[ebp]
sub    eax, DWORD PTR _str[ebp]
sub    eax, 1; ; subtract 1 and return result
mov    esp, ebp
pop    ebp
xor    edx, edx
$strlen_   
```

这里出现了两个新指令：MOVX和TEST 数据，并把它存储到32位

此处，MOVX从内存中读取8字节（单字），并把它存储到32位寄存器里。MOVX是mov带有Sign-Extend的缩写。在小空间数据转换为大空间数据时，存在填充高位数据的问题；例如中，MOVX将原始数据的位数据填充到EDX寄存器的低位；如果原始数据是负数，该指令将使用第8位到第31位（高24位），否则使用024位。

是为了保证符号型数据在类型转换后的数值不变char（有符号）数据。现在设有一把char型数据转换为整数型（都是有符号数）的情况：假设char型的原始值是-2（0xFE），直接将整个字节复制到整数型数据的低8位时，整数型的值变成0x000000FE，以有符号数据的角度看会被被转换为254，而没有保持原始值-2。二对的int型数据是0xFFFFFFFF。所以，在原始数据复制制到符号位扩展后，还要使用符号标记填充剩余的数据，而这就是MOVX的功能。

本书30章会更详细地介绍符号型数据转换的方法。

并不是确定数据是否有必要分配EDX寄存器专门保存char型数据，看上面只使用了寄存器的低8位（相对于DX）。显然，编译器根据自己的