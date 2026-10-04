```
mov     eax, DWORD PTR s
mov     DWORD PTR [esp], eax
call    puts
xor     eax, eax
leave
ret
.LC:
.string "a string"
.GLOBAL__sub_I_4:
sub     esp, 44
lea     eax, [esp+31]
mov     DWORD PTR [esp+8], eax
mov     DWORD PTR [esp+4], OFFSET FLAT:.LC
mov     DWORD PTR FLAT:ZNSsclIEpRCkSaIceE
mov     DWORD PTR [esp+8], OFFSET FLAT:_dso_handle
mov     DWORD PTR [esp+4], OFFSET FLAT:ZNSd1Ev
mov     DWORD PTR [esp], OFFSET FLAT:s
call    cxa_atexit
add     esp, 44
ret
.LFE64:
.size   GLOBAL__sub_I_s,.-GLOBAL__sub_I_s
.section .init_array,"aw"
.align  4
.long   GLOBAL__sub_I_s
.glob  s
.bss
.align  4
.type   s, @object
.size   s, 4
.zero  44
.hidden _dso_handle
```

但是GCC没有单独建立一个专用函数，而是把每个结构表的容器逐一传递给atexit()函数。

# 51.4.2 std::list

std::list是众所周知的双向链表的容器，它的每个元素可以通过指针（链域）串连接逻辑意义上的线性表。这种结构的每个元素都有2个指针，一个指针指向一个元素，另一个指针指向下一个元素。

链域的存在决定了，每个节点比单纯的数据节点元素占用2个字节的空间，即32位系统下占用8字节，而64位系统下会占用16字节。

C++的标准模板类只是给结构体扩展了“next”“previous”指针，使之形成逻辑上的有序序列。